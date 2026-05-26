# Arquitectura de Qubes OS: Aislamiento del Hipervisor Xen

*Estado: Manual de Arquitectura Empresarial | Audiencia: Planificadores de Infraestructura y Objetivos de Alto Riesgo*

> [!CAUTION]
> **AVISO DE SEGURIDAD OPERATIVA Y LEGAL**
> Qubes OS es un sistema operativo de seguridad avanzado basado en virtualización. Desbloquear todas sus capacidades requiere una selección rigurosa de hardware y disciplina operativa.
> - **Nunca** abra documentos no confiables dentro de dominios persistentes y conectados a Internet.
> - **Siempre** verifique las plantillas descargadas criptográficamente usando PGP.
> - **Siempre** mantenga su sistema actualizado a la versión estable activa.

## 0. Requisitos y Selección de Hardware

Qubes OS no es una distribución Linux estándar; es un hipervisor "bare-metal" (de metal desnudo). Tiene requisitos de hardware extremadamente estrictos porque se basa en características específicas de virtualización de la CPU (VT-x, VT-d, AMD-V, AMD-Vi) para aislar físicamente la memoria y los dispositivos de hardware.

### Especificaciones Mínimas vs. Recomendadas
*   **RAM:** 16 GB es el mínimo absoluto indispensable para un sistema utilizable. **Se recomiendan encarecidamente más de 32 GB** si planea ejecutar varias máquinas virtuales (VM) operativas simultáneamente.
*   **Almacenamiento:** Un SSD NVMe rápido (mínimo de 512 GB). Qubes utiliza una gran cantidad de operaciones de entrada/salida (I/O) en disco debido a que ejecuta múltiples plantillas de SO simultáneamente. No instale Qubes en un disco duro (HDD) mecánico.
*   **CPU:** Debe soportar virtualización por hardware e IOMMU (Unidad de Gestión de Memoria de Entrada-Salida). La mayoría de los procesadores modernos Intel Core i5/i7/i9 y AMD Ryzen lo soportan, pero verifíquelo en su BIOS.

### Lista de Compatibilidad de Hardware (HCL)
Siempre consulte la [Lista oficial de compatibilidad de hardware de Qubes (HCL)](https://www.qubes-os.org/hcl/) antes de comprar una máquina.
*   **Hardware Recomendado:** Las computadoras portátiles Lenovo ThinkPad (específicamente la serie T como la T480, T14, o la serie X como la X1 Carbon) son probadas exhaustivamente por la comunidad y generalmente ofrecen una excelente compatibilidad con controladores Wi-Fi y estados de suspensión (sleep).
*   **Evitar:** Máquinas con tarjetas gráficas discretas Nvidia (los controladores propietarios de Nvidia entran en fuerte conflicto con el hipervisor Xen). Manténgase con gráficos integrados de Intel o AMD.

---

## 0.5. Resumen de Instalación

1.  **Descargar y Verificar:** Descargue la ISO de Qubes OS desde el sitio oficial. Usted *debe* verificar criptográficamente la ISO usando la Clave de Firma Maestra de Qubes (PGP) antes de flashearla en una unidad USB.
2.  **Preparación de la BIOS:** Arranque en la BIOS/UEFI de su computadora. Asegúrese de que Intel VT-x y VT-d (o los equivalentes de AMD) estén habilitados. Desactive "Secure Boot" (Arranque seguro).
3.  **Instalar:** Arranque desde el USB. Durante la instalación, seleccione **Cifrado de disco completo (LUKS)**. Esto es obligatorio. Elija una frase de contraseña alfanumérica fuerte (más de 20 caracteres).
4.  **Configuración Inicial:** Permita que el instalador cree los dominios predeterminados `sys-net`, `sys-firewall` y `sys-usb` (si están disponibles).

---

## 1. Topografía de Red: Los Dominios Perimetrales (Edge Domains)

Las pilas de red (network stacks) son históricamente las superficies de ataque más vulnerables. Qubes mitiga esto aislando completamente el hardware de red del cortafuegos, y el cortafuegos de sus aplicaciones operativas.

*   **`sys-net` (Interfaz de Hardware):** Esta AppVM tiene acceso exclusivo de paso PCI (PCI passthrough) a sus controladores Wi-Fi y Ethernet. Es inherentemente no confiable. Si un controlador Wi-Fi malicioso explota su tarjeta de red, el atacante solo obtiene acceso a `sys-net`, no a sus datos personales.
*   **`sys-firewall` (Controlador de Tráfico):** Esta AppVM se encuentra detrás de `sys-net`. No contiene datos de usuario y no tiene acceso directo al hardware. Impone estrictamente reglas de `iptables`, controlando qué VM operativas tienen permitido conectarse a `sys-net`.

---

## 2. Enrutamiento Anónimo: El Par Gateway/Workstation de Whonix

Para investigaciones OSINT de alto riesgo o comunicaciones de denunciantes, las VPN estándar son insuficientes. Debe implementar una arquitectura impuesta por Tor utilizando el par de plantillas Whonix.

1.  **`sys-whonix` (La Puerta de Enlace o Gateway):** Esta ServiceVM se conecta directamente a `sys-firewall`. Su única función criptográfica es forzar todo el tráfico entrante a través de la red Tor. Es totalmente ignorante de las aplicaciones de usuario que generan el tráfico.
2.  **`anon-whonix` (La Estación de Trabajo o Workstation):** Esta AppVM se conecta *solo* a `sys-whonix`. Contiene su navegador Tor y archivos operativos. Debido a que no tiene conexión directa con `sys-firewall` o `sys-net`, es físicamente imposible que un exploit dentro de `anon-whonix` filtre su verdadera dirección IP.

---

## 3. Arquitectura Desechable: La DispVM No Confiable

Nunca abra un archivo adjunto no confiable (PDF, documento de Word, imagen) enviado desde una fuente no verificada en una máquina virtual operativa persistente.

*   **Despliegue:** Cree una plantilla de Máquina Virtual Desechable (DispVM). Cuando abra un archivo descargado en una máquina virtual no confiable, haga clic derecho y seleccione **Ver en DispVM**.
*   **Mecánica:** El hipervisor Xen crea una instancia nueva y aislada de VM en la memoria RAM, abre el documento y destruye toda la VM en el momento en que cierra la ventana. Cualquier malware integrado o píxeles de seguimiento se eliminan instantáneamente de la existencia junto con la DispVM.

---

## 3.5. Comprensión de la Gestión de Plantillas

Qubes utiliza una arquitectura de almacenamiento inteligente para ahorrar espacio y optimizar las actualizaciones.

*   **TemplateVMs (VMs de Plantilla):** Estos son sistemas de archivos raíz de solo lectura (por ejemplo, una instalación pura de Fedora 40 o Debian 12). Cuando actualiza una TemplateVM a través de la herramienta de actualización de Qubes, los cambios persisten.
*   **AppVMs (VMs de Aplicación):** Estos son sus espacios de trabajo diarios. Una AppVM monta el sistema de archivos raíz de su TemplateVM (solo lectura) y solo tiene acceso de escritura a su propio directorio `/home/user`. Si una AppVM está infectada con malware tipo rootkit, el simple hecho de reiniciar la AppVM elimina el rootkit, porque al arrancar extrae un sistema de archivos raíz nuevo y limpio de la TemplateVM.
*   **Minimización de la Superficie de Ataque:** Cree plantillas mínimas. Si solo necesita una AppVM para Signal Desktop, clone una plantilla de Debian, elimine todo el software innecesario (paquetes de oficina, reproductores multimedia), instale Signal y base su AppVM de comunicación en esa plantilla mínima.

---

## 4. La Bóveda sin Conexión (Air-Gapped): Gestión de Claves Raíz

Sus claves PGP maestras, semillas de criptomonedas y bases de datos de contraseñas nunca deben tocar un dominio conectado a Internet.

*   **`vault` (El Enclave Fuera de Línea):** Cree una AppVM basada en una plantilla mínima de Debian o Fedora.
*   **Configuración:** En la configuración de la VM, configure **NetVM** en `none`. Esto corta el cable ethernet virtual.
*   **Uso:** Genere sus claves PGP y guarde su base de datos de KeePassXC exclusivamente dentro de esta bóveda. Pasará los datos cifrados *hacia afuera* de la bóveda, pero las claves privadas nunca salen.

---

## 5. Protocolos Seguros Entre VM (`qvm-copy` / `qvm-move`)

Debido a que el hipervisor aísla completamente sus dominios, no puede arrastrar y soltar archivos ni usar un portapapeles compartido estándar. Esto evita que el malware migre lateralmente a través de su sistema.

*   **Protocolo de Portapapeles:** Para copiar una contraseña desde su `vault` a un navegador web en `personal`:
    1.  Resalte el texto en `vault` y presione `Ctrl+C`.
    2.  Presione `Ctrl+Shift+C` para indicar al hipervisor que mueva los datos de forma segura al portapapeles global.
    3.  Seleccione la ventana de la VM `personal` y presione `Ctrl+Shift+V` para extraer los datos del portapapeles global.
    4.  Presione `Ctrl+V` para pegar el texto en el navegador.
*   **Protocolo de Transferencia de Archivos:** Para mover un documento cifrado desde `work` (trabajo) a `sys-whonix` para su transmisión:
    1.  Abra la terminal Dom0 o use el administrador de archivos GUI.
    2.  Ejecute: `qvm-copy-to-vm anon-whonix manifest.pdf`.
    3.  El hipervisor interceptará el archivo, le pedirá autorización explícita y lo inyectará de forma segura en la VM de destino.

---

## 6. Ejemplos Prácticos de Flujo de Trabajo

¿Cómo se ve esto en la práctica para un operador de alto riesgo?

*   **Ejemplo 1: El Flujo de Trabajo del Periodista**
    *   Recibe una pista cifrada por correo electrónico en la VM `work-email`.
    *   Utiliza `qvm-copy` para enviar el archivo cifrado a la VM offline `vault`.
    *   Dentro de `vault`, descifra el archivo usando su clave privada PGP.
    *   Utiliza `qvm-copy` para enviar el archivo descifrado a una `analysis-dispVM` (VM Desechable) completamente fuera de línea para ver de forma segura el contenido sin poner en riesgo sus sistemas persistentes.
*   **Ejemplo 2: El Flujo de Trabajo del Organizador**
    *   `comms-public`: Se utiliza para Twitter, organización pública en Facebook, canales abiertos de Slack. Conectado a través del `sys-firewall` estándar.
    *   `comms-secure`: Utilizado solo para Signal Desktop y Matrix encriptado.
    *   `logistics`: Contiene hojas de cálculo, listas de donantes y contratos de lugares. Desconectado de Internet (NetVM: none) cuando no se está sincronizando activamente.
*   **Ejemplo 3: El Investigador OSINT**
    *   `osint-clearnet`: Se utiliza para buscar en bases de datos públicas a través de una puerta de enlace VPN estándar.
    *   `anon-whonix`: Se utiliza para la investigación en la web profunda (deep-web), completamente aislado, enrutando estrictamente a través de Tor. Si un sitio malicioso intenta un exploit en el navegador, no podrá ver la IP real del investigador ni acceder a los archivos de `osint-clearnet`.

---

## 7. Copias de Seguridad y Recuperación

Si su hardware falla, debe poder restaurar todo su entorno compartimentado.

*   **La Herramienta de Copia de Seguridad de Qubes:** Qubes incluye una sólida utilidad de respaldo a nivel de hipervisor en `dom0`. Puede realizar copias de seguridad de las configuraciones y los datos de todas sus AppVMs.
*   **Cifrado:** La utilidad de copia de seguridad cifra de forma nativa el archivo de respaldo con una frase de contraseña.
*   **Destino:** Haga una copia de seguridad en un disco USB externo conectado a `sys-usb`. Si se cambia a una máquina nueva, instalar Qubes y restaurar esta copia de seguridad recreará a la perfección toda su compleja arquitectura de máquinas virtuales.

---

## 8. Limitaciones y Cuándo NO Usar Qubes

Qubes OS es una increíble hazaña de ingeniería, pero no es para todo el mundo.

*   **Intolerancia al Hardware:** Si compra una computadora portátil sin revisar la HCL, es probable que Qubes no se instale, que el Wi-Fi no funcione, o que los estados de suspensión bloqueen la máquina.
*   **Curva de Aprendizaje:** Debe volver a aprender por completo cómo interactuar con una computadora. Copiar-pegar, mover archivos e instalar software requieren interacciones a nivel de hipervisor.
*   **Mucho Consumo de Recursos:** Ejecutar 8 sistemas operativos independientes simultáneamente agota la batería de las computadoras portátiles increíblemente rápido (espere un máximo de 2 a 4 horas en la mayoría del hardware) y requiere una gran cantidad de memoria RAM.
*   **La Alternativa:** Si solo necesita privacidad frente al seguimiento corporativo o seguridad básica, utilice **Linux Mint** o **Fedora Workstation**. Si necesita anonimato temporal, arranque **Tails OS** desde una memoria USB. Utilice Qubes únicamente si necesita *seguridad persistente y altamente compartimentada frente a adversarios avanzados.*

---

## 9. Ciclo de Vida de los Lanzamientos

> [!WARNING]
> **Alerta de Fin de Vida (EOL) de Qubes OS 4.2 (21 de Junio de 2026)**
> La serie Qubes OS 4.2 llegará a su Fin de Vida (EOL) oficial el **21 de Junio de 2026**. Después de esta fecha, Qubes 4.2 ya no recibirá actualizaciones de seguridad. Todos los operadores de alto riesgo deben actualizar sus instalaciones a **Qubes OS 4.3.0** antes de esta fecha límite para permanecer protegidos.

*Referencia:* Todas las especificaciones de arquitectura, guías de lanzamiento y documentación del ciclo de vida de soporte están verificadas frente a las listas oficiales de los desarrolladores [Documentación de Qubes OS, https://www.qubes-os.org/doc/, Mayo 2026].

[← Volver al Índice](../index.md)

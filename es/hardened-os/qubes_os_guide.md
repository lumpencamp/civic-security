# Arquitectura del sistema operativo Qubes: aislamiento del hipervisor Xen

*Estado: Manual de Arquitectura Empresarial | Público: Planificadores de infraestructura y objetivos de alto riesgo*

## Una nota sobre las opciones de SO de escritorio

* **Para principiantes (Linux Mint/Ubuntu):** Si actualmente utiliza Windows o macOS y desea una actualización de privacidad significativa sin una curva de aprendizaje pronunciada, comience por cambiar a una distribución de Linux fácil de usar como **Linux Mint** o **Ubuntu**. Son mucho menos invasivos que los sistemas operativos comerciales.
* **Para alta seguridad (Qubes y Tails):** Si su modelo de amenaza involucra adversarios a nivel estatal o vigilancia avanzada, use Qubes OS (para trabajo diario compartimentado) o Tails OS (para tareas temporales y anónimas).

---

Qubes OS no depende del entorno de pruebas de software; refuerza la seguridad a través de una compartimentación básica utilizando el hipervisor Xen. Si una única aplicación o dominio se ve comprometido por un exploit de día cero, el hipervisor garantiza que la infección no puede traspasar los límites del hipervisor para comprometer otros dominios o el hardware del host.

Este manual detalla la configuración paso a paso de una infraestructura de dominio Xen reforzada y multicapa optimizada para operaciones cívicas.

## 1. Topografía de la red: los dominios perimetrales

Las pilas de red son históricamente las superficies de ataque más vulnerables. Qubes mitiga esto aislando completamente el hardware de la red del firewall y el firewall de sus aplicaciones operativas.

* **`sys-net` (Interfaz de hardware):** Esta AppVM tiene acceso de paso PCI exclusivo a sus controladores Wi-Fi y Ethernet. Es inherentemente poco confiable. Si un controlador Wi-Fi malicioso explota su tarjeta de red, el atacante sólo obtendrá acceso a `sys-net`, no a sus datos personales.
* **`sys-firewall` (controlador de tráfico):** Esta AppVM se encuentra detrás de `sys-net`. No contiene datos de usuario y no tiene acceso directo al hardware. Hace cumplir estrictamente las reglas de "iptables", que rigen qué máquinas virtuales operativas pueden conectarse a "sys-net".

## 2. Enrutamiento anónimo: el par de puerta de enlace/estación de trabajo Whonix

Para investigaciones OSINT de alto riesgo o comunicaciones de denunciantes, las VPN estándar son insuficientes. Debe implementar una arquitectura reforzada por Tor utilizando el par de plantillas Whonix.

1. **`sys-whonix` (La puerta de enlace):** Este ServiceVM se conecta directamente a `sys-firewall`. Su única función criptográfica es forzar todo el tráfico entrante a través de la red Tor. Ignora por completo las aplicaciones de usuario que generan el tráfico.
2. **`anon-whonix` (La estación de trabajo):** Esta AppVM se conecta *solo* a `sys-whonix`. Contiene su navegador Tor y archivos operativos. Debido a que no tiene conexión directa con `sys-firewall` o `sys-net`, es físicamente imposible que un exploit dentro de `anon-whonix` filtre su verdadera dirección IP.

## 3. Arquitectura descartable: el DispVM que no es de confianza

Nunca abra un archivo adjunto que no sea de confianza (PDF, documento de Word, imagen) enviado desde una fuente no verificada en una máquina virtual operativa persistente.

* **Implementación:** Cree una plantilla de máquina virtual desechable (DispVM). Cuando abre un archivo descargado en una VM que no es de confianza, haga clic derecho y seleccione **Ver en DispVM**.
* **Mecánica:** El hipervisor Xen crea una instancia de una máquina virtual nueva y aislada en la RAM, abre el documento y destruye toda la máquina virtual en el momento en que cierra la ventana. Cualquier malware incrustado o píxeles de seguimiento se eliminan instantáneamente junto con DispVM.

## 4. La bóveda con espacio de aire: gestión de claves raíz

Sus claves PGP maestras, semillas de criptomonedas y bases de datos de contraseñas nunca deben tocar un dominio conectado a Internet.

* **`vault` (The Offline Enclave):** Cree una AppVM basada en una plantilla mínima de Debian o Fedora.
* **Configuración:** En Configuración de VM, establezca **NetVM** en `ninguno`. Esto corta el cable de Ethernet virtual.
* **Uso:** Genere sus claves PGP y almacene su base de datos KeePassXC exclusivamente dentro de esta bóveda. Pasará datos cifrados *fuera* de la bóveda, pero las claves privadas nunca saldrán.

## 5. Protocolos seguros entre máquinas virtuales (`qvm-copy` / `qvm-move`)

Debido a que el hipervisor aísla completamente sus dominios, no puede arrastrar y soltar archivos ni utilizar un portapapeles compartido estándar. Esto evita que el malware migre lateralmente a través de su sistema.

* **Protocolo del portapapeles:** Para copiar una contraseña desde su `bóveda` a un navegador web en `personal`:
    1.  Resalta el texto en `vault` y presiona `Ctrl+C`.
    2.  Presione `Ctrl+Shift+C` para indicarle al hipervisor que mueva los datos de forma segura al portapapeles global.
    3.  Seleccione la ventana de VM `personal` y presione `Ctrl+Shift+V` para extraer los datos del portapapeles global.
    4.  Presione `Ctrl+V` para pegar el texto en el navegador.
* **Protocolo de transferencia de archivos:** Para mover un documento cifrado de `work` a `sys-whonix` para su transmisión:
    1.  Abra la terminal Dom0 o utilice el administrador de archivos GUI.
    2.  Ejecute: `qvm-copy-to-vm [DestinationVM] [filename]` (p. ej., `qvm-copy-to-vm anon-whonix manifest.pdf`).
    3.  El hipervisor interceptará el archivo, le solicitará autorización explícita y lo inyectará de forma segura en el directorio `QubesIncoming` de la máquina virtual de destino.

_Última actualización: 2026_

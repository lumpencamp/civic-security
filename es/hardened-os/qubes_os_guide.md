# Una guía práctica y centrada en la seguridad del sistema operativo Qubes

## Una nota sobre las opciones de SO de escritorio

* **Para principiantes (Linux Mint/Ubuntu):** Si actualmente utiliza Windows o macOS y desea una actualización de privacidad significativa sin una curva de aprendizaje pronunciada, comience por cambiar a una distribución de Linux fácil de usar como **Linux Mint** o **Ubuntu**. Son mucho menos invasivos que los sistemas operativos comerciales.
* **Para alta seguridad (Qubes y Tails):** Si su modelo de amenaza involucra adversarios a nivel estatal o vigilancia avanzada, use Qubes OS (para trabajo diario compartimentado) o Tails OS (para tareas temporales y anónimas).

Esta guía está dirigida a usuarios técnicamente competentes que son nuevos en el paradigma del sistema operativo Qubes. Proporciona una descripción general completa de su filosofía, conceptos centrales y flujos de trabajo prácticos y seguros.

---

## 1. La Filosofía: ¿Qué es Qubes OS?

Qubes OS no es sólo otra distribución de Linux; es un enfoque fundamentalmente diferente a la seguridad informática. Su diseño central se basa en el principio de **Seguridad por compartimentación**.

Imagina que tu vida digital es una casa. En un sistema operativo tradicional (como Windows, macOS o una distribución de Linux estándar), esta casa es un estudio único de planta abierta. Si un ladrón (malware) ingresa a través de una ventana abierta (un navegador web vulnerable), tiene acceso inmediato a todo: su escritorio (documentos de trabajo), su archivador (contraseñas) y sus fotografías personales. Un único punto de falla compromete todo el sistema.

Qubes OS reconstruye esta casa en una serie de habitaciones separadas y selladas, cada una con su propia puerta reforzada. Su trabajo ocurre en una habitación, sus operaciones bancarias personales en otra y su navegación web aleatoria en una tercera. Allí se contiene un incendio que se inició en la sala de "navegación"; no puede propagarse a la sala de "banca" ni a la sala de "bóveda de contraseñas". Cada habitación es un **qube**, una máquina virtual aislada. Ésta es la esencia de la seguridad por compartimentación: si un componente se ve comprometido, el daño se contiene y el resto de su vida digital permanece segura.

### ¿Para quién es el sistema operativo Qubes?

Qubes OS está diseñado para aquellos cuya seguridad digital es primordial. Si bien cualquiera puede beneficiarse de su arquitectura, es particularmente vital para:

* **Periodistas y activistas:** Para proteger las fuentes, las investigaciones y las comunicaciones de la vigilancia y los ataques dirigidos.
* **Investigadores de seguridad:** Para analizar malware de forma segura e investigar amenazas en entornos aislados.
* **Abogados y Ejecutivos de Negocios:** Para proteger los datos confidenciales de los clientes y la propiedad intelectual.
* **Defensores de la privacidad y la seguridad:** Para cualquiera que quiera tomar el control de su huella digital y defenderse de las amenazas generalizadas de la Internet moderna.

---

## 2. Requisitos e instalación de hardware

La elección del hardware es fundamental para el sistema operativo Qubes. Debido a que depende de funciones de virtualización de hardware, no todas las computadoras son compatibles.

### La lista de compatibilidad de hardware (HCL)

El recurso más importante a la hora de elegir una máquina para Qubes es la **Lista de compatibilidad de hardware (HCL)**. Esta es una base de datos mantenida por la comunidad de sistemas que han sido probados con Qubes OS. Antes de intentar instalar Qubes, **debe** verificar la HCL para ver si su hardware está en la lista y qué nivel de compatibilidad esperar.

* **HCL oficial del sistema operativo Qubes:** [https://www.qubes-os.org/hcl/](https://www.qubes-os.org/hcl/)

Intentar instalar en hardware que no figura en la lista es una apuesta que puede llevar a una experiencia frustrante con dispositivos que no funcionan (Wi-Fi, suspensión, etc.) o a una falla total en la instalación.

### Características clave del hardware

Para que Qubes funcione correctamente, la CPU y el BIOS/UEFI de la placa base de su sistema deben admitir las siguientes tecnologías de virtualización:

* **Intel VT-x con EPT (tablas de páginas extendidas) / AMD-V con RVI (indexación de virtualización rápida):** Esta es la tecnología de virtualización asistida por hardware fundamental que permite que el hipervisor Xen (la base de Qubes) ejecute múltiples máquinas virtuales de manera eficiente.
* **Intel VT-d (tecnología de virtualización para E/S dirigida) / AMD-Vi (tecnología de virtualización de E/S):** Esto es crucial. VT-d permite a Qubes asignar de forma segura dispositivos de hardware, como su tarjeta de red o controladores USB, a qubes específicos y aislados (por ejemplo, `sys-net`). Sin él, se pierde una capa importante de seguridad.
* **Módulo de plataforma segura (TPM):** Si bien no es estrictamente necesario para la instalación, se recomienda encarecidamente utilizar un TPM con funciones como Anti-Evil Maid para proteger contra ataques físicos.

### Descripción general de la instalación

1. **Descargue la ISO:** Obtenga la última versión estable del sitio web oficial del sistema operativo Qubes.
2. **Verifique la ISO:** Utilice las firmas criptográficas proporcionadas para asegurarse de que su descarga sea auténtica y no haya sido manipulada.
3. **Cree un USB de arranque:** Utilice una herramienta como `dd` o Rufus para escribir el ISO en una unidad USB. La documentación de Qubes proporciona instrucciones específicas y seguras para este proceso.
4. **Configuración BIOS/UEFI:** Inicie la configuración BIOS/UEFI de su sistema y asegúrese de que VT-x/AMD-V y VT-d/AMD-Vi estén **habilitados**.
5. **Instale Qubes:** Inicie desde la unidad USB y siga las instrucciones del instalador de Anaconda. El instalador lo guiará a través de la partición del disco y la configuración inicial del usuario.

---

## 3. Comprender los conceptos básicos

Qubes OS tiene un vocabulario y una arquitectura únicos. Comprender estos conceptos básicos es clave para utilizarlos de forma eficaz.

### Qubes de aplicaciones (dominios)

Un **App Qube** (o **Dominio**) es una máquina virtual aislada donde ejecuta sus aplicaciones. Cada qube se basa en una TemplateVM (ver más abajo). Es posible que tenga un qube "de trabajo" para sus aplicaciones de oficina, un qube "personal" para su correo electrónico privado y un qube "no confiable" para navegación aleatoria. El indicador más visible de a qué qube pertenece la ventana de una aplicación es su **borde codificado por colores**. Esta es una característica de seguridad crítica: un borde rojo le indica instantáneamente que la ventana pertenece a su qube "no confiable", mientras que un borde verde puede pertenecer a su qube "personal", lo que le impide ingresar accidentalmente una contraseña en el contexto incorrecto.

### PlantillaVM

**TemplateVM** son las 'copias maestras' o 'imágenes doradas' para sus App Qubes. No ejecuta aplicaciones directamente en un TemplateVM. En su lugar, instala el software *en* TemplateVM. Por ejemplo, para instalar el editor de imágenes GIMP, iniciaría TemplateVM `fedora-39`, instalaría GIMP usando el administrador de paquetes estándar (`sudo dnf install gimp`) y luego lo cerraría. Todos los App Qubes basados ​​en `fedora-39` ahora tendrán GIMP disponible en el menú de su aplicación después de reiniciarlos.

Este diseño es increíblemente eficiente y seguro. Para actualizar el software de docenas de App Qubes, solo necesita actualizar su único TemplateVM subyacente. El proceso de actualización es centralizado y seguro.

### Máquinas virtuales desechables

**Las máquinas virtuales desechables** son qubes desechables y de un solo uso. Son perfectos para abrir un archivo adjunto de correo electrónico sospechoso o hacer clic en un enlace de una fuente desconocida. Cuando abre un archivo en una VM desechable, se crea un qube nuevo y limpio sobre la marcha. Puede ver el documento y, cuando cierra la ventana, *la máquina virtual completa se destruye instantánea y permanentemente*. Cualquier malware que pueda haber estado en el documento se destruye con él, sin haber tenido nunca la oportunidad de tocar sus qubes persistentes.

### La pila de redes

La creación de redes en Qubes es un excelente ejemplo de compartimentación.

* **`sys-net`:** Este es un qube especial y sin privilegios que tiene control directo del hardware de su red física (Wi-Fi, Ethernet). Su única función es gestionar el hardware y pasar el tráfico de red al "sys-firewall". Debido a que está aislado, un compromiso de `sys-net` (por ejemplo, a través de un controlador Wi-Fi malicioso) no compromete todo el sistema. Sólo compromete el propio dispositivo de red.
* **`sys-firewall`:** Este qube actúa como el firewall central para todo su sistema. No tiene ninguna aplicación de usuario. Su único propósito es hacer cumplir reglas sobre qué qubes pueden conectarse a la red y entre sí. Puede, por ejemplo, configurarlo para denegar todo el acceso a la red a su qube "vault" y al mismo tiempo permitir el acceso a su qube "trabajo".

#### **Análisis profundo: `sys-whonix` y redes anónimas**

Qubes OS proporciona un gran anonimato al integrar el proyecto **Whonix**. Whonix es un sistema operativo diseñado para enrutar todas las conexiones de red a través de la red Tor. En Qubes, esto se implementa a través de dos componentes clave:

1. **The Whonix Gateway (`sys-whonix`):** Este es un qube dedicado que actúa como una puerta de enlace Tor. Su único propósito es tomar el tráfico entrante de otros qubes y forzarlo a través de la red Tor. Está diseñado para ser seguro y evitar fugas de direcciones IP.

2. **La estación de trabajo Whonix (Plantilla para `anon-whonix`):** Esta es una TemplateVM especial que está preconfigurada para seguridad y anonimato. Las aplicaciones que se ejecutan desde esta plantilla (como el navegador Tor incluido) están protegidas contra huellas dactilares y están configuradas para funcionar de forma segura con Tor.

**Cómo funciona en la práctica:**

* Creas una App Qube (de forma predeterminada, se crea una llamada `anon-whonix`) basada en la plantilla de Whonix Workstation.
* Usted configura la red para esta aplicación Qube en `sys-whonix`.
* Ahora, *cualquier aplicación* que ejecutes dentro de `anon-whonix` tendrá su tráfico enrutado de forma automática y transparente a través de Tor. No es necesario configurar nada dentro del qube; el anonimato se aplica a nivel del sistema.

**Aislamiento de transmisión para un anonimato mejorado:**

Este es un concepto poderoso. Puede crear múltiples App Qubes basados ​​en la plantilla Whonix Workstation, cada uno para una actividad anónima diferente. Por ejemplo:

* **`anon-research`:** Se utiliza para investigar temas delicados de forma anónima.
* **`anon-social`:** Se utiliza para gestionar una persona anónima en las redes sociales.

Aunque ambos qubes se conectan a la misma puerta de enlace `sys-whonix`, el diseño de Tor garantiza que el tráfico de cada uno se envíe a través de un circuito Tor diferente (una ruta diferente a través de la red). Esto hace que sea extremadamente difícil para un observador externo correlacionar sus actividades de investigación con su personalidad en las redes sociales. Está utilizando 'flujos' de tráfico diferentes y aislados para cada identidad, al mismo tiempo que se beneficia de la protección central de Whonix Gateway.

---

## 4. Flujos de trabajo seguros y prácticos

Una instalación predeterminada de Qubes proporciona un buen punto de partida, pero su verdadero poder proviene de la creación de un flujo de trabajo que coincida con su modelo de amenaza personal. Aquí hay una configuración clásica y altamente efectiva:

* **`bóveda` Qube:**
    * **Propósito:** Almacenar sus datos más confidenciales: base de datos del administrador de contraseñas, claves privadas de PGP, documentos financieros.
    * **Configuración:** **Sin acceso a la red.** En la configuración de qube, establezca Redes en `(ninguno)`. Esto lo convierte en una bóveda fuera de línea. Es físicamente imposible que el malware extraiga datos de este qube a través de la red.
    * **Plantilla:** Basado en una plantilla mínima para reducir la superficie de ataque.

* **`trabajo` Qube:**
    * **Finalidad:** Todas las actividades profesionales. LibreOffice, perfiles de navegador relacionados con el trabajo, herramientas de desarrollo.
    * **Configuración:** Acceso a la red mediante `sys-firewall`. Puede crear reglas de firewall para restringirlo solo a la VPN de su empresa o a sitios web específicos.

* **Qube `personal`:**
    * **Finalidad:** Actividades personales de confianza. Cliente de correo electrónico personal, redes sociales confiables, banca en línea.
    * **Configuración:** Acceso a la red mediante `sys-firewall`. Se mantiene separado del "trabajo" para evitar que un compromiso en un dominio afecte al otro.

* **Qube `no confiable`:**
    * **Finalidad:** Navegación web general y no confiable. Hacer clic en enlaces de correos electrónicos, buscar información, visitar nuevos sitios web.
    * **Configuración:** Acceso a la red mediante `sys-firewall`. Esta es su 'zona de pruebas digital'. Si descarga un archivo aquí, puede pasarlo de forma segura a una máquina desechable para su inspección antes de moverlo a un qube más confiable.

---

## 5. Operaciones seguras entre Qube

Debido a que todos los qubes están aislados, acciones simples como copiar y pegar y transferir archivos requieren mecanismos especiales y seguros.

### Copiar/Pegar de forma segura

Un `Ctrl+C` y un `Ctrl+V` estándar solo funcionarán dentro del *mismo* qube. Para mover de forma segura los datos del portapapeles entre qubes:

1. En la ventana del qube de origen, seleccione el texto y presione **`Ctrl+Shift+C`**. Esto copia el texto en un portapapeles seguro entre qubes y notifica al sistema Qubes que los datos están listos para pegarse.
2. En la ventana del qube de destino, coloque el cursor y presione **`Ctrl+Shift+V`**. Esto pegará los datos.

Este proceso de dos pasos es intencional. Evita que un qube malicioso inyecte datos silenciosamente en su portapapeles y lo engañe para que pegue un comando malicioso en una terminal en otro qube más privilegiado.

### Transferencia segura de archivos

Para mover un archivo de un qube a otro:

1. En el administrador de archivos del qube fuente, haga clic derecho en el archivo.
2. Seleccione **Copiar a otra AppVM...** (o **Mover a otra AppVM...**).
3. Aparecerá un cuadro de diálogo que le pedirá que especifique el qube de destino en una lista desplegable.
4. Seleccione el qube de destino y haga clic en Aceptar.

Esto desencadena una transferencia segura y aprobada por el usuario. El archivo no se "mueve" simplemente en un sistema de archivos compartido; se pasa de forma segura de un entorno aislado a otro bajo su control explícito.

---

## 6. Mantenimiento y actualizaciones del sistema

Mantener el sistema actualizado es fundamental para la seguridad. Qubes proporciona una herramienta unificada para manejar esto de forma segura.

1. Haga clic en el **Menú de la aplicación Qubes** (el ícono 'Q').
2. Vaya a **Herramientas del sistema** -> **Actualización de Qubes**.
3. Aparecerá una ventana con una lista de todas sus TemplateVM (por ejemplo, `fedora-39`, `debian-12`, `whonix-gw-17`, `whonix-ws-17`).
4. De forma predeterminada, todos están seleccionados. Haga clic en **Aceptar**.

La herramienta de actualización de Qubes ahora de forma segura y secuencial:
* Inicie cada TemplateVM.
* Ejecute el administrador de paquetes nativo dentro de él para descargar y aplicar todas las actualizaciones disponibles.
* Apague TemplateVM cuando haya terminado.

Una vez que se complete el proceso, debe **reiniciar cualquier App Qubes en ejecución** para que las actualizaciones surtan efecto. Este proceso único garantiza que el software fundamental para todos sus compartimentos esté parcheado y sea seguro.

_Última actualización: 2026_
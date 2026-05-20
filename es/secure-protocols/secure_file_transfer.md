# Una guía detallada para la transferencia segura de archivos

Compartir archivos de forma segura es una tarea fundamental para los activistas.Ya sea que envíe una investigación a un colaborador o filtre documentos a un periodista, debe proteger el contenido del archivo y las identidades tanto del remitente como del receptor.Esta guía cubre dos potentes herramientas de referencia para diferentes escenarios.

---

### **Método 1: Compartir localmente sin conexión (para protestas y multitudes)**

**Caso de uso:** Estás en una protesta o acción.El servicio celular está bloqueado, apagado o sospecha que la policía está usando Stingrays (captadores IMSI) para monitorear la red.Necesita compartir rápidamente una foto, un vídeo o un documento con un miembro del grupo de afinidad que esté a su lado.

**Cómo funciona:** Utiliza herramientas que dependen de conexiones locales de dispositivo a dispositivo (Bluetooth o creación de un punto de acceso Wi-Fi temporal) para transferir el archivo sin siquiera tocar Internet.

* **LocalSend (altamente recomendado):** LocalSend es una aplicación gratuita de código abierto disponible para iOS, Android, macOS, Windows y Linux.No requiere conexión a Internet ni cuenta.Ambos dispositivos deben estar en la misma red Wi-Fi local (un dispositivo puede crear un punto de acceso móvil y el otro se conecta a él, sin que los datos móviles estén activados).Es rápido y seguro.
* **Briar:** Aunque Briar es principalmente una aplicación de mensajería, también puede transferir archivos de igual a igual a través de Bluetooth.Es más lento que LocalSend pero no requiere configuración de Wi-Fi.
* **Una advertencia sobre AirDrop/Near Share:** AirDrop de Apple y Near Share de Android son convenientes pero tienen fallas de privacidad conocidas (transmiten nombres de dispositivos y, a veces, números de teléfono/ID de Apple a escáneres cercanos).Si los usa, configúrelos en "Solo contactos" y apáguelos por completo inmediatamente después de que se complete la transferencia.Nunca los dejes en "Todos".

---

### **Método 2: OnionShare (para compartir directamente entre pares a través de Internet)**

**Caso de uso:** Debe enviar un archivo directamente a una persona específica en la que confíe.Quiere que la transferencia sea segura, anónima y que no deje rastro en un servidor de terceros (como Google Drive o Dropbox).

**Cómo funciona:** OnionShare convierte temporalmente su computadora en un servidor web anónimo y seguro utilizando la red Tor.El archivo se transfiere directamente desde su máquina a la del destinatario, Tor lo cifra y lo anonimiza.Una vez que se completa la transferencia, el servidor desaparece.

#### **Instrucciones paso a paso:**

1. **Requisitos previos de instalación:** Debes tener el **Navegador Tor** instalado y ejecutándose para que OnionShare se conecte a la red Tor.Descárgalo de `torproject.org`.
2. **Instalar OnionShare:** Descargue la aplicación oficial de OnionShare desde `onionshare.org`.
3. **Comience a compartir:**
* Abra OnionShare y navegue hasta la pestaña "Compartir archivos".
* Arrastre y suelte los archivos que desea compartir en la ventana.
* Desmarque la casilla "Dejar de compartir después de que se hayan enviado los archivos (desmarque para permitir la descarga varias veces)" si desea que el enlace sea de un solo uso.Esto es muy recomendable.
* Haga clic en **"Comenzar a compartir".**
4. **Comparte la dirección secreta:**
* OnionShare generará una dirección `.onion` única y una clave privada (contraseña).
* **Este es el paso más crítico.** Debes transmitir esta dirección y clave a tu destinatario a través de un canal seguro y cifrado de extremo a extremo, como **Señal** o **Sesión**.NO envíe este enlace por correo electrónico o mensaje de texto normal.
5. **El destinatario descarga el archivo:**
* El destinatario abre su navegador Tor y navega hasta la dirección `.onion` que proporcionaste.
* Se les solicitará la clave privada para acceder a la página de descarga.
* Una vez que descargan el archivo, el intercambio se detiene automáticamente (si dejó marcada la configuración predeterminada) y el enlace deja de ser válido.

---

### **Método 3: SecureDrop (para denuncias anónimas)**

**Caso de uso:** Usted es una fuente que necesita enviar de forma anónima documentos confidenciales a una organización de medios u ONG sin revelar su identidad.

**Cómo funciona:** SecureDrop es un sistema utilizado por periodistas para recibir archivos de fuentes anónimas.Todo el proceso está diseñado para proteger la identidad de la fuente.No ejecuta SecureDrop;Se utiliza el proporcionado por la organización.

#### **Instrucciones paso a paso:**

1. **NO USE SU PROPIA COMPUTADORA O RED DOMÉSTICA.** Esto no es negociable para envíos de alto riesgo.Vaya a un lugar con Wi-Fi público que no esté asociado con usted (por ejemplo, una biblioteca o cafetería lejos de su casa o trabajo).
2. **Utilice el sistema operativo Tails:** Para máxima seguridad, debe utilizar el sistema operativo Tails, que se ejecuta desde una memoria USB y fuerza todas las conexiones a través de Tor, sin dejar rastro en la máquina.Consulte nuestra guía del sistema operativo Tails para obtener más información.
3. **Busque la dirección de SecureDrop:** Desde un navegador normal en un dispositivo seguro, busque la dirección oficial de SecureDrop `.onion` de la organización.Lo incluirán en su sitio web público.Escríbelo con cuidado.
4. **Conectar y cargar:**
* En tu máquina con Tails OS en la ubicación pública de Wi-Fi, abre el navegador Tor y navega hasta la dirección `.onion` que anotaste.
* Siga las instrucciones en pantalla para cargar sus archivos.
5. **Reciba su nombre en clave:**
* Después de la carga, el sistema generará un **nombre en clave secreto y único**.Esta es su única clave para la presentación.**Memorízalo o escríbelo en una hoja de papel que puedas guardar de forma segura sin conexión.** NO lo guardes en ninguna computadora.
6. **Buscar respuestas:**
* Espere varios días.Luego, utilizando **exactamente el mismo método seguro** (sistema operativo Tails, Wi-Fi público), regrese a la dirección SecureDrop e inicie sesión con su nombre en clave secreto.Esto te permitirá ver si el periodista te ha dejado un mensaje.

_Última actualización: 2026_
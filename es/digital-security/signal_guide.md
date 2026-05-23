# Signal: Endurecimiento criptográfico y seguridad operativa

*Estado: Manual de refuerzo y auditoría de software | Público: activistas, fuentes y organizadores*

Signal es el estándar de oro para la mensajería cifrada de un extremo a otro. Sin embargo, su configuración predeterminada está optimizada para la comodidad del usuario, no para sobrevivir a la vigilancia a nivel estatal o a la captura de dispositivos físicos. El cifrado de Signal solo protege los datos *en tránsito*. Una vez que los datos llegan a un dispositivo, dependen completamente de la seguridad local del dispositivo.

Esta guía detalla el estricto bloqueo criptográfico de cuentas requerido para operaciones de alto riesgo.

---

## 1. Bloqueo de cuenta obligatorio (registro y PIN)

El ataque más común contra los usuarios de Signal no es romper el cifrado; está secuestrando la cuenta tomando el número de teléfono subyacente (mediante intercambio de SIM o ataques SS7) y volviendo a registrar Signal en el dispositivo de un adversario.

### El bloqueo de registro
Debe vincular físicamente su cuenta de Signal a un PIN criptográfico, eliminando la dependencia de la verificación por SMS.

1. Vaya a **Configuración** > **Cuenta** > **Bloqueo de registro**.
2. Active **ON**.
3. *El mecanismo:* Si un adversario roba su número de teléfono e intenta registrar Signal, será bloqueado sin su PIN personalizado. Después de 7 días de inactividad, el bloqueo expira, pero para entonces te habrás dado cuenta de que tu número está comprometido.

### Configuración de PIN alfanumérico personalizado
No utilice un PIN de 4 dígitos. Es trivial aplicar fuerza bruta si un adversario captura el hash.

1. Vaya a **Configuración** > **Cuenta** > **Cambiar su PIN**.
2. Seleccione **Crear PIN alfanumérico**.
3. Ingrese una frase de contraseña aleatoria y sólida (mínimo 12 caracteres, almacenada en un administrador de contraseñas fuera de línea como KeePassXC).

## 2. Verificación del número de seguridad (mitigación de ataques MitM)

El cifrado de extremo a extremo es inútil si cifra sus mensajes con la clave pública de un adversario en lugar de la de su contacto. Este es un ataque Man-in-the-Middle (MitM).

### Protocolo de verificación fuera de banda
Debe verificar el "Número de seguridad" criptográfico de cada contacto operativo *antes* de compartir activos confidenciales.

1. Abra el chat con su contacto, toque su nombre y seleccione **Ver número de seguridad**.
2. **La regla de oro:** Nunca verifiques un número de seguridad a través de Signal y nunca lo verifiques a través de un canal no cifrado como SMS.
3. **Métodos fuera de banda:**
    * *En persona:* El método absolutamente más seguro. Escanee físicamente el código QR en su dispositivo.
    * *VoIP/Vídeo cifrado:* Si la reunión física es imposible, llámelos a través de un canal cifrado independiente (por ejemplo, Wire, Matrix o correo electrónico cifrado con PGP) y lea los números en voz alta para confirmar que coinciden.
4. Una vez verificado, toque el botón **Marcar como verificado**. Si el número alguna vez cambia, Signal mostrará una pancarta roja de advertencia. *Detenga toda comunicación inmediatamente si esto ocurre.*

## 3. Minimización de datos: mensajes agresivos que desaparecen

Si su dispositivo es incautado mientras está desbloqueado (AFU - Después del primer desbloqueo), se podrá acceder a todos los mensajes descifrados. Debe aplicar una minimización agresiva de los datos.

* **La regla de los 5 minutos:** Para una planificación operativa activa y de alto riesgo, configure el temporizador de mensajes que desaparecen en **5 minutos o menos**.
* **Implementación:** Vaya a **Configuración** > **Privacidad** > **Temporizador predeterminado para nuevos chats**.
* *Justificación operativa:* Los mensajes que desaparecen garantizan que el "radio de explosión" de un dispositivo comprometido se limite a una ventana de conversación de 5 minutos, en lugar de meses de mapeo histórico de la red.

## 4. La vulnerabilidad de Signal Desktop

Vincular su cuenta de Signal móvil a una aplicación de escritorio (Windows, macOS o Linux) aumenta exponencialmente su superficie de ataque.

### El riesgo de la base de datos SQLite
Signal Desktop no utiliza los almacenes de claves respaldados por hardware (como Titan M) disponibles en los teléfonos inteligentes modernos.

1. **Almacenamiento local:** Signal Desktop almacena todos los mensajes localmente en un archivo de base de datos SQLite.
2. **La amenaza de extracción:** En Windows y macOS, la clave utilizada para cifrar esta base de datos local a menudo se almacena en el administrador de credenciales estándar del sistema operativo (Llavero/Administrador de credenciales). Si un adversario obtiene privilegios de ejecución local en su computadora a través de malware, o se apodera de la computadora portátil mientras está encendida, puede extraer trivialmente la clave de cifrado y volcar toda la base de datos SQLite no cifrada de sus comunicaciones.
3. **El mandato:** **No use Signal Desktop para operaciones de alto riesgo.** Si debe usar una computadora de escritorio para una comunicación segura, utilice un protocolo descentralizado como Matrix que se ejecuta dentro de una máquina virtual aislada y compartimentada (por ejemplo, dominio de "trabajo" del sistema operativo Qubes).

_Última actualización: 2026_

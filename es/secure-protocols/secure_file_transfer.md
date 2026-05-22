# Transferencia segura de archivos: infraestructura de exfiltración e ingestión

*Estado: Manual Administrativo de Infraestructura | Público: manejadores de fuentes, periodistas y operadores técnicos*

La exfiltración e ingestión de documentos altamente confidenciales (filtraciones, pruebas, imágenes sin editar) es la fase más peligrosa de cualquier operación. Los servicios en la nube estándar (Google Drive, Dropbox) están completamente comprometidos por el registro centralizado de metadatos y el cumplimiento de citaciones.

Como ingeniero de infraestructura, exijo que todas las transferencias de archivos se realicen a través de arquitecturas descentralizadas o físicamente aisladas diseñadas para eliminar las huellas de IP y la correlación entre remitente y receptor.

---

## 1. Compartir localmente sin conexión (para protestas y multitudes)

**Caso de uso:** Estás en una protesta o acción. El servicio celular está bloqueado, apagado o sospecha que la policía está usando Stingrays (captadores IMSI) para monitorear la red. Necesita compartir rápidamente una foto, un vídeo o un documento con un miembro del grupo de afinidad que esté a su lado.

**Cómo funciona:** Utiliza herramientas que dependen de conexiones locales de dispositivo a dispositivo (Bluetooth o creación de un punto de acceso Wi-Fi temporal) para transferir el archivo sin siquiera tocar Internet.

* **LocalSend (altamente recomendado):** LocalSend es una aplicación gratuita de código abierto disponible para iOS, Android, macOS, Windows y Linux. No requiere conexión a Internet ni cuenta. Ambos dispositivos deben estar en la misma red Wi-Fi local (un dispositivo puede crear un punto de acceso móvil y el otro se conecta a él, sin que los datos móviles estén activados). Es rápido y seguro.
* **Briar:** Aunque Briar es principalmente una aplicación de mensajería, también puede transferir archivos de igual a igual a través de Bluetooth. Es más lento que LocalSend pero no requiere configuración de Wi-Fi.
* **Una advertencia sobre AirDrop/Near Share:** AirDrop de Apple y Near Share de Android son convenientes pero tienen fallas de privacidad conocidas (transmiten nombres de dispositivos y, a veces, números de teléfono/ID de Apple a escáneres cercanos). Si los usa, configúrelos en "Solo contactos" y apáguelos por completo inmediatamente después de que se complete la transferencia. Nunca los dejes en "Todos".

---

## 2. OnionShare: enrutamiento P2P efímero

**Caso de uso:** Transferencia directa uno a uno a través de distancias geográficas donde ninguna de las partes desea revelar su dirección IP y no se confía en ningún servidor intermediario.

**La mecánica:** OnionShare activa temporalmente un servidor web localizado en su máquina y lo vincula a un servicio Tor V3 Onion. El archivo nunca sale de su computadora hasta que el destinatario lo descarga directamente a través de la red Tor.

### Ejecución operativa
1. **Implementación:** Abra OnionShare y seleccione **Compartir archivos**. Cargar los activos operativos.
2. **Configuración:** Asegúrese de que esté marcado **Dejar de compartir después de enviar los archivos**. Esto garantiza que el servicio se autodestruya en el momento en que se completa la transferencia, lo que evita ataques de reproducción o descubrimiento.
3. **Generación de dirección:** OnionShare generará una dirección `.onion` aleatoria y una clave privada de autenticación.
4. **Verificación fuera de banda (OOB):** El enlace `.onion` y la contraseña **nunca** deben enviarse a través del mismo canal que negoció la transferencia. Si aceptó la transferencia a través de Signal, envíe el enlace de OnionShare a través de un correo electrónico cifrado con PGP o un canal seguro de Matrix. Esto evita que un adversario que comprometa un canal intercepte tanto la intención como la carga útil.
5. **Terminación:** Una vez que el destinatario confirme la recepción, cierre OnionShare. La dirección `.onion` deja de existir.

---

## 3. SecureDrop: Arquitectura de ingesta institucional

**Caso de uso:** Una organización (ONG, sala de redacción, grupo de defensa cívica) necesita un método persistente y altamente seguro para recibir filtraciones anónimas sin comprometer la fuente ni infectar la red interna de la organización.

**La mecánica:** SecureDrop no es una aplicación única; es una arquitectura de red compleja y aislada por hardware que se ejecuta sobre Tor. Separa físicamente la fase de ingesta de red de la fase de visualización para derrotar el malware de día cero incrustado en los documentos enviados.

### La regla de aislamiento de hardware de cuatro niveles

Para ingerir archivos anónimos de forma segura, la organización debe implementar la siguiente arquitectura física:

1. **El servidor de aplicaciones (la página de inicio):**
    * *Función:* Este servidor mira a la red Tor. Aloja el sitio `.onion` donde la fuente sube el documento. Genera un "nombre en clave" criptográfico único para la fuente para permitir una comunicación segura bidireccional.
    * *Seguridad:* Inmediatamente encripta los documentos entrantes con la clave pública PGP de la organización. No posee la clave privada para descifrarlos.
2. **El servidor de monitorización:**
    * *Función:* Supervisa continuamente el servidor de aplicaciones en busca de intentos de intrusión o comportamientos inusuales.
3. **La Estación de Visualización Segura (SVS) - [Con espacio de aire]:**
    * *Función:* Esta es una computadora portátil dedicada, físicamente aislada que ejecuta Tails OS desde una unidad USB de solo lectura. Posee la clave privada PGP necesaria para descifrar los documentos. **Nunca** se conecta a internet.
    * *Protocolo:* Un operador técnico descarga los archivos cifrados desde el Servidor de Aplicaciones a un "USB de transferencia" cifrado. Llevan físicamente el USB de transferencia al SVS. Los archivos se descifran y se ven en el SVS. Si los archivos contienen malware de día cero diseñado para comunicarse a casa o exfiltrar datos, falla porque el SVS no tiene hardware de red.
4. **La Estación de Exportación:**
    * *Función:* Si un documento se verifica como seguro y necesario para la publicación, se le limpian en gran medida los metadatos (utilizando herramientas como MAT2 o Dangerzone) en el SVS, se mueve a un USB de exportación limpio y se transfiere a una máquina operativa estándar.

*Directiva: Omitir el protocolo Air-Gap al descargar y descifrar envíos de SecureDrop en una estación de trabajo conectada a Internet es una violación terminal de la seguridad de la organización.*

_Última actualización: 2026_

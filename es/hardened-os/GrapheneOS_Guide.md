# Guía: Endurecimiento posterior a la instalación de GrapheneOS

*Estado: Defensa de terminales de alto riesgo | Público: Objetivos de la explotación forense avanzada*

GrapheneOS es un sistema operativo móvil privado y seguro. Es una bifurcación reforzada del Proyecto de código abierto de Android (AOSP). Sin embargo, la instalación de la base es insuficiente contra la captura física por parte de adversarios T3/T4 equipados con modernas herramientas de extracción forense (por ejemplo, Cellebrite Premium, GrayKey).

Esta guía se centra exclusivamente en el **refuerzo posterior a la instalación** para garantizar que su dispositivo sobreviva la incautación física y permanezca en un estado que no sea explotable.

---

## 1. Lograr el dominio antes del primer desbloqueo (BFU)

Cuando un dispositivo está encendido pero aún no se ha desbloqueado con un PIN/contraseña, se encuentra en un estado "Antes del primer desbloqueo" (BFU). En BFU, las claves de cifrado permanecen cifradas de forma segura en el chip de hardware Titan M2. Las herramientas forenses modernas no pueden prácticamente forzar una contraseña alfanumérica segura mientras el dispositivo está en BFU.

Si el dispositivo se incauta mientras está desbloqueado, o después de haber sido desbloqueado una vez (después del primer desbloqueo o AFU), las claves de cifrado residen en la RAM del dispositivo, lo que hace que la extracción sea trivial. **Su objetivo es garantizar que el dispositivo regrese a BFU lo más rápido posible cuando no esté en uso.**

### Configurar reinicio automático
Fuerce el dispositivo a volver al estado BFU después de un breve período de inactividad.

1. Vaya a **Configuración** > **Seguridad** > **Reinicio automático**.
2. Configure el temporizador en **10 minutos** (máximo 30 minutos por necesidad operativa).
3. *Advertencia:* Debes memorizar tu contraseña principal. Si lo detienen y el dispositivo se reinicia automáticamente, el desbloqueo biométrico (huella digital) se desactiva.

### Implementar la aleatorización del diseño del PIN
Derrota los "ataques de manchas" (los análisis forenses mapean la grasa de los dedos en la pantalla) y la navegación visual por los hombros.

1. Navegue a **Configuración** > **Seguridad** > **Bloqueo de pantalla** (icono de engranaje).
2. Cambie **Diseño de PIN codificado** a **ACTIVADO**.
3. Asegúrese de que su bloqueo de pantalla sea un PIN aleatorio de al menos 6 dígitos, aunque una frase de contraseña alfanumérica de 12 caracteres es el estándar de oro.

---

## 2. Compartimentación avanzada: alcances y perfiles de almacenamiento

No otorgue permisos de almacenamiento global a ninguna aplicación, especialmente a clientes de mensajería o redes sociales.

### Aplicar alcances de almacenamiento
En lugar de otorgar "Permitir acceso a todos los archivos", utilice GrapheneOS Storage Scopes para alimentar a las aplicaciones con un sistema de archivos falso y muy restringido.

1. Navegue a la página **Información de la aplicación** de una aplicación > **Permisos** > **Fotos y videos**.
2. Seleccione **Configurar ámbitos de almacenamiento**.
3. Toque **Agregar archivo** o **Agregar carpeta** para incluir explícitamente en la lista blanca *solo* los medios específicos que la aplicación necesita para funcionar. La aplicación creerá que tiene acceso completo al almacenamiento, pero criptográficamente no ve nada que esté fuera del alcance.

### Perfiles multiusuario para aislamiento
Separe distintas personas operativas utilizando perfiles de usuario a nivel de hardware.

1. Vaya a **Configuración** > **Sistema** > **Múltiples usuarios**.
2. Cree perfiles separados (por ejemplo, "Comunicaciones", "OSINT", "Logística").
3. *Crucial:* Cambie **Enviar notificaciones al usuario actual** a **DESACTIVADO** para evitar la filtración de metadatos entre perfiles.
4. Los perfiles utilizan claves de cifrado independientes. Cuando un perfil secundario no está activo, sus datos están en reposo (BFU).

---

## 3. Implementación de Google Play en el espacio aislado

Algunas operaciones requieren aplicaciones propietarias (por ejemplo, plataformas VoIP cifradas específicas) que dependen de los servicios de Google Play para las notificaciones automáticas. GrapheneOS permite ejecutar Play Services como una aplicación estándar sin privilegios.

### Instalación sin privilegios
1. Abra el repositorio predeterminado de **Aplicaciones** en la pantalla de inicio de GrapheneOS.
2. Instale **Servicios de Google Play**, **Google Play Store** y **Marco de servicios de Google**.
3. Vaya a **Configuración** > **Aplicaciones** > **Servicios de Google Play** > **Permisos**.
4. Revocar *todos* los permisos (Ubicación, Contactos, Red, etc.).
5. Cambie **Sensores** a **DESACTIVADO** para evitar que el marco sondee los datos del giroscopio/acelerómetro para crear un perfil de patrón de vida físico.

---

## 4. Refuerzo de la red y la conectividad

Limite las emisiones de RF del dispositivo para evitar el seguimiento activo mediante receptores IMSI o balizas de monitoreo de multitudes.

### Desactivación de emisiones heredadas y en segundo plano
1. Navegue a **Configuración** > **Red e Internet** > **Internet** > [Su proveedor] (icono de engranaje).
2. Cambie **Permitir 2G** a **DESACTIVADO** para vencer los ataques estándar de degradación de Stingray.
3. Vaya a **Configuración** > **Ubicación** > **Servicios de ubicación**.
4. Cambie **Búsqueda de Wi-Fi** y **Búsqueda de Bluetooth** a **DESACTIVADO**. (Esto evita que el sistema operativo busque continuamente puntos de acceso cercanos incluso cuando Wi-Fi/Bluetooth están desactivados).
5. Vaya a **Configuración** > **Red e Internet**. Alterna **Apagar Wi-Fi automáticamente** y **Apagar Bluetooth automáticamente** durante las duraciones más cortas posibles.

### **Dispositivos compatibles**

GrapheneOS tiene requisitos de seguridad de hardware muy estrictos. Como resultado, **sólo es compatible oficialmente con teléfonos Google Pixel**.

A partir de 2026, esto generalmente incluye:
* Píxel 10, Píxel 10 Pro, Píxel 10 Pro XL, Píxel 10 Pro Fold, Píxel 10a
* Píxel 9, Píxel 9 Pro, Píxel 9 Pro XL, Píxel 9 Pro Fold, Píxel 9a
* Píxel 8, Píxel 8 Pro, Píxel 8a
* Píxel 7, Píxel 7 Pro, Píxel 7a
* Píxel 6, Píxel 6 Pro, Píxel 6a
* Pliegue de píxeles, tableta de píxeles

*Consulte siempre la [página de lanzamientos de GrapheneOS oficial](https://grapheneos.org/releases) para obtener la lista más actualizada antes de comprar un dispositivo.*

_Última actualización: 2026_

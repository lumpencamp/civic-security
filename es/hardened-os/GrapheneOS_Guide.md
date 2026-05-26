# Guía: Post-Instalación y Fortalecimiento de GrapheneOS

*Estado: Defensa de Dispositivos Terminales de Alto Riesgo | Audiencia: Objetivos de Explotación Forense Avanzada*

> [!CAUTION]
> **AVISO DE SEGURIDAD OPERATIVA Y LEGAL**
> Esta guía está destinada estrictamente para fines lícitos, defensivos y educativos. El fortalecimiento (hardening) del sistema operativo móvil personalizado es un mecanismo defensivo contra la explotación forense digital y física no autorizada. 
> - **Siempre** recuerde su frase de contraseña alfanumérica; las anulaciones biométricas se desactivan al reiniciar o bloquear el dispositivo.
> - **Nunca** use GrapheneOS para evadir actividades legítimas de las fuerzas del orden.
> - **Siempre** verifique el estado de bloqueo del gestor de arranque (bootloader) de su dispositivo.

GrapheneOS es un sistema operativo móvil privado y seguro. Es una bifurcación (fork) endurecida del Android Open Source Project (AOSP). Sin embargo, la instalación básica es insuficiente contra la captura física por parte de adversarios T3/T4 equipados con herramientas modernas de extracción forense (por ejemplo, Cellebrite Premium, GrayKey).

Esta guía se enfoca en el ciclo de vida completo: desde la instalación segura inicial hasta el fortalecimiento posterior a la instalación para garantizar que su dispositivo sobreviva a una incautación física y permanezca en un estado no explotable.

---

## 0. Guía de Instalación Segura

Instalar GrapheneOS es notablemente sencillo gracias al instalador oficial de WebUSB, pero se requiere un cumplimiento estricto del proceso para mantener el modelo de seguridad del hardware.

### 0.1 Requisitos
*   **Hardware:** Un dispositivo Google Pixel oficialmente compatible (consulte la Sección 9). Nunca compre un dispositivo bloqueado por un operador (por ejemplo, Verizon); el gestor de arranque no se puede desbloquear.
*   **Computadora Anfitriona:** Windows, macOS, Linux o ChromeOS.
*   **Navegador:** *Debe* usar un navegador basado en Chromium (Google Chrome, Microsoft Edge, Brave o Chromium) que soporte WebUSB. Firefox y Safari no funcionarán.
*   **Cable:** Un cable de datos de alta calidad (se recomienda el que vino con el teléfono).

### 0.2 El Proceso de Instalación
1.  **Habilitar el Desbloqueo OEM:** En su Pixel, vaya a *Configuración > Acerca del teléfono*. Toque el "Número de compilación" 7 veces para habilitar las Opciones de desarrollador. Regrese a *Configuración > Sistema > Opciones de desarrollador* y habilite **Desbloqueo de OEM** (OEM unlocking).
2.  **Arrancar en Fastboot:** Apague el teléfono, luego mantenga presionado el botón para Bajar Volumen mientras presiona el botón de Encendido hasta que aparezca el menú de Fastboot. Conecte el teléfono a su computadora.
3.  **Use el Instalador Web:** Vaya a [grapheneos.org/install/web](https://grapheneos.org/install/web) en su navegador Chromium.
4.  **Desbloquear el Gestor de Arranque:** Haga clic en el botón "Unlock bootloader" (Desbloquear gestor de arranque) en la página web. Aparecerá un mensaje en su teléfono; use las teclas de volumen para seleccionar "Unlock the bootloader" y presione el botón de encendido para confirmar.
5.  **Flashear el SO:** Haga clic en "Download release" (Descargar versión) en la página web, espere a que se descargue, y luego haga clic en "Flash release". No toque el dispositivo ni el cable durante este proceso.
6.  **Volver a Bloquear el Gestor de Arranque (CRÍTICO):** Una vez que se complete el flasheo, haga clic en "Lock bootloader" (Bloquear gestor de arranque) en la página web. Confirme la indicación en la pantalla de su teléfono. **Si no bloquea el gestor de arranque, no tendrá seguridad física. Un gestor de arranque desbloqueado permite manipulaciones triviales.**
7.  **Deshabilitar el Desbloqueo OEM:** Arranque GrapheneOS, omita inicialmente la configuración de Wi-Fi, vaya a Opciones de Desarrollador y deshabilite "Desbloqueo de OEM". Finalmente, deshabilite las Opciones de Desarrollador por completo.

### 0.3 Verificación de Arranque Seguro (Verified Boot)
GrapheneOS es compatible con Android Verified Boot, el cual garantiza que el SO no haya sido manipulado. Al encender el teléfono, debería ver brevemente una pantalla amarilla de advertencia que indica que el gestor de arranque está cargando un SO personalizado. Esto es normal y prueba que el gestor de arranque está bloqueado pero reconociendo las claves de firma de GrapheneOS.

---

## 1. Lograr Dominancia en el Estado "Antes del Primer Desbloqueo" (BFU)

Cuando un dispositivo está encendido pero aún no se ha desbloqueado con un PIN/contraseña, se encuentra en un estado "Before-First-Unlock" (BFU - Antes del Primer Desbloqueo). En BFU, las claves de cifrado permanecen firmemente encriptadas en el chip de hardware Titan M2. Las herramientas forenses modernas no pueden descifrar prácticamente por fuerza bruta una contraseña alfanumérica fuerte mientras el dispositivo esté en BFU.

Si el dispositivo es incautado estando desbloqueado, o después de que se haya desbloqueado al menos una vez (After-First-Unlock o AFU), las claves de cifrado residen en la memoria RAM del dispositivo, lo que hace que su extracción sea trivial. **Su objetivo es asegurar que el dispositivo regrese al estado BFU lo más rápido posible cuando no esté en uso.**

### Configurar Reinicio Automático (Auto-Reboot)
Fuerce al dispositivo a regresar al estado BFU después de un breve período de inactividad.
1.  Navegue a **Configuración > Seguridad > Reinicio automático** (Auto reboot).
2.  Establezca el temporizador en **10 Minutos** (máximo 30 minutos por necesidad operativa).
3.  *Advertencia:* Debe memorizar su código de acceso principal. Si es detenido y el dispositivo se reinicia automáticamente, el desbloqueo biométrico (huella dactilar) queda desactivado.

### Implementar Aleatorización de la Disposición del PIN
Derrote los ataques de "manchas" (forenses mapeando la grasa de los dedos en la pantalla) y la observación por encima del hombro.
1.  Navegue a **Configuración > Seguridad > Bloqueo de pantalla** (icono de engranaje).
2.  Active la opción **Aleatorizar disposición de PIN** (Scramble PIN layout).
3.  Asegúrese de que el bloqueo de su pantalla sea un PIN aleatorio de al menos 6 dígitos, aunque una frase de contraseña alfanumérica de 12 caracteres es el estándar de oro.

---

## 2. Compartimentación Avanzada: Alcances de Almacenamiento y Perfiles

No otorgue permisos de almacenamiento globales a ninguna aplicación, especialmente a clientes de mensajería o redes sociales.

### Hacer Cumplir los Alcances de Almacenamiento (Storage Scopes)
En lugar de otorgar "Permitir el acceso a todos los archivos", utilice los *Storage Scopes* de GrapheneOS para alimentar a las aplicaciones con un sistema de archivos falso y fuertemente restringido.
1.  Navegue a la página de **Información de la aplicación** (App Info) de una aplicación > **Permisos > Fotos y videos**.
2.  Seleccione **Configurar alcances de almacenamiento** (Configure Storage Scopes).
3.  Toque **Agregar archivo** o **Agregar carpeta** para poner en una lista blanca de manera explícita *solo* los medios específicos que la aplicación necesita para funcionar. La aplicación creerá que tiene acceso completo al almacenamiento, pero está criptográficamente ciega ante cualquier cosa fuera de ese alcance.

### Perfiles Multiusuario para el Aislamiento
Separe las distintas personas operativas utilizando perfiles de usuario a nivel de hardware.
1.  Navegue a **Configuración > Sistema > Varios usuarios** (Multiple users).
2.  Cree perfiles separados (por ejemplo, "Comunicaciones", "OSINT", "Logística").
3.  *Crucial:* Desactive la opción **Enviar notificaciones al usuario actual** (Send notifications to current user) para evitar la fuga de metadatos entre perfiles.
4.  Los perfiles utilizan claves de cifrado independientes. Cuando un perfil secundario no está activo, sus datos están en reposo (estado BFU).

---

## 3. Implementación Aislada (Sandboxed) de Google Play

Algunas operaciones requieren aplicaciones propietarias (por ejemplo, plataformas específicas de VoIP encriptadas) que dependen de los Servicios de Google Play para las notificaciones automáticas (push). GrapheneOS permite ejecutar los Servicios de Play como una aplicación estándar sin privilegios.

### Instalación con Cero Privilegios
1.  Abra el repositorio de **Aplicaciones** predeterminado en la pantalla de inicio de GrapheneOS.
2.  Instale los **Servicios de Google Play**, la **Google Play Store** y el **Marco de Servicios de Google** (Google Services Framework).
3.  Navegue a **Configuración > Aplicaciones > Servicios de Google Play > Permisos**.
4.  Revoque *todos* los permisos (Ubicación, Contactos, Red, etc.).
5.  Desactive **Sensores** para evitar que el marco de servicios recolecte datos del giroscopio/acelerómetro para construir un perfil de patrón de vida físico.

---

## 4. Fortalecimiento de Conectividad y Redes

Limite las emisiones de radiofrecuencia (RF) del dispositivo para evitar el seguimiento activo a través de captadores de IMSI o balizas de monitoreo de multitudes.

### Desactivación de Emisiones Heredadas y en Segundo Plano
1.  Navegue a **Configuración > Red e internet > Internet > [Su Operador]** (icono de engranaje).
2.  Desactive **Permitir 2G** para evitar los ataques estándar de degradación de Stingray.
3.  Navegue a **Configuración > Ubicación > Servicios de ubicación**.
4.  Desactive **Búsqueda de Wi-Fi** y **Búsqueda de Bluetooth**. (Esto evita que el SO busque continuamente puntos de acceso cercanos incluso cuando el Wi-Fi/Bluetooth están apagados).
5.  Navegue a **Configuración > Red e internet**. Configure **Apagar Wi-Fi automáticamente** y **Apagar Bluetooth automáticamente** en las duraciones más cortas posibles.

### Mezcla de Conexiones y Aleatorización de MAC
Por defecto, GrapheneOS implementa una fuerte aleatorización de la dirección MAC por cada conexión. Verifique que esté activa:
1. Navegue a **Configuración > Red e internet > Internet**.
2. Toque el ícono de engranaje de una red Wi-Fi guardada, vaya a **Privacidad**, y asegúrese de que esté configurado en **Usar MAC aleatoria**.
3. Nota: GrapheneOS va más allá que AOSP al implementar el anonimato de DHCP, lo que evita que el nombre de host (hostname) de su dispositivo se filtre a las redes locales.

---

## 5. Indicadores de Cámara y Micrófono

GrapheneOS incluye indicadores de privacidad respaldados por hardware para alertarle de inmediato si una aplicación intenta una grabación encubierta.

*   Cuando cualquier aplicación accede al micrófono o la cámara, un punto o ícono verde aparecerá de forma persistente en la esquina superior derecha de la barra de estado.
*   **Interruptores de Sensores:** Puede deshabilitar globalmente la cámara y el micrófono a través de los recuadros del menú de Configuración Rápida. Esto corta el acceso a nivel del sistema operativo, lo que significa que incluso las aplicaciones del sistema no pueden acceder a los sensores hasta que se vuelvan a activar.
*   **Auditoría de Acceso:** Vaya a **Configuración > Privacidad > Panel de privacidad** para ver una línea de tiempo cronológica de qué aplicaciones solicitaron exactamente acceso a la Ubicación, Cámara o Micrófono en las últimas 24 horas.

---

## 6. Funciones de Protección contra Exploits

GrapheneOS integra bajo el capó masivas mitigaciones de vulnerabilidades que evitan que los ataques de día cero tengan éxito. No necesita configurar esto; están activados de forma predeterminada.

*   **Hardened Malloc (Asignador de memoria fortalecido):** GrapheneOS reemplaza el asignador de memoria estándar de Android con una versión fortalecida diseñada para bloquear la aplicación inmediatamente si se desencadena una vulnerabilidad de corrupción de memoria (como un desbordamiento del búfer). Esto convierte un grave exploit de ejecución remota de código en un inofensivo bloqueo de aplicación.
*   **Ejecución de Procesos (Exec Spawning):** A diferencia del Android estándar que bifurca nuevos procesos desde un "Cigoto" central (compartiendo el mismo espacio de diseño de memoria, facilitando los exploits), GrapheneOS genera procesos nuevos para asegurar una fuerte Aleatorización del Diseño del Espacio de Direcciones (ASLR).
*   **MTE (Extensión de Etiquetado de Memoria):** En dispositivos Pixel 8 y más nuevos, GrapheneOS es compatible con ARM MTE acelerado por hardware. Esto detecta y bloquea fallas de seguridad de memoria a nivel del hardware de la CPU en tiempo real, neutralizando efectivamente clases enteras de vulnerabilidades de corrupción de memoria sin penalizaciones graves de rendimiento.

---

## 7. Configuración de Aplicaciones Recomendadas

Dado que probablemente no utilizará directamente la Google Play Store, debe confiar en repositorios seguros de código abierto.

### F-Droid y Repositorios Alternativos
1.  Descargue el APK de **F-Droid** desde fdroid.org.
2.  Agregue repositorios confiables de terceros:
    *   **DivestOS Repo:** Ofrece versiones fortalecidas (forks) de aplicaciones comunes (por ejemplo, el navegador Mull).
    *   **Guardian Project Repo:** Mantiene Orbot y otras herramientas de comunicación de alto riesgo.

### Conjunto de Herramientas Recomendado
*   **Navegador:** **Vanadium** (incorporado en GrapheneOS). Es una versión fortalecida de Chromium que implementa un estricto aislamiento de sitios. No use Firefox en Android, ya que carece de aislamiento de procesos por sitio.
*   **Comunicaciones:** **Signal** (descargue el APK directamente desde signal.org o use la Play Store en su caja de arena (Sandbox) para recibir actualizaciones oportunas).
*   **Anonimato:** **Orbot** (proxy de Tor) para enrutar aplicaciones específicas a través de la red Tor.
*   **Navegación:** **OsmAnd~** (a través de F-Droid) para mapas fuera de línea y sin rastreo. Descargue los datos de mapas de su región por Wi-Fi.
*   **2FA y Contraseñas:** **Aegis Authenticator** para tokens TOTP y **KeePassDX** para la administración de contraseñas.
*   **Cámara:** La aplicación de cámara predeterminada de GrapheneOS elimina todos los metadatos EXIF (GPS, información del dispositivo, marcas de tiempo) de fotos y videos de forma predeterminada. Úsela para toda fotografía operativa.

---

## 8. Guía de Decisión: GrapheneOS vs. CalyxOS

Ambos sistemas operativos son excelentes, pero sirven a modelos de amenazas diferentes.

| Característica | GrapheneOS | CalyxOS |
| :--- | :--- | :--- |
| **Enfoque Principal** | Seguridad absoluta, mitigación de exploits, sandboxing | Privacidad, "des-Googlear", amplia usabilidad de aplicaciones |
| **Servicios de Google** | Play Services en un entorno aislado (Sandboxed, se ejecuta como una aplicación normal, sin privilegios) | microG (reimplementación de código abierto de los Servicios de Google) |
| **Modelo de Amenazas** | Objetivos de actores estatales, periodistas de investigación de alto riesgo (T3/T4) | Defensores de la privacidad, organizadores generales que evitan la vigilancia comercial (T2/T3) |
| **Defensa de Exploits** | Líder en la industria (Hardened Malloc, MTE, Exec Spawning) | Nivel estándar de AOSP |
| **Usabilidad** | Alta fricción (algunas aplicaciones principales no funcionarán correctamente) | Baja fricción (microG engaña a la mayoría de las aplicaciones para que funcionen normalmente) |
| **Dispositivos Compatibles** | Solo Google Pixels | Pixels, Fairphone, selectos Motorola |
| **Veredicto** | Elija este si su vida o libertad dependen de la integridad del dispositivo. | Elija este si desea la máxima privacidad sin sacrificar la comodidad diaria. |

---

## 9. Dispositivos Compatibles y Ciclo de Vida del Dispositivo (Mayo 2026)

GrapheneOS tiene estándares de seguridad de hardware altamente rigurosos, que incluyen requisitos para un enclave de hardware seguro (Titan M2), atestación remota basada en hardware y etiquetado de memoria por hardware (MTE) [GrapheneOS Supported Devices, https://grapheneos.org/faq#supported-devices, May 2026]. En consecuencia, **solo es compatible oficialmente con dispositivos Google Pixel**.

A partir de **Mayo de 2026**, el catálogo de dispositivos oficialmente compatibles incluye:
*   **Serie Pixel 10:** Pixel 10, Pixel 10 Pro, Pixel 10 Pro XL, Pixel 10 Pro Fold, Pixel 10a
*   **Serie Pixel 9:** Pixel 9, Pixel 9 Pro, Pixel 9 Pro XL, Pixel 9 Pro Fold, Pixel 9a
*   **Serie Pixel 8:** Pixel 8, Pixel 8 Pro, Pixel 8a
*   **Serie Pixel 7:** Pixel 7, Pixel 7 Pro, Pixel 7a
*   **Serie Pixel 6 (Advertencia Crítica de Fin de Vida - EOL):** Pixel 6, Pixel 6 Pro, Pixel 6a
*   **Otros Factores de Forma:** Pixel Fold, Pixel Tablet

> [!WARNING]
> **Alerta EOL Serie Pixel 6 (Octubre de 2026)**
> Las actualizaciones de seguridad garantizadas de software y firmware de Google para los Pixel 6, 6 Pro y 6a terminarán en **Octubre de 2026**. Después de esta fecha, GrapheneOS ya no puede recibir parches críticos de firmware de proveedor propietario (blobs) para estos dispositivos, lo que significa que la serie Pixel 6 llegará al Fin de Vida (End of Life - EOL) en GrapheneOS. **Para operaciones seguras de alto riesgo, migre a un hardware Pixel 7 o más reciente antes de octubre de 2026.**

*Siempre verifique su modelo en la [página oficial de lanzamientos de GrapheneOS](https://grapheneos.org/releases) antes de comprar un dispositivo.*

[← Volver al Índice](../index.md)

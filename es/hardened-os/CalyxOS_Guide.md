# Guía: Post-Instalación y Fortalecimiento de CalyxOS

*Estado: Ingeniería de Privacidad Móvil | Audiencia: Activistas Conscientes de la Privacidad*

> [!CAUTION]
> **AVISO DE SEGURIDAD OPERATIVA Y LEGAL**
> CalyxOS proporciona un equilibrio fundamental entre privacidad y usabilidad de software. El fortalecimiento (hardening) de este sistema operativo es una medida defensiva para mitigar la telemetría comercial y el rastreo celular.
> - **Siempre** verifique que su operador de telefonía móvil permita el desbloqueo del gestor de arranque (bootloader) OEM antes de comprar un dispositivo (Verizon en los EE. UU. bloquea el desbloqueo).
> - **Nunca** confíe en MicroG para comunicaciones con metadatos completamente nulos (zero-metadata).
> - **Siempre** mantenga su sistema actualizado para recibir los parches de seguridad mensuales.

CalyxOS ofrece un puente vital entre la seguridad absoluta (GrapheneOS) y la usabilidad diaria. Está diseñado para eliminar la vigilancia corporativa generalizada manteniendo al mismo tiempo la compatibilidad con las aplicaciones necesarias. Sin embargo, para maximizar su potencial, debe configurar activamente sus herramientas de privacidad integradas.

Este manual detalla todo el proceso: instalación, configuración de microG, filtrado de red (firewalling) mediante Datura y el establecimiento de un flujo de trabajo de copias de seguridad seguro.

---

## 0. Guía de Instalación Segura

CalyxOS proporciona una utilidad de línea de comandos simplificada llamada "Device Flasher" (Flasheador de Dispositivos) para hacer que la instalación sea lo más segura y libre de errores posible.

### 0.1 Requisitos Previos
*   **Hardware:** Un dispositivo oficialmente compatible (Google Pixel, Fairphone o Motorola compatible — consulte la Sección 9). **Asegúrese de que esté desbloqueado de fábrica.**
*   **Computadora Anfitriona:** Windows, macOS o Linux.
*   **Cable:** Un cable de datos USB-C de alta calidad.

### 0.2 El Proceso del Flasheador
1.  **Habilitar el Desbloqueo OEM:** En su dispositivo, vaya a *Configuración > Acerca del teléfono*. Toque el "Número de compilación" 7 veces para habilitar las Opciones de desarrollador. Regrese a *Configuración > Sistema > Opciones de desarrollador* y habilite **Desbloqueo de OEM** y **Depuración por USB**.
2.  **Descargar el Flasheador:** Navegue a [calyxos.org/install](https://calyxos.org/install/) en su computadora y descargue el Device Flasher para su sistema operativo.
3.  **Ejecutar la Utilidad:** Conecte su teléfono a la computadora. Abra una terminal (macOS/Linux) o un Símbolo del Sistema (Windows) y ejecute el archivo ejecutable descargado.
4.  **Seguir las Indicaciones en Pantalla:** El Flasheador detectará automáticamente su dispositivo, descargará la imagen de fábrica correcta y lo guiará para reiniciar en el gestor de arranque.
5.  **Desbloquear el Gestor de Arranque:** Cuando se le solicite en la pantalla del teléfono, use las teclas de volumen para seleccionar "Unlock the bootloader" y presione el botón de encendido para confirmar.
6.  **Flashear y Volver a Bloquear:** La utilidad flasheará CalyxOS. **De manera crucial, se le pedirá que bloquee el gestor de arranque al final del proceso.** Usted debe confirmar esto en el teléfono. Dejar el gestor de arranque desbloqueado compromete todo el modelo de seguridad del dispositivo.

---

## 1. Firewall Datura: Redes de Denegación por Defecto (Default-Deny)

El cortafuegos Datura Firewall es la herramienta integrada más poderosa de CalyxOS. Por defecto, las aplicaciones comerciales intentarán conectarse a internet para recopilar analíticas, descargar anuncios y reportar su dirección IP. Su postura debe ser la de **Denegación por Defecto**.

### Configuración Granular de Aplicaciones
Debe incluir en la lista blanca (whitelist) el acceso a la red para las aplicaciones de forma manual.
1.  Navegue a **Configuración > Red e internet > Datura Firewall**.
2.  **La Postura Predeterminada:** Deshabilite "Datos en segundo plano" (Background data) globalmente para todas las aplicaciones no esenciales.
3.  **Configuración por Aplicación:** Para aplicaciones como la cámara, la calculadora o el lector de documentos fuera de línea (por ejemplo, CryptPad fuera de línea), deshabilite **todo** el acceso a la red (Wi-Fi, Datos móviles y VPN). Una herramienta fuera de línea no tiene ninguna razón legítima para comunicarse con un servidor remoto.
4.  **Aislamiento de Red:** Si una aplicación requiere acceso a Internet, pero solo desea que se sincronice cuando esté seguro, restrínjala a "Solo Wi-Fi" (evitando que use datos celulares mientras está en tránsito) o "Solo VPN" (asegurando que no pueda filtrar su verdadera IP si la VPN se cae).

---

## 2. Configuración y Mitigación de Riesgos de MicroG

MicroG es el reemplazo de código abierto de los Servicios de Google Play. Permite que las notificaciones push y los servicios de ubicación funcionen sin otorgar a Google privilegios profundos en el sistema. Sin embargo, MicroG sigue comunicándose con los servidores de Google. Debe configurarlo para minimizar esta telemetría.

### Los Riesgos de MicroG
Cuando MicroG está completamente habilitado, su dispositivo registra un identificador único con Google para recibir Mensajería en la Nube (notificaciones push). Esto crea un rastro de metadatos que conecta su dirección IP con su dispositivo.

### Fortalecimiento de la Configuración
1.  Abra la aplicación de **Configuración de MicroG**.
2.  **Registro del Dispositivo:** Deshabilite esto a menos que sea absolutamente necesario. Si está deshabilitado, las aplicaciones no pueden utilizar los servidores de Google para las notificaciones push. (Nota: Las aplicaciones seguras como Signal utilizan sus propias conexiones WebSocket y *no* necesitan MicroG para recibir mensajes).
3.  **Mensajería en la Nube (Cloud Messaging):** Si *debe* usar una aplicación patentada que requiera notificaciones push (por ejemplo, un cliente de correo electrónico seguro específico o una aplicación bancaria), habilite Cloud Messaging.
    *   *Mitigación:* Toque los tres puntos (menú) en Cloud Messaging y vaya a **Avanzado**. Aumente el "Intervalo de ping" (Ping interval) para reducir la frecuencia con la que su dispositivo se comunica con el servidor.
4.  **Google SafetyNet:** Asegúrese de que esté **Deshabilitado**. Es un servicio de atestación remota que envía perfiles de hardware del dispositivo a Google.
5.  **Módulos de Ubicación:** Deshabilite el backend de "Google Location Service". Confíe únicamente en Mozilla Location Service (MLS) o DejaVu para búsquedas de ubicación sin conexión de Wi-Fi/Torres celulares que respeten la privacidad.

---

## 3. El Botón de Pánico: Flujo de Trabajo de Despliegue de Emergencia

El Botón de Pánico (Panic Button) es un "interruptor de hombre muerto" diseñado para asegurar rápidamente su dispositivo durante una detención física o una amenaza inminente.

### Flujo de Trabajo de Despliegue
Debe configurar el Botón de Pánico *antes* de una acción. No espere hasta estar detenido.
1.  Abra la aplicación **Panic Button** desde el cajón de aplicaciones.
2.  **Configurar el Disparador:** Configure el mecanismo de activación (por ejemplo, presionar rápidamente el botón de encendido 5 veces o presionar una combinación específica de botones de volumen).
3.  **Mapear las Acciones:** Seleccione exactamente lo que hará el Botón de Pánico cuando se active.
    *   *Nivel de Amenaza T2 (Protesta / Control de Multitudes):* Asigne el botón a **Desinstalar Aplicaciones Específicas** (por ejemplo, borrar instantáneamente Signal, Element o su administrador de contraseñas) y **Ocultar Aplicaciones Seleccionadas**.
    *   *Nivel de Amenaza T3/T4 (Incautación Dirigida):* Asigne el botón a **Enviar SMS de Emergencia** (notificando a su contacto de apoyo en la cárcel con sus coordenadas) seguido inmediatamente por un **Apagado del Dispositivo**.
4.  **¿Por qué el Apagado?** Un apagado completo del dispositivo fuerza al teléfono de regreso al estado altamente seguro "Antes del Primer Desbloqueo" (BFU), encriptando las claves de sus datos y bloqueando a las herramientas de extracción forense como Cellebrite.

---

## 4. Copia de Seguridad Cifrada de SeedVault

Cuando se opera en entornos de alto riesgo, la pérdida física del dispositivo (confiscación o destrucción) es muy probable. CalyxOS incluye **SeedVault**, una solución de copia de seguridad totalmente cifrada y que respeta la privacidad, integrada directamente en el SO.

### Configuración
1.  Navegue a **Configuración > Sistema > Copia de seguridad**.
2.  SeedVault generará una **frase de recuperación de 12 palabras**. Escríbala en papel físico y guárdela en un lugar seguro (por ejemplo, una caja fuerte física). Si pierde esta frase, sus copias de seguridad serán permanentemente irrecuperables.
3.  **Destino de la Copia de Seguridad (Local vs. Nube):**
    *   *Alta Seguridad (USB Local):* Conecte una unidad flash USB-C. Indique a SeedVault que realice la copia de seguridad directamente en la unidad flash. Esto mantiene sus datos completamente fuera de Internet.
    *   *Alta Disponibilidad (Nextcloud):* Si ejecuta una instancia segura y autohospedada de Nextcloud, puede configurar SeedVault para que cifre la copia de seguridad localmente y cargue el texto cifrado (ciphertext) directamente a su almacenamiento en la nube.

---

## 5. Configuración de Aurora Store

Como no tiene la Google Play Store, necesita una forma de descargar aplicaciones convencionales (como la de un banco local o aplicación de transporte público) sin tener que iniciar sesión en una cuenta de Google.

### Uso Anónimo de Aurora Store
Aurora Store es un cliente de código abierto que interactúa con los servidores de Google Play.
1.  Abra **Aurora Store** (preinstalada en CalyxOS).
2.  Cuando se le pregunte cómo iniciar sesión, **seleccione siempre Anónimo**. Aurora Store utiliza un grupo de cuentas compartidas para solicitar los archivos APK de Google sin vincular la solicitud a su identidad personal.
3.  **Falsificación (Spoofing):** Puede entrar a la configuración de Aurora y "falsificar" el modelo de su dispositivo o ubicación si una aplicación afirma ser incompatible con su dispositivo.

---

## 6. Conjunto de Aplicaciones Recomendado

CalyxOS viene preconfigurado con varias aplicaciones de privacidad. Auméntelas con el siguiente grupo, totalmente disponible a través de F-Droid o Aurora Store:

*   **Navegador:** **Cromite** o **Mull**. Ambos son navegadores de privacidad reforzados. Cromite está basado en Chromium (excelente aislamiento de sitios); Mull se basa en Firefox (excelente protección contra el rastreo a través del user.js de arkenfox).
*   **Comunicaciones:** **Signal** (para mensajería sincrónica) y **Element** (para chat descentralizado Matrix).
*   **Anonimato:** **Orbot** (para enrutar el tráfico a través de Tor).
*   **Navegación:** **OsmAnd~** (para mapas fuera de línea).
*   **Autenticación:** **Aegis Authenticator** (administrador encriptado TOTP).
*   **Contraseñas:** **KeePassDX** (administrador de contraseñas fuera de línea).
*   **Medios/Privacidad:** **Scrambled Exif** (elimina los metadatos de las fotos antes de compartirlas) y **NewPipe** (cliente de YouTube que respeta la privacidad, no requiere cuenta y bloquea anuncios).

---

## 7. CalyxOS vs. GrapheneOS: La Matriz de Decisión

Si bien ambos eliminan el software espía comercial, tienen objetivos arquitectónicos fundamentalmente diferentes.

| Característica | CalyxOS | GrapheneOS |
| :--- | :--- | :--- |
| **Filosofía** | "Privacidad por Defecto, Usabilidad Intacta" | "Seguridad Absoluta y Mitigación de Exploits" |
| **Reemplazo de Servicios de Google** | microG (engaña a las aplicaciones para que piensen que existen los Servicios de Play, con alguna fuga de metadatos) | Servicios de Play Aislados / Sandboxed (ejecuta código de Google de forma segura en una jaula sin privilegios) |
| **Soporte de Dispositivos** | Pixels, Fairphone, Motorola | Solo Google Pixels |
| **Usabilidad / Fricción** | Extremadamente baja. Casi todas las aplicaciones principales funcionan perfectamente desde el primer momento. | Alta. Algunas aplicaciones colapsarán o se negarán a ejecutarse sin la integración nativa de Google. |
| **Ajuste al Modelo de Amenazas** | Perfecto para organizadores que evitan la vigilancia comercial masiva y el rastreo policial local generalizado (T2/T3). | Necesario para periodistas o disidentes atacados por actores de estado-nación con exploits de día cero (T3/T4). |

---

## 8. Actualizaciones y Mantenimiento

CalyxOS maneja las actualizaciones inalámbricas (OTA - Over-The-Air) de forma automática. Es fundamental que no posponga estas actualizaciones.

*   **Parches de Seguridad:** CalyxOS generalmente envía los parches de seguridad mensuales de Android Open Source Project (AOSP) a los pocos días de que Google los haya lanzado.
*   **Verificación:** Las actualizaciones están firmadas criptográficamente por el Calyx Institute. Su dispositivo verificará automáticamente la firma antes de aplicar la actualización en segundo plano. Simplemente reinicie cuando se le solicite.

---

## 9. Dispositivos Compatibles y Ciclo de Vida (Mayo de 2026)

CalyxOS es oficialmente compatible con Google Pixel, Fairphone y algunos dispositivos Motorola que permiten volver a bloquear el gestor de arranque de forma segura.

A partir de **Mayo de 2026**, el catálogo de dispositivos compatibles incluye:
*   **Google Pixel:** Serie Pixel 6, serie 7, serie 8, serie 9 (incluidos Fold y Tablet) y los recién lanzados **Pixel 9a** y **Serie Pixel 10** (Pixel 10, 10 Pro, 10 Pro XL, 10 Pro Fold, 10a).
*   **Fairphone:** Fairphone 4 y **Fairphone 5**.
*   **Motorola:** moto g 5G (2024), moto g84 5G, moto g34 5G, moto g45 5G, moto g52, moto g42 y moto g32.
*   **Próximo Soporte:** SHIFTphone 8.

> [!WARNING]
> **Advertencia de Desbloqueo del Gestor de Arranque OEM del Operador**
> Para instalar CalyxOS, debe poder desbloquear el gestor de arranque (bootloader) de su dispositivo. Muchos dispositivos comercializados por operadores de telefonía, y muy particularmente los **Google Pixels de la marca Verizon** en los Estados Unidos, prohíben por completo el desbloqueo del gestor de arranque a nivel de hardware. **No compre dispositivos Pixel bloqueados por el operador o de la marca Verizon para instalaciones de sistemas operativos personalizados.** Adquiera siempre dispositivos desbloqueados de fábrica directamente del fabricante.

*Verifique la compatibilidad del modelo en la [página oficial de soporte de dispositivos de CalyxOS](https://calyxos.org/docs/guide/device-support/) antes de comprar.*

[← Volver al Índice](../index.md)

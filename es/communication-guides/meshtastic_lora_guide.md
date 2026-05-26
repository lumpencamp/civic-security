# Meshtastic y LoRa: Comunicaciones Descentralizadas Fuera de la Red

> [!CAUTION]
> **AVISO LEGAL Y DE SEGURIDAD OPERACIONAL**
> Esta guía está destinada estrictamente a fines lícitos, defensivos y educativos. Algunas tácticas detalladas a continuación (como la ofuscación celular o la organización de protestas) pueden conllevar graves riesgos legales dependiendo de su jurisdicción local.
> - **Nunca** se resista al arresto ni obstruya físicamente a las fuerzas del orden.
> - **Nunca** participe en la interferencia ilegal de radiofrecuencia (RF jamming) ni en daños a la propiedad.
> - **Siempre** consulte a las redes locales de defensa legal (por ejemplo, el National Lawyers Guild) para obtener asesoramiento específico de su jurisdicción.

*Estado: Manual de Ingeniería de RF y Despliegue | Audiencia: Arquitectos de Redes y Equipos Tácticos de Comunicaciones*

Cuando actores estatales desactivan las redes celulares (o debe asumir que toda la infraestructura de telecomunicaciones está comprometida), las operaciones requieren una capa de comunicación secundaria y descentralizada. LoRa (Long Range) es un protocolo de radio de ancho de banda bajo y consumo ultrabajo que opera en la banda ISM (por ejemplo, 915 MHz en EE. UU., 868 MHz en Europa).

Combinado con el firmware de código abierto Meshtastic, permite el despliegue de una red en malla (mesh network) de mensajería de texto peer-to-peer completamente desvinculada de los ISP corporativos y las redes celulares. Esta guía detalla el despliegue técnico y las graves vulnerabilidades de SIGINT (Inteligencia de Señales) de una malla táctica LoRa.

---

## 1. Selección de Hardware y Flasheo de Firmware

Confíe en hardware construido alrededor del moderno transceptor LoRa Semtech SX1262. Los chips más antiguos (como el SX1276) tienen una sensibilidad inferior y un mayor consumo de energía.

### Tipos de Nodos Recomendados
*   **Nodos Operativos Móviles:** LILYGO T-Echo, Heltec V3 o LILYGO T-Beam. Estos son nodos del tamaño de un bolsillo, alimentados por batería, que se emparejan con su teléfono inteligente a través de Bluetooth.
*   **Nodos Repetidores Estacionarios:** RAK Wireless WisBlock (nRF52840). Estos consumen cantidades microscópicas de energía, lo que los hace ideales para relés alimentados por energía solar montados en techos o colinas para puentear la malla.

### Proceso de Despliegue
1.  Conecte la placa de radio a su computadora a través de un cable USB con capacidad de transferencia de datos.
2.  Navegue a `flasher.meshtastic.org` en un navegador basado en Chromium (Chrome, Edge, Brave).
3.  Seleccione el modelo de su dispositivo, el firmware estable más reciente y haga clic en Flashear (Flash).
4.  Una vez flasheado, instale la aplicación Meshtastic en su dispositivo Android o iOS bastionado y empareje con la radio a través de Bluetooth.

**Restricción Operativa:** **No utilice la configuración predeterminada del canal "LongFast" para operaciones cívicas de alto riesgo.** El canal predeterminado es público, no está cifrado y está altamente congestionado.

---

## 2. Configuración del Canal Criptográfico

Para asegurar la malla, debe establecer un canal cerrado y autenticado que utilice cifrado AES-256.

1.  **Generación de Claves:** Usando la aplicación móvil Meshtastic, navegue hasta Configuración del Canal (Channel Settings). Cree un nuevo canal (por ejemplo, "Equipo_OpSec_1") y configure el cifrado en **AES256**. El software generará una clave criptográfica de 256 bits.
2.  **Designación de Roles:** Configure su rol principal de canal. Los canales públicos secundarios se pueden dejar activados para un enrutamiento genérico, pero el tráfico operativo debe dirigirse al canal AES256.
3.  **Distribución Fuera de Banda (OOB):** *Nunca* transmita la URL de configuración del canal o el código QR a través del canal público LoRa o mediante SMS estándar. La clave debe distribuirse fuera de banda a través de Signal, un chat cifrado en Matrix o escaneando el código QR físicamente en persona.

---

## 3. La Vulnerabilidad del Encabezado no Cifrado

Si bien Meshtastic utiliza el cifrado AES-256-CTR para las cargas útiles de los mensajes (el texto real que escribe), la arquitectura de red requiere que ciertos metadatos de enrutamiento se transmitan en texto claro.

Para permitir que la malla funcione, los nodos deben poder enrutar paquetes incluso si no poseen la clave de descifrado. Esta capacidad de "relé ciego" (blind relay) significa que el encabezado del paquete siempre está sin cifrar.

| Punto de Datos | ¿Cifrado? | Ubicación |
| :--- | :--- | :--- |
| **ID del Nodo Remitente** | No | Encabezado del Paquete |
| **ID de Destino** | No | Encabezado del Paquete |
| **Límite de Saltos (Hop Limit) / Enrutamiento** | No | Encabezado del Paquete |
| **Hash del Canal** | No | Encabezado del Paquete |
| **Contenido del Mensaje** | Sí | Carga Útil (AES-256) |
| **Ubicación GPS** | Sí | Carga Útil (AES-256) |
| **Nombres de Nodos** | Sí | Carga Útil (AES-256) |

---

## 4. La Amenaza: Escucha Pasiva y SIGINT

Debido a que los encabezados se transmiten en texto claro, un adversario no necesita descifrar su cifrado para comprender su red.

1.  **Análisis de Tráfico:** Un oyente pasivo utilizando Radios Definidas por Software (SDR) económicas o su propio nodo Meshtastic puede mapear la topología exacta de su red. Pueden ver qué nodos actúan como concentradores centrales, quién se comunica con quién y la frecuencia de esas comunicaciones.
2.  **Identificación de Hardware (Fingerprinting):** El ID del Nodo (por ejemplo, `!a1b2c3d4`) se deriva directamente de la dirección MAC codificada en el hardware de la radio. Debido a que este ID está en el encabezado no cifrado, una vez que un adversario correlaciona un ID de Nodo específico con una persona o ubicación específica, puede rastrear esa radio cada vez que transmite.
3.  **Triangulación Física (Fox Hunting):** Cada transmisión es una baliza. Usando antenas direccionales o un conjunto distribuido de SDR calculando la Diferencia de Tiempo de Llegada (TDOA), un adversario puede triangular físicamente el origen de la señal de RF, localizando al operador en tiempo real.

---

## 5. Pautas Obligatorias de OpSec

Si se enfrenta a actores de amenazas sofisticados (Policía Antidisturbios T2, Agentes Federales T3), siga explícitamente estas reglas:

*   **Desactive el GPS:** Desactive toda la transmisión automática de GPS y posición en la configuración de la aplicación. Aunque los datos GPS están cifrados en la carga útil, la transmisión continua actúa como una baliza de RF constante, haciendo que la triangulación física sea trivial. Además, Meshtastic carece de Secreto Hacia Adelante Perfecto (PFS, Perfect Forward Secrecy); si un solo nodo es capturado y sus claves extraídas, todos los datos GPS interceptados previamente se vuelven legibles.
*   **Anonimizar Nombres de Nodos:** Los nombres largos y cortos se almacenan en la carga útil cifrada, pero si la clave de la red se ve comprometida, esos nombres quedan expuestos. Nunca use nombres reales, identificadores comunes en línea o alias predecibles.
*   **Elimine la Telemetría:** Desactive la telemetría de la batería, el voltaje y el estado del dispositivo. Cuanto menos transmita un dispositivo, más difícil será rastrearlo físicamente.
*   **Use Relés "Ciegos":** Si la red depende de nodos de retransmisión desatendidos (por ejemplo, repetidores alimentados por energía solar colocados en techos o colinas), no configure la clave del canal privado en ellos. Los nodos desatendidos son muy susceptibles a la captura física. Seguirán retransmitiendo ciegamente encabezados no cifrados sin necesidad de la clave para descifrar sus cargas útiles.
*   **Comprenda los Límites de LoRa:** Meshtastic es resistente contra las fallas de infraestructura, pero es altamente vulnerable a la interferencia dirigida de RF (jamming) y a la Inteligencia de Señales (SIGINT). Proporciona capacidad fuera de la red, no invisibilidad.

---

## 6. Optimización de Parámetros de RF (Urbano vs. Rural)

LoRa se basa en la modulación de Espectro Ensanchado por Chirp (CSS). Debe ajustar el Factor de Dispersión (SF, Spreading Factor) y el Ancho de Banda (BW, Bandwidth) según su entorno operativo para equilibrar el alcance frente a la velocidad/tiempo en el aire (airtime).

### Operaciones Urbanas Densas (Protestas/Ciudades)
En una ciudad, el rebote de la señal y el ruido de RF son altos, pero las distancias físicas suelen ser cortas.
*   **Configuración:** Utilice un Factor de Dispersión más bajo (SF 7 u 8) y un Ancho de Banda mayor (250 kHz o 500 kHz). Esto a menudo se etiqueta como "ShortFast" o "MediumFast" en la aplicación.
*   **Resultado:** Esto aumenta significativamente la velocidad de los datos y reduce el tiempo en el aire. Un menor tiempo en el aire significa que su radio transmite por menos tiempo, ahorrando batería y reduciendo la ventana de detección de RF para los rastreadores (fox-hunters).
*   **Límite de Saltos:** Establezca el Máximo de Saltos (Max Hops) en **3**. En una multitud densa con cientos de nodos, un límite de saltos de 7 (el valor predeterminado) causará una tormenta de transmisión, colapsando la malla.

### Operaciones en Campo Abierto (Rurales/Largo Alcance)
*   **Configuración:** Utilice un Factor de Dispersión alto (SF 11 o 12) y un Ancho de Banda bajo (125 kHz). Etiquetado como "LongSlow".
*   **Resultado:** Esto maximiza la sensibilidad y el alcance (a menudo más de 10 millas con línea de visión directa a través de valles o terreno abierto) pero reduce significativamente la velocidad de los datos. Los mensajes tardarán varios segundos en transmitirse.
*   **Límite de Saltos:** Aumente de 5 a 7 para permitir que los paquetes atraviesen múltiples millas a través de nodos repetidores dispersos.

[← Volver al Índice](../index.md)

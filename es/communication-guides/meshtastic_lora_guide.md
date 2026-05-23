# Meshtastic y LoRa: comunicaciones descentralizadas fuera de la red

*Estado: Manual de implementación e ingeniería de RF | Público: arquitectos de redes y equipos de comunicaciones tácticas*

Cuando los actores estatales desactivan las redes celulares (o se debe asumir que toda la infraestructura de telecomunicaciones está comprometida), las operaciones requieren una capa de comunicación secundaria y descentralizada. LoRa (largo alcance) es un protocolo de radio de potencia ultrabaja y ancho de banda bajo que opera en la banda ISM (por ejemplo, 915 MHz en EE. UU.). Combinado con el firmware Meshtastic de código abierto, permite la implementación de una red de malla de mensajería de texto de igual a igual desacoplada de los ISP corporativos.

Esta guía detalla la implementación técnica y las vulnerabilidades SIGINT graves de una malla LoRa táctica.

---

## 1. Selección de hardware y actualización del firmware

Confíe en el hardware creado en torno al moderno transceptor LoRa Semtech SX1262. Los chips más antiguos (como el SX1276) tienen una sensibilidad inferior y un mayor consumo de energía.

* **Nodos recomendados:** LILYGO T-Echo o Heltec V3 (para operadores móviles); RAK Wireless WisBlock (para nodos repetidores estacionarios equipados con energía solar y de baja potencia).
* **Implementación:** Actualice el último firmware estable de Meshtastic a través de `flasher.meshtastic.org`.
* **Restricción operativa:** **No utilice la configuración predeterminada del canal "LongFast" para operaciones cívicas de alto riesgo.** El canal predeterminado es público, no cifrado y está muy congestionado.

## 2. Configuración del canal criptográfico

Para proteger la malla, debe establecer un canal cerrado y autenticado utilizando cifrado AES-256.

1. **Generación de claves:** Usando la CLI Meshtastic o la aplicación móvil, cree un nuevo canal y configure el cifrado en **AES256**. El software generará una clave criptográfica de 256 bits.
2. **Distribución fuera de banda (OOB):** *Nunca* transmita la URL de configuración del canal o el código QR a través del canal público LoRa o mediante SMS estándar. La clave debe distribuirse fuera de banda a través de Signal, chat Matrix cifrado o escaneo físico de códigos QR en persona.

## 3. La vulnerabilidad del encabezado no cifrado

Si bien Meshtastic utiliza cifrado AES-256-CTR para cargas útiles de mensajes, la arquitectura de red requiere que ciertos metadatos de enrutamiento se transmitan de forma clara. Para permitir que la malla funcione, los nodos deben poder enrutar paquetes incluso si no poseen la clave de descifrado. Esta capacidad de "retransmisión ciega" significa que el encabezado del paquete siempre está sin cifrar.
| Punto de datos | ¿Cifrado? | Ubicación |
|:---|:---|:---|
| **ID del nodo remitente** | No | Encabezado del paquete |
| **ID de destino** | No | Encabezado del paquete |
| **Límite de saltos/enrutamiento** | No | Encabezado del paquete |
| **Hash de canal** | No | Encabezado del paquete |
| **Contenido del mensaje** | Sí | Carga útil |
| **Ubicación GPS** | Sí | Carga útil |
| **Nombres de nodos** | Sí | Carga útil |


## 4. La amenaza: escucha pasiva y SIGINT

Debido a que los encabezados se transmiten en texto sin formato, un adversario no necesita romper su cifrado para comprender su red.

1. **Análisis de tráfico:** Un oyente pasivo que utiliza radios definidas por software (SDR) económicas puede mapear la topología exacta de su red. Pueden ver qué nodos actúan como centros centrales, quién se comunica con quién y la frecuencia de esas comunicaciones.
2. **Triangulación Física (Caza del Zorro):** Cada transmisión es una baliza. Utilizando antenas direccionales o una matriz distribuida de SDR que calcula la diferencia horaria de llegada (TDOA), un adversario puede triangular físicamente el origen de la señal de RF.
3. **Huellas digitales del hardware:** La ID del nodo (por ejemplo, `!a1b2c3d4`) se deriva directamente de la dirección MAC codificada de la radio. Debido a que esta ID está en el encabezado no cifrado, una vez que un adversario correlaciona una ID de nodo específica con una persona o ubicación específica, puede rastrear esa radio en cualquier momento que transmita.

## 5. Directrices obligatorias de OpSec

Si se enfrenta a actores de amenazas sofisticados, siga explícitamente estas reglas:

* **Elimine el GPS:** Desactive todo el GPS automatizado y la transmisión de posición. Aunque los datos del GPS están cifrados en la carga útil, la transmisión continua actúa como una baliza de RF, lo que hace que la triangulación física sea trivial. Además, Meshtastic carece de Perfect Forward Secrecy (PFS); Si un adversario captura un solo nodo y se extraen sus claves, todos los datos GPS interceptados previamente se vuelven legibles retroactivamente.
* **Anonimizar nombres de nodos:** Los nombres largos y cortos se almacenan en la carga útil cifrada, pero si la clave de red se ve comprometida, esos nombres quedan expuestos. Nunca utilice nombres reales, identificadores comunes en línea ni alias predecibles.
* **Eliminar telemetría:** Desactiva la telemetría de batería, voltaje y estado del dispositivo. Cuanto menos transmite un dispositivo, más difícil es rastrearlo físicamente.
* **Utilice relés "ciegos":** Si la red depende de nodos de relé desatendidos (por ejemplo, repetidores alimentados por energía solar colocados en tejados o colinas), no configure la clave de canal privado en ellos. Los nodos desatendidos son muy susceptibles a la captura física. Seguirán transmitiendo ciegamente encabezados no cifrados sin necesidad de la clave para descifrar sus cargas útiles.
* **Comprenda los límites de LoRa:** Meshtastic es resistente a fallas de infraestructura, pero es altamente vulnerable a interferencias de RF específicas y a inteligencia de señales (SIGINT). Proporciona capacidad fuera de la red, no invisibilidad.

## 6. Optimización de parámetros de RF (urbano versus rural)

LoRa se basa en la modulación Chirp Spread Spectrum (CSS). Debe ajustar el factor de dispersión (SF) y el ancho de banda (BW) según su entorno operativo.

### Operaciones urbanas densas (protestas/ciudades)
En una ciudad, el rebote de la señal y el ruido de RF son elevados, pero las distancias físicas suelen ser cortas.
* **Configuración:** Utilice un factor de dispersión más bajo (SF 7 u 8) y un ancho de banda más alto (250 kHz o 500 kHz).
* **Resultado:** Esto aumenta significativamente la velocidad de los datos y reduce el tiempo de uso (ahorrando batería y reduciendo la ventana de detección de RF).
* **Límite de saltos:** Establece el máximo de saltos en **3**. En una multitud densa, un límite de saltos de 7 (el valor predeterminado) provocará una tormenta de transmisión.

### Operaciones de campo abierto (rurales/de largo alcance)
* **Configuración:** Utilice un factor de dispersión alto (SF 11 o 12) y un ancho de banda bajo (125 kHz).
* **Resultado:** Esto maximiza la sensibilidad y el alcance (a menudo más de 10 millas en la línea de visión) pero reduce significativamente la velocidad de los datos.
* **Límite de saltos:** Aumente a 5-7 para permitir que los paquetes atraviesen varias millas a través de nodos repetidores dispersos.

_Última actualización: 2026_

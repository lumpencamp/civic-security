# Meshtastic y LoRa: comunicaciones descentralizadas fuera de la red

*Estado: Manual de implementación e ingeniería de RF | Público: arquitectos de redes y equipos de comunicaciones tácticas*

Cuando los actores estatales desactivan las redes celulares (o se debe asumir que toda la infraestructura de telecomunicaciones está comprometida), las operaciones requieren una capa de comunicación secundaria y descentralizada. LoRa (largo alcance) es un protocolo de radio de potencia ultrabaja y ancho de banda bajo que opera en la banda ISM (por ejemplo, 915 MHz en EE. UU.). Combinado con el firmware Meshtastic de código abierto, permite la implementación de una red de malla de mensajería de texto punto a punto totalmente cifrada y completamente desacoplada de los ISP corporativos.

Esta guía detalla la implementación técnica y las vulnerabilidades SIGINT de una malla LoRa táctica.

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
3. **Designación de función:** Configure los nodos móviles como "Cliente" o "ClienteMudo" (que no transmite su ubicación GPS a la malla). Configure nodos estacionarios elevados como "enrutador" para priorizar la retransmisión de paquetes.

## 3. Optimización de parámetros de RF (urbano versus rural)

LoRa se basa en la modulación Chirp Spread Spectrum (CSS). Debe ajustar el factor de dispersión (SF) y el ancho de banda (BW) según su entorno operativo.

### Operaciones urbanas densas (protestas/ciudades)
En una ciudad, el rebote de la señal (desvanecimiento por trayectos múltiples) y el ruido de RF son altos, pero las distancias físicas entre los nodos suelen ser cortas.
* **Configuración:** Utilice un factor de dispersión más bajo (SF 7 u 8) y un ancho de banda más alto (250 kHz o 500 kHz).
* **Resultado:** Esto aumenta significativamente la velocidad de los datos y reduce el tiempo de uso (ahorrando batería y reduciendo la ventana de detección de RF), sacrificando un alcance extremo que es innecesario en multitudes densas.
* **Límite de saltos:** Establece el máximo de saltos en **3**. En una densa multitud con cientos de nodos, un límite de saltos de 7 (el valor predeterminado) provocará una tormenta de transmisión que colapsará la red.

### Operaciones de campo abierto (rurales/de largo alcance)
* **Configuración:** Utilice un factor de dispersión alto (SF 11 o 12) y un ancho de banda bajo (125 kHz).
* **Resultado:** Esto maximiza la sensibilidad y el alcance (a menudo más de 10 millas en la línea de visión) pero reduce significativamente la velocidad de los datos. El tiempo aire por mensaje será largo.
* **Límite de saltos:** Aumente a 5-7 para permitir que los paquetes atraviesen varias millas a través de nodos repetidores dispersos.

## 4. Vulnerabilidades de SIGINT y búsqueda de dirección de radio (RDF)

Si bien Meshtastic cifra el *contenido* del mensaje, no puede ocultar las emisiones físicas de RF. Los adversarios estatales (T2/T4) utilizan equipos automatizados de radiogoniometría (RDF) (como antenas de "caza del zorro") para triangular la ubicación física de un nodo transmisor.

### Postura defensiva de RF
1. **Reducir el tiempo de uso:** Cuanto más tiempo transmita un nodo, más fácil será triangular. La optimización urbana (bajo SF, alta velocidad) es fundamental para reducir la ventana de transmisión.
2. **Enmascaramiento de antena:** No camines con una antena de alta ganancia de 15 cm sobresaliendo de tu mochila. Utilice antenas pequeñas y rechonchas o antenas de PCB planas montadas al ras del interior de una bolsa. Sacrificas el alcance por la ocultación física.
3. **Antenas direccionales:** Si implementa un nodo de retransmisión estacionario (por ejemplo, en la ventana de un apartamento), no utilice una antena omnidireccional. Utilice una antena direccional Yagi o Moxon apuntada *lejos* de las áreas de concentración policial conocidas y hacia su zona operativa. Esto da forma a la columna de RF, reduciendo drásticamente la señal detectable desde detrás de la antena.
4. **Desacople el operador:** No sostenga la radio mientras está en funcionamiento. Coloque el nodo Meshtastic en lo alto de un árbol o edificio y conéctese a él mediante Bluetooth desde su teléfono a una distancia de entre 30 y 50 pies. Si el nodo se triangula y toma RDF, el operador no es capturado físicamente con el hardware de transmisión.

_Última actualización: 2026_

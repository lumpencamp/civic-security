# NYM Mixnet: Derrotando el análisis de tráfico global

*Estado: Manual de criptografía distribuida | Público: Operadores de alto riesgo y arquitectos de redes*

Las redes de anonimato estándar como Tor se basan en la ofuscación espacial (enrutar el tráfico a través de múltiples nodos geográficos). Sin embargo, Tor no ofusca *tiempo* o *volumen*. Si un Adversario Pasivo Global (GPA), como una agencia de inteligencia estatal, puede monitorear simultáneamente los puntos de entrada y salida de la red Tor, puede realizar un ataque de correlación de tiempo. Al hacer coincidir el tamaño exacto y el tiempo de un paquete que ingresa a la red con un paquete que sale de ella, pueden desanonimizar al usuario.

Como criptógrafo de sistemas distribuidos, presento **NYM Mixnet**, una arquitectura de próxima generación diseñada específicamente para derrotar los ataques de correlación de tiempo.

---

## 1. Tor/VPN versus arquitectura True Mixnet

Debe comprender por qué NYM es un cambio de paradigma en la privacidad de la red.

* **Circuitos estándar de 3 saltos (Tor/VPN):** Primero en entrar, primero en salir (FIFO). Los paquetes atraviesan los nodos lo más rápido posible. La principal defensa es el cifrado multicapa.
* **The Mixnet (NYM):** NYM no solo cifra datos; muta activamente los metadatos (tiempo, volumen y orden) del tráfico mismo.

### La mecánica de NYM
NYM derrota al análisis de tráfico a través de tres innovaciones criptográficas centrales:

1. **Formato de paquetes Sphinx:** Cada paquete enviado a través de NYM se rellena criptográficamente para que tenga exactamente el mismo tamaño. Un adversario que observe la red no puede diferenciar entre una descarga de imagen grande y un mensaje de texto pequeño porque todos los paquetes parecen idénticos.
2. **Retrasos de tiempo variables:** Cuando un paquete ingresa a un "nodo mixto" de NYM, no se reenvía inmediatamente. El nodo retiene el paquete durante una fracción de segundo aleatoria y determinada criptográficamente.
3. **Tráfico ficticio (tráfico de cobertura):** Si no envía datos, el cliente NYM genera automáticamente paquetes "ficticios" cifrados falsos y los envía a la red. Esto asegura que haya un flujo constante y constante de ruido.

**El resultado:** Los paquetes ingresan a un nodo en un orden, se mezclan con tráfico ficticio, se retrasan aleatoriamente y salen en un orden completamente diferente. Un adversario pasivo global no puede correlacionar el tráfico de entrada y salida.

---

## 2. Implementación de CLI: demonio de cliente NYM

Para operaciones tácticas, no confíe en una GUI. Debe inicializar el demonio del cliente NYM a través de la interfaz de línea de comandos (CLI) para garantizar un enrutamiento estricto y auditable.

### Paso 1: Inicialización
Descargue el binario `nym-client` precompilado para su arquitectura. Inicialice el cliente para generar su identidad criptográfica y archivos de configuración locales.

```bash
./nym-client init --id OpSec_Alpha
```
*Este comando genera una identificación local única (`OpSec_Alpha`) y proporciona sus claves criptográficas.*

### Paso 2: ejecutar el demonio
Inicie el demonio del cliente. Esto se conectará a la red NYM, descargará la topología de red actual y establecerá un puerto de escucha de proxy SOCKS5 o WebSocket local.

```bash
./nym-client run --id OpSec_Alpha
```
*El demonio generará una dirección de escucha, normalmente `127.0.0.1:1977`.*

## 3. Tráfico de aplicaciones de enrutamiento

Una vez que el demonio NYM esté activo, debe obligar a sus aplicaciones a enrutar su tráfico a través del proxy local.

### Integración SOCKS5
Si su aplicación admite la configuración de proxy SOCKS5 (por ejemplo, clientes de mensajería segura estándar, billeteras de criptomonedas o navegadores web):

1. Abra la configuración de Red o Proxy de la aplicación.
2. Establezca el Tipo de proxy en **SOCKS5**.
3. Configure el Host/IP en `127.0.0.1`.
4. Configure el Puerto en el puerto proporcionado por su demonio NYM (por ejemplo, `1977` o `9000` dependiendo de la iteración del cliente).
5. *Crucial:* Asegúrese de que "Proxy DNS cuando se usa SOCKS v5" esté marcado para evitar fugas de DNS.

**Advertencia operativa:** NYM es una red mixta asíncrona. Debido a que retrasa intencionalmente los paquetes para generar anonimato, se caracteriza por una **latencia muy alta**. Es completamente inadecuado para transmisión de video, VoIP o navegación web en vivo. NYM está diseñado para mensajería asincrónica y de alta seguridad (como puentes Matrix localizados) y transacciones de criptomonedas donde la privacidad supera con creces la velocidad.

_Última actualización: 2026_

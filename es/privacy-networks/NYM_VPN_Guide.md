# NYM Mixnet: Derrotando el Análisis de Tráfico Global

> [!CAUTION]
> **AVISO LEGAL Y DE SEGURIDAD OPERACIONAL**
> Esta guía está destinada estrictamente a fines lícitos, defensivos y educativos. Algunas tácticas detalladas a continuación pueden conllevar graves riesgos legales dependiendo de su jurisdicción local.
> - **Nunca** se resista al arresto ni obstruya físicamente a las fuerzas del orden.
> - **Nunca** participe en la interferencia ilegal de radiofrecuencia (RF jamming) ni en daños a la propiedad.
> - **Siempre** consulte a las redes locales de defensa legal (por ejemplo, el National Lawyers Guild) para obtener asesoramiento específico de su jurisdicción.

*Estado: Manual de Criptografía Distribuida | Audiencia: Operadores de Alto Riesgo y Arquitectos de Redes*

Las redes de anonimato estándar como Tor se basan en la ofuscación espacial (enrutamiento del tráfico a través de múltiples nodos geográficos). Sin embargo, Tor no ofusca el *tiempo* o el *volumen*. Si un Adversario Pasivo Global (GPA, por sus siglas en inglés) —como una agencia de inteligencia estatal (NSA, GCHQ)— puede monitorear tanto los puntos de entrada como los de salida de la red Tor simultáneamente, puede realizar un Ataque de Correlación de Tiempo.

Al hacer coincidir el tamaño exacto y el tiempo de un paquete que ingresa a la red con un paquete que sale de ella, pueden desanonimizar al usuario. La **Malla de NYM (NYM Mixnet)** es una arquitectura de próxima generación diseñada específicamente para derrotar estos ataques de correlación de tiempo.

---

## 1. Tor/VPN vs. Arquitectura de Mixnet Verdadera

Debe comprender por qué NYM es un cambio de paradigma en la privacidad de la red en comparación con los sistemas heredados.

*   **Circuitos Estándar de 3 Saltos (Tor/VPN):** Primero en entrar, primero en salir (FIFO). Los paquetes atraviesan los nodos lo más rápido posible para brindar una experiencia de usuario rápida. La principal defensa es el cifrado de múltiples capas. Un observador que observe toda la red puede rastrear la "forma" del tráfico.
*   **La Mixnet (NYM):** NYM no solo cifra datos; muta activamente los metadatos (tiempo, volumen y orden) del propio tráfico.

### La Mecánica de NYM
NYM derrota el Análisis de Tráfico a través de tres innovaciones criptográficas centrales:

1.  **Formato de Paquetes Sphinx:** Cada paquete enviado a través de NYM se rellena criptográficamente para tener exactamente el mismo tamaño. Un adversario que observe la red no puede diferenciar entre la descarga de una imagen grande y un mensaje de texto pequeño porque todos los paquetes se ven idénticos.
2.  **Retrasos de Tiempo Variables (La Mezcla):** Cuando un paquete ingresa a un "nodo de mezcla" (mix node) de NYM, no se reenvía de inmediato. El nodo retiene el paquete durante una fracción de segundo aleatorizada y determinada criptográficamente.
3.  **Tráfico Ficticio (Cover Traffic):** Si no está enviando datos, el cliente NYM genera automáticamente paquetes "ficticios" (dummy) falsos y cifrados, y los dispara a la red. Esto asegura que haya un flujo constante y estable de ruido.

**El Resultado:** Los paquetes ingresan a un nodo en un orden, se mezclan con tráfico ficticio, se retrasan aleatoriamente y salen en un orden completamente diferente. Un Adversario Pasivo Global no puede correlacionar el tráfico de ingreso y egreso.

---

## 2. Despliegue en CLI: Demonio del Cliente NYM

Para operaciones tácticas, no confíe en una GUI (interfaz gráfica). Debe inicializar el demonio del cliente NYM a través de la Interfaz de Línea de Comandos (CLI) para garantizar un enrutamiento estricto y auditable.

### Paso 1: Inicialización
Descargue el binario precompilado `nym-client` para su arquitectura desde el repositorio oficial de NYM. Inicialice el cliente para generar su identidad criptográfica y los archivos de configuración local.

```bash
./nym-client init --id OpSec_Alpha
```
*Este comando genera una ID local única (`OpSec_Alpha`) y provisiona sus claves criptográficas.*

### Paso 2: Ejecución del Demonio
Inicie el demonio del cliente. Esto se conectará a la red NYM, descargará la topología actual de la red y establecerá un puerto de escucha de proxy SOCKS5 local.

```bash
./nym-client run --id OpSec_Alpha
```
*El demonio emitirá una dirección de escucha, generalmente `127.0.0.1:1080` o `1977` dependiendo de la versión.*

---

## 3. Enrutamiento del Tráfico de la Aplicación

Una vez que el demonio NYM está activo, debe forzar a sus aplicaciones a enrutar su tráfico a través del proxy local.

### Integración SOCKS5
Si su aplicación admite la configuración de proxy SOCKS5 (por ejemplo, clientes de mensajería segura estándar, billeteras de criptomonedas o navegadores web):

1.  Abra la configuración de Red o Proxy de la aplicación.
2.  Establezca el Tipo de Proxy en **SOCKS5**.
3.  Establezca el Host/IP en `127.0.0.1`.
4.  Establezca el Puerto en el puerto proporcionado por su demonio NYM (por ejemplo, `1080`).
5.  *Crucial:* Asegúrese de que la opción "Proxy DNS cuando se use SOCKS v5" (Proxy DNS when using SOCKS v5) esté marcada para evitar la fuga de DNS. Si las solicitudes de DNS se filtran fuera del mixnet, su ISP sabrá con qué servicios se está comunicando.

---

## 4. Casos de Uso Operativos y Modelos de Amenazas

NYM no es un reemplazo directo de una VPN. Sirve a requisitos operativos altamente específicos.

### Cuándo Usar NYM (Amenazas T3/T4)
*   **Filtraciones de Denunciantes (Whistleblower Drops):** Enviar documentos a instancias de SecureDrop donde se sabe que el adversario monitorea el tráfico del ISP buscando la fuente.
*   **Transacciones de Criptomonedas:** Transmitir transacciones de Bitcoin o Monero. NYM evita que las empresas de análisis de blockchain vinculen su dirección IP residencial con el nodo que transmitió la transacción por primera vez.
*   **Mensajería Asíncrona:** Uso de protocolos de chat descentralizados (como configuraciones específicas de Matrix o Briar) donde la entrega inmediata es menos importante que la protección de metadatos.

### Cuándo NO Usar NYM
**Advertencia Operativa:** NYM es un mixnet asíncrono. Debido a que retrasa intencionalmente los paquetes para generar anonimato, se caracteriza por **una latencia muy alta**.
*   Es completamente inadecuado para la transmisión de video (streaming).
*   No puede soportar VoIP o llamadas de voz/video (como las llamadas de Signal).
*   La navegación web en vivo es dolorosamente lenta y a menudo se agota el tiempo de espera (timeouts).

NYM está diseñado para transferencias de datos asíncronas y de alta seguridad, donde la privacidad absoluta supera con creces a la velocidad.

---

## 5. Incentivación de la Red e Infraestructura

A diferencia de Tor, que depende completamente de voluntarios (creando una red frágil), NYM utiliza un modelo tecno-económico (token-economic).
*   Los nodos de mezcla son recompensados con tokens NYM por proporcionar servicios de mezcla confiables y ancho de banda.
*   Esto incentiva la creación de una red masiva, descentralizada y de alto ancho de banda capaz de manejar la intensa carga computacional requerida por el formateo de paquetes Sphinx y la generación de tráfico ficticio.
*   Como usuario final, dependiendo de la fase de la red, es posible que deba adquirir credenciales de NYM (tokens de ancho de banda) para enviar cantidades significativas de datos a través de la mixnet.

[← Volver al Índice](../index.md)

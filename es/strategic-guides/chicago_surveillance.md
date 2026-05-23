# Análisis profundo de la vigilancia de Chicago: un estudio de amenazas localizadas

*Estado: Análisis Regional Nivel 3 | Audiencia: Organizadores de Chicagoland y Equipos de Acción Directa*

Podría decirse que Chicago es la ciudad más vigilada de Estados Unidos. El Departamento de Policía de Chicago (CPD) y la Oficina de Comunicaciones y Manejo de Emergencias (OEMC) han construido una vasta red integrada de sistemas de monitoreo acústico, visual y celular diseñados para agregar datos públicos y privados en un solo panel. Este informe detalla la mecánica exacta de la red municipal y cómo mitigar la exposición.

---

## 1. Los centros nerviosos: centros de apoyo a las decisiones estratégicas (SDSC)

**La amenaza:** Los SDSC son centros de fusión localizados a nivel de distrito. Funcionan como centros de comando en tiempo real, extrayendo datos de llamadas al 911, cámaras públicas, lectores de placas y algoritmos predictivos en paneles de control en tiempo real para despachadores y comandantes.
**La Mecánica:** Las SDSC integran plataformas como Genetec Citigraf. Este software permite a los operadores ver datos de sensores dispares en un mapa unificado, convirtiendo puntos de datos aislados en inteligencia procesable en tiempo real.
**Mitigación:** No se puede "piratear" digitalmente un SDSC. La mitigación requiere reconocer que *cualquier* punto de datos generado en público se fusiona y analiza instantáneamente. No confíe en "perderse entre la multitud". Suponga que su línea de tiempo de movimiento se está modelando activamente si se encuentra cerca de un sitio operativo.

## 2. La cuadrícula visual: los POD y los programas de integración de cámaras

El verdadero poder de la red de cámaras de Chicago es la forma en que OEMC integra cámaras residenciales y comerciales privadas en la red pública.

### Los programas reales de integración de cámaras
Chicago opera dos pistas distintas para datos de cámaras privadas:
1. **La Iniciativa de Cámaras del Sector Privado (Direct Feed):** Esto es para propiedades comerciales e institucionales: negocios, complejos de apartamentos de gran altura, estacionamientos y agencias de ciudades hermanas. Instala sistemas de nivel empresarial con direcciones IP públicas directas y compatibilidad específica con sistemas de gestión de vídeo (VMS) (como Genetec). Los operadores OEMC pueden acceder a estas cámaras exteriores **en vivo** durante emergencias.
2. **El programa de registro de cámaras (sin transmisión en vivo):** Aquí es donde caen las cámaras residenciales Ring y Nest. Los residentes registran la ubicación de sus cámaras en un mapa de la ciudad. OEMC y la policía **no** tienen acceso directo y en vivo a estos feeds. Si ocurre un incidente, los detectives revisan el mapa y envían una solicitud automática al propietario pidiéndole que comparta voluntariamente las imágenes. Si bien Ring se asocia frecuentemente con empresas como Flock y Axon para agilizar estas solicitudes, el propietario aún tiene que hacer clic en "aprobar".

### Dispositivos de observación policial (POD)
**La amenaza:** Conocidas localmente como "cámaras de luz azul", son cámaras muy visibles montadas en postes de servicios públicos. Muchos de ellos están equipados con capacidades Pan-Tilt-Zoom (PTZ) y pueden ser controlados activamente por un operador en un centro de fusión SDSC.
**Mitigación:** Interrupción simétrica. Una mascarilla facial estilo N95 de alta calidad combinada con gafas de sol polarizadas y sombreros de perfil bajo es la única defensa confiable contra el mapeo facial. No monte ni desenmascare directamente debajo de ubicaciones POD conocidas.

## 3. Vigilancia acústica: la era posterior al ShotSpotter

**La amenaza (histórica y actual):** En septiembre de 2024, Chicago desmanteló el controvertido conjunto acústico ShotSpotter de 50 millones de dólares. Sin embargo, la vigilancia acústica no ha terminado.
**La mecánica:** A partir de 2025, CPD está poniendo a prueba los sistemas de detección de tiradores de Alarm.com en el distrito 15. Este sistema fusiona sensores acústicos con **cámaras infrarrojas** para reducir la notoria tasa de falsos positivos de los sistemas más antiguos.
**Mitigación:** Se requiere enmascaramiento térmico (ponchos especializados forrados con mylar) si se intenta moverse sin ser detectado a través del Distrito 15 o áreas donde se expande el piloto.

## 4. Seguimiento de vehículos: la red ALPR

**La amenaza:** Los lectores automatizados de matrículas (ALPR) están montados en postes fijos, POD, barredoras de calles, grúas y vehículos de patrulla móviles.
**Los Mecánicos:** Capturan la placa, la hora y la ubicación GPS de cada vehículo que pasa. Esto permite a los analistas establecer fácilmente "patrones de vida" o rastrear los movimientos físicos de un objetivo hacia atrás en el tiempo.
**Mitigación:** No conduzca vehículos personales u organizacionales a las zonas operativas. Estacione al menos a una milla de distancia de la ubicación objetivo en una estructura de estacionamiento comercial densa (lo que confunde a los algoritmos ALPR estacionarios) y recorra la última milla en bicicleta o en la CTA utilizando pases de transporte comprados en efectivo.

## 5. Intercepción celular: despliegue de granizo y mantarraya

**La amenaza:** Los receptores IMSI encubiertos (comúnmente conocidos como Stingrays o las unidades mejoradas Hailstorm) se despliegan durante operaciones específicas o grandes reuniones.
**La mecánica:** Estos dispositivos falsifican torres de telefonía móvil legítimas para obligar a los teléfonos móviles cercanos a conectarse a ellas. Captan números IMSI/IMEI y pueden usarse para rastrear ubicaciones de dispositivos o identificar quién estuvo en un área específica en un momento específico. A menudo obligan a las conexiones 4G/5G a protocolos 2G no cifrados.

### Rayhunter: Detectando la amenaza
La Electronic Frontier Foundation (EFF) desarrolló **Rayhunter**, una herramienta de código abierto diseñada específicamente para detectar la presencia de simuladores de sitios celulares.
* **Cómo funciona:** Rayhunter se ejecuta en dispositivos Android y escanea el entorno celular en busca de anomalías indicativas de un ataque Stingray, como degradaciones repentinas a redes 2G, parámetros de transmisión inusuales o torres a las que les faltan listas de vecinos.
* **Implementación:** Puede instalar Rayhunter en un dispositivo Android operativo. Para obtener instrucciones de instalación y código fuente, visite [EFF Rayhunter GitHub](https://github.com/EFForg/rayhunter) o la [Guía de instalación](https://efforg.github.io/rayhunter/installation.html).

### Mitigación
* **The Baseline:** Apaga tu teléfono personal y déjalo en casa. Utilice un teléfono desechable comprado en efectivo para comunicaciones operativas.
* **El bloque técnico:** En dispositivos GrapheneOS o CalyxOS, navegue hasta Configuración de red y **Desactivar conexiones 2G**.
* **El respaldo de Faraday:** Si Rayhunter le alerta sobre una anomalía o sospecha de un receptor IMSI activo, apague el dispositivo y colóquelo en una bolsa de Faraday con protección RF.

---
**Conclusión clave de OpSec:** La amenaza no es solo un analista que mira una transmisión de Ring en vivo. La amenaza es la correlación de datos retroactiva. Un adversario podría usar un simulador de sitio celular para obtener la identificación de un dispositivo, usar un ALPR para vincular ese dispositivo a un vehículo y luego solicitar imágenes de vigilancia comercial para identificar al conductor.

_Última actualización: 2026_

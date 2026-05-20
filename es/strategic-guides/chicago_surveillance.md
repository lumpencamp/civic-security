# Análisis profundo de la vigilancia de Chicago: un estudio de amenazas localizadas

*Estado: Análisis Regional Nivel 3 | Audiencia: Organizadores de Chicagoland y Equipos de Acción Directa*

Podría decirse que Chicago es la ciudad más vigilada de Estados Unidos. El Departamento de Policía de Chicago (CPD) ha creado una vasta red integrada de sistemas de monitoreo acústico, visual y celular diseñados para rastrear el movimiento y la asociación en todo el condado de Cook. Este informe detalla la mecánica exacta de la red municipal y cómo mitigar la exposición.

---

## 1. Los centros nerviosos: centros de apoyo a las decisiones estratégicas (SDSC)

**La amenaza:** Los SDSC son centros de inteligencia localizados y de alta tecnología desplegados en casi todos los distritos de CPD. Funcionan como centros de fusión en tiempo real, ingiriendo datos de miles de fuentes y enviándolos directamente a unidades de patrulla y equipos tácticos.
**La Mecánica:** Las SDSC integran la plataforma Genetec Citigraf. Este software obtiene transmisiones en vivo de cámaras POD, cámaras de seguridad privadas, ALPR y llamadas al 911, utilizando análisis predictivos para mapear el "riesgo de delito" y coordinar una respuesta rápida.
**Mitigación:** No se puede "piratear" digitalmente un SDSC. La mitigación requiere reconocer que *cualquier* punto de datos generado en público se fusiona y analiza instantáneamente. No confíe en "perderse entre la multitud". Suponga que su línea de tiempo de movimiento se está modelando activamente si se encuentra cerca de un sitio operativo.

## 2. La cuadrícula visual: cámaras POD y Genetec Clearview AI

**La amenaza:** Los dispositivos de observación policial (POD), conocidos localmente como "cámaras de luz azul", están en todas partes. Hay más de 30.000 cámaras de propiedad pública y privada conectadas a la red CPD.
**La mecánica:** Estas cámaras no se limitan a grabar; están cada vez más integrados con sistemas de reconocimiento facial como Clearview AI, que puede asignar un rostro capturado con una cámara POD a perfiles de redes sociales y bases de datos estatales.
**Mitigación:**
* **Físico:** CV Dazzle y el maquillaje asimétrico son en gran medida ineficaces contra la IA moderna. Las mascarillas faciales estilo N95 de alta calidad combinadas con gafas de sol polarizadas y sombreros de perfil bajo son la única defensa confiable contra el mapeo facial.
* **Comportamiento:** No mires las cajas de luz azul. No monte ni desenmascare directamente debajo de ubicaciones POD conocidas. Utilice herramientas como el "Mapa de cámara POD de Chicago" (mantenido por activistas locales) para planificar rutas que minimicen la exposición.

## 3. Vigilancia acústica: la era posterior al ShotSpotter

**La amenaza (histórica y actual):** En septiembre de 2024, Chicago desmanteló el controvertido conjunto acústico ShotSpotter de 50 millones de dólares. Sin embargo, la vigilancia acústica no ha terminado.
**La mecánica:** A partir de 2025, CPD está poniendo a prueba los sistemas de detección de tiradores de Alarm.com en el distrito 15. Este sistema fusiona sensores acústicos con **cámaras infrarrojas** para reducir la notoria tasa de falsos positivos de los sistemas más antiguos.
**Mitigación:** La introducción de infrarrojos significa que las operaciones nocturnas ya no están protegidas por la oscuridad en las zonas piloto. Se requiere máscara térmica (ponchos especializados forrados de mylar) si se intenta moverse sin ser detectado a través del Distrito 15 o áreas donde se expande el piloto.

## 4. Seguimiento de vehículos: la red ALPR

**La amenaza:** Los lectores automáticos de matrículas (ALPR, por sus siglas en inglés) están montados en patrullas CPD, barrenderos, grúas y postes estacionarios en toda la ciudad.
**La mecánica:** Estas cámaras escanean constantemente placas, registran la hora, la fecha y las coordenadas GPS en bases de datos a las que puede acceder el CPD y las agencias federales. Crean un historial masivo y con capacidad de búsqueda de los movimientos de su vehículo.
**Mitigación:**
* **Tránsito operativo:** No conduzca un vehículo registrado con su nombre verdadero o el de una organización activista conocida directamente a una acción.
* **Distanciamiento de estacionamiento:** Estacione al menos a una milla de distancia de la ubicación objetivo en una estructura de estacionamiento comercial densa (lo que confunde a los algoritmos ALPR estacionarios) y recorra la última milla en bicicleta o en la CTA.
* **Pases de tránsito:** Compre tarjetas CTA Ventra con **solo efectivo**. El uso de una tarjeta de crédito vincula sus movimientos de tránsito directamente con su identidad financiera.

## 5. Intercepción celular: despliegue de granizo y mantarraya

**La amenaza:** Las unidades tácticas del CPD y los socios federales despliegan activamente receptores IMSI encubiertos (comúnmente conocidos como Stingrays o unidades Hailstorm mejoradas) durante protestas a gran escala.
**La mecánica:** Estos dispositivos, a menudo montados en camionetas o aviones pequeños sin identificación, imitan torres de telefonía celular legítimas. Su teléfono se conecta a ellos, lo que permite al operador recopilar su IMSI (identidad del dispositivo), mapear su ubicación exacta y potencialmente interceptar SMS/llamadas no cifradas. A menudo obligan a las conexiones 4G/5G a protocolos 2G no cifrados.
**Mitigación:**
* **The Baseline:** Apaga tu teléfono personal y déjalo en casa. Utilice un teléfono desechable comprado en efectivo para comunicaciones operativas.
* **El bloque técnico:** En dispositivos GrapheneOS o CalyxOS, navegue hasta Configuración de red y **Desactivar conexiones 2G**. Esto anula los ataques de degradación más comunes utilizados por los modelos Stingray más antiguos.
* **El respaldo de Faraday:** Si sospecha que hay un receptor IMSI activo en el área (por ejemplo, descarga masiva y repentina de la batería o caída de la red EDGE), apague el dispositivo y colóquelo en una bolsa Faraday con protección RF. No confíes únicamente en el modo Avión.

_Última actualización: 2026_

# Rastreadores Bluetooth: Detección y Defensa

*Estado: Nivel 1 | Audiencia: Todos los miembros que viajan a ubicaciones sensibles*

Los dispositivos de rastreo Bluetooth (Apple AirTags, Samsung SmartTags, Tile y clones genéricos) son económicos, pequeños y pueden colocarse de forma encubierta en vehículos, bolsos o ropa. Utilizan redes colectivas (crowd-sourced) de teléfonos para reportar datos de ubicación a quien los haya colocado, creando un rastreo persistente y de bajo esfuerzo que no requiere un equipo de vigilancia dedicado.

---

## 1. Cómo Funcionan los Rastreadores Bluetooth

### 1.1 La Mecánica

Los rastreadores Bluetooth modernos emiten una señal rotativa de Bluetooth de Baja Energía (BLE). Cada teléfono inteligente compatible dentro del alcance detecta automáticamente y de forma silenciosa estas señales y sube la ubicación y la hora del rastreador a los servidores en la nube del fabricante. El propietario del rastreador puede luego consultar la nube para ver dónde ha estado el rastreador.

**Red Apple AirTag:**
- Más de mil millones de iPhones participan en la red "Encontrar" (Find My).
- Cada iPhone escanea pasivamente y automáticamente en busca de señales de AirTag y reporta la ubicación.
- Los propietarios de AirTags ven el historial de ubicación a través de la aplicación "Encontrar".
- **Precisión:** Puede ser precisa hasta unos pocos metros en áreas densas con muchos iPhones; menos precisa en áreas rurales.

**Samsung SmartTag, Tile y dispositivos similares:** Utilizan redes colectivas similares de dispositivos Samsung, usuarios de la aplicación Tile, etc.

### 1.2 Funciones Anti-Acecho (y sus Limitaciones)

Apple, Samsung y Tile han implementado funciones contra el acecho (stalking), pero son imperfectas:

**Apple AirTag:**
- Si un AirTag que no está registrado con su ID de Apple viaja con usted, su iPhone le alertará después de 8 a 24 horas (se requiere iOS 14.5+).
- El AirTag también emite un pitido audible después de haber estado separado de su dispositivo registrado durante un período prolongado (inicialmente 72 horas; esto se extendió a 8-24 horas después de las quejas de defensores contra la violencia doméstica).
- **Limitación:** Los usuarios de Android no reciben alertas automáticas. Apple lanzó la aplicación para Android "Tracker Detect" (Detector de Rastreadores), pero requiere un escaneo manual: no se ejecuta en segundo plano de forma automática.
- **Limitación:** La alerta contra el acecho solo se activa si el propietario y usted están separados. Si lo están rastreando en su casa y el propietario pasa por allí periódicamente, el temporizador se reinicia.
- **Limitación:** Los AirTags pueden modificarse para desactivar el altavoz.

**Samsung/Tile:**
- Políticas voluntarias similares contra el acecho, pero con una calidad de implementación variable.
- Menos confiables que el sistema de Apple debido a ecosistemas de dispositivos más pequeños.

---

## 2. Métodos de Detección

### 2.1 Usuarios de iPhone: Detección de la Red "Encontrar"

*Configuración → Privacidad y Seguridad → Servicios de Ubicación → Buscar (Find My) → Alertas sobre dispositivos desconocidos*

El iPhone le alerta automáticamente cuando un rastreador desconocido ha estado viajando con usted. Esto se ejecuta en segundo plano y no requiere ninguna acción de su parte. Mantenga esto habilitado.

### 2.2 Usuarios de Android: Escaneo Manual

Android no recibe alertas automáticas en segundo plano. Use estas aplicaciones para escanear manualmente:

**AirGuard (TU Darmstadt — gratis, código abierto):**
- Disponible en Google Play.
- Ejecuta escaneos en segundo plano periódicamente (por defecto cada 4 horas — redúzcalo a cada hora para un uso sensible).
- Le alerta sobre rastreadores Bluetooth desconocidos que viajan con usted.
- Más efectivo que la aplicación oficial Tracker Detect de Apple.

**Apple Tracker Detect (Detector de Rastreadores de Apple):**
- Disponible en Google Play.
- Requiere escaneo manual — no se ejecuta en segundo plano.
- Adecuado para barridos manuales antes de una acción.

**Escaneo manual de Bluetooth:**
- Configuración → Bluetooth → buscar dispositivos cercanos.
- Cualquier dispositivo desconocido que aparezca repetidamente cerca de usted en diferentes ubicaciones puede ser un rastreador.
- Los rastreadores rotan sus direcciones de Bluetooth (para evitar el rastreo fácil del propio rastreador), por lo que pueden aparecer como "Accesorio Desconocido" o con identificadores aleatorios rotativos.

### 2.3 Inspección Física

Cuando sospeche de la colocación de un rastreador o antes de un viaje sensible, inspeccione físicamente:

**En vehículos (puntos de colocación de mayor riesgo):**
- Debajo de los parachoques delantero y trasero (el más común: accesorio magnético).
- Dentro de los cuatro huecos de las ruedas (pase la mano por el interior de cada uno).
- Debajo del vehículo a lo largo de los rieles del chasis (use un espejo en un palo o la cámara del teléfono).
- Dentro del receptor de enganche de remolque (si está presente).
- Detrás de las placas de matrícula.
- Debajo del capó (cerca de la batería; algunos rastreadores usan la energía del vehículo).
- Puerto OBD-II (dentro del vehículo, debajo del tablero; los conectores OBD con capacidad celular pueden ser tanto rastreadores como registradores de datos).

**En bolsos y artículos personales:**
- Revise todos los bolsillos, incluidos los interiores.
- Revise el interior de las bolsas para computadoras portátiles, las cremalleras y los estuches.
- Revise los bolsillos de las chaquetas, especialmente los exteriores.

**Qué buscar:**
- AirTag: disco plateado del tamaño de una moneda (38 mm de diámetro), aproximadamente del grosor de cuatro monedas apiladas.
- Samsung SmartTag: etiqueta de plástico pequeña y rectangular, de aproximadamente 36 mm × 28 mm.
- Tile: varios factores de forma; cuadrado o rectángulo pequeño.
- Clones genéricos: varían mucho; típicamente pequeños rectángulos o discos de plástico.

**Detectores de RF:** Los detectores de RF portátiles (rango de $30 a $100) pueden detectar señales de Bluetooth de rastreadores activos incluso cuando no son visibles de inmediato. Haga un barrido con estos alrededor de su vehículo antes de viajes sensibles.

---

## 3. Respuesta a los Rastreadores Descubiertos

### 3.1 No lo Destruya de Inmediato

Resista el impulso de destruir un rastreador encontrado de inmediato. Un rastreador es evidencia:
- Documente su ubicación con fotos (anote la hora y la ubicación en las notas de su foto).
- No lo manipule con las manos desnudas si tiene la intención de preservar las huellas dactilares (use guantes o una bolsa).
- El número de serie del rastreador puede ayudar a las fuerzas del orden o a su asesor legal a identificar quién lo registró.

### 3.2 Consulte Antes de Actuar

- Comuníquese con su abogado antes de tomar cualquier otra medida.
- Si las fuerzas del orden colocaron el rastreador, destruirlo podría ser manipulación de pruebas.
- Si una parte privada lo colocó, es posible que tenga demandas civiles (acecho, acoso, allanamiento) que se beneficien de la evidencia conservada.

### 3.3 Si Necesita Desactivarlo de Inmediato

Si se encuentra en peligro inmediato o la situación legal lo permite claramente:
- AirTag: Presione y gire la cubierta posterior en sentido contrario a las agujas del reloj; retire la batería CR2032.
- Samsung SmartTag: Retire la batería o siga el procedimiento de desactivación del fabricante.
- Tile: Retire la batería o apáguelo.
- Clones genéricos: Retire la batería visible.

### 3.4 Documente la Vigilancia

Encontrar un rastreador en su vehículo o pertenencias es evidencia significativa de vigilancia y potencialmente de un delito:
- Presente un informe policial (es irónico, pero crea un registro legal).
- Póngase en contacto con el NLG o un abogado de derechos civiles.
- Documente todo por escrito con fechas y horas.
- Coordínese con el equipo de seguridad de su organización.

---

## 4. Prácticas Preventivas

### 4.1 Barridos de Vehículos Previos a la Acción

Antes de conducir a cualquier lugar sensible (reunión, acción, reunión con una fuente):
1. Haga un barrido del vehículo usando una de las aplicaciones de detección mientras camina alrededor de él.
2. Inspeccione físicamente los cuatro lugares de mayor riesgo: parachoques delantero, parachoques trasero, pasos de rueda, puerto OBD.
3. Anote la hora; si encuentra un rastreador más tarde, el momento del barrido establece cuándo fue colocado.

### 4.2 Variar los Lugares de Estacionamiento

Si su vehículo es rastreado hacia un lugar de estacionamiento constante (casa, lugar de reunión de la organización), los adversarios pueden confirmar asociaciones:
- Varíe dónde se estaciona cuando viaje a lugares sensibles.
- Estacione lejos del destino y camine la distancia final.
- Considere compartir un viaje (carpool) en vehículos no asociados con su identidad para las situaciones de mayor sensibilidad.

### 4.3 Separación del Vehículo y la Identidad de la Actividad

- No estacione su vehículo personal en los lugares de acción si es posible; use el transporte público, viajes compartidos bajándose a cierta distancia o vehículos no vinculados a su identidad.
- Tanto los ALPR (lectores de matrículas) como los Stingrays pueden revelar la ubicación del vehículo; un vehículo en el lugar de la acción crea un vínculo de identidad incluso sin un rastreador.

---

*Esta guía no constituye asesoramiento legal. Las leyes varían según la jurisdicción. Detectar y quitar un rastreador colocado por las fuerzas del orden puede tener implicaciones legales; consulte a un abogado.*

[← Back to Index](../index.md)
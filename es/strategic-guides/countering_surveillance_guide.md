# La Guía del Activista para la Contravigilancia

> [!CAUTION]
> **AVISO LEGAL Y DE SEGURIDAD OPERACIONAL**
> Esta guía está destinada estrictamente a fines lícitos, defensivos y educativos. Algunas tácticas detalladas a continuación pueden conllevar graves riesgos legales dependiendo de su jurisdicción local.
> - **Nunca** se resista al arresto ni obstruya físicamente a las fuerzas del orden.
> - **Nunca** participe en la interferencia ilegal de radiofrecuencia (RF jamming) ni en daños a la propiedad.
> - **Siempre** consulte a las redes locales de defensa legal (por ejemplo, el National Lawyers Guild) para obtener asesoramiento específico de su jurisdicción.

*Estado: Manual de Campo | Audiencia: Organizadores, Equipos de Acción Directa, Nodos de Alto Riesgo*

La contravigilancia no se trata de luchar contra el adversario; es el arte estratégico de detectar su presencia y romper su línea de visión *sin* dejarles saber que lo ha hecho.

Exhibir una conciencia de contravigilancia abierta (por ejemplo, mirar fijamente a quien lo sigue, dar giros en U repentinos, conducir de forma errática) eleva el nivel de amenaza y lo marca como un objetivo sofisticado y de alto valor. Este manual dicta los protocolos para la detección pasiva y la evasión segura tanto en los dominios físicos como en los de RF (Radiofrecuencia).

---

## 1. Detección Física: El Arte del 'Bucle Cronometrado' (Timed Loop)

Debe asumir que lo están siguiendo durante operaciones sensibles (movimiento de equipos, reunión con contactos seguros). Su objetivo es obligar al equipo de vigilancia a revelarse creando restricciones geográficas poco naturales, mientras aparenta ser completamente inocente.

### El Método del Bucle Cronometrado
Nunca viaje directamente del Punto A (casa de seguridad / safehouse) al Punto B (reunión operativa). Implemente un Bucle de Análisis de Ruta.
1.  **Establezca un Punto de Estrangulamiento (Choke Point):** Elija una ruta de tránsito que obligue a todo el tráfico que lo sigue a pasar por un cuello de botella específico e inevitable (por ejemplo, un puente largo, un túnel, una calle residencial tranquila de un solo sentido sin desvíos inmediatos).
2.  **La Primera Pasada:** Transite por el punto de estrangulamiento. Registre mentalmente (o use una grabadora de voz discreta) las descripciones de los tres vehículos directamente detrás de usted, incluidas las calcomanías en los parachoques o daños distintivos, y a los peatones que merodeen en la salida.
3.  **El Bucle:** Ejecute un bucle grande y de apariencia natural. Vaya a una cafetería, hojee una librería durante 20 minutos (una **Parada de Cobertura / Cover Stop**), y luego navegue de regreso hacia el punto de estrangulamiento desde un ángulo completamente diferente.
4.  **La Segunda Pasada:** Transite por exactamente el mismo punto de estrangulamiento de nuevo.
5.  **Evaluación:** Si alguno de los vehículos o peatones de la Primera Pasada está presente durante la Segunda Pasada, usted está bajo vigilancia activa. *No reaccione.*

### Reconociendo la Dinámica del Equipo
La vigilancia profesional (T3/T4) nunca es un solo auto. Es una "caja flotante" (floating box) diseñada para evitar que vea el mismo vehículo dos veces seguidas.
*   **El Vehículo de Mando (The Command Vehicle):** Se mantiene en paralelo, corriendo una cuadra más allá de su ruta.
*   **El Seguidor (The Follower):** Se queda atrás, entregando frecuentemente el liderazgo a otro vehículo para evitar la detección.
*   **El Ojo (The Eye):** Un peatón, ciclista o automóvil estacionado que se ubica en su destino antes incluso de que usted llegue.

---

## 2. Detección Digital: Identificación del Rastreo de RF Activo

La vigilancia moderna se basa en gran medida en la Radiofrecuencia (RF). Si no pueden verlo físicamente, están rastreando sus emisiones digitales.

### Detección de Monitoreo de Multitudes por Wi-Fi / Bluetooth
La policía local (T2) despliega sniffers (rastreadores) de RF móviles en las zonas de protesta para recolectar direcciones MAC de todos los dispositivos en el área, mapeando a la multitud e identificando a los organizadores en función de quién asiste a múltiples eventos.
*   **Protocolo:** Antes de ingresar a una zona operativa, ponga su dispositivo principal en modo avión. **Crucialmente, también debe desactivar manualmente el Wi-Fi y el Bluetooth.** El modo avión en los teléfonos inteligentes modernos *no desactiva* automáticamente las balizas de Bluetooth en segundo plano (como la red "Find My" / "Buscar" de Apple), que continúan transmitiendo la firma única de su dispositivo a los escáneres incluso cuando están desconectados.

### Identificación de Captadores de IMSI (Stingrays)
Los Stingrays imitan a las torres celulares, obligando a su teléfono a conectarse a ellos para recolectar su número IMSI y rastrear su ubicación.
*   **Firmas de un Ataque:**
    *   Caída repentina e inexplicable de las redes 5G/4G a redes 2G (EDGE). (Los Stingrays a menudo fuerzan a los teléfonos a protocolos 2G más antiguos y no cifrados para interceptar datos).
    *   Agotamiento de la batería inusualmente rápido.
    *   Fallo en la transmisión de llamadas/textos a pesar de mostrar señal de "barras completas".
*   **Contramedida:** En Android (específicamente en sistemas operativos reforzados como GrapheneOS), navegue a Configuración de Red y **Desactive 2G**. Esto anula los ataques de degradación (downgrade) más comunes. Si sospecha que hay un Stingray activo, apague el dispositivo por completo y colóquelo en una bolsa de Faraday.

---

## 3. Evasión: El Protocolo de Ruptura Segura (Safe Break)

Si confirma la vigilancia, su objetivo es "romper la cola" de forma natural. Debe proporcionar al equipo de vigilancia una razón plausible e inocente para perderlo de vista.

### Retirada Natural
*   **No Hacer:** Correr, conducir erráticamente, pasarse los semáforos en rojo o confrontar al operativo de vigilancia.
*   **Qué Hacer:** Entrar en un entorno muy concurrido con múltiples salidas (unos grandes almacenes grandes, una estación de metro concurrida, un denso vestíbulo de hotel).

### La Trampa del Metro (Ruptura Física)
Ingrese a una estación de metro. Espere en el andén, leyendo un libro o mirando su teléfono, hasta que las puertas del tren se estén cerrando. Suba al tren en el último segundo posible.
*   Si el agente de vigilancia intenta seguirlo, debe apresurarse hacia las puertas (revelándose) o quedarse atrás.
*   Si se quedan atrás, asumen que simplemente alcanzó el tren por suerte, no que los estaba evadiendo.

### El Intercambio de Desechables (Ruptura Digital)
Si debe romper la vigilancia digital (por ejemplo, están rastreando la ubicación de su teléfono a través de la triangulación de torres):
1.  Ingrese a una "Parada de Cobertura" (Cover Stop) (por ejemplo, el baño de un centro comercial o una cafetería concurrida).
2.  Apague su dispositivo principal. Retire la batería si es posible, o colóquela inmediatamente en una bolsa de Faraday para eliminar todas las emisiones de RF.
3.  Encienda un dispositivo desechable (Burner) no vinculado, previamente preparado.
4.  Salga de la Parada de Cobertura utilizando una salida diferente. El rastreo digital del adversario quedará congelado en la Parada de Cobertura.

**Directiva:** La operación de contravigilancia más exitosa es aquella en la que el adversario regresa a la base creyendo que usted es simplemente un objetivo aburrido y poco interesante que fue de compras y regresó a casa.

[← Volver al Índice](../index.md)

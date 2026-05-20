# Principios básicos de OPSEC: un manual de compartimentación del flujo de trabajo dinámico

*Estado: Directiva de Nivel 1 | Público: Organizadores principales y nodos de alto riesgo*

La Seguridad Operacional (OPSEC) no es una lista de verificación; es un estado activo y continuo de postura defensiva. Este manual describe la mecánica exacta de la compartimentación de identidades y la gestión dinámica del flujo de trabajo necesaria para evitar fallos en cascada contra adversarios sofisticados.

---

## 1. Compartimentación de la identidad (el principio de la 'brecha de aire')

La regla fundamental de la OPSEC moderna es la estricta separación de personas. Su identidad personal (Nombre verdadero, familia, empleo) nunca debe cruzarse con su identidad organizacional (Alias, red, operaciones).

### Separación de hardware
* **Regla:** Nunca utilices dispositivos personales para operaciones organizacionales.
* **Mecánica:** Adquirir dispositivos "limpios" (portátiles/teléfonos desechables) utilizando dinero en efectivo imposible de rastrear. Estos dispositivos nunca deben conectarse a la red Wi-Fi de su hogar ni asociarse con sus cuentas celulares personales.
* **Aislamiento físico:** Guarde los dispositivos operativos en bolsas de Faraday cuando no estén en uso activo para evitar sondeos pasivos de ubicación y grabación de audio ambiental.

### Separación de IP y red
* **Regla:** Nunca permita que el tráfico operativo comparta la misma huella IP que su tráfico personal.
* **Mecánica:** Todos los dispositivos operativos deben enrutarse exclusivamente a través de redes anónimas (Tor) o VPN dedicadas compradas en efectivo que se ejecuten en puntos de acceso físicamente separados (Wi-Fi público lejos de su residencia). Nunca inicie sesión en una cuenta operativa desde una IP personal y viceversa. Una única intersección crea un vínculo criptográfico inmutable.

### Separación conductual
* **Regla:** Su alias operativo debe exhibir un "Patrón de vida" (PoL) distinto de su verdadera identidad.
* **Mecánica:** Modifique su estilo de escritura (use diferente vocabulario, gramática y estructura de oraciones). No acceda a cuentas operativas y personales al mismo tiempo. Si su verdadera identidad trabaja de 9 a 5, su alias operativo no debe exhibir actividad exclusivamente fuera de ese horario, ya que esto crea una correlación negativa reconocible.

---

## 2. Compartimentación dinámica del flujo de trabajo

Las operaciones deben dividirse en celdas independientes y que no se superpongan basándose en un acceso estricto de "necesidad de saber".

### La estructura celular
* **Estructura:** Organizar en células discretas (p. ej., Logística, Comunicaciones, Acción). Los miembros de una célula sólo conocen las identidades (alias) y funciones de los miembros dentro de su propia célula.
* **Comunicación:** La comunicación entre células se maneja estrictamente a través de "recortes" designados (enlaces de un solo punto). Esto garantiza que si la célula de Logística se ve comprometida, el adversario no tenga acceso lateral a la célula de Comunicaciones.

### El peligro de la habituación
Los adversarios utilizan el aprendizaje automático para mapear el comportamiento humano predecible (análisis de patrones de vida). La habituación es una vulnerabilidad crítica.
* **Tránsito:** Nunca tome dos veces la misma ruta hacia una reunión o un sitio operativo. Variar los modos de transporte (caminar, autobús, bicicleta) y alterar aleatoriamente los horarios de salida/llegada.
* **Transmisiones digitales:** No establecer ventanas de comunicación predecibles. Aleatorizar el momento del envío de mensajes. Utilice funciones de envío retrasado en Tor para desacoplar su actividad física de su actividad de red.

---

## 3. Matriz de mitigación de amenazas: respuesta al compromiso del nodo

Cuando se sospecha que un solo nodo (un individuo o un dispositivo) está comprometido, se requiere una acción inmediata y planificada previamente para evitar una falla en cascada en toda la red.
| Condición | Indicador | Acción Inmediata (T-0) | Acción Secundaria (T+24h) |
|:---|:---|:---|:---|
| **Sospecha de dispositivo comprometido** | Descarga de batería inexplicable, reinicios inesperados, comunicaciones interceptadas. | Apague el dispositivo inmediatamente. Colocar en bolsa de Faraday. NO intente investigar en el dispositivo. | Purgar claves de sesión remota. Inicie protocolos de borrado seguro si está configurado el borrado remoto. Supongamos que se capturan todos los datos del dispositivo. |
| **Compromiso de alias** | Alias ​​está vinculado públicamente a True Name (Doxing) o es objetivo de phishing específico. | Corta todas las comunicaciones con el alias comprometido. El alias se considera "quemado". | Evaluar el radio de la explosión. Alerta a todas las células conectadas a través de canales secundarios que el alias está quemado. Rote todas las credenciales compartidas. |
| **Arresto físico / Incautación** | Nodo es detenido por fuerzas del orden; Los dispositivos son incautados. | Inicie el **Protocolo de conocimiento cero**. Los nodos conectados cortan inmediatamente todos los enlaces a los alias del nodo capturado. | Rotar todos los canales de comunicación organizacional. Abandonar los lugares de reunión físicos conocidos por el nodo comprometido. Suponga que el adversario tiene acceso total a la memoria y los datos del nodo. |
| **Descubrimiento de informantes** | Evidencia irrefutable de que un nodo está colaborando con un adversario. | **Aislamiento silencioso.** No confrontes. Restrinja gradualmente el acceso del nodo a información confidencial ("Nadar en su carril"). | Suministre información falsa y compartimentada (Canary Trap) para mapear el alcance de la fuga e identificar las prioridades de inteligencia del adversario. Prepárese para cortar limpiamente. |


---
**Directiva:** La confianza es una vulnerabilidad. Confíe en la compartimentación, la criptografía y una rígida disciplina de comportamiento.

_Última actualización: 2026_

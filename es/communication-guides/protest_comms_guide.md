# Comunicaciones tácticas de protesta y defensa SIGINT

*Estado: Manual de Operaciones Tácticas | Público: Coordinadores de Campo y Equipos de Acción Directa*

Durante acciones cívicas de alta fricción, debes asumir que la red celular fallará. Ya sea debido a una congestión natural de multitudes, una limitación localizada intencional o el despliegue de bloqueadores de celulares/captadores IMSI por parte de actores estatales, su arquitectura de comunicación debe ser resiliente.

Como instructor de defensa de inteligencia de señales tácticas (SIGINT), ordeno que ninguna operación comience sin una arquitectura de comunicaciones predefinida de varios niveles.

---

## 1. El Plan de Comunicación PACE

Cada equipo operativo debe establecer un plan PACE antes de desplegarse en el campo. Esto garantiza una transición perfecta cuando la red primaria se degrada.

* **P - Primario (Celular cifrado):** Signal Messenger o Session. Se utiliza cuando la red celular funciona normalmente. Todas las comunicaciones principales deben estar basadas en texto para minimizar el ancho de banda y la huella de ruido.
* **A - Alternativo (Celular descentralizado):** Matrix/Element ejecutándose en un servidor autohospedado. Se utiliza si los servidores centrales de Signal están bloqueados o experimentan aceleración.
* **C - Contingencia (RF fuera de la red):** Meshtastic (LoRa) o Briar (Bluetooth/Wi-Fi local). Se utiliza cuando la red celular está completamente bloqueada o bloqueada. Esto requiere hardware previamente emparejado y proximidad física (para Briar) o relés de línea de visión (para LoRa).
* **E - Emergencia (Protocolo Físico):** Señalización acústica (silbatos/bocinas de aire) y puntos de reunión físicos predesignados. Se utiliza cuando todas las comunicaciones digitales y de RF fallan catastróficamente o se incautan dispositivos.

### Ejecutando el cambio de comunicaciones
Se debe llamar explícitamente a un "cambio de comunicaciones". Si un líder de equipo reconoce que el canal principal está fallando (por ejemplo, los mensajes se cuelgan al "enviar"), emite el comando: *"Cuadrícula degradada. Cambie a alternativo".* Todos los miembros abandonan inmediatamente el canal principal y pasan al canal alternativo. No divida las comunicaciones en varios niveles simultáneamente.

---

## 2. Derrotar la huella digital por voz y SIGINT

La comunicación de voz a través de frecuencias de radio abiertas (walkie-talkies FRS/GMRS) o canales celulares no cifrados es completamente transparente para las operaciones de SIGINT. Los adversarios estatales utilizan algoritmos de reconocimiento de voz para mapear a los organizadores individuales en múltiples eventos.

### Brevedad y protocolos de palabras clave
Si debe transmitir por voz (por ejemplo, en una radio no cifrada debido a un turno de contingencia):

* **Sin nombres verdaderos:** Nunca utilice nombres reales, apodos comunes ni títulos organizacionales. Asigne indicativos aleatorios y rotativos para cada operación (por ejemplo, "Sierra-1", "Echo-Actual").
* **Matriz de brevedad:** Mantenga las transmisiones en menos de 5 segundos. Utilice un código de brevedad previamente memorizado.
    * *Ejemplo:* En lugar de decir "La policía avanza desde la calle norte con equipo antidisturbios", diga: "Condición roja, vector norte".
* **Disfraz de voz:** No grites ni muestres una cadencia emocional reconocible. Hable en un susurro monótono y plano si transmite cerca de fuerzas hostiles.

---

## 3. Contingencias: Jamming y Apagones Celulares

Cuando nos enfrentamos a apagones celulares localizados (a menudo provocados por las autoridades municipales o por el despliegue de Stingray), la coordinación digital termina.

### Reconociendo el apagón
* Los mensajes no se envían, pero el teléfono muestra "barras completas". (Un fuerte indicador de una trampa Stingray).
* Pérdida total de la conexión de datos (bajando a 1G/EDGE o "Sin servicio") en un entorno urbano denso.

### El protocolo físico de emergencia (puntos de reunión)
Al pasar al nivel de "Emergencia", los dispositivos digitales deben apagarse y colocarse en bolsas de Faraday para evitar el seguimiento.

1. **El punto de reunión principal (PRP):** Un lugar seguro y observable justo fuera de la zona inmediata de fricción (por ejemplo, una cafetería específica a tres cuadras de distancia). Si un equipo se dispersa durante un apagón, todos se trasladan de forma independiente al PRP.
2. **El punto de reunión alternativo (FRP):** Una ubicación secundaria y altamente segura a millas de distancia del evento (por ejemplo, una casa segura residencial confiable).
3. **El protocolo de tiempo:** Si están separados, espere en el PRP durante un período previamente acordado (por ejemplo, 15 minutos). Si el equipo no se ha reunido o el PRP se vuelve hostil, proceda inmediatamente al FRP. No holgazanees. No intente utilizar las comunicaciones hasta llegar al FRP.

_Última actualización: 2026_

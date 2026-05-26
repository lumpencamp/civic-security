# Guía de Comunicaciones en Protestas: Coordinación de Campo en Tiempo Real

*Estado: Nivel 2 | Audiencia: Coordinadores de Acción y Líderes de Grupos de Afinidad*

La comunicación efectiva durante una acción directa es la diferencia entre un evento coordinado y efectivo, y uno caótico y vulnerable. Esta guía cubre la arquitectura de comunicación, la selección de herramientas, los protocolos de campo y la operación en modo degradado cuando las comunicaciones se interrumpen.

---

## 1. Arquitectura de Comunicación

### 1.1 El Modelo de Comunicaciones en Capas

Diseñe su sistema de comunicaciones con capas redundantes. Si el canal principal falla, los participantes recurren al canal secundario sin confusión.

| Capa | Herramienta | Propósito | Resiliencia |
|-------|------|---------|-----------|
| Digital principal | Signal (grupo) | Coordinación, actualizaciones, alertas de emergencia | Dependiente de Internet |
| Digital secundaria | Briar (malla) | Cuando el Internet está interrumpido o monitoreado | Malla (mesh) Bluetooth/Wi-Fi |
| Malla LoRa | Meshtastic | Malla de largo alcance fuera de la red | Sin infraestructura |
| Física/analógica | Señales preestablecidas | Comunicación directa sin dispositivos | Sin modo de fallo |
| Audio de emergencia | Señales de silbato | Simple, inequívoco, sin batería | Siempre funciona |

### 1.2 Estructura de Comunicación Basada en Células

Refleje la estructura celular de su organización en sus canales de comunicación:
- **Grupo de Signal de toda la acción:** Tráfico mínimo — solo actualizaciones para toda la acción (cambio de ruta, dispersión, emergencia médica)
- **Canales de grupos de afinidad:** 4–7 personas por canal para coordinación de grupos de afinidad en tiempo real
- **Canal de liderazgo/coordinador:** Líderes de acción, enlace legal, líder médico
- **Apoyo en la cárcel / fuera del sitio:** Hilo de conversación separado con su coordinador de apoyo carcelario fuera del sitio

**Limitar las notificaciones:** Los canales de alto tráfico para todos los participantes que suenan constantemente durante una acción serán silenciados o ignorados. Envíe al canal más amplio solo lo que todos realmente necesiten saber.

---

## 2. Configuración de la Comunicación Previa a la Acción

### 2.1 Configuración de Grupos de Signal

Antes de la acción:
- [ ] Cree grupos de Signal específicos para la acción (no use grupos organizativos permanentes para tráfico operativo)
- [ ] Agregue a todos los participantes a sus grupos apropiados
- [ ] Establezca mensajes efímeros (disappearing messages): 1 semana para grupos de acción, 1 día o menos para los canales operativos más sensibles
- [ ] Confirme que todos los participantes tengan Signal configurado correctamente (bloqueo de registro, sin biometría)
- [ ] Designe a dos administradores de grupo por canal (así, si una persona es arrestada, el grupo continúa)

### 2.2 Palabras en Código y Señales

Establezca un vocabulario compartido antes de la acción:
- **Todo despejado (All clear):** Palabra en código que significa que está a salvo y contabilizado
- **Dispersarse hacia [dirección]:** Palabra en código para la dispersión ordenada hacia una salida específica
- **Médico [ubicación]:** Emergencia médica en la ubicación especificada
- **Legal:** Alguien está siendo detenido o arrestado
- **Luz verde/luz roja:** Proceder según lo planeado / abortar y dispersarse

Señales físicas (para cuando el uso del dispositivo está restringido o es imposible):
- **Puño derecho levantado:** Detenerse; mantener la posición
- **Brazo izquierdo levantado:** Moverse a la izquierda
- **Palmas abiertas hacia adelante:** Retroceder
- **Un solo silbatazo:** Atención; detenerse y buscar a un coordinador
- **Tres silbatazos:** Emergencia; dispersión inmediata

Discuta, acuerde y practique estas señales antes de la acción. Las señales nuevas bajo estrés no son confiables.

### 2.3 Reunión Informativa sobre Disciplina de la Información

Informe a todos los participantes antes de la acción sobre los protocolos de comunicación:
- Qué va en el grupo de Signal para todos frente a los canales de los grupos de afinidad
- Nada de redes sociales en tiempo real durante la acción (espere hasta que esté a salvo lejos de ahí)
- No tomar fotos de las caras de otros participantes sin su consentimiento
- Revisión de palabras en código y señales físicas
- Confirmación del número de apoyo de la cárcel fuera del sitio (escrito en el cuerpo)

---

## 3. Durante la Acción

### 3.1 Protocolos de Comunicación Digital

**Control de volumen:**
- Signal para todos: transmita solo actualizaciones críticas (cambio de ruta, movimiento policial, necesidad médica)
- Signal del grupo de afinidad: coordinación local en tiempo real
- Resista la tentación de compartir "comentarios de color" en tiempo real en el grupo de todos — esto crea ruido que entierra los mensajes críticos

**Formato de mensaje para actualizaciones críticas:**
Use un formato estructurado para mensajes sensibles al tiempo que se pueda escanear al instante:
```
[TIPO]: [CONTENIDO BREVE] | [UBICACIÓN/DIRECCIÓN] | [ACCIÓN NECESARIA]

Ejemplo:
POLICÍA: Grupo grande moviéndose al este en Clark | Acercándose desde Michigan | Mantener posición / estar listos para dispersarse al oeste
```

### 3.2 Protocolo de Control de los Grupos de Afinidad

Establezca una cadencia de reportes (check-in) para los grupos de afinidad:
- Cada 30 minutos o en cada transición de fase (llegada, inicio, transición, dispersión)
- El líder designado del grupo de afinidad envía un reporte al canal de coordinación: "Grupo [identificador]: Los [N] miembros contabilizados, [ubicación]"
- La falta de un reporte desencadena una consulta al canal del grupo de afinidad, luego al apoyo de la cárcel si no hay respuesta

### 3.3 Cuando Alguien es Detenido o Arrestado

El grupo de afinidad tiene responsabilidades inmediatas:
1. Anotar la hora, la ubicación y qué oficial(es) realizó la detención/arresto (número de placa si es visible)
2. Intentar quedarse con la persona detenida hasta ser separados por la policía
3. Anotar la dirección en la que se los llevaron
4. Enviar inmediatamente al canal de coordinación: "LEGAL: [nombre o identificador] detenido en [ubicación] por [ID del oficial] a las [hora]"
5. El canal de coordinación notifica al apoyo de la cárcel con la información de identificación

**Las responsabilidades de la persona detenida:**
- Repetir la afirmación de la Quinta Enmienda (derecho a guardar silencio); no decir nada más
- Cumplir físicamente; no resistirse
- Anotar todo lo que pueda; reconstruirlo al ser liberado

### 3.4 Comunicación Médica

- Designe un identificador específico para emergencias médicas: "MÉDICO: [tipo de necesidad] en [ubicación]"
- La información médica se posiciona previamente con los médicos designados — los líderes de los grupos de afinidad no necesitan transmitir detalles médicos
- Los médicos y la coordinación tienen un canal dedicado para la coordinación médica que no obstruye el canal de todos

---

## 4. Comunicaciones en Modo Degradado

Cuando los canales de comunicación normales fallan, recurra a las alternativas preestablecidas.

### 4.1 Interrupción de Internet

Si los datos celulares y el Wi-Fi no están disponibles (interrupción dirigida, interferencia de Stingray, congestión de red en una multitud de alta densidad):
- Cambie a Briar sobre una malla (mesh) de Bluetooth (preinstalar antes de la acción; asegurarse de que todos los participantes lo tengan)
- Briar no requiere internet — crea una red en malla directa peer-to-peer entre teléfonos cercanos
- Alcance efectivo: ~10m (Bluetooth), mayor sobre malla Wi-Fi
- Limitación: los mensajes se propagan a través de la malla; las personas en el borde de la malla reciben mensajes con retraso

### 4.2 Incautación de Dispositivos

Si se incautan los dispositivos de los comunicadores clave:
- Los coordinadores de respaldo predesignados asumen las responsabilidades de coordinación
- Los canales de comunicación continúan (el arresto de ninguna persona individual debería colapsar la estructura de comunicación)
- Los coordinadores restantes envían una breve notificación: "Coordinador [identificador] está detenido. [Identificador de respaldo] ahora está coordinando".

### 4.3 Fallo Total de Comunicaciones

Si todas las comunicaciones digitales fallan:
- Recurra a señales físicas preestablecidas (Sección 2.2)
- Recurra a puntos de reunión preestablecidos (establezca 2 o 3 antes de la acción)
- Los grupos de afinidad operan de forma autónoma utilizando sus planes de dispersión preestablecidos
- **Crítico:** Cada grupo de afinidad debe poder operar independientemente si fallan todas las comunicaciones. Acuerde previamente: ¿adónde vamos? ¿Cuáles son nuestras rutas de dispersión? ¿Cuándo nos reunimos de nuevo?

---

## 5. Comunicaciones Posteriores a la Acción

### 5.1 Control de Dispersión

Después de la dispersión:
- Cada grupo de afinidad hace un recuento y se reporta al canal de coordinación: "Grupo [identificador]: los [N] contabilizados, [ubicación]"
- Los miembros ausentes activan el protocolo de apoyo de la cárcel

### 5.2 Seguridad Operacional Posterior a la Acción

- Continúe utilizando el grupo de Signal específico de la acción para la coordinación sobre miembros arrestados, seguimiento legal y logística de debriefing
- Elimine o archive el grupo de Signal de la acción una vez que se resuelva la situación legal/operativa
- No publique en redes sociales públicas hasta que esté a salvo y haya eliminado los metadatos y borrado todas las fotos de rostros identificables

### 5.3 Coordinación de Medios y Narrativas

- Designe un coordinador de comunicaciones específico para interacciones con los medios
- Establezca quién está autorizado para hablar públicamente sobre la acción y quién no
- Asegúrese de que cualquier video o foto publicado haya sido despojado de metadatos y se hayan desenfocado los rostros de los participantes que no hayan dado su consentimiento
- La narrativa sobre lo que sucedió debe pasar a través de su célula de comunicaciones, no ser algo improvisado por participantes individuales

---

## 6. Resumen de Seguridad de las Comunicaciones

| Práctica | Por qué |
|---------|-----|
| Usar Signal (no SMS, WhatsApp, ni redes sociales) | Cifrado de extremo a extremo; sin metadatos que puedan incautar de usted |
| Separar grupos de acción de grupos fijos de la organización | Limita la exposición de la red organizativa si el grupo de acción se ve comprometido |
| Mensajes efímeros activados | Los teléfonos incautados no tienen un historial de mensajes para analizar |
| Palabras en código para situaciones delicadas | Reduce la claridad de las comunicaciones para los observadores |
| Señales físicas pre-planeadas | Sobrevive a cualquier fallo de comunicaciones |
| Apoyo de cárcel en canal separado | Siempre accesible incluso si los coordinadores de la acción son arrestados |
| Sin redes sociales en tiempo real | La información en tiempo real ayuda a la conciencia situacional del adversario |

---

*Esta guía no constituye asesoramiento legal. Las leyes varían según la jurisdicción.*

[← Volver al Índice](../index.md)

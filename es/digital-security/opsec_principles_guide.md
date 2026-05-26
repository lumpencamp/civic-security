# Principios Básicos de OPSEC: Un Manual de Compartimentación de Flujo de Trabajo Dinámico

*Estado: Directiva de Nivel 1 | Audiencia: Todos los Organizadores — Lea Esto Primero*

La Seguridad Operativa (OPSEC) no es una lista de verificación — es un estado activo y continuo de postura defensiva. Es la disciplina de proteger información sensible mediante la identificación de qué datos usted genera, quién los quiere y qué pueden hacer con ellos. Este manual describe la mecánica exacta de la compartimentación de identidad, el control del flujo de información y la gestión dinámica del flujo de trabajo necesarios para prevenir fallas en cascada frente a adversarios en cualquier nivel.

> **La Regla de Oro de la OPSEC:** La fuerza de su seguridad está determinada por su eslabón más débil. Una persona usando WhatsApp en un grupo de Signal, una foto subida con datos EXIF, un correo electrónico no cifrado a un abogado — cualquiera de estos por sí solo puede desentrañar una postura operativa que de otro modo sería sólida. La OPSEC es una práctica colectiva, no individual.

---

## 1. El Proceso OPSEC de Cinco Pasos

El marco clásico de OPSEC del ejército de EE. UU., adaptado para uso cívico:

1. **Identificar la Información Crítica (CI):** ¿Qué información, si fuera conocida por un adversario, dañaría a su organización? Nombres de los participantes, ubicaciones de reuniones, fechas planificadas de acciones, estrategia legal, fuentes financieras, conflictos internos.

2. **Analizar las Amenazas:** ¿Quién quiere su información crítica? (Consulte el [Modelado de Amenazas](./threat_modeling_guide.md)). ¿Cuáles son sus capacidades de recolección?

3. **Analizar las Vulnerabilidades:** ¿Por dónde se filtra su información crítica? Publicaciones en redes sociales, metadatos del teléfono, transacciones con tarjetas de crédito, conversaciones escuchadas a escondidas, datos de dispositivos digitales.

4. **Evaluar el Riesgo:** Para cada vulnerabilidad, calcule probabilidad × impacto. Centre su esfuerzo primero en los riesgos ALTOS y CRÍTICOS.

5. **Aplicar Contramedidas:** Implemente protecciones específicas y viables. Reevalúe continuamente.

---

## 2. Compartimentación de la Identidad (El Principio de "Espacio de Aire" o Air Gap)

La regla fundamental de la OPSEC moderna es la **separación estricta y permanente de las personas (identidades)**. Su identidad personal (nombre real, familia, empleo, dirección de casa) nunca debe cruzarse con su identidad operativa (alias, red, operaciones). Una sola intersección crea un vínculo inmutable que el análisis retroactivo puede explotar.

### 2.1 Separación de Hardware

**Regla:** Nunca use dispositivos personales para operaciones de la organización.

**Por qué es importante:** Los identificadores de dispositivo (IMEI, número de serie, dirección MAC, ID de publicidad) son permanentes y únicos. Las radios de Wi-Fi y Bluetooth transmiten estos identificadores pasivamente. Su teléfono personal se conecta a torres de telefonía celular cerca de su casa, lugar de trabajo, gimnasio — construyendo un mapa preciso de su patrón de vida. Si ese dispositivo aparece en un lugar restringido, su identidad queda vinculada a él.

**Implementación:**
- Obtenga dispositivos operativos "limpios" (teléfonos, computadoras portátiles) usando efectivo irrastreable en una tienda física. No haga pedidos en línea — los registros de envío vinculan su dirección.
- Estos dispositivos **nunca** deben conectarse a la red Wi-Fi de su hogar. Incluso conectarse para establecer una VPN compromete el historial de ubicación del dispositivo.
- No empareje dispositivos operativos con accesorios Bluetooth personales (auriculares, teclados, rastreadores de fitness).
- Guarde los dispositivos operativos en bolsas Faraday cuando no estén en uso activo. Esto evita el sondeo celular pasivo, la captura por Stingray y los exploits de transmisión inalámbrica. Bolsas Faraday de calidad: Silent Pocket, Mission Darkness.
- No cargue dispositivos operativos en casa usando cargadores que permanezcan enchufados (las regletas de enchufes inteligentes pueden registrar patrones de uso de energía).

### 2.2 Separación de Dirección IP y Red

**Regla:** Nunca permita que el tráfico operativo comparta la misma huella de IP que el tráfico personal.

**Por qué es importante:** La dirección IP de su hogar está registrada en la cuenta de su proveedor de servicios de internet (ISP) bajo su nombre legal y dirección de facturación. Cada sitio web, servicio y plataforma a los que accede registra esta IP. Si inicia sesión en una cuenta operativa desde la IP de su hogar incluso una sola vez, esa cuenta queda permanentemente vinculada a su identidad a través de los registros de citación del ISP.

**Implementación:**
- Todos los dispositivos operativos deben enrutar exclusivamente a través de redes de anonimato. En orden ascendente de anonimato: **Solo VPN** → **VPN + Tor** → **Solo Tor** → **SO Tails + Tor**.
- Las VPN por sí solas son insuficientes para adversarios T2+: se puede citar a su proveedor de VPN. Utilice proveedores con sólidas políticas de no registro (no-log), jurisdicción extraterritorial y un historial comprobado de resistencia a demandas legales (Mullvad es el estándar de oro actual).
- Utilice redes Wi-Fi públicas lejos de su residencia o ubicaciones habituales para cualquier actividad operativa que no se pueda realizar a través de Tor. Rote las ubicaciones; no regrese a la misma cafetería repetidamente.
- Nunca inicie sesión en una cuenta operativa desde una IP personal y nunca inicie sesión en una cuenta personal desde un dispositivo/IP operativo. Una sola intersección crea un vínculo criptográfico inmutable en los registros de la plataforma que el análisis retroactivo encontrará.
- Para la máxima sensibilidad, utilice el **SO Tails** arrancado desde un USB en una máquina no personal. Tails enruta todo el tráfico a través de Tor de forma predeterminada y no deja rastro en la máquina anfitriona.

### 2.3 Separación de Cuentas e Identidad

**Regla:** Cada cuenta operativa debe crearse y mantenerse exclusivamente desde dispositivos e IPs operativos.

**Implementación:**
- Cree cuentas de correo electrónico operativas utilizando un proveedor que respete la privacidad (Proton Mail, Tutanota) a través de Tor o una VPN limpia, que no estén vinculadas a ninguna información de recuperación personal.
- Utilice un nombre de usuario único para cada plataforma que no refleje su nombre real, ubicación ni ningún otro identificador persistente.
- No reutilice nombres de usuario en diferentes plataformas. Los nombres de usuario reutilizados se cruzan trivialmente utilizando herramientas OSINT.
- Nunca proporcione un número de teléfono real para la recuperación de cuentas. Utilice un número VOIP (JMP.chat a través de Tor, MySudo) o salte la verificación telefónica por completo siempre que sea posible.
- No vincule cuentas operativas a ningún método de pago personal. Utilice tarjetas virtuales privacy.com financiadas por tarjetas de regalo compradas con efectivo, o Monero para máxima privacidad.

### 2.4 Separación de Comportamiento (Patrón de Vida)

**Regla:** Su alias operativo debe exhibir un "Patrón de Vida" (PoL) distinto al de su verdadera identidad.

**Por qué es importante:** Incluso sin identificación directa, el análisis de comportamiento puede desanonimizarlo. Si siempre publica en línea entre las 9 PM y la 1 AM en horario central de EE. UU., escribe en inglés americano con ortografías idiosincrásicas específicas, y sus cuentas con nombre real guardan silencio precisamente cuando su alias está activo — estas correlaciones son estadísticamente significativas.

**Implementación:**
- **Estilo de escritura:** Altere su vocabulario, evite frases características, ajuste patrones gramaticales. Los asistentes de escritura de IA pueden ayudar, pero también introducen sus propios patrones. Practique antes del despliegue.
- **Sincronización de actividad:** No acceda a cuentas operativas exclusivamente durante las horas en que sus cuentas personales están inactivas. Introduzca ruido deliberado.
- **Correlación de temas:** No discuta temas operativos en cuentas personales, ni siquiera de forma oblicua. "No puedo decir mucho, pero algo grande está sucediendo" es una filtración.
- **Geográfico:** Evite publicar fotos o registrarse (check-ins) en lugares que, combinados con su hora de publicación, puedan triangular su ubicación.

---

## 3. Compartimentación de Flujo de Trabajo Dinámico

Las operaciones deben dividirse en células independientes y no superpuestas basadas en un estricto control de acceso de **necesidad de saber**. Esto no es una obstrucción burocrática — es la arquitectura fundamental que previene que un solo compromiso destruya a toda la organización.

### 3.1 La Estructura Celular

**Estructura:** Organícese en células discretas (por ejemplo, Logística, Comunicaciones, Legal, Alcance Comunitario, Acción Directa). Los miembros de una célula solo conocen las identidades de los miembros en su propia célula y a un solo enlace designado con las células adyacentes.

**Racionalidad:** Si un miembro de la célula de Logística es arrestado y su dispositivo es incautado, la información extraída compromete solo a la célula de Logística. La célula de Acción permanece intacta. Sin esta estructura, cualquier arresto individual expone a toda la red.

**Implementación:**
- Las células de 4–7 personas son óptimas. Las células más pequeñas son más seguras; las células más grandes se vuelven inmanejables y propensas a filtraciones.
- Los enlaces entre células deben ser sus miembros más experimentados y capacitados en seguridad.
- Las decisiones operativas que requieren coordinación entre células se realizan a través de los enlaces únicamente, nunca a través de comunicación directa entre células.
- No documente nada que no necesite ser documentado. Si una decisión se puede tomar verbalmente en persona y ejecutarse sin un rastro en papel, prefiera eso.

### 3.2 El Principio de "Necesidad de Saber"

**Regla:** Nadie recibe información más allá de la que requiere para realizar su tarea específica.

**Violaciones comunes a evitar:**
- Compartir listas completas de participantes cuando subgrupos específicos para tareas serían suficientes.
- Poner en copia (CC) a todos en correos electrónicos que conciernen solo a un subconjunto.
- Publicar detalles de acciones en un canal general en lugar de un canal específico y apropiado para el rol.
- Compartir información verbalmente "solo para mantener a la gente informada".

**Implementación:**
- Mantenga grupos de Signal separados para cada célula. El grupo general de todos los miembros recibe solo información que todos los miembros necesitan.
- La información legal y médica (antecedentes de arresto de participantes, condiciones de salud) es estrictamente bajo "necesidad de saber", y debe ser conservada solo por el coordinador legal/médico designado.
- La información financiera (identidades de donantes, cuentas bancarias) es "necesidad de saber" únicamente a nivel de tesorería de la organización.

### 3.3 Clasificación de la Información

Aplique un marco de clasificación simple a toda la información de la organización:

| Nivel | Etiqueta | Definición | Manejo |
|-------|-------|-----------|----------|
| 0 | **Público** | Publicado intencionalmente; cualquiera puede saberlo | Redes sociales, volantes, comunicados de prensa |
| 1 | **Interno** | Para miembros en general; no sensible | Grupo general de Signal, wiki interna |
| 2 | **Sensible** | Restringido a la célula relevante; la exposición causa disrupción | Grupo de Signal específico de la célula, "necesidad de saber" verbal |
| 3 | **Crítico** | Seguridad operativa central; la exposición causa daños significativos | Solo en persona, sin registro digital, enlaces específicos |

---

## 4. Contrainteligencia: Detección y Manejo de Infiltración

Toda organización cívica importante debería asumir la posibilidad de infiltración. Esto no es paranoia — es un hecho histórico documentado a través de divulgaciones FOIA (COINTELPRO, archivos sobre grupos ambientales, organizaciones pacifistas, capítulos de Black Lives Matter).

### 4.1 Indicadores de Comportamiento de un Posible Informante

Ningún indicador individual es definitivo. Patrones de múltiples indicadores justifican una investigación:
- Presiona constantemente por la escalada hacia tácticas que generarían cargos penales graves.
- Hace preguntas inusualmente detalladas sobre aspectos operativos específicos, cronogramas o identidades de los participantes que no son relevantes para su rol.
- Llegó sin una red de confianza social verificable (nadie puede responder de forma independiente por ellos).
- Se resiste a los protocolos de seguridad, califica la privacidad como paranoia o elitismo.
- Tiene recursos financieros inexplicables inconsistentes con sus antecedentes declarados.
- Busca de inmediato posiciones de autoridad o acceso a información confidencial.
- Frecuentemente no está disponible o da explicaciones vagas para sus ausencias.
- Crea divisiones sutiles entre organizadores clave.

### 4.2 El Sistema de Aval (Vouching)

**Implementación:**
- Los nuevos participantes en espacios sensibles requieren **aval personal por parte de dos miembros de confianza existentes** que puedan verificar independientemente la identidad y el historial de la persona.
- Avalar conlleva responsabilidad: si alguien por quien usted respondió resulta ser un informante, su juicio será cuestionado.
- Mantenga un período de prueba para los nuevos miembros: participación plena en actividades públicas, participación restringida en discusiones operativas sensibles hasta que se establezca la confianza.
- Nunca avale a alguien que solo conozca en línea.

### 4.3 La Trampa del Canario (para presuntas filtraciones)

Si sospecha que una persona en específico es la fuente de las filtraciones pero no puede confirmarlo, utilice una prueba de información controlada:
1. Proporcione versiones sutilmente diferentes de un dato operativo no crítico a cada sospechoso de manera individual.
2. Monitoree si esa variante específica aparece externamente (en la actividad policial, informes de prensa o publicaciones en línea del adversario).
3. La variante que salió a la luz identifica a la fuente.
4. **Precaución:** Ejecute esto solo con líderes experimentados. Los falsos positivos destruyen la confianza y pueden ser usados contra miembros inocentes.

### 4.4 Cuando Confirme a un Infiltrado

- **No lo confronte de inmediato.** La confrontación los pone sobre aviso, alertando potencialmente a sus superiores y desencadenando una mayor vigilancia.
- **Evalúe el daño:** ¿A qué tenían acceso? ¿Qué puede estar comprometido?
- **Consulte a un abogado inmediatamente.** Su abogado puede asesorarlo sobre cómo proceder de manera que no cree exposición legal adicional.
- **Limite discretamente su acceso** mientras se evalúa la situación.
- **Después de una evaluación completa y consulta legal**, tome una decisión organizacional sobre la divulgación y los próximos pasos.

---

## 5. Reuniones Seguras en Persona

La seguridad digital es irrelevante si sus reuniones físicas están vigiladas o sus conversaciones son grabadas.

### 5.1 Selección de Ubicación
- Nunca se reúnan en el mismo lugar repetidamente para discusiones sensibles. Rote las ubicaciones.
- Evite lugares con cámaras de vigilancia en los puntos de entrada, o llegue/salga de manera que evite la captura por reconocimiento facial.
- Las residencias privadas suelen ser más seguras que los locales comerciales (sin cámaras de vigilancia, sin personal como posibles testigos). Sopese esto contra los lectores ALPR/CCTV que capturan las matrículas de los vehículos en la ruta.
- Los lugares al aire libre (parques, bosques) anulan la grabación de audio, pero introducen otros riesgos de vigilancia (observación aérea, micrófonos direccionales de largo alcance). Evalúe en consecuencia.
- Nunca mantenga conversaciones delicadas en vehículos: los vehículos modernos tienen múltiples micrófonos, radios Bluetooth y chips celulares que pueden ser explotados de forma remota.

### 5.2 Política de Dispositivos en Reuniones Sensibles
- **Teléfonos apagados y en bolsas Faraday, o dejados en vehículos.** El "modo avión" es insuficiente: desactiva las conexiones de red pero no desactiva todas las radios, y puede ser activado por exploits. Se requiere separación física.
- Realice un barrido en busca de dispositivos electrónicos desconocidos en el espacio antes de comenzar.
- Indique a los participantes que no lleven relojes inteligentes (smart watches), rastreadores de fitness ni dispositivos de hogar inteligente.
- Si graba la reunión para la memoria de la organización, use una grabadora dedicada en modo avión, almacenada de forma encriptada y aprobada explícitamente por todos los participantes.

### 5.3 Contramedidas de Audio
- Las máquinas de ruido blanco colocadas cerca de puertas y ventanas reducen drásticamente la efectividad de los micrófonos direccionales y de contacto en el vidrio.
- No sostenga conversaciones sensibles cerca de las ventanas (la vibración del vidrio puede ser leída por micrófonos láser desde distancias significativas).
- Hable en un volumen normal; susurrar y taparse la boca se ve como sospechoso en videos de vigilancia y no burla la captura de audio sofisticada.

---

## 6. Fundamentos de Higiene Digital

### 6.1 El Principio de la Huella Mínima
Genere la cantidad mínima de datos necesarios para realizar cada tarea. Los datos que nunca crea no pueden ser incautados, requeridos legalmente ni filtrados. Específicamente:
- Elimine los mensajes operativos después de haberlos procesado (use los mensajes temporales de Signal).
- No tome fotografías en reuniones sensibles.
- No utilice la sincronización en la nube para archivos operativos.
- Borre el historial del navegador, las cookies y el almacenamiento local después de cada sesión en los dispositivos operativos.
- Elimine las aplicaciones que no esté utilizando activamente.

### 6.2 Actualizaciones de Software
El software sin parches (actualizaciones) es la superficie de ataque más común explotada tanto por piratas informáticos comerciales como por la ciencia forense digital de la policía. Active las actualizaciones automáticas en todos los dispositivos. No hay ninguna ventaja de seguridad en ejecutar versiones de software antiguas.

### 6.3 Auditoría de Permisos de Aplicaciones
Realice una auditoría mensual de los permisos de las aplicaciones en todos los dispositivos:
- Revoque el acceso a la ubicación a todas las aplicaciones que no lo requieran para funcionar.
- Revoque el acceso al micrófono y a la cámara de todas las aplicaciones que no lo requieran.
- Elimine aplicaciones con permisos amplios que no tengan justificación operativa (Facebook, TikTok, aplicaciones comerciales de clima — todas tienen historiales documentados de recolección masiva de datos).

### 6.4 Seguridad del Navegador
- Utilice **Firefox** con **uBlock Origin** para la navegación operativa. Configure la "Protección mejorada contra el rastreo" (Enhanced Tracking Protection) en modo Estricto.
- Para el máximo anonimato, utilice el **Navegador Tor** — este enruta a través de Tor, estandariza la huella digital y bloquea JavaScript por defecto.
- Nunca use Chrome para trabajo operativo sensible. Chrome es un instrumento de recolección de datos para Google.
- Utilice perfiles de navegador separados (o navegadores completamente separados) para la navegación operativa y personal.
- Considere **Brave** como un punto medio para el uso diario, pero no lo utilice como un sustituto de Tor cuando se requiere anonimato.

---

*Esta guía no constituye asesoramiento legal. Las leyes varían según la jurisdicción.*

[← Volver al Índice](../index.md)

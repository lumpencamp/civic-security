# Modelado de Amenazas Avanzado para Organizaciones Cívicas

*Estado: Directiva de Nivel 2 | Audiencia: Planificadores de Operaciones y Equipos de Seguridad*

El modelado de amenazas no es paranoia — es la evaluación calculada y objetiva de su entorno operativo. Este marco adapta metodologías de seguridad corporativa (STRIDE, PASTA y DREAD) a un modelo cuantitativo y accionable específicamente para actores no estatales, activistas y organizaciones cívicas.

> **Regla Principal:** Nunca se prepare para un adversario de un nivel superior al que realmente enfrenta. La sobreingeniería de su seguridad crea parálisis operativa, agota a los participantes y aísla a los posibles partidarios. La subingeniería hace que la gente sea arrestada, doxeada o perjudicada. Calibre con precisión.

---

## 1. Perfil del Adversario: Los Niveles de Amenaza

Para defenderse de forma eficaz, debe comprender las **capacidades**, **presupuesto**, **autorizaciones legales** y **limitaciones políticas** de su adversario. Cada nivel requiere una postura defensiva cualitativamente diferente.

### T1: El Ruido (Doxxers, Trolls, Redes de Acoso)
*   **Ejemplos:** Foros de extrema derecha (4chan, canales de Telegram), grupos de contra-protesta, acosadores, hostigadores oportunistas.
*   **Capacidades:**
    - Inteligencia de Fuentes Abiertas (OSINT): Google dorking, búsqueda inversa de imágenes, raspado de LinkedIn/Facebook, agregación de intermediarios de datos
    - Ingeniería social (llamadas de phishing, cuentas falsas)
    - Presencia física en eventos públicos
    - Ataques a nivel de plataforma: denuncias masivas de cuentas, bombardeo de reseñas
    - Swatting (llamadas de emergencia falsas para enviar a la policía armada a su ubicación)
*   **Limitaciones:** Sin autoridad legal, sin financiamiento garantizado, generalmente baja sofisticación técnica, sujetos a demandas civiles, vulnerables a contra-OSINT
*   **Contramedidas Principales:** Optar por no participar en bases de datos (data brokers), presencia pública seudónima, cuentas sociales privadas, disciplina de higiene de la información, redes de alerta temprana de la comunidad

### T2: Fuerzas del Orden Locales (Policía, Alguaciles, Centros de Fusión Regionales)
*   **Ejemplos:** Policía municipal, alguaciles (sheriffs) del condado, fuerzas de tarea conjuntas contra el terrorismo (JTTFs), DEA, centros de fusión como CLOCC en Chicago.
*   **Capacidades:**
    - Autoridad de arresto y detención
    - Vigilancia física (seguimientos, puestos de observación fijos)
    - Simuladores de Sitios Celulares (CSS/Captadores IMSI, "Stingrays"): Capturan números IMEI/IMSI e interceptan SMS no cifrados dentro de un radio geográfico
    - Lectores Automáticos de Matrículas (ALPRs): Rastreo de ubicación en tiempo real y retroactivo
    - Bases de datos de reconocimiento facial (a menudo con bajos umbrales de precisión y sesgo racial)
    - Acceso a intermediarios de datos comerciales: datos de ubicación, gráficos sociales, historial de compras
    - Poder de citación judicial para compañías tecnológicas nacionales (Google, Apple, Meta, Verizon)
    - Informantes confidenciales infiltrados en comunidades activistas
    - Consultas a la base de datos del Centro Nacional de Información Criminal (NCIC)
    - Solicitudes de volcado de torres celulares (Tower dumps): todos los dispositivos conectados a una torre en una ventana de tiempo
*   **Limitaciones:** Fricción burocrática, cadena de mando, limitaciones presupuestarias, límites geográficos de jurisdicción, riesgo de litigios por derechos civiles, responsabilidad pública (cámaras corporales, FOIA)
*   **Contramedidas Principales:** Comunicaciones encriptadas (Signal), bloqueo de dispositivos, entrenamiento contra-vigilancia, ocultamiento facial, redes de observadores legales, capacitación para conocer sus derechos, bolsas Faraday, no llevar dispositivos personales a las acciones

### T3: Inteligencia Corporativa (Firmas de Seguridad Privada, Grupos Industriales)
*   **Ejemplos:** Pinkerton (ahora Securitas), Kroll, Guidepost Solutions, firmas de "inteligencia de amenazas" financiadas por la industria como TigerSwan (vigilancia del Dakota Access Pipeline).
*   **Capacidades:**
    - Profundos recursos financieros, a menudo financiados por corporaciones o asociaciones industriales
    - Infiltración mediante informantes de calidad profesional con identidades sostenidas
    - Herramientas OSINT avanzadas (Palantir, Maltego, ShadowDragon)
    - Vigilancia de flujos financieros y declaraciones de organizaciones sin fines de lucro
    - Litigios estratégicos (Demandas SLAPP) para llevar a la quiebra y silenciar organizaciones
    - Coordinación con o contratación de policías fuera de servicio
    - Manipulación mediática y campañas de desinformación
    - Investigaciones de antecedentes de los empleadores, familias y asociados de los organizadores
*   **Limitaciones:** Sin autoridad de arresto directo (deben involucrar a la policía), sujetos a responsabilidad civil y malas relaciones públicas, los riesgos de infiltración y exposición (sus agentes pueden volverse en su contra), sujetos a leyes RICO y de conspiración si cruzan ciertos límites
*   **Contramedidas Principales:** Estructuras celulares de "necesidad de saber", higiene financiera, separación legal de entidades, protocolos de contrainteligencia, documentar todos los intentos de intimidación para litigios civiles

### T4: Inteligencia Federal a Nivel Estatal (FBI, DHS, NSA, Inteligencia Militar)
*   **Ejemplos:** Sucesores de COINTELPRO del FBI, equipos de evaluación de amenazas del DHS, programas de recolección de la NSA, escuchas de la DEA, centros de fusión estatales con subvenciones federales.
*   **Capacidades:**
    - Presupuesto esencialmente ilimitado para objetivos designados
    - Cartas de Seguridad Nacional (NSLs): citaciones secretas con órdenes de mordaza, no se requiere revisión judicial
    - Órdenes de vigilancia FISA que cubren contactos extranjeros y sus asociados domésticos
    - Recolección de metadatos de la NSA: registros de llamadas, encabezados de correo electrónico, datos de ubicación a gran escala
    - Exploits de dispositivos de día cero (Pegasus, tipo Triangulation): compromiso remoto de teléfonos completamente actualizados
    - Operaciones encubiertas "Black bag": entrada física, implantes de dispositivos
    - Persecución coordinada: elaboración de cargos penales a partir de actividades vigiladas
    - Autoridad de búsqueda fronteriza: búsqueda sin orden judicial de dispositivos en todos los puertos de entrada a los EE. UU.
    - Detención indefinida como testigo material
    - Intercambio de inteligencia internacional con socios de los Cinco Ojos (Five Eyes)
*   **Limitaciones:** Umbral muy alto para su implementación (se requieren recursos significativos); los litigios genuinos por las libertades civiles (ACLU, EFF) han limitado algunos programas; exposición política por apuntar a un activismo puramente doméstico; existen denunciantes (whistleblowers)
*   **Aplicabilidad Realista:** A menos que su organización esté interrumpiendo directamente infraestructura crítica, tenga fondos internacionales considerados adversarios, o haya sido formalmente designada como una amenaza de terrorismo nacional, un objetivo T4 dedicado y sostenido es improbable. Es más probable una recopilación incidental y el intercambio de datos con los centros de fusión.
*   **Contramedidas Principales:** Sistema Operativo Tails, dispositivos aislados (air-gapped) para el trabajo más sensible, comunicaciones con cifrado de extremo a extremo para todo, nada de servicios en la nube para datos operativos, compartimentación física, estructura organizacional legal, transparencia pública como escudo

---

## 2. La Matriz de Evaluación de Riesgos 5×5

El riesgo se define como **Probabilidad × Impacto**. Evalúe cada vector de amenaza utilizando esta matriz antes de asignar recursos de seguridad.

**Escala de Probabilidad (1–5):**
| Puntuación | Etiqueta | Descripción |
|-------|-------|-------------|
| 1 | Raro | Casi nunca le ha sucedido a grupos similares |
| 2 | Improbable | Ha sucedido ocasionalmente pero no recientemente |
| 3 | Posible | Le ha sucedido a grupos comparables en esta ciudad |
| 4 | Probable | Le ha sucedido a su grupo o a afiliados cercanos |
| 5 | Casi Seguro | Está sucediendo activamente o se anticipa de forma inminente |

**Escala de Impacto (1–5):**
| Puntuación | Etiqueta | Descripción |
|-------|-------|-------------|
| 1 | Insignificante | Inconveniente menor, recuperable en horas |
| 2 | Menor | Interrupción breve, sin daños duraderos |
| 3 | Moderado | Interrupción significativa, detención a corto plazo, fuga parcial de información |
| 4 | Severo | Organizador clave arrestado, compromiso mayor de la información |
| 5 | Crítico | Colapso organizacional, encarcelamiento a largo plazo, daño físico |

**Puntuación de Riesgo = Probabilidad × Impacto** (Rango: 1–25)

| Rango de Puntuación | Prioridad | Acción Requerida |
|-------------|----------|-----------------|
| 20–25 | **CRÍTICO** | Implementar todas las contramedidas inmediatamente |
| 12–19 | **ALTA** | Priorizar; implementar dentro de las 48 horas |
| 6–11 | **MEDIA** | Programar; implementar antes de la próxima acción |
| 1–5 | **BAJA** | Monitorear; documentar; aceptar o mitigar de manera oportunista |

---

## 3. Ejemplos Prácticos de Modelado de Amenazas

### Ejemplo A: Sindicato de Inquilinos Local (Entorno de Amenaza T1/T2)
*Organizando huelgas de alquiler contra una gran empresa de gestión inmobiliaria.*

| Vector de Amenaza | Probabilidad | Impacto | Puntuación | Prioridad |
|---------------|-----------|--------|-------|----------|
| Doxxing a organizadores principales | 4 | 3 | 12 | ALTA |
| Propietario contrata investigadores privados | 3 | 2 | 6 | MEDIA |
| Policía observa reuniones públicas | 2 | 2 | 4 | BAJA |
| Desalojo como represalia | 4 | 4 | 16 | ALTA |
| Infiltración en el grupo de WhatsApp | 3 | 3 | 9 | MEDIA |

**Contramedidas Principales:** Signal en lugar de WhatsApp, portavoces públicos seudónimos, exclusión de bases de datos de información, observador legal en todas las reuniones públicas.

### Ejemplo B: Periodista Cubriendo Operativos Federales (Entorno de Amenaza T2/T4)
*Informando sobre operativos de aplicación de leyes de inmigración.*

| Vector de Amenaza | Probabilidad | Impacto | Puntuación | Prioridad |
|---------------|-----------|--------|-------|----------|
| Identificación de la fuente por metadatos | 4 | 5 | 20 | CRÍTICA |
| Incautación de dispositivos en la frontera | 3 | 4 | 12 | ALTA |
| Citación judicial por comunicaciones | 3 | 4 | 12 | ALTA |
| Intrusión digital dirigida | 2 | 5 | 10 | MEDIA |
| Vigilancia física de reuniones con fuentes | 2 | 4 | 8 | MEDIA |

**Contramedidas Principales:** Signal con mensajes temporales, SecureDrop para la recepción de fuentes, SO Tails para el manejo de documentos confidenciales, dispositivo cifrado al cruzar fronteras, asesoramiento legal bajo contrato.

---

## 4. El Marco de Amenazas STRIDE (Adaptado)

STRIDE es una metodología estructurada para identificar vectores de ataque. Evalúe cada categoría frente a los activos específicos de su organización.

| Categoría | Definición | Ejemplo Activista | Contramedida |
|----------|-----------|------------------|----------------|
| **S**poofing (Suplantación) | El adversario se hace pasar por una identidad confiable | Aliado falso se une al grupo de Signal | Protocolos de verificación, establecimiento de confianza en persona |
| **T**ampering (Manipulación) | Los datos o sistemas se modifican sin autorización | Pruebas adulteradas, comunicaciones alteradas | Firmas criptográficas, cadena de custodia |
| **R**epudiation (Repudio) | Acciones tomadas sin rendición de cuentas | Un informante niega la filtración; disputas legales | Registros seguros con marca de tiempo, documentación de testigos |
| **I**nformation Disclosure (Divulgación) | Exposición de información confidencial | OSINT revela la dirección de un organizador | Minimización de datos, estricta necesidad de saber |
| **D**enial of Service (Denegación) | Interrupción de las operaciones | Prohibiciones de plataforma, DDoS al sitio web | Canales redundantes, capacidades sin conexión |
| **E**levation of Privilege (Elevación) | Obtención de acceso no autorizado | Compromiso de cuentas, robo de dispositivos | Autenticación robusta, cifrado de dispositivos |

---

## 5. Protocolo de Evaluación de Amenazas Continuo

El modelado de amenazas no es un ejercicio de una sola vez. Vuelva a evaluar después de cada evento significativo.

**Reevalúe inmediatamente cuando:**
- Un miembro es arrestado, detenido o se le incauta el dispositivo
- Las fuerzas del orden despliegan nueva tecnología en su ciudad (por ejemplo, nueva red de cámaras, contrato de reconocimiento facial)
- Se identifica un informante o infiltrado conocido
- Su organización recibe una atención mediática o legal inusual
- Un miembro informa haber sido abordado o reclutado por la policía
- Hay una escalada significativa en el entorno político (nueva legislación, represión)

**Cadencia de revisión regular:** Como mínimo, realice una sesión completa de modelado de amenazas trimestralmente, o antes de cualquier acción importante planificada.

---

*Esta guía no constituye asesoramiento legal. Las leyes varían según la jurisdicción. Para asuntos legales, consulte a un abogado con licencia.*

[← Volver al Índice](../index.md)

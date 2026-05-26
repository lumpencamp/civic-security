# Alternativas a Signal: Eligiendo el Mensajero Seguro Adecuado

*Estado: Nivel 2 | Audiencia: Organizadores evaluando herramientas de comunicación para entornos de amenaza específicos*

Signal es la recomendación predeterminada para la mayoría de las comunicaciones de activistas, pero no es la herramienta adecuada para cada situación. Esta guía evalúa las alternativas a Signal más relevantes, explicando contra qué protegen que Signal no lo haga (y viceversa), y cuándo usar cada una.

---

## 1. Cuándo Signal Podría no Ser Suficiente

Las limitaciones de Signal en escenarios de amenaza específicos:

- **Requisito de número de teléfono:** Signal requiere un número de teléfono para el registro. Esto crea un vínculo de identidad; incluso con un número VOIP, un adversario sofisticado puede potencialmente rastrear patrones de registro.
- **Visibilidad de metadatos:** Si bien Signal oculta el contenido, su ISP y los observadores de red pueden ver que se está conectando a los servidores de Signal. Esto es significativo en jurisdicciones donde Signal es monitoreado o bloqueado.
- **Infraestructura centralizada:** Signal es operado por una corporación sin fines de lucro con servidores en los EE. UU. Si bien Signal tiene un sólido historial de resistencia a las citaciones (tienen muy pocos datos para dar), son una entidad legal a la que se puede apuntar.
- **Dependencia de la red:** Signal requiere conectividad a Internet (Wi-Fi o celular). Si las redes se interrumpen o monitorean en un punto de estrangulamiento (*chokepoint*), Signal deja de estar disponible o se vuelve riesgoso.

---

## 2. Briar

**Mejor para:** Situaciones en las que el acceso a Internet no está disponible, está bloqueado o monitoreado específicamente

**Cómo funciona:**
- Mensajería cifrada entre pares (*peer-to-peer*) sin servidor central
- Se conecta a través de Tor (cuando hay Internet disponible), Wi-Fi (malla local o *mesh*) o Bluetooth (directo de dispositivo a dispositivo)
- Los mensajes se almacenan en su dispositivo, no en ningún servidor
- No se requiere número de teléfono o correo electrónico — la identidad se basa en claves criptográficas

**Qué la hace única:**
- Funciona sin Internet en absoluto, mediante Bluetooth y redes de malla (*mesh networking*) Wi-Fi. Los dispositivos dentro de un radio de aproximadamente 10 metros pueden intercambiar mensajes a través de Bluetooth; dentro del rango de Wi-Fi a través de Wi-Fi local.
- No hay metadatos almacenados en los servidores porque no hay servidores
- De código abierto, mantenido por el Briar Project

**Limitaciones:**
- Base de usuarios más pequeña: ambas partes deben tener instalado Briar
- El alcance de Bluetooth es limitado (~10 metros); el de Wi-Fi un poco más
- No hay llamadas de voz o video (solo mensajería)
- Se sincroniza solo cuando los dispositivos están dentro del alcance (para el modo de malla sin conexión)

**Ajuste al modelo de amenazas:**
- ✅ Interrupción de Internet (protestas con comunicaciones bloqueadas)
- ✅ Sin exposición del número de teléfono
- ✅ Entornos de amenaza T2 donde el uso de Signal en sí es monitoreado
- ❌ Comunicaciones diarias (menos conveniente que Signal)
- ❌ Grupos grandes (la malla de Bluetooth/Wi-Fi escala de forma deficiente)

**Descarga:** briarproject.org (Solo Android; el desarrollo para iOS está en curso)

---

## 3. Session

**Mejor para:** Situaciones que no requieren número de teléfono y exigen una infraestructura descentralizada

**Cómo funciona:**
- Red de enrutamiento cebolla descentralizada (similar a Tor) para enrutar mensajes
- No se requiere número de teléfono o correo electrónico — la identidad es un "ID de Session" alfanumérico generado aleatoriamente
- No hay servidores centrales que citar — los mensajes se enrutan a través de la red descentralizada de Session
- Construida sobre el cifrado del Protocolo Signal

**Qué la hace única:**
- No se requiere información de la cuenta: recibe un ID de Session, lo comparte con las personas que desea contactar
- El enrutamiento descentralizado hace que el análisis de tráfico sea más difícil
- De código abierto; operada por OPTF (Oxen Privacy Tech Foundation), una organización sin fines de lucro con sede en Australia

**Limitaciones:**
- Relativamente nueva; base de usuarios más pequeña
- Sin un equivalente de remitente sellado (*sealed sender*) (los metadatos son más difíciles de ocultar en la capa de enrutamiento)
- Cliente de escritorio disponible pero menos maduro que Signal Desktop
- Las llamadas de voz están disponibles, pero son de menor calidad que en Signal

**Ajuste al modelo de amenazas:**
- ✅ El número de teléfono no está vinculado a la identidad
- ✅ Infraestructura descentralizada (sin una única entidad a la que citar judicialmente)
- ✅ Comunicaciones de la organización que necesitan estar totalmente compartimentadas de la identidad del teléfono
- ❌ No supera a Signal en cuanto a la seguridad diaria del contenido de los mensajes
- ❌ La comunidad más pequeña hace que la solicitud de adopción sea más difícil

**Descarga:** getsession.org

---

## 4. Element / Matrix

**Mejor para:** Comunicaciones organizacionales que requieran infraestructura de grupo persistente y autoalojada

**Cómo funciona:**
- Matrix es un protocolo de comunicación abierto y federado
- Element es el cliente principal (al igual que Gmail es un cliente para correo electrónico)
- Puede alojar su propio servidor base (*homeserver*) de Matrix (eliminando la dependencia de terceros)
- Cifrado de extremo a extremo disponible para las salas (debe habilitarse explícitamente)
- Son posibles los puentes hacia otras plataformas (Signal, Telegram, IRC, Slack)

**Qué la hace única:**
- **Autoalojamiento (*Self-hosting*):** Ejecute su propio servidor. Sus mensajes nunca tocan la infraestructura de terceros. Las citaciones de las fuerzas del orden no tienen una empresa estadounidense a la que notificar.
- **Salas de grupo persistentes:** A diferencia de los grupos de Signal, las salas de Matrix pueden tener un historial persistente en el que los miembros pueden retroceder (configurable). Mejor para la coordinación organizacional.
- **Federación:** Las salas de Matrix pueden incluir miembros de diferentes servidores base, como el correo electrónico: usted controla su servidor, otros controlan el suyo y todos pueden comunicarse.

**Limitaciones:**
- Complejidad de configuración: el autoalojamiento requiere infraestructura técnica (servidor, dominio, mantenimiento)
- El cifrado de extremo a extremo requiere una configuración deliberada; no todas las salas están cifradas por defecto
- La verificación de las claves de otros usuarios es más compleja
- Las cuentas de Matrix alojadas (matrix.org) están sujetas a la jurisdicción legal de esa empresa

**Ajuste al modelo de amenazas:**
- ✅ Comunicación organizacional persistente (proyectos, grupos de trabajo)
- ✅ Autoalojado = no hay servidor de terceros al que citar
- ✅ Entornos de amenaza T3 donde el compromiso del servidor corporativo es una preocupación
- ❌ No es apropiado para uso anónimo (la creación de cuentas generalmente requiere correo electrónico)
- ❌ Excesivo para la mayoría de las comunicaciones personales

**Descarga:** element.io | Servidor base (*Homeserver*) Matrix: matrix.org (alojado) o matrix.org/docs/guides/homeserver-setup (autoalojado)

---

## 5. SimpleX Chat

**Mejor para:** Máxima protección de metadatos para conversaciones bilaterales

**Cómo funciona:**
- Sin cuentas de usuario, sin números de teléfono, sin ID de usuario de ningún tipo: totalmente descentralizado
- Los mensajes se enrutan a través de servidores de retransmisión (*relay*), pero los servidores de retransmisión no pueden asociar las identidades del remitente y el receptor
- Cada conversación utiliza una dirección de conexión única de un solo uso
- De código abierto, creado por SimpleX Chat Ltd.

**Qué la hace única:**
- La protección de metadatos más radical de cualquier mensajero popular: los servidores de retransmisión literalmente no pueden saber quién habla con quién, porque las direcciones de conexión son de un solo uso y no están vinculadas a identidades persistentes.
- Sin un registro de identidad centralizado que pueda ser citado.

**Limitaciones:**
- Aún no hay grupos (en desarrollo)
- Relativamente nueva; base de usuarios más pequeña
- El no tener número de teléfono significa que debe compartir códigos QR de conexión o enlaces fuera de banda (*out-of-band*) para iniciar una conversación

**Ajuste al modelo de amenazas:**
- ✅ Máxima protección de metadatos para conversaciones uno a uno
- ✅ Protección de fuentes (periodistas que reciben información de fuentes)
- ✅ Situaciones en las que incluso la existencia de una relación de comunicación debe ocultarse
- ❌ Aún no es adecuada para la comunicación organizacional grupal

**Descarga:** simplex.chat

---

## 6. Wire

**Mejor para:** Equipos que necesitan comunicación cifrada de nivel profesional sin números de teléfono personales

**Cómo funciona:**
- Mensajería, voz, video e intercambio de archivos cifrados de extremo a extremo
- La cuenta se puede crear solo con una dirección de correo electrónico (no se requiere número de teléfono)
- Versión Wire Pro comercializada para empresas; Wire Personal es gratis

**Limitaciones:**
- Empresa europea con infraestructura de servidores — sujeta a los procesos legales de la UE
- Metadatos: Wire almacena algunos metadatos sobre las comunicaciones
- La compañía ha recibido solicitudes de las fuerzas del orden

**Ajuste al modelo de amenazas:**
- ✅ Equipos incómodos con el requisito del número de teléfono de Signal
- ✅ Uso organizacional profesional
- ❌ No recomendado para comunicaciones de alto riesgo — Signal es más fuerte en general

---

## 7. Guía de Decisión

| Pregunta | Recomendación |
|---------|---------------|
| Mensajería segura diaria con contactos conocidos | **Signal** |
| Sin número de teléfono, sin cuenta de servidor | **Briar** o **Session** |
| Comunicaciones cuando Internet no está disponible | **Briar** (Bluetooth/Wi-Fi mesh) |
| Infraestructura de grupo persistente organizacional | **Element/Matrix** (autoalojado) |
| Máxima protección de metadatos, uno a uno | **SimpleX Chat** |
| Colaboración en equipo sin números de teléfono personales | **Wire** o **Session** |
| Comunicación anónima de fuente a periodista | **SecureDrop** + **Signal** |

---

## 8. Qué NO Usar Nunca para Comunicaciones Organizacionales Sensibles

| Plataforma | Por Qué No |
|---------|--------|
| **WhatsApp** | Propiedad de Meta; los metadatos se recopilan; el modelo de negocio son los datos |
| **Telegram** | No cifrado de extremo a extremo por defecto; los chats predeterminados están cifrados en el servidor; la nube de Telegram almacena todos los chats no secretos |
| **Facebook Messenger** | Infraestructura de vigilancia de Meta; no está cifrado de extremo a extremo por defecto |
| **Discord** | Sin cifrado de extremo a extremo; empresa estadounidense con un extenso historial de cooperación con las fuerzas de seguridad |
| **Slack** | Diseñado para la vigilancia corporativa; los administradores ven todos los mensajes; sin cifrado de extremo a extremo |
| **Correo electrónico estándar (no cifrado)** | Sin protección de contenido; los metadatos se registran extensamente |
| **SMS/Text** | Sin cifrado; interceptable por Stingrays; los registros del operador se retienen |

---

*Esta guía no constituye asesoramiento legal. Las leyes varían según la jurisdicción.*

[← Volver al Índice](../index.md)
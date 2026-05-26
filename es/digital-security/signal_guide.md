# Signal Messenger: Guía Completa de Seguridad

*Estado: Nivel 1 | Audiencia: Todos los miembros — comience aquí para comunicaciones seguras*

Signal es el estándar de oro para la mensajería cifrada entre activistas, periodistas, abogados e investigadores de seguridad. Utiliza el Protocolo Signal, un sistema de cifrado de extremo a extremo de última generación que ha sido auditado de forma independiente, es de código abierto y cuenta con la confianza de criptógrafos de todo el mundo. Esta guía cubre no solo la instalación, sino todas las funciones y configuraciones relevantes para la seguridad.

> **¿Por qué Signal y no WhatsApp?** WhatsApp utiliza el Protocolo Signal para el cifrado de mensajes, pero es propiedad de Meta (Facebook), está sujeto a procesos legales de EE. UU., retiene metadatos (con quién habla y cuándo) y tiene un historial problemático de vulnerabilidades de seguridad en su implementación. La recopilación de metadatos de Signal es mínima por diseño, y es operada por una fundación sin fines de lucro sin interés comercial en sus datos.

---

## 1. Instalación y Configuración Inicial de Seguridad

### 1.1 Descargar Signal Correctamente

- **Android:** Descargue desde Google Play Store (signal.org/android/apk para una descarga directa del APK sin Play Store si es necesario)
- **iOS:** Descargue desde Apple App Store
- **Escritorio:** Descargue solo desde signal.org — nunca desde sitios de terceros

**Verifique la descarga:** En signal.org, compare la suma de comprobación (checksum) del APK con la suma de comprobación publicada antes de la instalación. Esto protege contra descargas manipuladas.

### 1.2 Consideraciones sobre el Número de Teléfono

Signal requiere un número de teléfono para el registro. Esta es una limitación significativa para los usuarios de alto riesgo:

- **Opción 1 (La mayoría de los usuarios):** Use su número de teléfono móvil real. Signal no expone este número a las personas a menos que lo comparta específicamente, pero las citaciones de las fuerzas del orden a Signal podrían revelar que su número está registrado (aunque Signal retiene datos mínimos — consulte su informe de transparencia).
- **Opción 2 (Mayor riesgo):** Regístrese con un número VOIP (Google Voice, JMP.chat) para separarlo de su número real. JMP.chat sobre Tor es la opción más privada.
- **Opción 3 (Riesgo más alto):** Regístrese con una SIM prepaga comprada en efectivo, activada a través de una red Wi-Fi pública. Use este número solo para Signal, nunca para ningún otro propósito.

### 1.3 Bloqueo de Registro

**Habilitar inmediatamente después de la instalación:**

*Configuración → Cuenta → Bloqueo de registro*

El Bloqueo de Registro evita que alguien vuelva a registrar su número de Signal sin su PIN, incluso si obtienen su tarjeta SIM (ataque de intercambio de SIM o *SIM swap*). Esta es una protección crítica. Establezca un PIN seguro y guárdelo de forma segura.

---

## 2. Configuraciones de Privacidad Críticas

Abra *Configuración → Privacidad* y configure lo siguiente:

### 2.1 Privacidad del Número de Teléfono
- **Quién puede ver mi número:** Establecer en "Nadie" o "Mis contactos"
- **Quién puede encontrarme por mi número:** Establecer en "Nadie"

*Esto evita que las personas encuentren su cuenta a través de su número, incluso si lo tienen.*

### 2.2 Mensajes Desaparecidos
- **Temporizador predeterminado para chats nuevos:** Establezca un temporizador de mensajes desaparecidos predeterminado para todas las conversaciones nuevas.
  - **Recomendación para la mayoría de los usuarios:** 1 semana
  - **Recomendación para comunicaciones de alto riesgo:** 1 día o menos
  - **Para las conversaciones más sensibles:** 1 hora, con acuerdo explícito de la otra parte

*Los mensajes desaparecidos lo protegen si su dispositivo es incautado. Los mensajes que ya no existen no se pueden leer.*

### 2.3 Confirmaciones de Lectura e Indicadores de Escritura
- **Mostrar confirmaciones de lectura:** Deshabilitar
- **Mostrar indicadores de escritura:** Deshabilitar

*Estos revelan patrones de comportamiento (cuándo lee los mensajes, cuándo está escribiendo) que, aunque parecen menores, contribuyen a una imagen de vigilancia.*

### 2.4 Vistas Previas de Enlaces
- **Generar vistas previas de enlaces:** Deshabilitar

*Las vistas previas de enlaces requieren que Signal acceda a la URL: esto crea un registro de que se accedió a la URL, potencialmente desde su IP si no usa una VPN.*

### 2.5 Bloqueo de Pantalla
- **Bloqueo de pantalla:** Habilitar
- Establezca un tiempo de espera de 5 minutos o menos

### 2.6 Seguridad de Pantalla
- **Seguridad de pantalla (Android):** Habilitar — evita que Signal aparezca en el selector de aplicaciones y deshabilita las capturas de pantalla dentro de la aplicación

### 2.7 Teclado Incógnito
- **Teclado incógnito (Android):** Habilitar — evita que su aplicación de teclado aprenda y almacene lo que escribe en Signal

---

## 3. Seguridad de la Conversación Individual

### 3.1 Verificación de Números de Seguridad

Cada conversación de Signal tiene un "Número de seguridad": una huella criptográfica única para su conversación con esa persona específica en su dispositivo específico.

**Por qué importa:** Si las fuerzas del orden o un atacante realizan un ataque de hombre en el medio (insertándose entre usted y su contacto), el Número de seguridad cambiará.

**Cómo verificar:**
1. Abra una conversación → toque el nombre del contacto → *Verificar números de seguridad*
2. Compare el número de seguridad **en persona** o a través de un canal seguro separado (no a través de Signal — si está comprometido, una confirmación comprometida es inútil)
3. Marque como verificado una vez confirmado

**Cuándo volver a verificar:**
- Si Signal le notifica que el número de seguridad ha cambiado (esto podría significar que el contacto obtuvo un nuevo dispositivo, reinstaló Signal o — lo que es más preocupante — alguien más tiene su número)
- Antes de compartir información altamente sensible
- Después de cualquier período de tiempo donde la seguridad haya estado en duda

### 3.2 Notas Personales

Use la conversación "Notas personales" como un bloc de notas personal cifrado. Los mensajes que se envía a sí mismo están cifrados de extremo a extremo y desaparecen en el temporizador establecido. Úselo para almacenar:
- Información sensible temporal a la que se deba acceder brevemente
- Notas de reuniones en persona
- Información de contacto legal

### 3.3 Solicitudes de Mensaje

Si alguien con quien no ha hablado antes le envía un mensaje, aparece como una "Solicitud de mensaje". Puede aceptar o eliminar sin que el remitente sepa que recibió el mensaje. Esto evita que extraños sepan de inmediato que su cuenta está activa.

---

## 4. Seguridad de Grupo

Los grupos son la superficie de seguridad más compleja en Signal.

### 4.1 Administración del Grupo

- **Permisos de administrador:** Configure para que solo los administradores puedan agregar nuevos miembros y cambiar la configuración del grupo (*Configuración del grupo → Permisos*)
- **Mantenga pequeño el recuento de administradores:** 2–3 administradores máximo. Más administradores significan más posibles puntos de compromiso.
- **Revise la membresía regularmente:** Elimine a los miembros que han abandonado la organización o cuya confianza es incierta
- **Enlaces de grupo:** Deshabilite los enlaces de grupo (*Configuración del grupo → Enlace de grupo*) a menos que los esté utilizando activamente para una campaña de reclutamiento controlada. Un enlace de grupo abierto puede permitir que cualquiera con el enlace se una.

### 4.2 Lo que los Grupos NO Protegen

Incluso en un grupo de Signal cifrado de extremo a extremo:
- **Cualquier miembro del grupo puede tomar capturas de pantalla o reenviar mensajes.** No hay prevención técnica.
- **Cualquier miembro del grupo puede revelar la existencia del grupo y la membresía general.**
- **Los metadatos del grupo** (que existe un grupo de cierto tamaño y que números específicos son miembros) pueden ser visibles para los servidores de Signal en algunas configuraciones.
- **Los grupos grandes tienen inherentemente más probabilidades de contener miembros no evaluados.** Trate los grupos grandes como semipúblicos.

**Regla operativa:** El grupo es tan seguro como su miembro menos seguro. No comparta información en un grupo que no querría que tuviera el miembro menos confiable.

### 4.3 Segmentación de Grupos

Siga el modelo celular: mantenga grupos separados y pequeños para cada célula operativa. No mantenga un grupo grande para todos los asuntos de la organización.

- **Grupo de todo el personal:** Anuncios de cara al público, información conocida públicamente, construcción de moral y comunidad
- **Grupos específicos de la célula:** Discusión operativa restringida a los miembros de esa célula
- **Grupo de liderazgo:** Coordinación estratégica entre los organizadores principales
- **Grupo legal:** Incluye a abogados y participantes afectados únicamente; estrictamente según la necesidad de saber

---

## 5. Llamadas y Video

### 5.1 Llamadas de Signal
- Las llamadas de voz y video de Signal están cifradas de extremo a extremo
- En Android, puede habilitar *Retransmitir llamadas* (*Configuración → Privacidad → Avanzado → Siempre retransmitir llamadas*), lo que enruta el audio de la llamada a través de los servidores de Signal en lugar de hacerlo directamente entre los dispositivos. Esto oculta su dirección IP de su contacto a costa de una latencia ligeramente mayor. **Habilite esto para contactos de alto riesgo.**

### 5.2 Llamadas de Grupo
- Signal admite llamadas grupales cifradas para hasta 50 participantes
- Se aplican las mismas reglas que en los chats de grupo: la llamada es tan segura como su participante menos seguro

---

## 6. Remitente Sellado

*Configuración → Privacidad → Avanzado → Remitente sellado*

El remitente sellado (*Sealed sender*) es una función en la que los metadatos sobre quién envía un mensaje a quién se ocultan incluso para los servidores de Signal. Habilite "Permitir de cualquiera" para recibir mensajes de remitente sellado de contactos que no están en su lista, y asegúrese de tenerlo habilitado para el envío.

---

## 7. Nota Personal: Lo que Signal No Puede Proteger

Signal cifra el contenido de los mensajes en tránsito y en su dispositivo. No puede proteger contra:

- **Compromiso del dispositivo:** Si su teléfono tiene malware o un exploit de día cero, un atacante puede leer sus mensajes mientras los escribe, independientemente del cifrado
- **Acceso físico al dispositivo:** Si su dispositivo es incautado y se obtiene su código de acceso, todos los mensajes que aún no han desaparecido son accesibles
- **Traición de los participantes:** Signal es una herramienta, no un sistema de evaluación. Una persona que tiene acceso legítimo a una conversación siempre puede revelar su contenido
- **Metadatos de los extremos:** Signal no puede ocultar que está usando Signal (su ISP y los operadores de red pueden ver conexiones a los servidores de Signal, aunque no el contenido)
- **Errores operativos:** Decir lo incorrecto a la persona incorrecta, usar Signal en un dispositivo de otra manera inseguro

---

## 8. Signal para Escritorio

Signal de escritorio es útil para escribir mensajes más largos y coordinar desde una computadora. Consideraciones de seguridad:

- **Dispositivo vinculado:** Signal de escritorio es un dispositivo vinculado secundario — comparte su identidad de Signal y tiene acceso a todos sus mensajes
- **Seguridad física:** Su computadora puede ser menos segura que su teléfono; considere quién tiene acceso físico a ella
- **Bloqueo de pantalla:** Habilite el bloqueo de pantalla en la aplicación de escritorio
- **Nota:** Si las fuerzas del orden incautan su computadora, los mensajes de Signal de escritorio son accesibles si la computadora está desbloqueada o si se vence el cifrado. Los mensajes desaparecidos se aplican por igual.

---

*Esta guía no constituye asesoramiento legal. Las leyes varían según la jurisdicción.*

[← Volver al Índice](../index.md)

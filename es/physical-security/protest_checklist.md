# Lista de Verificación Táctica para Despliegue en el Campo

*Estado: Manual de Logística y Preparación en el Campo | Audiencia: Equipos de Acción Directa y Organizadores de Campo*

La seguridad física y la seguridad digital están indisolublemente unidas durante cualquier evento de acción directa. Una falla en un dominio compromete instantáneamente al otro. Esta lista de verificación sigue un estricto cronograma de despliegue cronológico: **T-Menos 72 Horas**, **T-Menos 24 Horas**, **T-Menos 2 Horas**, **Durante la Acción** y **Posterior a la Acción**.

> **Requisito previo obligatorio:** Antes de usar esta lista de verificación, complete la [Guía de Modelado de Amenazas](../digital-security/threat_modeling_guide.md) para su acción específica. El nivel apropiado de precaución escala de acuerdo a su nivel de amenaza.

---

## Fase 0: T-Menos 72 Horas — Planificación y Coordinación

### Preparación Organizacional
- [ ] **Evaluación de amenazas completada:** El equipo de seguridad revisó el modelo de amenazas específico de la acción.
- [ ] **Roles asignados:** Líder de la acción, enlace con observadores legales, paramédicos, coordinador de apoyo de cárcel, coordinador de comunicaciones, contacto de medios (si aplica).
- [ ] **Grupos de afinidad formados:** Grupos de 4 a 7 personas que actuarán juntas, se mantendrán juntas y serán responsables entre sí.
- [ ] **Protocolo de toma de decisiones acordado:** ¿Qué decisiones requieren consenso del grupo de afinidad vs. la autoridad del líder de acción? ¿Bajo qué condiciones los grupos de afinidad se retiran independientemente?
- [ ] **Apoyo legal asegurado:** Se contactó al NLG o su equivalente, se solicitaron observadores legales, se distribuyó el número de emergencia.
- [ ] **Apoyo médico asegurado:** Médicos callejeros invitados o identificados, ubicaciones de primeros auxilios exploradas.
- [ ] **Plan de comunicaciones establecido:** Canal principal (Signal), canal de respaldo (Meshtastic o alternativa acordada), contacto de emergencia fuera de la red (out-of-band).

### Configuración de Apoyo de Cárcel
- [ ] **Coordinador de apoyo de cárcel designado:** Esta persona NO asiste a la acción. Permanece accesible por teléfono.
- [ ] **Información de los participantes recopilada:** Nombre legal completo, fecha de nacimiento, cualquier información médica crítica (alergias, medicamentos, condiciones), contacto de emergencia de cada persona que podría ser arrestada.
- [ ] **Estado del fondo de fianza confirmado:** ¿El fondo es accesible? ¿Quién tiene autorización para desembolsar fondos?
- [ ] **Plan de monitoreo de lectura de cargos:** ¿Quién verificará los horarios de los tribunales si los participantes son retenidos durante la noche?

---

## Fase 1: T-Menos 24 Horas — Preparación y Seguridad del Dispositivo

### Preparación Digital
- [ ] **Copia de seguridad completa del dispositivo:** Haga una copia de seguridad de su teléfono principal en una unidad externa segura, fuera de línea y encriptada. Si su dispositivo es incautado, esta copia de seguridad preservará sus datos.
- [ ] **Decisión del dispositivo tomada:** ¿Llevará su teléfono principal, un teléfono desechable (burner) o ningún teléfono? Esta decisión depende de su modelo de amenazas.
  - **Acciones de bajo riesgo** (marchas permitidas, reuniones comunitarias): Se acepta el teléfono principal con las configuraciones a continuación.
  - **Acciones de riesgo medio** (acciones sin permiso, desobediencia civil): Se prefiere un teléfono desechable; si usa el teléfono principal, aplique sanitización agresiva.
  - **Acciones de alto riesgo** (posibles cargos por delitos graves, entorno de amenaza T3/T4): Ningún teléfono personal. Teléfono desechable o sin dispositivo.
- [ ] **Bloqueo biométrico:** Desactive Face ID y Touch ID. Establezca una frase de contraseña alfanumérica fuerte (mínimo 12 caracteres: mayúsculas, minúsculas, números y símbolos). Registre esta frase en un lugar seguro al que pueda acceder después de su liberación.
- [ ] **Sanitización de datos (si lleva el teléfono principal):**
  - Elimine todos los datos organizativos no esenciales, fotos y mensajes.
  - Vacíe las carpetas "Eliminados recientemente" (fotos y notas).
  - Borre el historial del navegador y las cookies.
  - Cierre sesión en aplicaciones confidenciales (banca, correo electrónico de trabajo).
  - Desactive temporalmente la sincronización de iCloud/Google Drive.
  - Revise y revoque los permisos de aplicaciones innecesarios.
- [ ] **Configuración de Signal:**
  - Habilite los mensajes temporales en todos los chats (1 semana o menos para contactos operativos).
  - Active el bloqueo de registro (Configuración → Cuenta → Bloqueo de registro).
  - Habilite "Nota personal" (Note to Self) como un bloc de notas seguro.
  - Confirme su número de seguridad con los contactos clave en persona si es posible.
- [ ] **Contacto de emergencia escrito:** Número de NLG/FDLA escrito en el antebrazo con un marcador permanente.
- [ ] **Número de abogado guardado:** Guardado en el teléfono bajo un nombre neutral (en caso de que el teléfono sea incautado y revisado) Y memorizado o escrito en el cuerpo.

### Adquisición de Teléfono Desechable (si aplica)
- [ ] **Comprado con efectivo** en una tienda física (no en línea — sin vínculo con la dirección de envío).
- [ ] **Comprado mientras NO llevaba su teléfono personal** (los datos de ubicación de su teléfono personal lo situarían en el lugar de la compra).
- [ ] **Comprado en una tienda sin reconocimiento facial** (las grandes cadenas de tiendas lo usan cada vez más).
- [ ] **Tarjeta SIM prepaga comprada con efectivo** en una ubicación y momento diferente, si es posible.
- [ ] **Dispositivo activado a través de una red Wi-Fi pública** que no usa habitualmente, preferiblemente con una VPN o Tor ejecutándose.
- [ ] **Sin cuentas de Google/Apple vinculadas** — utilícelo sin iniciar sesión, o cree una nueva cuenta anónima a través de Tor.
- [ ] **Solo aplicaciones necesarias instaladas:** Signal, un mapa descargado sin conexión (OsmAnd, Maps.me), el número de teléfono del NLG guardado.

### Preparación Física y Legal
- [ ] **Información médica escrita en el cuerpo:** Tipo de sangre, alergias graves y cualquier condición que los paramédicos deban saber — escrito en el antebrazo interno o en el muslo con marcador permanente.
- [ ] **Decisión sobre identificación personal:** Conozca las leyes de su estado. En Illinois, debe proporcionar su nombre si es detenido legalmente. Considere si debe llevar identificación — confirma su identidad ante la policía si lo detienen, pero también ante los hospitales si resulta herido.
- [ ] **Sesión informativa legal atendida o revisada:** Conozca las leyes específicas relevantes para esta acción en esta jurisdicción.
- [ ] **Condiciones médicas divulgadas:** A su grupo de afinidad y a los paramédicos — no a toda su organización.

---

## Fase 2: T-Menos 2 Horas — Preparación y Bloqueo Final

*Esta fase ocurre en un área de concentración segura, lejos de la zona de acción, antes de transitar hacia el lugar.*

### Equipo Físico y Equipo de Protección Personal (PPE)
- [ ] **Ocultación facial:**
  - Mascarilla N95 (máxima eficacia contra el reconocimiento facial y los irritantes químicos).
  - Lentes de sol polarizados o de lentes oscuros.
  - Sombrero de ala corta (sin marca).
  - *Nota:* Los sistemas de reconocimiento facial analizan la geometría de la parte superior del rostro — cubrirse la nariz y la boca dejando los ojos visibles es insuficiente. Cúbrase desde la frente hasta la barbilla si su objetivo es la ocultación.
- [ ] **Ropa:**
  - Ropa sin marca, de color sólido y en capas. Los logotipos distintivos, los patrones o los colores crean "marcadores" identificables en los videos de vigilancia.
  - Las capas le permiten cambiar de apariencia rápidamente (quitarse una chaqueta exterior cambia su perfil en segundos).
  - Calzado cerrado, de suela gruesa.
  - Adecuada para el clima (la hipotermia es un riesgo médico real en acciones prolongadas al aire libre en invierno).
- [ ] **Botiquín de primeros auxilios:** Como mínimo, para su grupo de afinidad:
  - Guantes de nitrilo.
  - Almohadillas de gasa y cinta médica.
  - Toallitas antisépticas.
  - Lavaojos (solución salina) — para exposición a gas pimienta.
  - Manta térmica de emergencia (Mylar).
  - Cualquier medicamento personal (lleve suficiente para 24 horas en caso de una detención prolongada).
- [ ] **Nutrición e hidratación:**
  - Agua (mínimo 1 litro por persona).
  - Comida alta en calorías (nueces, barras energéticas — nada perecedero).
  - Medicamentos, incluidos los medicamentos psiquiátricos — omitir una dosis durante la detención es un daño real.
- [ ] **Solo efectivo:** Sin tarjetas de crédito que puedan ser rastreadas hasta su identidad. Efectivo para transporte, comida, llamadas telefónicas de fianza. Mínimo recomendado: $40.

### Configuración Final del Dispositivo
- [ ] **Revisión final del dispositivo:** Confirme que la biometría esté desactivada. Confirme que la contraseña esté configurada.
- [ ] **Decisión sobre el modo avión:** En acciones de alto riesgo, considere activar el modo avión a su llegada (evita que los simuladores Stingray capturen su IMEI/IMSI y evita el rastreo de ubicación en tiempo real a través de las torres de telefonía celular). Todavía puede usar mapas fuera de línea y tomar fotos; perderá la comunicación celular.
- [ ] **Bolsa Faraday lista:** Si no va a usar el dispositivo en absoluto, colóquelo en la bolsa Faraday antes de entrar a la zona de acción.
- [ ] **Plan fotográfico:** Si va a documentar la acción, utilice una cámara dedicada independiente (o teléfono desechable) para la fotografía. Los metadatos de las fotos (EXIF) incluyen la hora y las coordenadas GPS; borre o deshabilite el GPS antes de tomar fotos.
- [ ] **Registro con el grupo de afinidad completado:** Todos los miembros han confirmado: tienen el número de apoyo de cárcel, conocen el plan de dispersión, conocen el protocolo médico, conocen el canal de comunicaciones.

---

## Fase 3: Durante la Acción

### Mantener la OPSEC en el Campo
- [ ] **Permanezca con su grupo de afinidad** — no se fragmenten a menos que se ordene la dispersión.
- [ ] **Comuníquense solo por canales seguros** — sin redes sociales públicas sobre detalles operativos en tiempo real.
- [ ] **No fotografíe los rostros** de otros participantes sin consentimiento explícito — incluso en espacios públicos, distribuir fotos puede exponer a personas que querían anonimato.
- [ ] **No transmita en vivo detalles operativos** — las transmisiones en vivo (livestreams) son monitoreadas en tiempo real por las unidades de redes sociales de las fuerzas del orden.
- [ ] **Sea testigo y documente la conducta policial** — anote los números de placa, los números de los vehículos y los nombres de cualquier oficial que dé órdenes o use la fuerza.

### Protocolo Médico
- [ ] **Conozca los signos de exposición a irritantes químicos:**
  - Ojos: ardor intenso, cierre involuntario, pérdida temporal de la visión — no se frote; enjuague inmediatamente con agua o solución salina.
  - Respiratorio: tos, dificultad para respirar — muévase contra el viento, al aire fresco.
  - Piel: ardor, enrojecimiento — enjuague con grandes cantidades de agua; NO use leche (a pesar de la creencia popular, la leche es menos efectiva que el agua y puede introducir contaminación).
- [ ] **Conozca los signos de una conmoción cerebral/lesión en la cabeza:** Si lo golpean en la cabeza, no continúe participando. Busque atención médica.
- [ ] **Conozca la ubicación del lugar seguro predeterminado más cercano** (área de concentración o punto médico de emergencia).

### Si Es Detenido o Arrestado
- [ ] Diga claramente: *"Estoy invocando mi derecho a permanecer en silencio y mi derecho a un abogado"*.
- [ ] No diga nada más. No dé explicaciones. No negocie. No intente librarse hablando.
- [ ] Notifique a su grupo de afinidad que está siendo detenido (si es seguro hacerlo — un puño en alto, una palabra clave específica o un mensaje de texto antes de que le quiten su teléfono).
- [ ] La responsabilidad de su grupo de afinidad: comunicarse de inmediato con el apoyo de cárcel proporcionando su nombre y su última ubicación conocida.

---

## Fase 4: Posterior a la Acción — 0 a 48 Horas Después

### Inmediatamente Después de la Acción (dentro de 1 hora)
- [ ] **Protocolo de verificación:** Todos los miembros del grupo de afinidad se reportan con el coordinador de comunicaciones. Cualquier miembro ausente desencadena el protocolo de apoyo de cárcel de inmediato.
- [ ] **Reunión informativa con su grupo de afinidad** en un lugar seguro lejos de la zona de acción. ¿Qué pasó? ¿Quién fue detenido? ¿Qué observaron sobre las tácticas policiales?
- [ ] **Reporte al apoyo de cárcel:** Confirme todas las verificaciones o reporte a los miembros no contabilizados con toda su información de identificación.
- [ ] **Documente la conducta policial:** Mientras la memoria está fresca, anote los nombres de los oficiales, números de placa, números de vehículos, cualquier uso de la fuerza presenciado y cualquier orden escuchada.

### Digital - Posterior a la Acción
- [ ] **Limpie el teléfono desechable** si lo usó: restablecimiento de fábrica, retire la tarjeta SIM, deseche el dispositivo y la SIM por separado si no volverá a usarlo.
- [ ] **Elimine las comunicaciones operativas** que hayan cumplido su propósito. Los mensajes temporales de Signal deberían haberse encargado de esto; verifíquelo manualmente.
- [ ] **Cambie las credenciales** de cualquier cuenta a la que se haya accedido en el dispositivo operativo, especialmente si el estado del dispositivo es incierto.
- [ ] **Limpie todos los metadatos EXIF de las fotos** antes de compartirlas. Use ExifTool, Scrambled EXIF (Android) o Photo Investigator (iOS) para verificar que las fotos no contengan metadatos antes de su distribución.
- [ ] **No publique fotos de otros participantes sin su consentimiento** — incluso las imágenes difuminadas pueden ser desanonimizadas.
- [ ] **Desactive la sincronización en la nube innecesaria** — vuelva a activarla con precaución.

### Físico - Posterior a la Acción
- [ ] **Preserve pruebas de mala conducta policial:** Ropa con residuos de gas lacrimógeno, fotografíe las lesiones, documente relatos de los testigos.
- [ ] **Seguimiento médico:** Toda persona expuesta a agentes químicos, golpeada por proyectiles o que experimente síntomas debe buscar una evaluación médica.
- [ ] **Sesión informativa psicológica:** Presenciar o experimentar la violencia policial es traumático. Normalice las consultas sobre el bienestar emocional. Consulte la sección sobre [Salud Mental y Seguridad Psicológica](./mental_security.md).

### Seguimiento Organizacional
- [ ] **Reunión informativa completa** (dentro de las 48 horas): ¿Qué funcionó? ¿Qué falló? ¿Qué cambió en el entorno de amenazas?
- [ ] **Actualice el modelo de amenazas** si se observaron nuevas tácticas, tecnologías de vigilancia o desarrollos legales.
- [ ] **Apoyo a los participantes arrestados:** Defensa legal, apoyo emocional, cobertura de turnos de trabajo perdidos.
- [ ] **Revise los contactos del apoyo de cárcel y el fondo de fianza** — repóngalos si se usaron.

---

*Esta guía no constituye asesoramiento legal. Las leyes varían según la jurisdicción.*

[← Volver al Índice](../index.md)

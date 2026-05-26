# Defensa OSINT: Protegiendo su Huella Digital

*Estado: Nivel 2 | Audiencia: Organizadores, Portavoces Públicos y Cualquier Persona en Riesgo de Doxxing*

La Inteligencia de Fuentes Abiertas (OSINT) es la recopilación de información a partir de fuentes disponibles públicamente: Google, redes sociales, corredores de datos (data brokers), registros públicos, LinkedIn, expedientes judiciales, registros de propiedad y más. No requiere hackeo, ni autoridad legal, ni tecnología especial: solo persistencia, tiempo y herramientas disponibles de forma gratuita. Los adversarios de todos los niveles utilizan OSINT. Esta guía le enseña a reducir sistemáticamente su huella OSINT.

> **Punto clave:** Usted no puede volverse invisible en línea, pero puede volverse costoso como objetivo. Si un adversario debe gastar 10 horas para encontrar su dirección en lugar de 10 minutos, la mayoría de los adversarios de Nivel 1 se darán por vencidos y seguirán adelante. Es posible lograr una fricción significativa.

---

## 1. Entendiendo su Exposición Actual

Antes de poder reducir su huella, debe entenderla.

### 1.1 Búsquese en Google

Comience con una autoauditoría integral:

1. **Busque su nombre completo en Google** entre comillas (`"Nombre Apellido"`), luego agregue combinaciones: `"Nombre Apellido" Chicago`, `"Nombre Apellido" activista`, su nombre de usuario, el nombre de su empleador.
2. **Busque su número de teléfono:** Solo su número, sin formato, entre comillas.
3. **Busque la dirección de su casa:** `"123 Main St Chicago"` — esto a menudo revela registros de propiedad, registros comerciales, expedientes judiciales.
4. **Busque su dirección de correo electrónico:** Esto vincula su correo electrónico con cualquier perfil visible públicamente, publicaciones en foros o bases de datos que lo publiquen.
5. **Busque sus nombres de usuario:** Cualquier nombre de usuario que haya usado públicamente: foros, Reddit, juegos, blogs antiguos.

**Documente todo lo que encuentre.** Cree una hoja de cálculo: qué se encontró, dónde y qué prioridad darle para abordarlo primero.

### 1.2 Búsqueda Inversa de Imágenes

Si tiene fotos suyas asociadas públicamente con su activismo:
- Súbalas a Google Images, TinEye y PimEyes (una búsqueda inversa de imágenes con reconocimiento facial).
- PimEyes es particularmente poderoso: encuentra rostros en toda la web, incluyendo imágenes de vigilancia en algunos casos.
- Use PimEyes para comprender su exposición antes de que lo hagan sus adversarios.

### 1.3 Auditoría de Corredores de Datos

Los corredores de datos (data brokers) son empresas que agregan información personal de registros públicos, encuestas y datos comerciales y la venden. Los principales corredores incluyen:
- Spokeo, WhitePages, Intelius, BeenVerified, Radaris, TruthFinder, Pipl
- FamilyTreeNow (particularmente detallado para conexiones familiares)
- MyLife, PeopleFinder, Instantcheckmate

Búsquese en cada uno de estos. Lo que ellos tienen es lo que tienen sus adversarios.

---

## 2. Exclusión de Corredores de Datos (Opt-Outs)

Excluirse de los corredores de datos es la acción de defensa OSINT de mayor impacto disponible para la mayoría de las personas. Es tedioso pero efectivo.

### 2.1 Exclusiones Manuales

Cada corredor de datos tiene un proceso de exclusión (opt-out). La mayoría requiere:
- Enviar su nombre e información de identificación para ser eliminados (irónico pero necesario).
- Esperar de 30 a 60 días para la eliminación.
- Repetir el proceso: los corredores vuelven a agregar datos de sus fuentes, y es probable que su información reaparezca dentro de 6 a 12 meses.

**Lista de exclusión prioritaria:**
1. Spokeo: spokeo.com/optout
2. WhitePages: whitepages.com/suppression_requests
3. BeenVerified: beenverified.com/opt-out
4. Intelius: intelius.com/opt-out
5. Radaris: radaris.com/ng/public/profile/remove
6. TruthFinder: truthfinder.com/opt-out
7. Instantcheckmate: instantcheckmate.com/opt-out
8. MyLife: mylife.com/optout
9. FamilyTreeNow: familytreenow.com/optout

**Recurso a nivel nacional (EE. UU.):** Privacy Rights Clearinghouse mantiene una guía completa de exclusión en privacyrights.org/data-broker-opt-out.

### 2.2 Servicios de Exclusión Automatizados

Si no puede completar las exclusiones manuales, los servicios automatizados lo hacen por usted (con eliminación recurrente a medida que los datos reaparecen):

- **DeleteMe:** ~$129/año por persona; eliminación integral de corredores, publica informes de verificación.
- **Kanary:** Alternativa con buena cobertura.
- **Mozilla Monitor Plus:** Nueva opción de la Fundación Mozilla, integrada con Firefox.

**Limitación:** Ningún servicio automatizado cubre a todos los corredores, y los corredores agregan constantemente nuevas fuentes de agregación. La eliminación automatizada es un complemento, no un reemplazo, de las exclusiones manuales prioritarias.

### 2.3 Eliminación de Resultados de Búsqueda de Google

Google le permite solicitar la eliminación de cierta información personal de los resultados de búsqueda:
- Dirección de casa, número de teléfono, dirección de correo electrónico
- Credenciales de inicio de sesión
- Imágenes de menores
- Imágenes íntimas no consensuadas

Envíe solicitudes de eliminación en myaccount.google.com/data-and-privacy o a través de la herramienta de eliminación directa en support.google.com/websearch/troubleshooter/9685456.

**Nota:** Esto elimina el resultado de búsqueda, no la página subyacente. Póngase en contacto con el sitio de alojamiento directamente para eliminar la fuente.

---

## 3. Endurecimiento de Redes Sociales

### 3.1 Audite sus Perfiles Públicos

Para cada cuenta de red social:
- Revise lo que es visible públicamente (foto de perfil, nombre, biografía, publicaciones).
- Revise a quién sigue y quién lo sigue: estos gráficos sociales son públicos de forma predeterminada en la mayoría de las plataformas.
- Revise las fotos etiquetadas: fotos en las que otros lo han etiquetado y que usted no publicó.

### 3.2 Acciones Específicas de la Plataforma

**Facebook:**
- *Configuración de privacidad → Tu actividad → ¿Quién puede ver tus futuras publicaciones? → Amigos* (o *Solo yo* para máxima privacidad).
- *Configuración de privacidad → Cómo pueden encontrarte y contactarte los demás → ¿Quién puede buscarte usando tu número de teléfono? → Solo yo*.
- *Configuración → Privacidad → Tu información de Facebook → Actividad fuera de Facebook → Borrar historial* — y deshabilite el seguimiento de actividad futura fuera de Facebook.
- Elimine su número de teléfono y correo electrónico de su perfil público.
- Revise y elimine publicaciones antiguas que revelen ubicación, asociaciones o información que no le gustaría que saliera a la luz ahora.

**Instagram:**
- Cambie a cuenta privada: *Configuración → Privacidad de la cuenta → Cuenta privada*.
- Elimine u oculte fotos etiquetadas: *Tu perfil → Fotos → [foto] → ⋯ → Ocultar foto*.
- Deshabilite: *Configuración → Anuncios → Preferencias de anuncios → Anuncios de Instagram → Datos sobre tu actividad de socios*.

**Twitter/X:**
- Haga la cuenta protegida/privada si es posible para usuarios sensibles.
- Elimine el número de teléfono: *Configuración → Información de la cuenta → Teléfono*.
- Deshabilite los datos de ubicación: *Configuración → Privacidad y seguridad → Información de ubicación*.

**LinkedIn:**
- *Configuración → Visibilidad → Editar tu perfil público* — reduzca lo que es visible para los que no son conexiones.
- Elimine su número de teléfono y dirección exacta.
- Deshabilite: *Configuración → Privacidad de datos → Preferencias de búsqueda de empleo → Señala tu interés a los reclutadores* (esto transmite su información a terceros).
- Considere si LinkedIn es necesario para su situación: es uno de los perfiles públicos más detallados disponibles sobre la mayoría de los profesionales.

### 3.3 Consistencia de Nombre de Usuario en Plataformas

- No reutilice nombres de usuario en plataformas que desea mantener separadas.
- Los diferentes nombres de usuario evitan la correlación trivial entre sus cuentas activistas y cuentas personales.
- Use Namechk.com o KnowEm.com para identificar dónde aparece un nombre de usuario en todas las plataformas; luego decida si desea reclamar y vaciar esas cuentas o dejarlas.

---

## 4. Eliminación de Cuentas y Minimización de Datos

### 4.1 Eliminar Cuentas Antiguas

Las cuentas antiguas de años pasados acumulan brechas de datos, publicaciones olvidadas y correlaciones de identidad de las que se ha olvidado.

- **JustDeleteMe.com:** Un directorio de enlaces directos a páginas de eliminación de cientos de servicios, con una calificación de dificultad.
- Elimine las cuentas que ya no use activamente.
- Donde la eliminación no sea posible, archive y bloquee la cuenta (hágala privada, elimine la información personal, cambie el nombre de usuario a algo genérico).

### 4.2 Higiene de Direcciones de Correo Electrónico

- Use una **dirección de correo electrónico diferente para el activismo que para la vida personal**.
- Cree una dirección de correo electrónico dedicada en un proveedor que respete la privacidad (Proton Mail, Tutanota) para registros de organizaciones y comunicaciones.
- Use **alias de correo electrónico** (SimpleLogin, AnonAddy) para registrarse en servicios: cada servicio obtiene una dirección de alias única. Si ese alias comienza a recibir spam, usted sabe qué servicio vendió sus datos. Desactive el alias para detenerlo.

### 4.3 Higiene de Números de Teléfono

- **No dé su número de teléfono real a aplicaciones o servicios a menos que sea legalmente requerido u operativamente necesario.**
- Use un número VOIP (Google Voice, MySudo, JMP.chat) para los registros de servicios.
- Elimine su número de teléfono de las cuentas existentes donde sea posible.
- Algunos servicios usan números de teléfono como recuperación de cuenta: reemplácelos con autenticación TOTP y elimine el número de teléfono después (verifique que la cuenta permanezca accesible).

---

## 5. Reducción OSINT en el Mundo Físico

La huella digital es solo la mitad del panorama. Los registros físicos también alimentan las bases de datos OSINT.

### 5.1 Registro de Votantes

En la mayoría de los estados de EE. UU., los registros de inscripción de votantes son públicos e incluyen su nombre, domicilio y afiliación partidaria. Algunos estados venden estos datos a corredores comerciales.

- Verifique las reglas de su estado sobre la privacidad del registro de votantes en ncsl.org.
- Muchos estados permiten el registro confidencial para sobrevivientes de violencia doméstica, víctimas de delitos o, en algunos estados, activistas: verifique si su estado tiene un "Programa de Confidencialidad de Direcciones".
- En los estados que lo permiten, use un apartado de correos o la dirección de un servicio de correo para el registro de votantes (verifique la legalidad en su estado).

### 5.2 Registros de Propiedad

Si es propietario, su nombre y la dirección de la propiedad son registros públicos en todos los estados de EE. UU.

- Si es posible, considere mantener la propiedad a través de una LLC o fideicomiso por privacidad (tiene implicaciones legales y fiscales: consulte a un abogado).
- Si alquila, el nombre de su arrendador y su dirección aproximada aún pueden aparecer en las agregaciones de corredores de datos.

### 5.3 Registros Comerciales y Profesionales

- Los registros comerciales (presentaciones de la Secretaría de Estado) son registros públicos que incluyen la dirección del agente registrado.
- Use un servicio de agente registrado en lugar de su domicilio para cualquier presentación comercial.
- Las declaraciones de impuestos de organizaciones sin fines de lucro (990) son públicas e incluyen nombres de funcionarios y, a veces, direcciones: use la dirección de su organización, no la de su casa, para cualquier presentación oficial.

### 5.4 Expedientes Judiciales

Las presentaciones judiciales (demandas civiles, reclamos menores, infracciones de tránsito, asuntos penales) son generalmente registros públicos y aparecen con frecuencia en agregaciones de corredores de datos. Opciones limitadas:
- Muchos tribunales permiten sellar registros para asuntos delicados: consulte a un abogado.
- Las infracciones de tránsito a menudo aparecen y no pueden sellarse.
- Minimice los litigios frívolos que generan registros adicionales.

---

## 6. OSINT Defensiva: Monitoreando su Propia Exposición

Una vez que haya reducido su huella, configure el monitoreo para detectar cuándo aparece nueva información.

### 6.1 Alertas de Google

Configure Alertas de Google (google.com/alerts) para:
- Su nombre completo entre comillas
- Sus nombres de usuario conocidos
- El nombre de su organización
- La dirección de su casa

Las alertas le enviarán un correo electrónico cuando aparezca contenido nuevo que coincida con estos términos en el índice de Google.

### 6.2 Have I Been Pwned

Regístrese para recibir notificaciones de violaciones de datos en haveibeenpwned.com: se le notificará si su correo electrónico aparece en una violación de datos recientemente descubierta.

### 6.3 Re-Auditorías Regulares

Repita la auditoría inicial de OSINT (Sección 1) cada 6 meses. Aparecen constantemente nuevas fuentes de datos y los corredores existentes vuelven a agregar datos después de que usted se excluye. El tratamiento es continuo, no de una sola vez.

---

## 7. Protegiendo a la Familia y Asociados

Los adversarios de OSINT se dirigirán a personas conectadas a usted para encontrar información que no pueden encontrar sobre usted directamente: miembros de la familia (especialmente padres, hermanos, parejas), empleadores y amigos cercanos.

- **Advierta a los miembros clave de la familia:** Dígale a su familia más cercana que usted puede ser blanco de investigaciones en línea y que pueden ser contactados. Lo que deben decir: nada más allá de confirmar que no son usted. Proporcione la información de contacto de NLG si son acosados.
- **No etiquete a miembros de la familia** en fotos conectadas a sus cuentas activistas.
- **No mencione los lugares de trabajo, las rutinas o la información de identificación de los miembros de la familia** en ningún contexto público relacionado con su identidad activista.
- **Reduzca su asociación en los datos del gráfico social:** Revise las listas de amigos de Facebook, seguidores de Instagram y conexiones de LinkedIn. ¿Hay conexiones que vinculen sus identidades activistas y personales?

---

*Esta guía no constituye asesoramiento legal. Las leyes varían según la jurisdicción.*

[← Back to Index](../index.md)
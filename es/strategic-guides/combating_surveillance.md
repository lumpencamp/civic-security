# Una guía práctica para combatir la vigilancia gubernamental

**Para el activista no técnico**

---

## Introducción: Por qué es importante esta guía

En la era digital, el activismo depende en gran medida de la tecnología para la organización, la comunicación y la divulgación.Sin embargo, las agencias gubernamentales pueden utilizar estas mismas herramientas para la vigilancia.Comprender el panorama de la vigilancia moderna no se trata de paranoia;se trata de seguridad estratégica.Esta guía está diseñada para desmitificar las técnicas principales utilizadas por los actores a nivel estatal y brindarle una comprensión fundamental sobre cómo protegerse a sí mismo, a su comunidad y a su trabajo.El principio básico es simple: el conocimiento le permite tomar decisiones informadas sobre su seguridad.

---

## Parte 1: Recopilación masiva de datos: The Dragnet

El concepto fundamental de la vigilancia moderna es "recolectarlo todo".Las agencias gubernamentales operan bajo el supuesto de que la mayoría de las comunicaciones digitales no cifradas se recopilan y almacenan de forma predeterminada.Esto se logra mediante programas masivos y automatizados que forman una amplia red.

### Programa PRISMA

* **Qué es:** Un programa de vigilancia clandestino en el que la NSA obliga a las principales empresas de tecnología estadounidenses (como Google, Facebook, Apple, Microsoft) a proporcionarles datos de los usuarios.
* **Cómo funciona:** El gobierno utiliza una orden legal secreta para obligar a una empresa a entregar todos los datos que tiene sobre una persona.La empresa tiene prohibido legalmente comunicar al usuario su solicitud.
* **Datos recopilados:** Correos electrónicos, chats, fotos, videos, documentos almacenados, información de inicio de sesión y actividad en las redes sociales.
* **Defensa estratégica:** Utilice servicios de **cifrado de extremo a extremo (E2EE)** como Signal.Con E2EE, sus datos están codificados en su dispositivo y solo el destinatario puede descifrarlos.Incluso si la empresa entrega los datos, están en un formato ilegible.

### Colección ascendente

* **Qué es:** Un programa de la NSA que intercepta datos directamente de la infraestructura física de Internet: los enormes cables de fibra óptica que forman la "columna vertebral" de Internet.
* **Cómo funciona:** La NSA coloca "intervenciones" en estos cables, a menudo con la cooperación de compañías de telecomunicaciones (como AT&T y Verizon), lo que les permite copiar y filtrar enormes volúmenes de tráfico de Internet a su paso.
* **Datos recopilados:** El contenido de correos electrónicos no cifrados, actividad de navegación web, chats y más de millones de personas.
* **Defensa estratégica:**
* **Usa HTTPS:** Busca siempre el icono del candado en tu navegador.Esto cifra su conexión a un sitio web.
* **Utilice E2EE:** Al igual que con PRISM, E2EE protege el contenido de sus comunicaciones mientras viaja por Internet.
* **Utilice una VPN o Tor confiable:** Estas herramientas dirigen su tráfico a través de túneles cifrados, lo que hace que sea mucho más difícil interceptar y analizar sus datos.

---

## Parte 2: Vigilancia dirigida: el microscopio

Si bien la recopilación masiva es una red de control, las agencias también utilizan herramientas específicas para acercarse a individuos y grupos.

### Simuladores de sitios celulares (rayas/atrapa IMSI)

* **Qué son:** Una torre de telefonía celular falsa, llevada físicamente a un área objetivo (como una protesta), que engaña a todos los teléfonos cercanos para que se conecten a ella.
* **Cómo funcionan:** Stingray transmite una señal más fuerte que las torres de telefonía móvil legítimas, lo que obliga a los teléfonos a conectarse.Esta posición de "hombre en el medio" le permite interceptar las señales de su teléfono.
* **Datos interceptados:** la identificación única de su teléfono (IMSI), su ubicación precisa, metadatos de llamadas/mensajes de texto y, a veces, el contenido de llamadas y mensajes de texto no cifrados.
* **Defensa estratégica:** **Limite la conexión celular de su teléfono.** Apague su teléfono o póngalo en modo avión en lugares sensibles.Para comunicarse, utilice aplicaciones E2EE a través de una red Wi-Fi confiable en lugar de llamadas y SMS tradicionales.

### Monitoreo de redes sociales

* **Cómo funciona:** Las autoridades policiales utilizan software automatizado para escanear constantemente las plataformas de redes sociales públicas (Facebook, Twitter, etc.).Analizan millones de publicaciones en tiempo real y pueden utilizar cuentas encubiertas para acceder a grupos privados.
* **Lo que buscan:** Mapear redes de activistas, identificar organizadores clave, monitorear el sentimiento público y rastrear planes de protesta.
* **Defensa estratégica:** Practique una **cuidadosa higiene y compartimentación digital.** Suponga que todo lo público está monitoreado.Mueva la planificación confidencial a canales privados E2EE (como los chats grupales de Signal).Considere la posibilidad de utilizar seudónimos para las cuentas públicas de activistas.

### El papel de los intermediarios de datos

* **Qué son:** Empresas cuyo negocio es recopilar su información personal de miles de fuentes (aplicaciones, rastreadores en línea, historial de tarjetas de crédito) y venderla.
* **Cómo los usan las agencias:** Las agencias gubernamentales pueden simplemente comprar vastos conjuntos de datos sobre personas de estos corredores, incluido el historial de ubicación preciso, los hábitos de navegación y las afiliaciones políticas.Esto a menudo se ve como una "laguna jurídica" para eludir la necesidad de una orden judicial.
* **Defensa estratégica:** **Minimiza tu huella digital.** Desactiva el seguimiento de ubicación y otros permisos para aplicaciones que no los necesitan.Utilice navegadores centrados en la privacidad (como Firefox con uBlock Origin) y motores de búsqueda (como DuckDuckGo) para bloquear rastreadores.

---

## Parte 3: Técnicas de investigación: ocultar el rastro

Más allá de la tecnología, es crucial comprender las tácticas legales utilizadas para ocultar cómo se lleva a cabo la vigilancia.

### Construcción paralela

* **Qué es:** Una práctica en la que las autoridades utilizan una fuente secreta de información (como una intervención telefónica sin orden judicial) para iniciar una investigación y luego construyen un segundo caso "paralelo" utilizando métodos convencionales para ocultar la fuente original.
* **Cómo funciona (una analogía):** La policía recibe un aviso secreto de que un automóvil contiene pruebas.No pueden usar ese consejo en la corte.Entonces, siguen el auto, esperan a que se pase un semáforo en rojo y usan esa infracción de tránsito como razón oficial para detenerse y registrar el auto, "encontrando" la evidencia que ya sabían que estaba allí.El consejo secreto nunca se menciona.
* **Por qué es un problema:** Oculta la verdad al sistema legal.Impide que un acusado cuestione la legalidad de la vigilancia original, blanqueando efectivamente pruebas potencialmente ilegales.
* **Defensa estratégica:** Esto es difícil de contrarrestar directamente.Las estrategias son:
* **Descubrimiento legal agresivo:** Los abogados defensores deben ser implacables para obligar a la fiscalía a revelar cada detalle sobre cómo comenzó una investigación, buscando inconsistencias.
* **Conciencia pública y promoción:** Los activistas deben crear conciencia pública sobre esta práctica para crear presión política para la reforma y una mayor transparencia en la vigilancia.

---

## Conclusión: un enfoque estratégico para la seguridad

El objetivo de esta guía no es inducir miedo, sino fomentar una mentalidad estratégica.No puede detener la recopilación masiva, pero puede cifrar sus comunicaciones para que los datos recopilados sean inútiles.Es posible que no sepas si un Stingray está activo, pero puedes optar por dejar tu teléfono en casa.Al comprender estas técnicas de vigilancia, podrá pasar de una postura de seguridad reactiva a una proactiva.Adoptar herramientas y prácticas que preserven la privacidad es un acto fundamental y necesario de autodefensa digital para el activismo moderno.

_Última actualización: 2026_
# Una guía de alternativas de señales: Session, Briar, Matrix y SimpleX

La señal es excelente, pero situaciones especializadas exigen herramientas especializadas.Esta guía cubre alternativas para escenarios de alto riesgo en los que Signal podría no ser la opción perfecta.

* **Session y SimpleX**: utilícelo cuando su principal amenaza sea el **anonimato** (ocultar su identidad por completo de la red).
* **Briar**: utilícelo cuando su principal amenaza sea **fallo de red** (apagado de Internet/celular).
* **Matriz (Elemento)**: utilícela cuando necesite una **coordinación de grupo** sólida y descentralizada sin un servidor central que controle la plataforma.

---

## 1. Session: The Anonymous Onion Messenger

* **Tecnología principal:** Utiliza una red de enrutamiento de cebolla descentralizada (originalmente basada en Loki/Oxen, ahora pasando a su propia arquitectura) para ocultar su dirección IP.**No** requiere un número de teléfono, sino que utiliza un ID de sesión generado aleatoriamente.
* **Configuración y OPSEC:**
1. Crea tu identificación.**Haga una copia de seguridad segura de su frase de recuperación sin conexión.** Perder esta frase significa perder su cuenta para siempre.
2. Tenga en cuenta las desventajas: los mensajes son más lentos que Signal, pero proporcionan un grado mucho mayor de anonimato.*Nota: Si bien Session oculta las direcciones IP, el análisis de metadatos en la red sigue siendo un riesgo teórico.*

---

## 2. SimpleX Chat: el mensajero sin identificadores

* **Tecnología principal:** SimpleX lleva el anonimato un paso más allá que Session.Tiene **cero identificadores de usuario**.No hay números de teléfono, ni nombres de usuario, ni siquiera ID de sesión aleatorios.En cambio, las conexiones se establecen mediante códigos QR temporales de un solo uso o enlaces de invitación.
* **Configuración y OPSEC:**
1. Para hablar con alguien, genera un enlace de invitación/código QR y se lo envía a través de un canal seguro fuera de banda.
2. Una vez que se conectan, el enlace está inactivo.El tráfico se enruta a través de servidores descentralizados.
3. Como no hay identificaciones, no existe un directorio global para buscarte, lo que te hace prácticamente invisible en la red.

---

## 3. Briar: el mensajero resistente y fuera de la red

* **Tecnología principal:** Un mensajero de igual a igual sin servidor central.Puede sincronizar mensajes directamente entre teléfonos mediante **Bluetooth o Wi-Fi local**, evitando Internet por completo.Cuando se conecta a Internet, utiliza la red Tor para sincronizarse.
* **Configuración y OPSEC:**
1. Cree su cuenta y establezca una contraseña segura.**No hay recuperación de contraseña.**
2. **Agregue contactos en persona escaneando códigos QR.** Este es el método más seguro y es fundamental para el modelo de seguridad de Briar.
3. **Advertencia:** Debido a que Briar es peer-to-peer y debe ejecutarse constantemente en segundo plano para mantener las conexiones de red, **agota la batería muy rápidamente.** Tenga esto en cuenta durante implementaciones de protesta prolongadas.

---

## 4. Matrix (aplicación Element): El organizador federado

* **Tecnología principal:** Matrix es un protocolo de red federado y descentralizado.Es como el correo electrónico, pero para mensajería instantánea.Cualquiera puede crear su propio servidor Matrix.La aplicación más popular para acceder a Matrix se llama **Element**.
* **Configuración y OPSEC:**
1. Puede registrarse en el servidor predeterminado `matrix.org` o, mejor aún, su organización puede alojar su propio servidor Matrix privado.
2. Matrix admite un cifrado sólido de extremo a extremo (E2EE), pero debe verificar manualmente los dispositivos para garantizar que los chats permanezcan seguros.
3. Es muy preferido por los grupos activistas para chats grupales organizados y masivos (similares a Slack o Discord), pero con cifrado y descentralización.

_Última actualización: 2026_
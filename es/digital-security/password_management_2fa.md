# Gestión de Contraseñas y Autenticación de Dos Factores

*Estado: Nivel 1 | Audiencia: Todos los miembros — higiene de seguridad fundamental*

La higiene de contraseñas es la inversión de seguridad con mayor retorno que puede hacer. El compromiso de credenciales (contraseñas débiles, contraseñas reutilizadas, phishing, violaciones de datos) es la forma más común en que los activistas, periodistas y personas comunes sufren el robo de sus cuentas. Esta guía cubre los gestores de contraseñas, la generación de contraseñas seguras y todas las formas de autenticación de dos factores, desde la más débil hasta la más fuerte.

---

## 1. El Problema de las Contraseñas

### Por qué no puede gestionar las contraseñas usted mismo

La persona promedio tiene más de 100 cuentas en línea. El cerebro humano no puede:
- Generar contraseñas verdaderamente aleatorias y únicas
- Recordar más de 100 contraseñas complejas diferentes
- Saber cuáles de esas contraseñas han sido expuestas en violaciones de datos

**Modos de falla comunes:**
- **Reutilización de contraseñas:** Usar la misma contraseña en varios sitios significa que cuando un sitio es vulnerado (como eventualmente lo son todos los sitios importantes), cada cuenta con esa contraseña se ve comprometida.
- **Contraseñas débiles:** "Verano2024!" pasa la mayoría de los requisitos de los sitios, pero puede descifrarse en segundos con herramientas modernas.
- **Patrones predecibles:** "Password1!", "P@ssw0rd", nombre+cumpleaños — todos están en las listas de palabras de los atacantes.

### La Solución: Un Gestor de Contraseñas

Un gestor de contraseñas genera, almacena y autocompleta contraseñas largas, aleatorias y únicas para cada sitio. Usted recuerda una contraseña maestra; el gestor se encarga del resto.

---

## 2. Opciones de Gestores de Contraseñas

### 2.1 Bitwarden (Recomendado para la mayoría de los usuarios)

**Qué es:** Gestor de contraseñas multiplataforma, de código abierto, auditado, con niveles gratuitos y de pago.

**Por qué se recomienda:**
- Código abierto — el código es auditable públicamente
- Arquitectura de conocimiento cero — Bitwarden nunca ve sus contraseñas; se cifran en su dispositivo antes de sincronizarse
- Auditorías de seguridad independientes publicadas públicamente
- El nivel gratuito incluye todo lo que la mayoría de los usuarios necesitan
- Funciona en iOS, Android, Windows, Mac, Linux y como extensiones de navegador

**Configuración:**
1. Cree una cuenta en bitwarden.com utilizando una dirección de correo electrónico segura
2. Instálelo en todos sus dispositivos y navegadores
3. Genere una contraseña maestra: larga (16+ caracteres), fácil de recordar, única — una frase de contraseña (*passphrase*) funciona bien: al estilo "correct-horse-battery-staple"
4. Habilite la autenticación de dos factores en su cuenta de Bitwarden de inmediato (consulte la Sección 3)
5. Importe las contraseñas existentes si ha utilizado otro gestor, o agregue cuentas a medida que inicie sesión

**Opción de autoalojamiento:** Bitwarden puede ser autoalojado usando Vaultwarden — control máximo, sin servidores de terceros. Requiere cierta configuración técnica.

### 2.2 KeePassXC (Recomendado para usuarios de alto riesgo)

**Qué es:** Gestor de contraseñas de código abierto y solo sin conexión. Almacena su bóveda como un archivo local cifrado.

**Por qué elegirlo:**
- Sin sincronización en la nube — su bóveda nunca sale de su dispositivo a menos que la copie explícitamente
- De código abierto y ampliamente auditado
- Ideal para configuraciones aisladas (*air-gapped*) o aquellos que no confían en ningún proveedor de la nube

**Compensación:** Debe administrar manualmente la sincronización entre dispositivos (por ejemplo, a través de una unidad USB cifrada o Syncthing). Más esfuerzo, más control.

### 2.3 1Password

Opción comercial ampliamente utilizada con un sólido historial de seguridad. No es de código abierto. Bueno si necesita funciones sólidas para compartir contraseñas en equipos u organizaciones.

### 2.4 Lo que NO debe usar

- **Gestores de contraseñas integrados en el navegador** (Chrome, Firefox, Safari): Aceptables para cuentas de bajo riesgo, pero están vinculados a su cuenta de Google/Apple/Mozilla y no proporcionan el registro de auditoría, la organización ni las funciones multiplataforma de un gestor dedicado.
- **Hojas de cálculo o archivos de texto:** Nunca. Incluso los cifrados son frágiles.
- **Solo su memoria:** No es escalable y no puede generar contraseñas verdaderamente aleatorias.

---

## 3. Mejores Prácticas para Contraseñas

### Generación de contraseñas seguras

**Para contraseñas aleatorias (la mayoría de las cuentas):** Use el generador de su gestor de contraseñas. Configúrelo para:
- Longitud: 20+ caracteres
- Incluir: mayúsculas, minúsculas, números, símbolos
- Excluir caracteres ambiguos solo si el sitio lo requiere

**Para frases de contraseña (contraseña maestra, desbloqueo de dispositivo):** Una frase de contraseña (*passphrase*) es una secuencia de palabras aleatorias:
- Ejemplo: `turbina-oraculo-glaciar-8-lampara`
- Longitud en palabras: 5 como mínimo, 6–7 para usos críticos
- Use un aleatorizador de palabras (metodología Diceware) — verdaderamente aleatorio, no palabras que usted eligió
- Más fácil de escribir en un teclado sin un gestor de contraseñas
- Fuerte debido a la longitud, incluso si las palabras individuales parecen simples

### Prioridad de cuentas para higiene de contraseñas

Aborde estas en orden:

1. **Cuentas de correo electrónico** (las más críticas: el correo electrónico es el vector de recuperación para todas las demás cuentas)
2. **Contraseña maestra del gestor de contraseñas**
3. **Cuentas bancarias y financieras**
4. **Cuentas legales y médicas**
5. **Cuentas organizacionales** (correo electrónico de la organización, plataformas compartidas)
6. **Redes sociales** (de cara al público; su compromiso causa daño a la reputación)
7. **Todo lo demás**

### Monitoreo de violaciones de datos

- **haveibeenpwned.com:** Compruebe si su correo electrónico ha aparecido en violaciones de datos conocidas. Ingrese todas sus direcciones de correo electrónico allí.
- **Bitwarden premium** incluye monitoreo automático de violaciones para contraseñas almacenadas
- Si una contraseña ha sido vulnerada, cámbiela inmediatamente en todos los lugares donde se utilizó

---

## 4. Autenticación de Dos Factores (2FA)

La autenticación de dos factores agrega un segundo paso de verificación más allá de su contraseña. Incluso si su contraseña se ve comprometida, un atacante no puede acceder a su cuenta sin el segundo factor.

### 4.1 Métodos 2FA: Del más débil al más fuerte

**⚠️ SMS / Mensaje de Texto (Evitar para cuentas sensibles)**
- Se envía un código de texto a su número de teléfono
- Vulnerable a ataques de intercambio de SIM (*SIM swap*): el atacante engaña a su operador para que transfiera su número a su SIM, recibiendo todos sus SMS
- Vulnerable a ataques SS7: los atacantes explotan la infraestructura de telecomunicaciones para interceptar SMS globalmente
- **Úselo solo si no hay una opción más fuerte disponible. Nunca para correo electrónico, gestor de contraseñas o cuentas organizacionales sensibles.**

**✓ Aplicaciones de contraseñas de un solo uso basadas en el tiempo (TOTP) (Bueno)**
- Una aplicación genera un código de 6 dígitos que cambia cada 30 segundos
- Los códigos se generan localmente: sin SMS, sin dependencia del operador
- Los ataques de intercambio de SIM no funcionan contra TOTP
- Siguen siendo vulnerables al phishing (el atacante crea una página de inicio de sesión falsa que captura tanto la contraseña como el TOTP en tiempo real)

**Aplicaciones TOTP recomendadas:**
- **Aegis Authenticator (Android):** De código abierto, copia de seguridad cifrada, la mejor opción actual para Android
- **Raivo OTP (iOS):** De código abierto, copia de seguridad en iCloud (cifrada)
- **Bitwarden Authenticator:** Integrado con Bitwarden — conveniente pero significa que su 2FA y contraseñas están en la misma bóveda (ligera compensación de seguridad)
- Evite: Google Authenticator (sin exportación), Authy (propietario, algunas preocupaciones)

**Configuración:** Cuando un sitio ofrece 2FA TOTP ("Aplicación de autenticación"), muestra un código QR. Escanéelo con su aplicación TOTP. Guarde los códigos de respaldo que proporciona el sitio en su gestor de contraseñas o bóveda cifrada.

**✓✓ Llaves de seguridad de hardware (El Mejor)**
- Un dispositivo físico USB o NFC (YubiKey, Google Titan) que presiona para autenticar
- Inmune al phishing: la llave utiliza criptografía vinculada al dominio del sitio web específico; un sitio falso no puede usarla
- Inmune al intercambio de SIM — autenticación completamente fuera de línea
- Inmune a la interceptación basada en la red

**Llaves de hardware recomendadas:**
- **Serie YubiKey 5:** El estándar de la industria. Funciona a través de USB-A, USB-C o NFC. Soporta FIDO2/WebAuthn y TOTP. Compre dos: una principal, una de respaldo.
- **Google Titan Key:** Buena alternativa de Google, disponible en versiones USB-A, USB-C y Bluetooth

**Dónde usar llaves de hardware:**
1. Gestor de contraseñas (Bitwarden, 1Password)
2. Correo electrónico (Gmail, Proton Mail, Fastmail)
3. GitHub, GitLab
4. Cualquier servicio compatible con FIDO2/WebAuthn

**Limitación:** No todos los sitios son compatibles con llaves de hardware. Use TOTP donde no se admitan llaves de hardware.

---

## 5. Defensa Contra el Phishing

El 2FA reduce significativamente el riesgo de phishing, pero no lo elimina. Las llaves de hardware son la contramedida de phishing más efectiva.

**Señales de alerta de phishing:**
- Correo electrónico de una dirección que parece correcta pero no lo es (support@paypa1.com vs. support@paypal.com)
- Lenguaje urgente ("Su cuenta será suspendida en 24 horas")
- Enlaces a páginas que parecen correctas pero tienen un dominio diferente (paypal.com.security-update.net)
- Archivos adjuntos que no esperaba, especialmente .zip, .doc, .pdf, .exe

**Defensa contra el phishing:**
- **Nunca haga clic en enlaces de correos electrónicos para cuentas sensibles.** Escriba la URL directamente en su navegador o use un marcador.
- **Verifique la URL en la barra de su navegador** antes de ingresar credenciales. Busque el dominio exacto (signal.org, no signal.org.login.com)
- **Use una llave de hardware** — se negará a autenticarse en un sitio de phishing
- **Reporte el phishing** a su organización para que otros estén advertidos

---

## 6. Gestor de Contraseñas para Organizaciones

Si su organización comparte credenciales (por ejemplo, una cuenta de redes sociales compartida, servidores compartidos), necesita un gestor de contraseñas organizacional:

- **Bitwarden Organizations:** Permite compartir credenciales específicas con miembros específicos del equipo, con registros de auditoría completos. El nivel gratuito cubre a equipos pequeños.
- **1Password Teams:** Opción sólida con buenos controles administrativos
- **Vaultwarden** (Bitwarden autoalojado): Control total, sin dependencia de la nube, requiere configuración técnica

**Prácticas organizacionales clave:**
- No comparta contraseñas verbalmente ni a través de Signal: use la función de uso compartido del gestor de contraseñas
- Revoque el acceso inmediatamente cuando un miembro se va o la confianza cambia
- Utilice el registro de auditoría para supervisar patrones de acceso inusuales
- Habilite 2FA para todas las cuentas organizacionales; haga de esto una política obligatoria

---

*Esta guía no constituye asesoramiento legal. Las leyes varían según la jurisdicción.*

[← Volver al Índice](../index.md)
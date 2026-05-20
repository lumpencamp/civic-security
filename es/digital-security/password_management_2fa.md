# Una guía para la gestión de contraseñas y 2FA

Las contraseñas son las claves de tu vida digital. Si un adversario obtiene acceso a sus contraseñas, también obtiene acceso a sus comunicaciones, sus archivos y su identidad. Esta guía cubre las prácticas esenciales para proteger sus cuentas.

## El problema con las contraseñas

La mayoría de la gente comete dos errores críticos:
1. **Reutilización de contraseñas:** Si usa la misma contraseña para su correo electrónico y para un foro aleatorio, y ese foro es pirateado, los piratas informáticos ahora tendrán la contraseña de su correo electrónico.
2. **Uso de contraseñas débiles:** El software automatizado puede adivinar fácilmente "Contraseña123" o el nombre de su mascota en segundos.

## La solución: administradores de contraseñas

Un administrador de contraseñas es una bóveda segura que genera, almacena y completa automáticamente contraseñas únicas y seguras para cada cuenta que tenga. Sólo necesita recordar una "contraseña maestra" segura para desbloquear la bóveda.

### Administradores de contraseñas recomendados

* **Bitwarden (altamente recomendado):** El nivel gratuito y de código abierto es excelente y es compatible con todas las plataformas (iOS, Android, Windows, Mac, Linux).
* **KeePassXC:** De código abierto y solo sin conexión. Su base de datos de contraseñas se almacena localmente en su dispositivo, no en la nube. Excelente para modelos de amenazas de alta seguridad, pero requiere sincronización manual entre dispositivos.

### Qué NO usar

* **Administradores integrados del navegador:** No utilice Chrome, Safari (llavero de iCloud) ni los administradores de contraseñas integrados de Firefox para cuentas de activistas confidenciales. Si alguien obtiene acceso físico a su computadora desbloqueada, podrá extraer fácilmente todas sus contraseñas.

## Autenticación multifactor (MFA / 2FA)

Incluso la contraseña más segura puede ser robada mediante phishing (sitios web falsos) o registradores de pulsaciones de teclas. La autenticación multifactor (MFA), también conocida como autenticación de 2 factores (2FA), agrega una segunda capa de seguridad. Requiere no sólo *algo que sabes* (tu contraseña), sino también *algo que tienes* (un dispositivo físico).

### La jerarquía de los métodos 2FA

1. **Llaves de seguridad de hardware (óptimas):** Dispositivos USB pequeños como una **YubiKey** o una llave Google Titan. Lo conectas físicamente o lo tocas a través de NFC para iniciar sesión. Esto es completamente inmune a los ataques de phishing. **Muy recomendado para organizadores de alto riesgo.**
2. **Aplicaciones de autenticación (buenas):** Aplicaciones como **Aegis** (Android) o **Raivo OTP** (iOS) que generan códigos temporales de 6 dígitos. Mucho más seguro que los SMS. Evite Google Authenticator, ya que carece de funciones de copia de seguridad adecuadas y es de código cerrado.
3. **SMS/Mensajes de texto (PELIGROSOS):** El uso de mensajes de texto para 2FA es fundamentalmente inseguro. Los piratas informáticos o los actores estatales pueden interceptar fácilmente mensajes SMS o realizar un ataque de "intercambio de SIM" (convencer a su operador telefónico para que transfiera su número a su tarjeta SIM). **Nunca utilices SMS 2FA si hay otras opciones disponibles.**

_Última actualización: 2026_
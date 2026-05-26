# Cifrado de Dispositivos: Protección de Disco Completo y a Nivel de Archivo

*Estado: Nivel 1 | Audiencia: Todos los miembros — seguridad base no negociable*

El cifrado de dispositivos es su última línea de defensa cuando un dispositivo es incautado físicamente. Sin él, cualquiera que tome su teléfono o computadora portátil puede acceder a cada foto, mensaje, documento y credencial en él, sin necesidad de contraseña. Con el cifrado de disco completo configurado correctamente, un dispositivo incautado es un ladrillo cifrado que requiere su contraseña para acceder.

> **La Ley y el Cifrado:** La Quinta Enmienda puede protegerlo de ser obligado a revelar un código de acceso (los tribunales están divididos; consulte [Conozca Sus Derechos](../legal-rights/know_your_rights.md)). El cifrado físico es su protección técnica; los derechos legales son su protección legal. Necesita ambos.

---

## 1. Cifrado de Dispositivos Móviles

### 1.1 iPhone / iOS

**Estado por defecto:** Todos los iPhones desde el iPhone 3GS (2009) cifran los datos en el dispositivo. **Sin embargo, la fuerza de este cifrado depende por completo de su código de acceso.**

**Por qué importa el código de acceso:** iOS utiliza su código de acceso como parte de la derivación de la clave de cifrado. Un PIN numérico de 6 dígitos tiene 1,000,000 de combinaciones — descifrable en minutos mediante herramientas forenses comerciales (GrayKey, Cellebrite UFED) si el dispositivo no está en un modo de alta seguridad.

**Reforzando su iPhone:**
1. *Configuración → Face ID y código → Cambiar código → Opciones de código → Código alfanumérico personalizado*
2. Establezca una contraseña de más de 8 caracteres aleatorios (mayúsculas, minúsculas, números, símbolos)
3. Deshabilite Face ID y Touch ID para el desbloqueo del dispositivo (estos pueden ser obligados físicamente a usarse)
   - Face ID: *Configuración → Face ID y código → Usar Face ID para → Desbloqueo del iPhone → DESACTIVADO*
   - Touch ID: *Configuración → Touch ID y código → Desbloqueo del iPhone → DESACTIVADO*
4. Habilite *Borrar datos* después de 10 intentos fallidos de código (*Configuración → Face ID y código → Borrar datos*)
5. Establezca *Solicitar código* en *De inmediato*

**Bloqueo de emergencia:**
- Presione rápidamente el botón de encendido + el botón de volumen para activar el modo Emergencia SOS — esto deshabilita el desbloqueo biométrico hasta que se ingrese el código de acceso
- Alternativamente, apague el dispositivo por completo antes de un contacto policial anticipado

**Verificar que el cifrado está activo:**
- *Configuración → [Su Nombre] → iCloud → Copia de seguridad de iCloud* — si las copias de seguridad están activas, confirme que estén cifradas
- *Configuración → Privacidad y seguridad → Análisis y mejoras* — deshabilite para reducir los datos compartidos con Apple

### 1.2 Android

**Estado:** Android ha admitido el cifrado de disco completo desde Android 5.0 (2014) y el cifrado basado en archivos desde Android 7.0 (2016). La mayoría de los dispositivos Android modernos habilitan el cifrado de forma predeterminada, pero esto varía según el fabricante.

**Verificar y habilitar:**
1. *Configuración → Seguridad → Cifrado y credenciales → Cifrar teléfono*
   - En Samsung: *Configuración → Datos biométricos y seguridad → Cifrar dispositivo*
   - En Pixel: *Configuración → Seguridad → Cifrado y credenciales*
2. Si se muestra "Cifrado" o "Dispositivo cifrado", está bien
3. Si no, el proceso de cifrado se lo solicitará — toma de 30 a 60 minutos

**Reforzando su Android:**
1. Establezca un PIN alfanumérico o contraseña fuerte (*Configuración → Seguridad → Bloqueo de pantalla*)
2. Deshabilite el desbloqueo por huella dactilar y facial
3. Habilite *Bloquear de inmediato* cuando la pantalla se apague
4. Habilite *Restablecer a la configuración de fábrica automáticamente* después de 10 intentos fallidos (si su dispositivo lo admite)
5. Considere **GrapheneOS** o **CalyxOS** para una privacidad y cifrado significativamente más reforzados (consulte las guías separadas)

### 1.3 La Realidad de los Exploits

Las herramientas forenses comerciales (Cellebrite, GrayKey) a veces pueden extraer datos de dispositivos cifrados utilizando:
- Vulnerabilidades conocidas del sistema operativo (las versiones parcheadas son inmunes)
- Craqueo de códigos de acceso por fuerza bruta (las contraseñas alfanuméricas resisten esto; los PIN de 4 a 6 dígitos no)
- Extracción de datos de la memoria del dispositivo cuando el dispositivo está en un estado "Después del primer desbloqueo" (AFU - *After First Unlock*)

**Crítico:** Un dispositivo que ha sido desbloqueado desde el último arranque (estado AFU) es significativamente más vulnerable que uno que ha sido apagado por completo. **Apague su dispositivo antes de cualquier contacto policial anticipado.** Un dispositivo apagado y cifrado en estado "Antes del primer desbloqueo" (BFU - *Before First Unlock*) es drásticamente más difícil de analizar forensemente.

---

## 2. Cifrado de Computadoras Portátiles y de Escritorio

### 2.1 macOS: FileVault 2

FileVault es el cifrado de disco completo incorporado de Apple para macOS. Utiliza cifrado AES-256.

**Habilitar FileVault:**
1. *Preferencias del Sistema (o Configuración del Sistema) → Privacidad y seguridad → FileVault → Activar*
2. Elija si usar su cuenta de iCloud o una clave de recuperación local para desbloquear el disco si olvida su contraseña
   - **Para usuarios de alto riesgo:** Cree una clave de recuperación local, guárdela en su gestor de contraseñas y **no** la vincule a iCloud. Las claves de recuperación de iCloud pueden ser obtenidas potencialmente a través de Apple mediante un proceso legal.
3. Permita que FileVault cifre el disco (ocurre en segundo plano, puede tomar horas en máquinas más antiguas)
4. Reinicie para completar la configuración

**Verificar:** *Configuración del Sistema → Privacidad y seguridad → FileVault → FileVault está activado*

**Notas de seguridad:**
- FileVault protege los datos solo cuando la máquina está apagada o en hibernación
- Cuando haya iniciado sesión y esté funcionando, el disco está descifrado en la memoria
- Configure su Mac para requerir contraseña *inmediatamente* después del protector de pantalla o suspensión (*Configuración del Sistema → Pantalla de bloqueo → Requerir contraseña después de que comience el protector de pantalla o se apague la pantalla → Inmediatamente*)
- Habilite FileVault en el disco de inicio Y en cualquier unidad externa que contenga datos sensibles

### 2.2 Windows: BitLocker

BitLocker es el cifrado de disco completo incorporado en Windows, disponible en Windows 10/11 Pro, Enterprise y Education. (Windows Home no incluye el BitLocker completo, pero tiene "Cifrado de dispositivo" en hardware compatible).

**Habilitar BitLocker:**
1. Abra el *Panel de control → Sistema y seguridad → Cifrado de unidad BitLocker*
2. Seleccione su unidad y haga clic en *Activar BitLocker*
3. Elija un método de autenticación de inicio:
   - **TPM + PIN** (recomendado): Combina el Módulo de Plataforma Confiable (TPM) de hardware con un PIN para una protección fuerte
   - Solo TPM: Menos seguro — protege solo contra la extracción física del disco, no contra alguien que tenga el dispositivo encendido
4. Guarde o imprima la clave de recuperación: guárdela en su gestor de contraseñas, **no** en OneDrive ni en ninguna cuenta de Microsoft (estas pueden ser objeto de citaciones)
5. Elija cifrar solo el espacio utilizado (más rápido) o la unidad completa (más completo para unidades con datos eliminados)

**Habilitar en Windows 10/11 Home:**
- *Configuración → Actualización y seguridad → Cifrado de dispositivo* — disponible en dispositivos que cumplen con los requisitos de modo de espera moderno con una cuenta de Microsoft
- Limitación: La clave de recuperación se respalda automáticamente en su cuenta de Microsoft — considere las implicaciones legales

### 2.3 Linux: LUKS (Linux Unified Key Setup)

LUKS es el método de cifrado de disco estándar para Linux. La mayoría de las distribuciones lo ofrecen durante la instalación.

**Configurar LUKS durante la instalación:**
- Ubuntu, Fedora, Debian y la mayoría de las distribuciones principales ofrecen una casilla de verificación "Cifrar el disco" durante la instalación. Selecciónela. Establezca una contraseña segura.

**Verificar:** `lsblk -f | grep LUKS`

**LUKS de disco completo:**
- La contraseña de LUKS se ingresa en el arranque, antes de que se cargue el sistema operativo
- Todo el disco está cifrado en reposo
- Apagado = totalmente cifrado; iniciado sesión = descifrado en memoria

**VeraCrypt para cifrado portátil en Linux:**
- Use VeraCrypt para contenedores cifrados o unidades externas que comparta entre sistemas operativos (consulte la Sección 3)

### 2.4 Tails OS

Tails es un sistema operativo en vivo que se arranca desde una unidad USB. Enruta todo el tráfico a través de Tor, no deja rastro en la máquina anfitriona y usa almacenamiento persistente cifrado para cualquier dato que guarde entre sesiones.

**Para el trabajo de mayor sensibilidad** (manejo de fuentes, trabajo con documentos filtrados, planificación de operaciones sensibles), Tails proporciona cifrado + anonimato + amnesia en un solo paquete. Consulte la [Guía de Tails OS](../digital-security/tails_os_guide.md) para ver las instrucciones completas de configuración.

---

## 3. Unidades Externas y Almacenamiento Portátil

### 3.1 VeraCrypt (Todas las plataformas)

VeraCrypt es gratuito, de código abierto y crea contenedores cifrados o unidades completamente cifradas compatibles en Windows, macOS y Linux.

**Casos de uso:**
- Archivo cifrado de documentos sensibles en una unidad externa
- Contenedor cifrado en un servicio en la nube (almacenamiento de conocimiento cero — incluso si la nube es vulnerada, el contenedor está cifrado)
- Crear un "volumen oculto" para negación plausible (avanzado)

**Crear un contenedor cifrado:**
1. Descargue VeraCrypt desde veracrypt.fr — verifique la firma
2. Abra VeraCrypt → *Crear volumen*
3. Seleccione *Crear un contenedor de archivo cifrado*
4. Elija *Volumen VeraCrypt Estándar*
5. Seleccione una ubicación y un nombre de archivo (parece cualquier archivo)
6. Elija el algoritmo de cifrado (AES es estándar y rápido; cascada AES-Twofish para uso paranoico)
7. Establezca el tamaño y una contraseña segura
8. Formatee y monte — el contenedor aparece como una letra de unidad/punto de montaje
9. Desmonte al terminar — el archivo está completamente cifrado en reposo

**Unidades cifradas por hardware:**
- Serie Apricorn Aegis: Teclado numérico físico, no requiere software anfitrión, cifrado de hardware que no se puede forzar desde el software. Recomendado para uso en campo.
- iStorage datAshur: Cifrado de hardware con teclado numérico físico similar, certificado FIPS 140-2

### 3.2 Unidades USB Cifradas

**Nunca use una unidad USB no cifrada para datos sensibles.** Las unidades USB se pierden fácilmente, se roban fácilmente y se incautan fácilmente.

Opciones:
- **Unidades cifradas por hardware** (Apricorn, iStorage): El estándar de oro
- **Contenedor VeraCrypt** en una unidad USB normal: Funciona, pero requiere tener instalado VeraCrypt para acceder
- **macOS:** Use la Utilidad de Discos para crear un DMG cifrado o formatee la unidad USB como APFS (Cifrado)
- **Linux:** Use LUKS para formatear la unidad USB (`cryptsetup luksFormat /dev/sdb`)

---

## 4. Copias de Seguridad Cifradas

Una copia de seguridad no cifrada anula el propósito del cifrado de dispositivos.

### 4.1 Copias de Seguridad de iPhone (iTunes/Finder)
Al hacer copias de seguridad en una computadora (no en iCloud):
- En iTunes o Finder, seleccione *Cifrar copia de seguridad local* y establezca una contraseña segura
- Esta contraseña de la copia de seguridad es independiente del código de acceso de su dispositivo: guárdela en su gestor de contraseñas
- Una copia de seguridad local cifrada no puede ser leída por las fuerzas del orden ni siquiera con el archivo de la copia de seguridad, sin esta contraseña

**Copias de seguridad de iCloud:**
- Las copias de seguridad de iCloud se cifran en tránsito y en reposo, pero Apple tiene las claves de cifrado y puede proporcionarlas a las fuerzas del orden
- Para usuarios de alto riesgo: deshabilite la copia de seguridad de iCloud (*Configuración → [Su Nombre] → iCloud → Copia de seguridad de iCloud → Inactiva*) y use copias de seguridad locales cifradas en su lugar

### 4.2 Copias de Seguridad de Android
- Deshabilite la copia de seguridad automática de Google si usted es de alto riesgo (*Configuración → Sistema → Copia de seguridad → Inactiva*)
- Use una herramienta de copia de seguridad local cifrada (Seedvault, disponible en GrapheneOS/CalyxOS) para copias de seguridad locales cifradas

### 4.3 Copias de Seguridad de Computadoras
- Use Time Machine (macOS) con una unidad de copia de seguridad cifrada (habilite *Cifrar copia de seguridad* al configurar el destino)
- Use Duplicati o Restic para copias de seguridad cifradas multiplataforma — estas herramientas cifran antes de cargar, por lo que incluso el almacenamiento en la nube está protegido
- Mantenga las copias de seguridad en unidades externas cifradas; almacene en una ubicación separada de su dispositivo principal (en caso de incautación física en su hogar)

---

## 5. Lista de Verificación de Higiene de Cifrado

**Revisiones mensuales:**
- [ ] Todos los dispositivos (teléfono, laptop, unidades externas) tienen el cifrado activo y verificado
- [ ] Las contraseñas de cifrado se almacenan de forma segura (gestor de contraseñas)
- [ ] Las claves de recuperación se almacenan por separado (no en el dispositivo cifrado mismo)
- [ ] Los sistemas operativos están completamente actualizados (los parches solucionan vulnerabilidades que explotan las herramientas forenses)
- [ ] Datos biométricos deshabilitados en dispositivos utilizados para trabajo sensible

**Antes de cualquier situación de alto riesgo:**
- [ ] Dispositivo apagado (no solo bloqueado) antes de cualquier contacto policial anticipado
- [ ] Datos sensibles eliminados o en una unidad cifrada no conectada

---

*Esta guía no constituye asesoramiento legal. Las leyes varían según la jurisdicción.*

[← Volver al Índice](../index.md)

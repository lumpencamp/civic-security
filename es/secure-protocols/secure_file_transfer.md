# Transferencia Segura de Archivos: Compartir Documentos Sensibles de Forma Segura

*Estado: Nivel 2 | Audiencia: Organizadores, periodistas y cualquiera que comparta documentos sensibles*

Compartir archivos de forma segura es uno de los desafíos de seguridad operativa más comunes. Los archivos adjuntos de correo electrónico no están cifrados de forma predeterminada, los servicios de almacenamiento en la nube cooperan con las fuerzas del orden e incluso las plataformas "seguras" como WhatsApp pueden filtrar metadatos. Esta guía cubre el conjunto completo de herramientas para la transferencia segura de archivos, desde el intercambio simple uno a uno hasta la protección de fuentes anónimas.

---

## 1. Evaluación de Amenazas para la Transferencia de Archivos

Antes de elegir un método, comprenda de qué se está protegiendo:

| Amenaza | Preocupación | Método Apropiado |
|--------|---------|-------------------|
| ISP u observador de la red viendo el contenido del archivo | Correo electrónico, sincronización en la nube | Transferencia cifrada de extremo a extremo |
| Operador del servidor leyendo los archivos almacenados | Servicios en la nube, servidores de correo electrónico | Cifrado de conocimiento cero |
| Citación de las fuerzas del orden a un proveedor de servicios | Signal, nube | Servicios sin registros de contenido + canary warrant |
| Metadatos que revelan quién envió qué a quién | Signal (no sellado), correo electrónico | OnionShare, Magic Wormhole, remitente sellado |
| Contenido del archivo con metadatos de identificación (EXIF, autor) | Fotos, documentos | Eliminación de metadatos antes de transferir |
| Identidad del destinatario | Canales normales | Métodos de transferencia anónima |

---

## 2. Signal para la Transferencia de Archivos

Signal es adecuado para la mayor parte del intercambio de archivos sensibles del día a día dentro de su red de contactos de confianza.

**Qué protege Signal:**
- El contenido del archivo (cifrado de extremo a extremo)
- Metadatos entre usted y los servidores de Signal (con el remitente sellado o *sealed sender*)

**Limitaciones:**
- Los archivos se almacenan tanto en los dispositivos del remitente como en los del destinatario hasta que se eliminan
- Signal puede ver (e históricamente se le ha exigido divulgar) metadatos de la cuenta (cuándo se registró, hora de la última conexión)
- No es adecuado para transferencias anónimas — Signal requiere un número de teléfono

**Mejores prácticas:**
- Habilite los mensajes desaparecidos para que los archivos compartidos se eliminen automáticamente
- Confirme los números de seguridad con los destinatarios antes de compartir documentos altamente sensibles
- Envíe archivos desde el modo avión a través de Wi-Fi para evitar los metadatos de la red celular

---

## 3. OnionShare

**OnionShare** es una herramienta gratuita y de código abierto que crea una dirección .onion temporal en la red Tor y le permite compartir archivos a través de ella. El remitente ejecuta un Servicio Oculto (Hidden Service) de Tor local directamente en su máquina — no hay servidor intermediario, ni cuenta, ni registro.

**Capacidades:**
- Compartir archivos: los destinatarios descargan directamente desde su máquina a través de Tor
- Recibir archivos: crear un buzón de entrega anónimo para que otros le suban archivos
- Alojar una sala de chat temporal: efímera, sin cuentas, sin registros
- Alojar un sitio web: sitio web temporal alojado en Tor

**Por qué es poderoso:**
- **Sin registros del servidor:** Los archivos se transfieren directamente entre máquinas a través de Tor; ningún intermediario registra la transacción
- **No se requiere cuenta:** Ni el remitente ni el destinatario necesitan una cuenta
- **Anónimo para ambas partes:** Tanto el remitente como el destinatario son anonimizados por Tor
- **Sin límite de tamaño de archivo** (en la práctica, limitado por la velocidad de conexión y el ancho de banda de Tor)

### 3.1 Configuración y Uso de OnionShare

**Instalación:**
- Descargue desde onionshare.org — verifique la firma PGP
- Disponible para Windows, macOS, Linux (como .deb o .rpm), y como paquete de F-Droid para Android

**Compartir archivos:**
1. Abra OnionShare → pestaña *Compartir archivos*
2. Arrastre archivos o carpetas a la ventana
3. Configure las opciones:
   - *Dejar de compartir después de que se hayan enviado los archivos* (compartir una vez — recomendado)
   - *Temporizador de inicio automático* (opcional — el recurso compartido está disponible a una hora específica)
4. Haga clic en *Empezar a compartir* — OnionShare genera una URL .onion y una contraseña (clave)
5. Comparta la dirección .onion Y la clave con su destinatario a través de un canal seguro (Signal)
6. El destinatario abre Tor Browser, ingresa la URL .onion y la clave, y descarga el archivo
7. OnionShare muestra el estado de descarga en tiempo real; cierre cuando termine

**Recibir archivos (buzón de entrega):**
1. OnionShare → pestaña *Recibir archivos*
2. Inicie el servicio — genere una URL .onion
3. Comparta esta URL con personas que necesiten enviarle archivos (por ejemplo, un periodista que crea un buzón para recibir documentos de una fuente)
4. Los archivos se suben directamente a una carpeta en su máquina; usted ve las cargas en tiempo real

**Nota de seguridad:** El destinatario necesita Tor Browser u Orbot para acceder a las direcciones .onion. Esto limita la audiencia. Planifique en consecuencia.

### 3.2 OnionShare para Protección de Fuentes (Periodistas)

SecureDrop (abajo) es el estándar de la industria para la recepción de fuentes, pero OnionShare ofrece una alternativa más simple y liviana para periodistas individuales u organizaciones más pequeñas:

- Use el modo "Recibir archivos" para crear un buzón de entrega anónimo
- Comparta la dirección .onion pública o selectivamente
- No se requiere cuenta ni autenticación de la fuente
- Los archivos llegan directamente a su máquina, sin intermediarios en la nube

---

## 4. SecureDrop

SecureDrop es el estándar de oro para la comunicación anónima entre fuente y periodista, desarrollado por la Freedom of the Press Foundation (FPF). Está diseñado específicamente para proteger fuentes vulnerables que comparten documentos sensibles con organizaciones de noticias.

**Cómo funciona:**
- La sala de redacción ejecuta SecureDrop en un servidor dedicado y aislado de la red (*air-gapped*)
- Las fuentes acceden a él solo a través del Tor Browser, recibiendo un nombre en código aleatorio
- Los periodistas acceden a SecureDrop solo desde una computadora dedicada y aislada que ejecuta Tails OS
- No se requiere cuenta, correo electrónico, ni información de identificación

**Qué salas de redacción tienen SecureDrop:**
La Freedom of the Press Foundation mantiene un directorio en freedom.press/news/directory

**Para las fuentes:** Si tiene información confidencial para una organización de noticias, use su dirección de SecureDrop; encuéntrela en el directorio de la FPF. Acceda a ella solo desde Tor Browser en un dispositivo confiable y privado.

**Para las organizaciones:** La configuración de SecureDrop requiere una infraestructura técnica significativa. La FPF brinda apoyo: contáctelos en freedom.press.

---

## 5. Magic Wormhole

Magic Wormhole es una herramienta de línea de comandos para la transferencia rápida, cifrada y única de archivos entre dos máquinas. Genera una frase de código simple que conecta el remitente y el receptor directamente, con cifrado de extremo a extremo.

**Por qué usarlo:**
- Más simple que OnionShare cuando ambas partes son usuarios técnicos familiarizados con la línea de comandos
- Rápido: Transferencia directa, sin limitación de ancho de banda de Tor
- Sin cuenta, sin servidor intermediario (aunque usa un servidor de retransmisión para iniciar la conexión)
- Código de un solo uso: cada transferencia usa un código único que caduca

**Limitación:** No proporciona anonimato: su IP es visible para el servidor de retransmisión y potencialmente para su par. Use OnionShare si se requiere anonimato.

**Instalación:**
```
pip install magic-wormhole
# o: brew install magic-wormhole (macOS)
# o: apt install magic-wormhole (Debian/Ubuntu)
```

**Uso:**
```
# Remitente:
wormhole send /ruta/al/archivo.pdf
# Produce: wormhole receive 7-crossword-galaxy (código de ejemplo)

# Receptor (en una máquina diferente):
wormhole receive 7-crossword-galaxy
```

---

## 6. Correo Electrónico Cifrado (PGP)

El cifrado de correo electrónico PGP (Pretty Good Privacy) es el método tradicional para la transferencia cifrada de archivos por correo electrónico. Es poderoso pero técnicamente exigente, y la mayoría de los activistas encuentran Signal u OnionShare más prácticos para el uso diario.

**Cuándo tiene sentido el correo electrónico PGP:**
- Comunicarse con alguien que solo tiene correo electrónico (no Signal)
- Archivar registros cifrados que deben almacenarse a largo plazo con autoría verificable
- Firmar documentos para demostrar que no han sido manipulados

### 6.1 Conceptos Básicos de PGP

PGP utiliza cifrado asimétrico:
- Tiene una **clave pública** que comparte ampliamente — otros la usan para cifrar mensajes para usted
- Tiene una **clave privada** que mantiene en secreto — la usa para descifrar mensajes que se le envían
- Puede **firmar** mensajes con su clave privada para probar la autoría

**Conceptos clave:**
- Un documento firmado prueba que proviene de usted y no ha sido modificado
- Un archivo cifrado solo puede ser leído por quien tenga la clave privada correspondiente

### 6.2 Herramientas PGP

- **GPG (GNU Privacy Guard):** Implementación de PGP en la línea de comandos, disponible en todas las plataformas. La herramienta fundamental.
- **Kleopatra (Windows/Mac):** Interfaz gráfica de usuario para GPG
- **GPG Suite (Mac):** Integra PGP en macOS Mail y Finder
- **Enigmail (Thunderbird):** El cliente de correo electrónico Thunderbird tiene soporte OpenPGP integrado

**Flujo de trabajo básico:**
1. Generar un par de claves: `gpg --full-generate-key`
2. Exportar su clave pública: `gpg --export --armor su@correo.com > clavepublica.asc`
3. Compartir su clave pública con contactos
4. Cifrar un archivo para un destinatario: `gpg --encrypt --recipient destinatario@correo.com archivo.pdf`
5. Enviar el archivo cifrado (es seguro enviarlo a través de un correo electrónico no cifrado)
6. El destinatario descifra: `gpg --decrypt archivo.pdf.gpg`

### 6.3 Limitaciones de PGP

- **Metadatos:** PGP cifra el contenido del mensaje, pero no los metadatos: quién envió qué a quién, y cuándo, es visible para su proveedor de correo electrónico.
- **Gestión de claves:** Debe verificar que la clave pública a la que cifra pertenece realmente a su destinatario previsto (de lo contrario, cifra a la clave de un atacante). Use fiestas de firmas de claves (*key signing parties*), o Signal para verificar las huellas dactilares de manera fuera de banda (*out-of-band*).
- **Complejidad:** PGP es famoso por ser difícil de usar correctamente. Para la mayoría de los activistas, Signal y OnionShare son más prácticos y menos propensos a errores.

---

## 7. Eliminación de Metadatos

Incluso después de usar un método de transferencia seguro, los archivos a menudo contienen metadatos incrustados que pueden identificarlo.

### 7.1 Metadatos de Documentos

**Archivos de Microsoft Office (.docx, .xlsx, .pptx):** Contienen el nombre del autor (desde la cuenta de Windows/Office), organización, nombre de la computadora, fecha de creación, historial de edición y, a veces, el historial de revisiones que muestra el contenido eliminado.

**Eliminación en LibreOffice:**
1. *Archivo → Propiedades → General → Restablecer propiedades* (elimina algunos metadatos)
2. *Archivo → Exportar → Exportar a PDF*, luego use una herramienta de eliminación de metadatos de PDF (más completo)

**Eliminación con ExifTool (línea de comandos):**
```
exiftool -all= documento.docx
```

**Archivos PDF:** Contienen el autor, el software de creación, la fecha de creación y, a veces, las coordenadas GPS si se crearon en un dispositivo móvil.
```
exiftool -all= documento.pdf
```

### 7.2 Datos EXIF de Fotos/Imágenes

Las fotos contienen extensos metadatos EXIF:
- Coordenadas GPS (ubicación exacta donde se tomó la foto, a menudo con precisión de metros)
- Marca y modelo del dispositivo
- Fecha y hora
- Ajustes de la cámara
- A veces: número de serie de la cámara

**Herramientas:**
- **ExifTool (todas las plataformas):** La herramienta definitiva
  ```
  exiftool -all= foto.jpg           # Eliminar todos los metadatos
  exiftool -GPS= foto.jpg           # Eliminar solo datos GPS
  exiftool -j foto.jpg              # Ver todos los metadatos
  ```
- **Scrambled EXIF (Android):** Comparta fotos sin metadatos a través de la hoja de compartir de esta aplicación
- **Image Scrubber (navegador):** imgscrubber.com — arrastre y suelte, elimina EXIF en el navegador
- **Dangerzone:** Para documentos — los convierte en archivos PDF en un contenedor aislado, elimina todos los metadatos

### 7.3 Regla Operativa

**Antes de compartir cualquier foto o documento de una acción o contexto sensible:**
1. Elimine todos los metadatos con ExifTool o equivalente
2. Verifique que los metadatos hayan desaparecido: `exiftool foto.jpg` no debería mostrar datos EXIF
3. Luego, comparta a través de un canal seguro

Este debe ser un paso no negociable en su flujo de trabajo de información.

---

## 8. Almacenamiento y Uso Compartido Seguro de Archivos para Equipos

### 8.1 Proton Drive

**Proton Drive** (de los creadores de Proton Mail) proporciona almacenamiento en la nube cifrado de conocimiento cero:
- Los archivos se cifran en su dispositivo antes de subirlos: Proton no puede leerlos
- Enlaces de uso compartido cifrados con contraseñas y fechas de vencimiento
- Con sede en Suiza, sujeto a la ley de privacidad suiza (más fuerte que la de EE. UU.)

**Uso para:** Compartir documentos organizativos confidenciales con los miembros del equipo; almacenar archivos cifrados

### 8.2 Cryptomator

**Cryptomator** es una herramienta de código abierto que crea una "bóveda" cifrada sobre cualquier proveedor de almacenamiento en la nube (Dropbox, Google Drive, iCloud, etc.):
- Los archivos se cifran localmente antes de sincronizarse con la nube
- El proveedor de la nube solo ve archivos cifrados e ilegibles
- Funciona en Windows, macOS, Linux, iOS, Android

**Uso para:** Agregar cifrado de conocimiento cero a su almacenamiento en la nube existente sin cambiar de proveedor.

### 8.3 Keybase Teams

**Keybase** proporciona uso compartido de archivos en equipo cifrado de extremo a extremo:
- Los archivos compartidos en Teams (Equipos) están cifrados y solo pueden leerlos los miembros del equipo
- Se integra con chat cifrado, por lo que el intercambio de archivos y la comunicación están en un solo lugar
- La creación de la cuenta requiere cierta información de identificación; considere esto en su modelo de amenazas

---

*Esta guía no constituye asesoramiento legal. Las leyes varían según la jurisdicción.*

[← Volver al Índice](../index.md)

# Eliminación de Datos y Metadatos: Eliminando Rastros Digitales

*Estado: Nivel 1 | Audiencia: Todos los miembros*

Cada archivo que crea, cada foto que toma, cada documento que edita genera metadatos invisibles: datos sobre datos. Estos metadatos a menudo revelan más que el contenido en sí: quién creó un archivo, cuándo, dónde, con qué software y en qué dispositivo. Esta guía cubre cómo encontrar, eliminar y destruir permanentemente metadatos y datos sensibles.

---

## 1. Qué Son los Metadatos y Por Qué Importan

### 1.1 Tipos de Metadatos

**Metadatos de archivos (EXIF, propiedades de documentos):**
- Fotos: Coordenadas GPS (ubicación exacta), marca de tiempo, modelo de cámara, lente, número de serie de la cámara, software de edición, nombre del fotógrafo si está almacenado en la configuración de la cámara.
- Documentos: Nombre del autor (desde la configuración del SO/Office), organización, nombre de la computadora, fecha de creación, fechas de modificación, historial de edición, a veces el seguimiento de cambios y contenido eliminado.
- Audio/Video: Dispositivo de grabación, marca de tiempo, coordenadas GPS si se grabó en un teléfono inteligente.

**Metadatos del sistema:**
- Registros de acceso a archivos (cuándo se abrió un archivo por última vez)
- Cachés de miniaturas (vistas previas de imágenes, incluidas las eliminadas)
- Historial del navegador, cookies, páginas en caché
- Registros de aplicaciones (qué aplicaciones se abrieron, cuándo, por cuánto tiempo)
- Metadatos de la cola de impresión (muchas impresoras incrustan códigos de identificación de máquina invisibles en cada documento impreso)

**Metadatos de red:**
- Registros de direcciones IP (qué IP accedió a qué servicio, cuándo)
- Consultas DNS (qué nombres de dominio se resolvieron, desde qué IP)
- Tamaño y tiempo de conexión (utilizable para análisis de tráfico incluso cuando el contenido está cifrado)

### 1.2 Consecuencias en el Mundo Real de los Metadatos no Gestionados

- **El atentado con bomba a Bari/Cherney (1990):** Judi Bari y Darryl Cherney, organizadores de Earth First!, resultaron heridos en un coche bomba. El FBI los identificó erróneamente como sospechosos en parte debido a la investigación de sus materiales y asociaciones: un estudio de caso sobre cómo el análisis de documentos sirve a la investigación.
- **Reality Winner (2017):** Contratista de la NSA que filtró un documento clasificado. El documento contenía puntos amarillos de la impresora (códigos de identificación de máquina incrustados por la impresora) que identificaron la impresora específica que ella utilizó, lo que llevó a su identificación y arresto.
- **Innumerables casos de doxxing:** Fotos de activistas compartidas en las redes sociales retuvieron datos EXIF de GPS que revelaron su dirección particular.

---

## 2. Eliminación de Metadatos de Archivos

### 2.1 ExifTool (Todas las Plataformas) — La Herramienta Esencial

ExifTool es la herramienta de código abierto definitiva para leer y eliminar metadatos de prácticamente todos los tipos de archivos. Está basada en la línea de comandos pero es poderosa.

**Instalación:**
- macOS: `brew install exiftool`
- Ubuntu/Debian: `sudo apt install exiftool`
- Windows: Descargue desde exiftool.org
- F-Droid (Android): No disponible directamente; use Scrambled EXIF para fotos

**Comandos esenciales:**

```bash
# Ver todos los metadatos en un archivo
exiftool photo.jpg
exiftool document.docx
exiftool video.mp4

# Eliminar TODOS los metadatos de un archivo
exiftool -all= photo.jpg

# Eliminar todos los metadatos de TODOS los archivos en un directorio
exiftool -all= /ruta/a/la/carpeta/

# Eliminar solo las coordenadas GPS, mantener otros datos
exiftool -GPS= photo.jpg

# Eliminar metadatos por lotes y guardar los originales como archivos _original
exiftool -all= -overwrite_original_in_place photo.jpg

# Verificar: ver qué queda después de la eliminación
exiftool photo.jpg  # Debería mostrar campos EXIF mínimos o nulos
```

### 2.2 Metadatos de Fotos en Dispositivos Móviles

**Android — Scrambled EXIF:**
- Aplicación de F-Droid
- Comparta una foto en Scrambled EXIF; elimina los datos EXIF y crea una copia limpia
- Alternativa: integrado en algunas aplicaciones de cámara (la cámara de CalyxOS los elimina por defecto)

**iOS — Visor de Metadatos de Imágenes:**
- iOS 16+: *Fotos → Seleccionar foto → Compartir → Eliminar ubicación* (elimina solo el GPS; no elimina todos los datos EXIF)
- Para la eliminación completa: use una aplicación de terceros como Metapho (de pago) o exporte la foto a Archivos y procese con un Atajo (Shortcut) usando acciones compatibles con ExifTool.
- Mejor práctica: use Scrambled EXIF en un dispositivo Android confiable o procese en el escritorio antes de compartir.

**Signal:** Signal elimina automáticamente los metadatos de las fotos compartidas a través de la aplicación. Las imágenes recibidas a través de Signal también tienen los metadatos eliminados. Esta es una razón para compartir fotos a través de Signal en lugar de por correo electrónico o un enlace en la nube.

### 2.3 Metadatos de Documentos

**Documentos de Microsoft Office / LibreOffice:**

Eliminación incorporada:
- *Archivo → Información → Inspeccionar documento → Inspeccionar* (Office): Encuentra y elimina información personal, control de cambios, contenido oculto, comentarios
- *Archivo → Propiedades → Estadísticas/Descripción*: Verifique y borre los campos de autor

ExifTool para documentos:
```bash
exiftool -all= document.docx
exiftool -all= presentation.pptx
exiftool -all= spreadsheet.xlsx
```

**Enfoque más seguro: Convertir a PDF con Dangerzone**

**Dangerzone** (dangerzone.rocks) es una herramienta gratuita y de código abierto que:
1. Abre su documento en un contenedor aislado (*sandbox* de Docker)
2. Lo renderiza a una imagen perfecta a nivel de píxeles
3. Convierte la imagen de nuevo a un PDF
4. Este proceso elimina TODOS los metadatos incrustados, macros, contenido activo y malware potencial del documento

El PDF resultante contiene solo información visual: sin nombres de autores, sin historial de edición, sin código incrustado. Este es el método más seguro para compartir documentos de fuentes desconocidas o compartir documentos donde desea cero fuga de metadatos.

### 2.4 Esteganografía de Impresora (Códigos de Identificación de Máquina)

Muchas impresoras láser a color incrustan puntos de seguimiento amarillos invisibles en cada página impresa. Estos puntos codifican:
- El número de serie de la impresora
- La fecha y hora de impresión

Así fue como identificaron a Reality Winner. EFF mantiene una lista de impresoras que se sabe que usan este sistema (eff.org/issues/printers).

**Contramedidas:**
- Imprima desde una impresora que no esté asociada con su identidad (biblioteca, imprenta: en efectivo, sin tarjeta de fidelidad)
- Use una impresora que no esté en la lista de impresoras identificadas de EFF
- Para documentos extremadamente sensibles: imprima, luego fotografíe el documento y comparta la fotografía (con los metadatos eliminados) en lugar del documento impreso o el archivo original.

---

## 3. Eliminación Segura de Datos

### 3.1 Por Qué la Eliminación Normal no Funciona

Cuando "elimina" un archivo, el sistema operativo marca el espacio como disponible para su reutilización, pero los datos permanecen en el disco hasta que se sobrescriben con nuevos datos. Las herramientas forenses (Autopsy, EnCase, FTK) pueden recuperar archivos "eliminados" de discos duros convencionales y, a veces, de SSD y almacenamiento flash.

### 3.2 Eliminación Segura de Archivos

**En discos duros tradicionales (HDD):**
Sobrescribir con datos aleatorios hace que la recuperación sea computacionalmente inviable.

- macOS: `rm -P file.txt` (obsoleto en macOS más recientes; use el borrado seguro de la Utilidad de Discos para unidades)
- Linux: `shred -vzn 3 file.txt` (sobrescribe 3 veces con datos aleatorios, luego ceros, luego elimina)
- Windows: Eraser (herramienta gratuita) o `sdelete -z -p 3 file.txt` (SDelete de Sysinternals)

**En SSD, unidades flash y teléfonos:**
Los SSD usan algoritmos de nivelación de desgaste (*wear-leveling*) que distribuyen los datos a través del almacenamiento físico de manera que la sobrescritura de archivos individuales no sea confiable. Los datos que usted "destruye" pueden no ser los datos que terminan sobrescritos.

**Mejor práctica para SSD y teléfonos:**
- Habilite el cifrado de disco completo desde el principio (si la unidad siempre estuvo cifrada, los datos eliminados son basura cifrada, incluso si son técnicamente recuperables)
- Para retirar un SSD o teléfono: restablecimiento de fábrica + llene la unidad con datos basura + restablecimiento de fábrica nuevamente
- Para la mayor seguridad: destrucción física del chip de almacenamiento

### 3.3 Borrado Seguro de Unidades Completas

**Al retirar un dispositivo:**

*macOS:*
- Para unidades internas: *Utilidad de Discos → Seleccionar unidad → Borrar → Opciones de seguridad → Borrado seguro de 3 pasadas* (no disponible en SSD en macOS modernos; use cifrado + restablecimiento en su lugar)
- Unidades cifradas con FileVault: Borre la unidad (los datos ya son basura cifrada)

*Linux:*
```bash
# Borrar una unidad completa (reemplace /dev/sdX con la unidad de destino — TENGA CUIDADO)
sudo shred -vzn 3 /dev/sdX

# O con dd:
sudo dd if=/dev/urandom of=/dev/sdX bs=1M status=progress
```

*Windows:*
- Descargue DBAN (Darik's Boot and Nuke) para borrar discos duros desde un medio de arranque
- Para SSD: use la utilidad de borrado seguro del fabricante, o use el cifrado BitLocker + formatear

### 3.4 Tails para Operación Efímera

El enfoque más completo para la eliminación de datos: nunca escribir datos confidenciales en el almacenamiento persistente en primer lugar.

Tails OS se ejecuta completamente en RAM. Cuando apaga una computadora Tails, toda la RAM se borra. No quedan rastros en la máquina anfitriona. Este es el estándar de oro para el trabajo sensible.

Consulte la [Guía de Tails OS](../digital-security/tails_os_guide.md) para ver las instrucciones de configuración.

---

## 4. Datos del Navegador y de Aplicaciones

### 4.1 Limpieza de Datos del Navegador

Los navegadores almacenan cantidades significativas de datos potencialmente sensibles:

**Qué borrar regularmente:**
- Historial de navegación
- Historial de descargas
- Cookies y datos de sitios
- Imágenes y archivos en caché
- Datos de formularios guardados y autocompletar
- Contraseñas guardadas (use un gestor de contraseñas dedicado en su lugar)

**Firefox:**
*Configuración → Privacidad y seguridad → Limpiar datos* → seleccione todas las categorías → Limpiar

**Automatización:** Configure Firefox para borrar todos los datos al cerrar (*Configuración → Privacidad y seguridad → Cookies y datos del sitio → Eliminar cookies y datos del sitio cuando se cierre Firefox*)

**Para la máxima privacidad:** Use Tor Browser (borra todos los datos de sesión al cerrar por diseño) o use Firefox en modo de Navegación Privada para sesiones sensibles.

### 4.2 Registros (Logs) y Cachés de Aplicaciones

Los sistemas operativos y las aplicaciones generan registros extensos:

*macOS:*
- Registros del sistema: `/var/log/` (requiere root para acceso completo)
- Registros de aplicaciones: `~/Library/Logs/` — bórrelos periódicamente
- Los informes de fallos contienen información del sistema: `~/Library/Logs/DiagnosticReports/`
- Elementos recientes: *Menú Apple → Elementos recientes → Borrar menú*

*Linux:*
- `/var/log/` — registros del sistema, puede requerir root para eliminarlos
- `journalctl --vacuum-time=1d` — borrar registros del diario de systemd con más de 1 día de antigüedad
- BleachBit (herramienta gratuita): automatiza la limpieza de cachés de aplicaciones, registros y archivos temporales

*Windows:*
- Registros del Visor de eventos: `eventvwr.msc` → Haga clic derecho en cada registro → Vaciar registro
- Archivos de captura previa (*Prefetch*): `C:\Windows\Prefetch` — eliminar (registros de programas ejecutados recientemente)
- Archivos temporales: `%temp%` en el cuadro de diálogo Ejecutar → eliminar todo
- BleachBit para Windows automatiza la limpieza integral

### 4.3 Limpieza de Signal

Signal almacena mensajes en su dispositivo. Cuando elimina una conversación o mensaje en Signal, se elimina de la base de datos local de Signal, pero es posible que no se sobrescriba de inmediato en el almacenamiento.

- **Mensajes desaparecidos** es el método de limpieza más confiable; úselo como predeterminado
- Borrado completo y periódico de los datos de la aplicación: desinstale y vuelva a instalar Signal (perderá el historial de mensajes; haga una copia de seguridad primero si es necesario)
- Nota: Las copias de seguridad de Signal (Android) están cifradas; guárdelas solo en unidades cifradas

---

## 5. Minimización de Datos: Generar Menos en Primer Lugar

La gestión de metadatos más eficaz es no generarlos en absoluto.

**Principios:**
- Use aplicaciones y servicios que recopilen menos datos: Signal en lugar de WhatsApp, Firefox en lugar de Chrome, DuckDuckGo en lugar de Google.
- Desactive la sincronización automática en la nube y la copia de seguridad para datos confidenciales
- Use aplicaciones en modo sin conexión cuando no sea necesaria la sincronización
- Tome menos fotos de situaciones delicadas; lo que no existe no se puede analizar
- Revise y elimine mensajes, archivos y fotos antiguos regularmente: si no lo necesita, elimínelo

**Práctica mensual de higiene de datos:**
- [ ] Borrar el historial del navegador, las cookies y el caché
- [ ] Revisar y eliminar archivos y fotos innecesarios de sus dispositivos
- [ ] Comprobar los permisos de las aplicaciones para aquellas con amplio acceso a datos que no haya revisado recientemente
- [ ] Revisar y eliminar cualquier dato de aplicación que ya no necesite
- [ ] Ejecutar ExifTool en cualquier foto que planee compartir públicamente

---

*Esta guía no constituye asesoramiento legal. Las leyes varían según la jurisdicción.*

[← Volver al Índice](../index.md)
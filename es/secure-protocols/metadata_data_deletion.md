# Depuración de metadatos y eliminación segura de datos

Esta guía cubre cómo limpiar datos ocultos de archivos antes de compartirlos y cómo eliminar datos permanentemente para que no puedan recuperarse con herramientas forenses.

## ¿Qué son los metadatos?

Los metadatos son "datos sobre datos".Es información oculta incrustada dentro de archivos (fotos, vídeos, documentos).

* **Fotos/vídeos (datos EXIF):** Una fotografía tomada con un teléfono inteligente a menudo contiene las coordenadas GPS exactas del lugar donde se tomó, la hora y la fecha, el modelo de teléfono e incluso la dirección en la que apuntaba la cámara.
* **Documentos (Word, PDF):** Suelen contener el nombre del autor, el nombre de la organización, el software utilizado y la fecha de creación.

Si publica una fotografía de protesta en línea o envía un documento de planificación a un periodista sin borrar los metadatos, puede revelar accidentalmente su identidad o ubicación.

### Herramientas para limpiar metadatos

* **Móvil (Android):** Utilice **ExifEraser** o **Scrambled Exif**.Compartes la foto con la aplicación, esta elimina los metadatos y luego compartes la foto limpia.
* **Móvil (iOS):** Utilice **Metapho**.
* **Escritorio (Windows/Mac/Linux):** **MAT2** (Kit de herramientas de anonimización de metadatos) es el estándar de oro.Funciona a través de la línea de comando o como complemento para el navegador Tor.
* **Documentos:** Para archivos PDF y documentos de Office, utilice **Dangerzone**.Convierte el documento en un PDF seguro representándolo en píxeles y viceversa, destruyendo por completo todos los metadatos y el malware potencial.

## Eliminación segura de datos

Cuando arrastra un archivo a la "Papelera" y lo vacía, la computadora en realidad no borra el archivo.Simplemente marca el espacio como "disponible".El software forense (como Cellebrite, utilizado por la policía) puede recuperar fácilmente estos archivos "borrados".

### El papel del cifrado de disco completo (FDE)

La forma más eficaz de proteger los datos eliminados es asegurarse de que todo el dispositivo esté cifrado (cifrado de disco completo).
* Si su disco duro está cifrado y la policía lo confisca mientras está apagado, no podrán leer *ningún* dato, ya sea activo o eliminado.
* Los teléfonos inteligentes modernos (iOS/Android) y los sistemas operativos modernos (macOS FileVault, Windows BitLocker, Linux LUKS) utilizan FDE.Asegúrese de que esté encendido.

### Herramientas de limpieza segura

Si necesita asegurarse de que un archivo específico se destruya mientras la computadora aún está en uso:

* **Escritorio:** Utilice **BleachBit**.Puede sobrescribir el espacio libre en un disco duro con datos aleatorios, haciendo imposible la recuperación.
* **Nota sobre las SSD:** Las unidades de estado sólido (SSD) manejan los datos de forma diferente a los discos duros magnéticos antiguos.Sobrescribir repetidamente archivos específicos en una SSD no es confiable y degrada la unidad.Confiar en el cifrado de disco completo es el enfoque más seguro para el hardware moderno.

_Última actualización: 2026_
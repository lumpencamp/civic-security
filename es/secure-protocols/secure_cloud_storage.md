# Colaboración y almacenamiento seguro en la nube

Los grupos de activistas necesitan compartir documentos, hojas de cálculo y archivos.Sin embargo, el uso de servicios convencionales para el consumidor crea enormes vulnerabilidades de seguridad.

## El problema con Google Drive y Dropbox

Servicios como Google Drive, Dropbox y Microsoft OneDrive contienen las claves de cifrado de sus datos.Esto significa:
1. Pueden escanear sus archivos en busca de violaciones de contenido.
2. **Entregarán sus archivos a las autoridades** si reciben una citación o orden judicial, a menudo sin notificárselo.

Para documentos de planificación, listas de miembros o estrategias legales confidenciales, estas plataformas no son seguras.

## La solución: almacenamiento cifrado de extremo a extremo (E2EE)

El almacenamiento E2EE significa que los archivos se cifran en su dispositivo *antes* de cargarlos en la nube.La empresa que aloja los archivos no tiene las claves para descifrarlos.Si la policía cita al servidor, solo obtendrá texto cifrado ilegible.

### Proveedores recomendados

* **Proton Drive:** Parte de la suite Proton (ProtonMail, ProtonVPN).Ofrece una interfaz muy segura y fácil de usar para almacenar y compartir archivos.
* **Tresorit:** Un proveedor de almacenamiento en la nube E2EE premium y altamente pulido diseñado para empresas y organizaciones que necesitan un cumplimiento estricto de la seguridad.
* **Cryptomator (bricolaje avanzado):** Si debes usar Google Drive o Dropbox (tal vez porque una organización ya pagó por ello), puedes usar Cryptomator.Es un programa gratuito de código abierto que crea una bóveda cifrada en su computadora.Colocas tus archivos en la bóveda, Cryptomator los cifra y *luego* sincronizas la bóveda cifrada con Google Drive.

## Colaboración segura en tiempo real (alternativas a Google Docs)

Si su grupo necesita escribir un documento o crear una hoja de cálculo juntos en tiempo real, Google Docs es el valor predeterminado, pero no es privado.

* **CryptPad.fr (altamente recomendado):** CryptPad es una alternativa totalmente E2EE a Google Workspace.Ofrece documentos colaborativos de texto enriquecido, hojas de cálculo y diapositivas de presentación.Debido a que es E2EE, los administradores del servidor no pueden leer sus documentos.Puede utilizar la instancia principal de CryptPad.fr o una organización con conocimientos de tecnología puede alojar su propia instancia.

_Última actualización: 2026_
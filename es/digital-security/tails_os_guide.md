# Una guía completa del sistema operativo Tails

Tails (The Amnesic Incognito Live System) es un sistema operativo gratuito centrado en la seguridad que puedes iniciar en casi cualquier computadora desde una memoria USB. Está diseñado para proteger tu privacidad y anonimato forzando todas tus conexiones a Internet a través de la red Tor y sin dejar rastro en la computadora que utilizas.

**Caso de uso:** Tails es la herramienta adecuada cuando necesitas realizar una tarea delicada (como investigar a un oponente, comunicarte con un periodista o administrar cuentas anónimas) sin dejar una huella digital en la computadora o la red.

---

### **Sección 1: Adquirir Tails de forma segura**

Asegurarse de que su copia de Tails sea genuina y no esté alterada es el primer paso más importante.

#### **Paso 1: Descargar Tails**

* Navegue al sitio web oficial de Tails: **`https://tails.net`**
* Vaya a la sección "Instalar" y descargue la imagen USB (archivo `.img`).

#### **Paso 2: Verifique su descarga (PASO CRÍTICO)**

La verificación garantiza que el archivo que descargaste sea el archivo auténtico de los desarrolladores de Tails y que no esté dañado ni reemplazado por una versión maliciosa. Utilizará PGP (Pretty Good Privacy) para esto.

1. **Instala GnuPG:** Si no lo tienes, instala una herramienta PGP. Para Linux, es `sudo apt-get install gnupg`. Para macOS, utilice `brew install gnupg`. Para Windows, utilice `Gpg4win`.
2. **Descargue la clave de firma de Tails:** Esta es una clave especial utilizada por los desarrolladores de Tails para firmar sus lanzamientos. Puedes descargarlo desde el sitio web de Tails o ejecutando:
    ```bash
    wget https://tails.net/tails-signing.key
    ```
3. **Importar la clave:** Importe la clave a su conjunto de claves PGP:
    ```bash
    gpg --import tails-signing.key
    ```
4. **Descargue el archivo de firma:** En la página de descarga de Tails, habrá un archivo `.sig` correspondiente para su descarga. Descargue este archivo en el mismo directorio que su archivo `.img`.
5. **Verificar:** Abra su terminal, navegue hasta su directorio de descargas y ejecute el comando de verificación:
    ```bash
    gpg --verify tails-amd64-X.XX.img.sig tails-amd64-X.XX.img
    ```
    *(Reemplace `X.XX` con el número de versión que descargó)*

    You are looking for the output **"Good signature from..."**. This confirms your download is authentic. Ignore any warnings about "trust."

---

### **Sección 2: Creación del USB de arranque**

#### **Método 1: balenaEtcher (recomendado para la mayoría de los usuarios)**

`balenaEtcher` es una herramienta gráfica que funciona en Windows, macOS y Linux. Es el método más fácil y seguro.

1. Descargue e instale Etcher desde `https://www.balena.io/etcher/`.
2. Abra Grabador.
3. Seleccione el archivo `.img` de Tails que descargó.
4. Seleccione su unidad USB de destino (al menos 8 GB). **Asegúrese absolutamente de haber seleccionado la unidad correcta, ya que esto borrará todos los datos que contiene.**
5. Haga clic en "¡Flash!"

#### **Método 2: Comando `dd` (Avanzado - Linux y macOS)**

Esta herramienta de línea de comandos es poderosa pero peligrosa si se usa incorrectamente. Puede borrar fácilmente el disco equivocado.

1. **Identifique su unidad USB:** Conecte su USB. Abra una terminal y ejecute `lsblk` (Linux) o `diskutil list` (macOS) para identificar el nombre del dispositivo (por ejemplo, `/dev/sdb`, `/dev/disk2`).
2. **Desmonte la unidad:** Asegúrese de que la unidad no esté montada. Utilice `umount /dev/sdX*` o `diskutil unmountDisk /dev/diskX`.
3. **Escribe la imagen:** Usa el comando `dd`. La sintaxis es:
    ```bash
    # ADVERTENCIA: Este comando es destructivo. Vuelva a verificar el nombre de su dispositivo.
    sudo dd if=/ruta/a/tu/tails.img of=/dev/sdX bs=4M status=progress
    ```
    *(Reemplace `/path/to/your/tails.img` con la ruta real y `/dev/sdX` con el nombre de su dispositivo USB)*

---

### **Sección 3: Primer arranque y configuración**

1. **Arranque desde USB:** Conecte el USB de Tails a la computadora que desea usar. Reinicie la computadora y acceda al menú de inicio (generalmente presionando F2, F10, F12 o Esc durante el inicio). Seleccione la unidad USB desde la que iniciar.
2. **Pantalla de bienvenida:** En la pantalla de bienvenida de Tails, puedes configurar el idioma y la distribución del teclado.
3. **Cree almacenamiento persistente cifrado (altamente recomendado):**
    * **Qué es:** Una sección cifrada en su unidad USB donde puede guardar archivos, marcadores del navegador, claves PGP y algunas configuraciones. Estos datos están protegidos por una contraseña y persisten entre reinicios.
    * **Cómo crear:** En la pantalla de bienvenida, antes de iniciar Tails, vaya a Aplicaciones -> Tails -> Configurar volumen persistente. Siga las instrucciones que aparecen en pantalla para crear el volumen y elija una frase de contraseña segura. Sólo harás esto una vez.
4. **Iniciando Tails:** Después de su primer inicio, se le pedirá que ingrese su frase de contraseña de Almacenamiento Persistente para desbloquearla cada vez que inicie Tails.

---

### **Sección 4: Seguridad operativa (OPSEC) dentro de Tails**

Usar Tails no es una solución mágica. Tu comportamiento importa.

* **No inicies sesión en cuentas personales:** No inicies sesión en tus cuentas personales de Google, Facebook u otras cuentas dentro de Tails. Esto vincularía su sesión anónima directamente con su identidad real.
* **Utilice el Navegador Tor:** Toda su navegación web debe realizarse a través del Navegador Tor incluido. No intente instalar otros navegadores.
* **Tenga cuidado con los documentos:** Los documentos pueden contener metadatos que pueden identificarlo (por ejemplo, nombre del autor, detalles de la computadora). Utilice la herramienta "Limpiador de metadatos" incluida en Tails antes de compartir cualquier documento.
* **No maximizar Windows:** El navegador Tor se abre en un tamaño estándar. Maximizarlo puede permitir que los sitios web tomen huellas digitales de la resolución de su pantalla, una forma potencial de anonimizarlo.

---

### **Sección 5: Solución de problemas comunes**

* **Tails no arranca:** El problema más común es el **Arranque seguro**. Esta es una característica de las computadoras modernas que evita que se carguen sistemas operativos no autorizados. Deberá ingresar la configuración BIOS/UEFI de su computadora (generalmente presionando F2 o Supr al inicio) y **deshabilitar el arranque seguro**.
* **No puedo conectarme a Tor:** Si estás en una red que censura Tor (como una biblioteca pública o un país restrictivo), es posible que necesites usar un **Puente Tor**. En la pantalla de bienvenida de Tails, puedes configurar Tor para que use un puente para conectarse.
* **Problemas de volumen persistentes:** Si olvida su frase de contraseña, sus datos desaparecerán para siempre. No hay recuperación. Escriba su frase de contraseña y guárdela en una ubicación segura y fuera de línea.

_Última actualización: 2026_
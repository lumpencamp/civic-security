# Cifrado de dispositivos: defensa criptográfica de datos en reposo

*Estado: Manual de criptografía de almacenamiento | Público: manejadores de fuentes y custodios de datos de alto riesgo*

Si se incauta un dispositivo físico mientras está apagado, Full Disk Encryption (FDE) es su única línea de defensa. Los algoritmos de cifrado rara vez se "rompen". El punto de falla casi siempre es una generación de claves débil (entropía de frase de contraseña) o una implementación defectuosa.

Esta guía detalla la implementación de FDE y las arquitecturas de cifrado denegables necesarias para resistir la extracción forense dirigida y la fuerza bruta acelerada por GPU.

---

## 1. Primitivas criptográficas y requisitos de entropía

No confíe en la configuración predeterminada sin comprender las matemáticas que protegen sus datos.

### Primitivas recomendadas
Al configurar el software de cifrado (como VeraCrypt o LUKS), se le pedirá que seleccione algoritmos.
* **Algoritmo de cifrado:** Utilice **AES-256**. Es el estándar global, altamente auditado y acelerado por hardware en CPU modernas (AES-NI), que proporciona velocidades rápidas de lectura/escritura sin comprometer la seguridad. El modo de cifrado debe ser **XTS** (modo de libro de códigos modificado basado en XEX con robo de texto cifrado), que está diseñado específicamente para resistir ataques de manipulación en el almacenamiento en bloque.
* **Algoritmo hash:** Utilice **SHA-512** o **Whirlpool**. Esto se utiliza para la derivación de claves (convertir su contraseña en la clave matemática real).

### Entropía de frase de contraseña contra fuerza bruta de GPU
Los adversarios forenses (T3/T4) utilizan grupos masivos de GPU para adivinar frases de contraseña a una velocidad de millones por segundo.
* **El mandato:** Su frase de contraseña debe poseer suficiente entropía (aleatoriedad) para hacer que la fuerza bruta sea matemáticamente imposible antes de la muerte por calor del universo.
* **Implementación:** Utilice una frase de contraseña de **Diceware** que conste de un mínimo de **6 palabras completamente aleatorias** (por ejemplo, `correct horse battery staple...`). Esto genera más de 77 bits de entropía, que es segura contra todas las capacidades de fuerza bruta convencionales conocidas. *No* utilices una contraseña compleja y memorizada que contenga sustituciones (por ejemplo, `P@ssw0rd!123`); descifrar diccionarios los derrota instantáneamente.

## 2. Implementaciones de cifrado de disco completo (FDE)

FDE cifra cada sector de su disco, incluido el espacio de intercambio y los archivos temporales, que a menudo contienen fragmentos de datos confidenciales no cifrados.

### Linux (LUKS)
* **Implementación:** La configuración de clave unificada de Linux (LUKS) es el estándar para las distribuciones de Linux. Durante la instalación de un sistema operativo Linux seguro (como Debian, Ubuntu o Qubes), se le pedirá que cifre la instalación.
* **Estándar de seguridad:** Asegúrese de que el instalador utilice LUKS2. LUKS2 utiliza la función de derivación de claves Argon2id (KDF). Argon2id está diseñado específicamente para tener memoria dura, lo que aumenta exponencialmente el costo financiero y el tiempo requerido para que un adversario aplique fuerza bruta a su frase de contraseña utilizando GPU o ASIC.

### Multiplataforma (VeraCrypt)
Para discos duros externos, memorias USB o para crear contenedores cifrados en Windows/macOS, utilice **VeraCrypt** (el sucesor auditado y de código abierto de TrueCrypt).

## 3. Cifrado negable: el volumen oculto de VeraCrypt

Si se enfrenta a coerción física o compulsión legal (una orden judicial que exige su frase de contraseña), el FDE estándar falla porque se ve obligado a entregar la clave. El cifrado denegable resuelve esto creando dos volúmenes en el mismo espacio: un volumen externo y un volumen oculto.

### La mecánica de la negación plausible
VeraCrypt crea un volumen exterior lleno de datos señuelo. Dentro del "espacio libre" aparentemente aleatorio de ese Volumen Exterior, construye un Volumen Oculto. No existe ninguna firma criptográfica que demuestre que existe el volumen oculto.

Si se ve obligado a entregar una frase de contraseña, usted proporciona la frase de contraseña para el volumen externo. El adversario descifra el disco, encuentra los datos del señuelo y no tiene pruebas matemáticas de que haya datos secundarios ocultos en su interior.

### Protocolo de configuración
1. Abra VeraCrypt y seleccione **Crear volumen**.
2. Elija **Crear un volumen VeraCrypt oculto**.
3. **Crea el volumen exterior:**
    * Establezca la frase de contraseña del Volumen Externo.
    * Móntelo y llénelo con datos de señuelo plausibles (por ejemplo, documentos fiscales, fotografías personales benignas). Los datos del señuelo *deben* parecer realistas.
4. **Crea el volumen oculto:**
    * VeraCrypt ahora le pedirá que cree el Volumen Oculto dentro del espacio libre del Volumen Externo.
    * Establezca una frase de contraseña Diceware completamente diferente y de alta seguridad para el Volumen Oculto.
5. **Restricción de comportamiento (CRÍTICA):** Cuando monta el volumen externo para agregar más datos señuelo, *debe* seleccionar "Proteger volumen oculto" en las opciones de montaje e ingresar la contraseña del volumen oculto. Si no hace esto, agregar datos al volumen externo sobrescribirá y destruirá permanentemente el volumen oculto.

_Última actualización: 2026_

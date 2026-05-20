# La guía completa para el cifrado de dispositivos

Esta guía cubre el "por qué" y el "cómo" del cifrado de dispositivos, desde el cifrado esencial de disco completo en sus dispositivos principales hasta el cifrado avanzado basado en archivos para sus datos más confidenciales.

---

## Parte 1: Cifrado de disco completo (FDE): la primera capa esencial

El cifrado de disco completo (FDE) cifra toda la unidad del sistema operativo.Es su primera línea de defensa no negociable contra el robo físico o la incautación.Cuando su dispositivo está apagado, todos sus datos están protegidos.

### **Windows: BitLocker**

1. **Compruebe su versión:** BitLocker está disponible en las ediciones Windows Pro, Enterprise y Education.
2. **Habilitar:** Vaya a Panel de control > Sistema y seguridad > Cifrado de unidad BitLocker.Haga clic en "Activar BitLocker" para su unidad C:.
3. **Guarde su clave de recuperación:** Esto es CRÍTICO.Se le pedirá que guarde una clave de recuperación.**Guarde esta clave en un lugar seguro y separado de la computadora.** Un administrador de contraseñas, una copia impresa en una caja fuerte o una cuenta segura de almacenamiento en la nube son buenas opciones.Perder esta clave y su contraseña significa perder sus datos para siempre.

### **macOS: FileVault**

1. **Habilitar:** Vaya a Configuración del sistema > Privacidad y seguridad > FileVault.Haga clic en "Activar..."
2. **Clave de recuperación:** Se te dará la opción de usar tu cuenta de iCloud o crear una clave de recuperación local.Para máxima seguridad, **elija crear una clave de recuperación local** y guárdela de forma segura sin conexión, al igual que la clave BitLocker.

### **iOS y Android**

Los teléfonos inteligentes modernos (iOS y Android) tienen el cifrado de dispositivo habilitado de forma predeterminada.Su protección principal es un **código de acceso alfanumérico seguro**.No confíe únicamente en la biometría (Face ID, huellas dactilares), ya que a veces pueden ser obligatorias por ley.Un código de acceso seguro es su mejor defensa.

---

## Parte 2: VeraCrypt: cifrado avanzado basado en contenedores

Para sus archivos más confidenciales, necesita una segunda capa de protección.VeraCrypt le permite crear un 'disco virtual' (un contenedor) cifrado y protegido con contraseña al que solo se puede acceder cuando lo monta.

### **Paso a paso: creación de un contenedor cifrado estándar**

1. **Instale VeraCrypt** desde `https://www.veracrypt.fr`.
2. **Crear volumen:** Inicie VeraCrypt, haga clic en `Crear volumen` y elija `Crear un contenedor de archivos cifrados` -> `Volumen estándar de VeraCrypt`.
3. **Seleccione la ubicación del archivo:** Elija una ubicación y asigne a su contenedor un nombre inofensivo (por ejemplo, `research.dat`).
4. **Opciones de cifrado:** Utilice los valores predeterminados: `AES` y `SHA-512`.
5. **Establecer tamaño de volumen:** Especifique el tamaño que necesita (por ejemplo, 10 GB).
6. **Establecer contraseña:** Utilice una frase de contraseña larga y única de más de 20 caracteres.**No hay recuperación si lo olvidas.**
7. **Formato:** Mueva el mouse aleatoriamente en la ventana para generar claves criptográficas seguras, luego haga clic en "Formatear".

### **Cómo utilizar su volumen VeraCrypt**

1. Abra VeraCrypt, seleccione una letra de unidad (por ejemplo, `G:`), seleccione su archivo contenedor y haga clic en `Montar`.
2. Ingrese su contraseña.La unidad aparecerá en su explorador de archivos.
3. Cuando termine, seleccione la unidad en VeraCrypt y haga clic en "Desmontar".La unidad desaparece y sus datos están seguros.

### **Avanzado: Negación plausible con un volumen oculto**

Un volumen oculto es un volumen secreto creado dentro del espacio libre de un volumen "externo" estándar, protegido por una contraseña diferente.Esto le permite revelar la contraseña externa bajo coerción sin exponer sus datos más confidenciales.

1. **Creación:** Al crear un volumen, seleccione "Volumen oculto de VeraCrypt".Primero deberá proporcionar la contraseña para el volumen externo y luego volver a realizar el proceso de creación para el volumen oculto con una **contraseña diferente**.
2. **OPSEC crítico:** Después de crear un volumen oculto, **nunca escriba archivos nuevos en el volumen externo**.Para protegerse contra esto, al montar el volumen exterior, utilice las "Opciones de montaje" para "Proteger el volumen oculto al montar el volumen exterior" proporcionando la contraseña del volumen oculto.

_Última actualización: 2026_
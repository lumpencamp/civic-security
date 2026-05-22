# Tails OS: operaciones amnésicas y seguridad de la memoria volátil

*Estado: Manual de contramedidas forenses | Público: denunciantes e investigadores de alto riesgo*

Tails (The Amnesic Incognito Live System) no es un conductor diario; es un entorno de despliegue táctico. Como ingeniero de sistemas Linux e investigador forense, debo enfatizar que su principal utilidad no es sólo el cifrado: es **amnesia**. No deja rastro en la máquina host.

Esta guía detalla las limitaciones operativas exactas y la auditoría de hardware necesarias para implementar Tails de forma segura.

---

## 1. Auditoría de la computadora host (seguridad BIOS/UEFI)

Tails se ejecuta completamente en RAM. Sin embargo, antes de que se cargue, el firmware de la computadora host controla el proceso de inicio. Debe asegurarse de que el hardware del host no comprometa el entorno en vivo.

### Endurecimiento de la secuencia de arranque
1. **Ingrese UEFI/BIOS:** Encienda la máquina host y presione repetidamente la tecla de configuración (generalmente F2, F12, Eliminar o Esc).
2. **Desactivar el arranque seguro:** Si bien está diseñado para detener el malware, el arranque seguro a menudo bloquea los USB de Linux activos. Desactívelo temporalmente para la operación.
3. **Desactivar el arranque rápido:** el arranque rápido omite las comprobaciones de inicialización del hardware y puede interferir con la detección de USB. Desactívelo.
4. **Contraseña de administrador:** Establezca una contraseña de administrador BIOS/UEFI. Esto evita que un adversario altere la secuencia de inicio para iniciar desde un USB malicioso antes de que se cargue Tails si la máquina se deja desatendida.

## 2. Ataques de arranque en frío y mitigación de RAM

Cuando apaga una computadora, los datos almacenados en la RAM (memoria de acceso aleatorio) no desaparecen instantáneamente. Los investigadores forenses pueden realizar un "ataque de arranque en frío" congelando los módulos de RAM (usando aire comprimido o nitrógeno líquido), transfiriéndolos a una máquina especializada y extrayendo las claves de cifrado antes de que se degraden.

### Protocolo de apagado
Tails está diseñado para sobrescribir la mayor parte de la RAM durante el proceso de apagado, pero debes activarlo correctamente.
* **No realice un reinicio completo:** Nunca mantenga presionado simplemente el botón de encendido. Esto deja la RAM intacta.
* **El Apagado Seguro:** Siempre apaga Tails a través del menú del sistema.
* **La extracción de emergencia:** Si se ve físicamente comprometido durante una operación, extraiga rápidamente la memoria USB de la computadora. Tails está diseñado para detectar instantáneamente la eliminación, activar un borrado de memoria de emergencia y apagarse.

## 3. Almacenamiento persistente LUKS: configuración y riesgos

Un sistema amnésico lo olvida todo. Si debe guardar archivos entre sesiones, debe configurar un volumen de almacenamiento persistente. Esto introduce un riesgo enorme: si se ve comprometido, el volumen contiene un historial inalterable de sus operaciones.

### Configuración segura
1. Abra **Aplicaciones** > **Tails** > **Almacenamiento persistente**.
2. Tails utiliza LUKS (Configuración de clave unificada de Linux) para el cifrado.
3. **Entropía de frase de contraseña:** El volumen debe estar protegido con una frase de contraseña de no menos de 6 palabras aleatorias (diceware).
4. *Advertencia forense:* El recuento de iteraciones LUKS predeterminado en versiones anteriores era susceptible a la fuerza bruta de la GPU. Asegúrese de estar ejecutando la última versión de Tails, que utiliza la derivación de claves Argon2id, lo que aumenta exponencialmente el tiempo necesario para los ataques de fuerza bruta.

## 4. Evitar la trampa de la "construcción de puentes"

La forma más común en que los activistas comprometen una sesión de Tails es a través de un cruce de comportamiento: creando un "puente" entre su identidad amnésica y su verdadera identidad.

### Restricciones operativas
* **Nunca te conectes al Wi-Fi doméstico:** Tails dirige todo el tráfico a través de Tor, pero tu ISP y el nodo de entrada de Tor seguirán viendo que se estableció una conexión Tor desde la dirección IP de tu hogar en un momento específico. Si estás subiendo documentos filtrados, un adversario puede correlacionar el tiempo de carga con el tiempo de conexión Tor en tu residencia. **Utilice siempre Wi-Fi público y que no sea de confianza para las operaciones de Tails.**
* **La regla de la sesión única:** Nunca inicies sesión en una cuenta personal (por ejemplo, tu Gmail real) y una cuenta operativa (por ejemplo, tu ProtonMail anónimo) durante la misma sesión de Tails. Incluso a través de Tor, los nodos de salida o las técnicas avanzadas de toma de huellas digitales pueden vincular las dos sesiones, quemando por completo su alias operativo.
* **Suplantación de hardware:** Tails falsifica automáticamente la dirección MAC de tu tarjeta de red para ocultar tu identidad de hardware del enrutador Wi-Fi público. **No desactive esta función** en la pantalla de bienvenida a menos que se requiera explícitamente para conectarse a un portal cautivo.

_Última actualización: 2026_

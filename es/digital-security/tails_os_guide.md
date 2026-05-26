# Guía de Tails OS: El Sistema Operativo Amnésico y Anónimo

*Estado: Nivel 3 | Audiencia: Usuarios de alto riesgo, periodistas y quienes manejan información extremadamente sensible*

Tails (The Amnesic Incognito Live System) es un sistema operativo en vivo que se arranca desde una unidad USB. Está diseñado específicamente para:
1. **No dejar rastro** en la computadora anfitriona en la que se utiliza
2. **Enrutar todo el tráfico de internet a través de Tor** por defecto
3. **Proporcionar un entorno seguro y consistente** independientemente de lo que esté instalado en la máquina anfitriona

Tails es utilizado por periodistas, informantes (whistleblowers), activistas y trabajadores de derechos humanos en todo el mundo. Fue utilizado por Glenn Greenwald y Laura Poitras para recibir y procesar los documentos de Snowden.

---

## 1. Cuándo usar Tails

Tails no es para el uso diario; es una herramienta especializada para situaciones específicas de alto riesgo:

**Use Tails cuando:**
- Maneje documentos extremadamente sensibles (archivos filtrados, estrategia legal, comunicaciones con fuentes)
- Se comunique con fuentes confidenciales desde un contexto periodístico u organizacional
- Trabaje en una computadora en la que no confía (biblioteca pública, máquina de otra persona, un dispositivo que puede estar comprometido)
- Acceda a materiales donde necesite asegurarse de que no quede ningún rastro forense
- Trabaje en un entorno donde sus dispositivos puedan ser monitoreados o incautados

**Tails es probablemente excesivo si:**
- Solo quiere Signal o una VPN
- Está realizando comunicaciones organizacionales de rutina
- La principal preocupación es su teléfono en lugar de su computadora portátil

---

## 2. Cómo funciona Tails

### 2.1 La arquitectura del sistema en vivo

Tails arranca completamente desde la unidad USB; el disco duro de la computadora anfitriona nunca se accede ni se escribe en él. Cuando apaga Tails:
- Toda la memoria RAM se sobrescribe (borra) automáticamente
- No quedan datos de sesión, archivos descargados ni claves de cifrado en la máquina anfitriona
- La unidad USB vuelve a su estado normal a menos que haya guardado explícitamente en el Almacenamiento Persistente cifrado

### 2.2 Integración con Tor

Cada conexión de red en Tails se enruta a través de Tor automáticamente. Si una aplicación intenta establecer una conexión directa a internet (evitando Tor), Tails la bloquea. Esto garantiza que incluso si una aplicación se comporta de manera inesperada, su dirección IP real no se filtre.

### 2.3 Herramientas de seguridad preinstaladas

Tails viene con:
- **Tor Browser:** Configurado para el máximo anonimato
- **Thunderbird con OpenPGP:** Para correo electrónico cifrado con periodistas y organizaciones
- **KeePassXC:** Gestor de contraseñas sin conexión
- **OnionShare:** Intercambio de archivos anónimo
- **Electrum:** Billetera de Bitcoin (para transacciones anónimas)
- **LibreOffice:** Suite ofimática completa para trabajar con documentos
- **Herramientas de cifrado LUKS:** Para crear volúmenes cifrados
- **MAT2:** Herramienta de anonimización de metadatos para documentos e imágenes
- **Kleopatra:** Interfaz gráfica para la gestión de claves PGP

---

## 3. Instalación de Tails

### 3.1 Requisitos

- Una unidad USB de **al menos 8 GB** (se recomiendan 16+ GB para el Almacenamiento Persistente)
- Una computadora que pueda arrancar desde USB
- Un segundo dispositivo (teléfono o computadora diferente) para seguir las instrucciones de instalación
- Alrededor de 30–60 minutos para la instalación

### 3.2 Obtención de Tails

**Solo descargue Tails desde el sitio web oficial: tails.boum.org**

Tails proporciona instrucciones de instalación muy claras con verificación de firma. Sígalas exactamente:
1. Vaya a tails.boum.org/install
2. Seleccione su sistema operativo para ver las instrucciones detalladas
3. Descargue la imagen de Tails
4. **Verifique la firma criptográfica:** Tails proporciona instrucciones de verificación paso a paso. Este paso confirma que su descarga no ha sido manipulada.

### 3.3 Métodos de instalación

**Desde macOS:**
1. Instale Etcher (balena.io/etcher) o use la línea de comandos
2. Inserte la unidad USB
3. Abra Etcher → Flash from file → Seleccione la imagen de Tails → Seleccione la unidad USB → Flash

**Desde Windows:**
1. Instale Rufus (rufus.ie) o Balena Etcher
2. Inserte la unidad USB
3. Abra la herramienta → Seleccione la imagen de Tails → Seleccione la unidad USB → Write (Escribir)

**Desde Linux:**
```bash
# Verifique el nombre del dispositivo USB primero: lsblk
sudo dd if=tails-amd64-X.XX.img of=/dev/sdb bs=16M oflag=direct status=progress
# Reemplace /dev/sdb con su unidad USB — COMPRUEBE DOS VECES antes de ejecutar
```

### 3.4 Arrancar Tails

1. Inserte el USB de Tails en la computadora
2. Reinicie la computadora
3. Acceda al menú de arranque (generalmente F12, F9 o la tecla Suprimir durante el inicio — varía según la computadora)
4. Seleccione la unidad USB desde la cual arrancar
5. Aparece la pantalla de bienvenida de Tails — haga clic en *Start Tails* (Iniciar Tails)

**Si la computadora no arranca desde el USB:**
- Deshabilite el Secure Boot en la configuración de BIOS/UEFI (Tails no está firmado para Secure Boot en versiones antiguas — consulte la documentación actual de Tails)
- Asegúrese de que el USB esté conectado directamente a un puerto USB 2.0 o 3.0 (no a un concentrador o hub)

---

## 4. Almacenamiento Persistente

Por defecto, Tails olvida todo cuando se apaga. El Almacenamiento Persistente le permite guardar tipos específicos de datos en la unidad USB entre sesiones.

### 4.1 Configuración del Almacenamiento Persistente

En Tails: *Applications → Tails → Configure persistent volume* (Aplicaciones → Tails → Configurar volumen persistente)

Establezca una **contraseña segura**: esto protege sus datos persistentes si la unidad USB es incautada.

### 4.2 Qué persistir

Configure solo lo que realmente necesita persistir. Cada categoría de datos persistentes es un posible objetivo forense si el USB es incautado.

**Razonable para persistir:**
- Marcadores del navegador (Tor Browser)
- Base de datos de contraseñas de KeePassXC
- Claves OpenPGP (para periodistas que necesitan comunicación continua con fuentes)
- Claves SSH (para acceso a servidores)
- Claves de cifrado LUKS para contenedores específicos

**NO persistir:**
- Historial de comunicaciones más allá de lo operativamente necesario
- Documentos sensibles con los que esté trabajando (almacénelos en una unidad cifrada separada y móntela cuando sea necesario)

### 4.3 Uso del Almacenamiento Persistente

Al iniciar Tails con un Almacenamiento Persistente existente:
1. En la pantalla de bienvenida, ingrese su contraseña del Almacenamiento Persistente
2. Tails carga su configuración guardada
3. Su base de datos de KeePassXC, marcadores del navegador, etc. están disponibles

---

## 5. Uso Operacional

### 5.1 Tor Browser en Tails

El Tor Browser en Tails está preconfigurado para el máximo anonimato:
- JavaScript deshabilitado por defecto en el nivel de seguridad "Safest" (El más seguro)
- No se recomienda la instalación de extensiones (altera la huella digital o *fingerprint*)
- Tamaño de ventana estandarizado

Para acceder a servicios .onion (SecureDrop, Proton Mail onion, etc.), escriba la dirección .onion directamente en la barra de direcciones.

### 5.2 Trabajo con documentos

**Recepción de documentos:**
- Descargue archivos a través de Tor Browser
- Antes de abrir, considere pasarlos por **MAT2** (anonimización de metadatos) o **Dangerzone** (si está disponible en su versión de Tails)
- Abra los documentos en LibreOffice de Tails: NO son automáticamente seguros solo por abrirlos en Tails
- Los documentos maliciosos (macros, JavaScript en PDF) aún pueden ejecutarse; use el Document Converter (Convertidor de documentos) de Tails o ábralos con precaución

**Exfiltración de documentos:**
- Después de limpiar los metadatos, comparta vía OnionShare o SecureDrop
- Guarde las versiones procesadas en el Almacenamiento Persistente o en una unidad externa cifrada

### 5.3 Correo electrónico en Tails (Thunderbird + OpenPGP)

Tails incluye Thunderbird configurado para correo electrónico seguro con cifrado OpenPGP:
1. Agregue su cuenta de correo electrónico (use Proton Mail o similar para cifrado de extremo a extremo)
2. Configure su clave PGP en la configuración OpenPGP de Thunderbird
3. Verifique las claves de sus contactos antes de enviar mensajes sensibles

**Para periodistas:** Configure Tails con su cuenta de Proton Mail y úsela exclusivamente para las comunicaciones con las fuentes. Esto proporciona: anonimización de Tor de su conexión + cifrado de Proton Mail en tránsito + su propio cifrado PGP del contenido.

---

## 6. Consideraciones de Seguridad

### 6.1 Lo que Tails no puede proteger

- **Implantes de hardware:** Si la computadora que está usando tiene un keylogger a nivel de hardware o un implante de red, Tails no puede detectarlo
- **Shoulder surfing (Mirar por encima del hombro):** Personas mirando su pantalla
- **Documentos maliciosos:** Un documento con exploits activos aún puede comprometer la sesión de Tails (use el Convertidor de documentos de Tails para archivos no confiables)
- **Rootkits de BIOS/UEFI:** Si el firmware de la computadora anfitriona está comprometido, Tails no puede detectarlo
- **Seguridad operativa débil:** Iniciar sesión en cuentas personales desde Tails, por ejemplo, lo desanonimiza de inmediato

### 6.2 Protección de la unidad USB de Tails

Su USB de Tails (especialmente con Almacenamiento Persistente) es sensible:
- Guárdelo por separado de sus dispositivos habituales
- No lo lleve en situaciones donde podría ser incautado
- Considere tener un USB de Tails "limpio" (sin almacenamiento persistente) para uso general y uno separado con almacenamiento persistente para proyectos sensibles en curso
- Si es incautado, el Almacenamiento Persistente está cifrado con su contraseña: no proporcione la contraseña

### 6.3 Computadoras confiables vs. no confiables

Tails está diseñado para ejecutarse en computadoras no confiables: no necesita confiar en la computadora desde la que está arrancando. Sin embargo:
- El hardware con keyloggers físicos o monitoreo a nivel de red no puede ser protegido por Tails
- Utilice el hardware más confiable disponible cuando los riesgos sean más altos
- Las bibliotecas y las computadoras públicas generalmente están bien para el uso de Tails de riesgo bajo a medio; use su propio hardware para el trabajo más sensible

---

## 7. Obtener ayuda con Tails

- **Documentación oficial:** tails.boum.org/doc (completa, clara, actualizada regularmente)
- **Mesa de ayuda de Tails:** tails.boum.org/support (el equipo de soporte responde en 1–3 días hábiles)
- **Línea de Ayuda de Seguridad Digital de Access Now:** accessnow.org/help — proporciona asistencia de seguridad directa a organizaciones de la sociedad civil y activistas a nivel mundial

---

*Esta guía no constituye asesoramiento legal. Tails es legal en la mayoría de las jurisdicciones, pero puede atraer atención en contextos de vigilancia. Conozca su entorno legal local.*

[← Volver al Índice](../index.md)

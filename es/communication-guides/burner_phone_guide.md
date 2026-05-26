# Guía de Teléfonos Desechables ("Burners"): Adquisición, Configuración y Retiro de Dispositivos Operativos

*Estado: Nivel 2 | Audiencia: Organizadores de Campo y Participantes de Alto Riesgo*

Un "burner" o teléfono desechable es un dispositivo temporal y no vinculado que se utiliza con fines operativos y luego se retira, limitando su exposición si el dispositivo es incautado, examinado forensemente o comprometido de forma remota. Esta guía cubre el ciclo de vida completo: adquisición, configuración, uso operativo y retiro.

> **¿Cuándo se necesita realmente un teléfono desechable?** Evalúe esto con honestidad utilizando su [Modelo de Amenazas](../digital-security/threat_modeling_guide.md). Para la mayoría de las situaciones T1–T2, un teléfono principal bastionado (hardened) es suficiente. Los teléfonos desechables son más valiosos en entornos de amenazas T2–T3 donde la incautación del dispositivo es un riesgo significativo, o cuando la naturaleza de la acción exige una separación de identidad que no se puede lograr en un dispositivo principal.

---

## 1. Adquisición: Creando un Dispositivo No Vinculado

Todo el valor de un teléfono desechable depende de que esté genuinamente desvinculado de su identidad. Cada paso en la adquisición puede crear un vínculo.

### 1.1 Elección del Dispositivo

**En general, se prefiere Android** sobre iPhone para los teléfonos desechables porque:
- Puede ser activado y utilizado sin crear ni vincular nunca una cuenta de Apple ID
- Mejor soporte para tiendas de aplicaciones alternativas (F-Droid) sin vinculación de cuentas
- GrapheneOS o CalyxOS se pueden instalar en dispositivos Pixel para una seguridad reforzada sin ninguna cuenta de Google

Los **teléfonos desechables iPhone** son posibles pero menos ideales:
- Muchas funciones requieren un Apple ID, lo que vincula el dispositivo a una cuenta
- Sin un Apple ID, la instalación de aplicaciones a través de la App Store es imposible
- AltStore o la carga lateral (sideloading) son soluciones alternativas pero añaden complejidad

**Opciones de dispositivos:**
- **Google Pixel (cualquier modelo):** La mejor opción para instalar GrapheneOS; ampliamente disponible en formato de prepago
- **Cualquier Android con bootloader desbloqueable:** Para CalyxOS
- **Teléfonos Android genéricos de prepago:** Más accesibles y económicos; con menor capacidad de refuerzo de seguridad, pero suficientes para la mayoría de los usos

**Dónde comprar:**
- Minoristas físicos: Walmart, Target, Best Buy, tiendas de a dólar, tiendas de conveniencia — todos venden teléfonos Android de prepago en efectivo
- NO haga pedidos en línea: las compras en línea vinculan las direcciones de envío, las tarjetas de pago y el historial de compras al dispositivo

### 1.2 La Operación de Adquisición

**Antes de salir:**
- Deje su teléfono principal en casa (o en una bolsa de Faraday). Los datos de ubicación de su teléfono principal lo situarán en el lugar de la compra, creando un vínculo entre usted y el dispositivo.
- Planifique la compra en una tienda que no frecuente habitualmente y a una hora en la que no se le pueda rastrear fácilmente en su rutina normal.
- Pague en efectivo. Las compras con tarjeta de crédito o débito crean un registro de transacción permanente que vincula su identidad a los números de serie del dispositivo y de la SIM.

**En la tienda:**
- Compre el teléfono y una tarjeta SIM de prepago al mismo tiempo, o preferiblemente en tiendas diferentes.
- No hable con el personal de ventas sobre su caso de uso; no proporcione su nombre ni información de contacto para ningún registro promocional.
- Utilice cajas de autopago (self-checkout) si están disponibles.

**Transporte:**
- No tome un viaje compartido (rideshare) ni conduzca su vehículo personal para la compra; ambos crean registros de ubicación. Camine o use el transporte público sin su teléfono personal.

### 1.3 Adquisición de la SIM

Una tarjeta SIM comprada en efectivo y sin verificación de identidad es el componente clave de las comunicaciones.

- Muchas SIMs de prepago no requieren identificación para su activación: las SIMs de prepago de Tracfone, Straight Talk o Mint Mobile compradas en tiendas minoristas son ejemplos
- Algunas SIMs sí requieren verificación de identidad; evítelas para uso operativo
- Alternativa: use el teléfono desechable exclusivamente con Wi-Fi (sin SIM) para comunicaciones basadas en Signal y Tor, aceptando que no tendrá capacidad de voz/SMS celular

**Leyes de registro de SIM:** Varios estados de EE. UU. y muchas jurisdicciones internacionales requieren identificación para registrar una SIM. Consulte las leyes locales. A nivel federal en EE. UU., no existe un requisito universal de registro de SIM para los operadores de prepago.

---

## 2. Configuración Inicial

Configure el teléfono desechable antes de conectarlo a cualquier red asociada con su identidad.

### 2.1 Configuración en el Primer Arranque

Durante la configuración inicial de Android:
- **Omita toda la configuración de la cuenta de Google.** No necesita una cuenta de Google. Cuando se le solicite, seleccione "Omitir" (Skip) o "Configurar más tarde" (Set up later).
- **Desactive todos los avisos opcionales de telemetría, análisis y personalización de funciones.**
- **No se conecte a la red Wi-Fi de su hogar.** Utilice una red Wi-Fi pública lejos de su residencia, o actívelo mediante datos celulares.
- **Activación de la SIM:** Si activa a través del sitio web del operador, utilice un navegador a través de Tor o una VPN en un dispositivo separado para acceder a la URL de activación; no utilice sus dispositivos personales.

### 2.2 Instalación de Software

**Sin una cuenta de Google**, instale aplicaciones a través de:
- **F-Droid:** Una tienda de aplicaciones de código abierto para Android que contiene aplicaciones gratuitas y de código abierto que respetan la privacidad. No se requiere cuenta. Instale F-Droid descargando el APK desde f-droid.org.
- **Descarga directa de APK:** Para las aplicaciones que no están en F-Droid, descargue los APKs directamente desde los sitios web oficiales de los proyectos. Verifique los sumas de comprobación (checksums) siempre que sea posible.

**Aplicaciones esenciales para un teléfono desechable operativo:**
| Aplicación | Propósito | Fuente |
|-----|---------|--------|
| Signal | Comunicaciones seguras | signal.org/android/apk o F-Droid |
| Orbot | Tor para Android | guardianproject.info o F-Droid |
| Briar | Mensajería cifrada peer-to-peer; funciona a través de Tor y Bluetooth | F-Droid |
| OsmAnd | Mapas sin conexión (no se necesita cuenta de Google Maps) | F-Droid |
| Aegis Authenticator | 2FA TOTP | F-Droid |

**NO instale:**
- Aplicaciones de redes sociales (todas recopilan identificadores de dispositivos)
- Aplicaciones de correo electrónico comercial
- Cualquier aplicación que requiera los Servicios de Google Play o una cuenta de Google, a menos que haya configurado deliberadamente una cuenta de Google anónima a través de Tor solo para el teléfono desechable

### 2.3 Configuración de Signal en un Teléfono Desechable

El registro de Signal requiere un número de teléfono. Opciones:

**Opción A: Registrarse con el número de la SIM del teléfono desechable**
- Es lo más directo
- El número de la SIM es el identificador; si la SIM no está vinculada a su identidad, el registro de Signal tampoco lo está
- Limitaciones: si retira la SIM, esa cuenta de Signal se retira con ella

**Opción B: Registrarse con un número VOIP**
- Use JMP.chat (proporciona un número de teléfono XMPP real, accesible a través de Tor)
- Registre el número de JMP en jmp.chat a través del Navegador Tor (Tor Browser)
- Este número se puede mantener incluso después de que el teléfono desechable físico sea retirado

**Después del registro:**
- Habilite el Bloqueo de Registro de inmediato (Ajustes → Cuenta → Bloqueo de Registro)
- Establezca los mensajes efímeros (disappearing messages) por defecto para todos los chats
- Desactive las confirmaciones de lectura, las vistas previas de enlaces y los indicadores de escritura (consulte la [Guía de Signal](../digital-security/signal_guide.md))

### 2.4 Bastionado (Hardening) del Dispositivo

- **Bloqueo de pantalla:** Frase de contraseña alfanumérica, no PIN ni biometría
- **Bloqueo automático:** 1 minuto o menos
- **Cifrado:** Verifique que el cifrado de disco completo esté habilitado (Android moderno: habilitado por defecto)
- **Desactivar:** Bluetooth, NFC, servicios de ubicación; enciéndalos solo cuando los necesite activamente
- **Wi-Fi:** No configure el dispositivo para que se conecte automáticamente a ninguna red, excepto a una red deliberada y controlada
- **MAC Aleatoria:** Verifique que la aleatorización de la dirección MAC esté habilitada para las conexiones Wi-Fi (Ajustes → Red → Wi-Fi → [Red] → Privacidad → MAC Aleatoria)
- **Google Play:** Si la Play Store está presente (sin cuenta), desactívela. Vaya a Ajustes → Aplicaciones → Google Play Store → Desactivar.
- **Desactivar Servicios de Google:** La mayoría de los teléfonos Android incluyen los Servicios de Google Play, que recopilan telemetría de forma agresiva. Para una seguridad máxima, use un dispositivo con GrapheneOS (que se distribuye sin los Servicios de Google Play) o desactive los Servicios de Google Play y las aplicaciones relacionadas.

---

## 3. Uso Operativo

### 3.1 La Regla de Separación Geográfica

El poder del teléfono desechable proviene de la separación geográfica y conductual de su identidad principal:

- **Nunca lleve el teléfono desechable a lugares asociados con su identidad principal:** hogar, lugar de trabajo, gimnasio habitual, casa familiar
- **Nunca use el teléfono desechable en redes asociadas con su identidad:** Wi-Fi del hogar, Wi-Fi del lugar de trabajo, redes que usa frecuentemente en su teléfono principal
- **Nunca encienda el teléfono desechable y su teléfono principal en el mismo lugar simultáneamente:** este es el error más común. Si ambos dispositivos están en el mismo lugar, pueden correlacionarse a través de datos de torres celulares y registros de Wi-Fi.
- **El protocolo de la bolsa de Faraday:** Cuando transite entre lugares con ambos dispositivos, mantenga uno en una bolsa de Faraday (encendido en la bolsa de Faraday = sigue siendo seguro; apagado = aún más seguro)

### 3.2 Comunicaciones Operativas

- Todas las comunicaciones operativas se realizan a través de la cuenta de Signal del teléfono desechable
- El número del teléfono desechable se comparte solo con contactos operativos; los contactos personales no lo tienen
- No use el teléfono desechable para ninguna comunicación personal, ni siquiera "solo una vez"
- Si recibe una llamada en el teléfono desechable de un número desconocido, no conteste; evalúe a través de Signal si un contacto está tratando de comunicarse con usted

### 3.3 Fotografía y Documentación

Si usa el teléfono desechable para documentar una acción:
- Habilite el modo avión antes de tomar fotos (evita la carga automática a cualquier servicio en la nube)
- Elimine los datos EXIF antes de compartir cualquier foto (ExifTool o Scrambled EXIF)
- Transfiera fotos a su sistema operativo seguro, no a dispositivos o cuentas personales

---

## 4. Retiro: Decomisando un Teléfono Desechable de Forma Segura

Un teléfono desechable que ha cumplido su propósito debe retirarse limpiamente. Un teléfono desechable retirado incorrectamente que luego se encuentra y se analiza forensemente puede exponer operaciones pasadas.

### 4.1 Retiro Digital

1. **Elimine todas las cuentas** vinculadas a este dispositivo (Cuenta de Signal: Ajustes → Cuenta → Eliminar Cuenta)
2. **Elimine todos los datos:** Mensajes, fotos, contactos, datos de aplicaciones
3. **Restablecimiento de fábrica:** Ajustes → Administración general → Restablecer → Restablecer valores predeterminados
4. **Verifique el restablecimiento:** Después de restablecer, el dispositivo debe mostrar la pantalla de configuración inicial como si fuera nuevo

**Nota sobre las limitaciones del restablecimiento de fábrica:** Un restablecimiento de fábrica elimina el acceso lógico a los datos, pero puede que no sobrescriba completamente el almacenamiento físico: las herramientas forenses a veces pueden recuperar datos de dispositivos Android restablecidos. Para obtener la máxima seguridad, use la opción "Sobrescribir datos" si está disponible, o llene el almacenamiento manualmente antes de restablecer (paso 4.2).

### 4.2 Retiro Físico

Después del retiro digital, decida según su modelo de amenazas:

**Retiro de bajo riesgo:** Restablecimiento de fábrica + extraer la SIM → donar, vender o simplemente dejar de usar el dispositivo. Los datos se eliminan lógicamente; el análisis forense físico es poco probable en la mayoría de los escenarios T1–T2.

**Retiro de alto riesgo:** Restablecimiento de fábrica → extracción de la SIM → destrucción física del dispositivo. Romper el chip de almacenamiento evita la recuperación forense. Métodos:
- Desmonte y destruya físicamente el chip de memoria (requiere herramientas)
- Desmagnetización (desmagnetizadores: solo para almacenamiento magnético, no aplicable a flash)
- Destrucción: perfore el teléfono con un taladro, particularmente el área del chip de memoria

**Retiro de la SIM:** Extraiga la SIM. Destrúyala físicamente (corte el chip con tijeras) si el nivel de amenaza lo justifica. Deseche la SIM y el dispositivo por separado.

### 4.3 Manejo del Dispositivo Físico Posterior al Retiro

- No venda un teléfono desechable en una tienda que requiera identificación
- No lo deseche en la basura de su casa si la evidencia física del mismo pudiera vincularlo con usted
- Los contenedores de reciclaje de productos electrónicos en las tiendas aceptan dispositivos anónimos

---

## 5. Errores Comunes y Cómo Evitarlos

| Error | Consecuencia | Prevención |
|---------|------------|------------|
| Llevar el teléfono desechable y el teléfono principal a la misma ubicación | Los datos de las torres celulares los vinculan | Estricta separación física; poner un dispositivo en bolsa de Faraday |
| Usar el Wi-Fi del hogar en el teléfono desechable | La dirección IP vincula el teléfono desechable a su dirección | Nunca conectarse a ninguna red vinculada a su identidad |
| Comprar con tarjeta de crédito | El registro de la transacción lo vincula al número de serie del dispositivo | Siempre en efectivo |
| Comprar en línea | El registro de envío vincula su dirección al dispositivo | Siempre en tienda física |
| Iniciar sesión en una cuenta personal "solo una vez" | Vincula permanentemente su identidad al dispositivo | Nunca. Ni siquiera una vez. |
| Dejar la SIM en el teléfono desechable después del retiro | Los registros de la SIM + los registros del dispositivo se pueden cruzar | Extraer y destruir la SIM al retirarlo |
| Llevar el teléfono desechable a una protesta en el bolsillo junto con el teléfono principal | Ambos aparecen en los registros de torres celulares en la misma acción | Lleve solo un dispositivo a una acción; ponga el otro en una bolsa de Faraday o déjelo en casa |

---

*Esta guía no constituye asesoramiento legal. Las leyes varían según la jurisdicción.*

[← Volver al Índice](../index.md)

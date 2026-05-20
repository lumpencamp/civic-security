# Lucha contra la vigilancia estatal: estrategia de defensa institucional

*Estado: Directiva de Nivel 3 | Público: miembros de la junta directiva, organizadores principales, equipos legales*

La defensa contra la vigilancia a nivel estatal (por ejemplo, la recopilación de metadatos al estilo PRISM de la NSA, los centros de fusión federales, la recopilación masiva de datos por parte de intermediarios) requiere más que aplicaciones de chat cifradas. Requiere incorporar resistencia criptográfica y firewalls legales directamente en la infraestructura de su organización.

Cuando te enfrentas a un adversario con recursos infinitos, tu objetivo principal es **privarlo de metadatos** y **convertir el proceso legal en un arma** para ganar tiempo.

---

## 1. Arquitectura de conocimiento cero (ZKA)

La vigilancia estatal se basa en obligar a los proveedores de servicios a entregar sus datos. Si el proveedor no posee las claves para descifrar sus datos, la citación es inútil.

* **Restricción operativa:** La organización no utilizará ningún servicio digital que contenga las claves de descifrado de sus datos.
* **Implementación:**
    * **Almacenamiento en la nube:** Abandone Google Workspace y Microsoft 365 inmediatamente. Transfiera todos los documentos organizativos a proveedores de cifrado de extremo a extremo (E2EE) (por ejemplo, Tresorit, Proton Drive o CryptPad autohospedado).
    * **Trabajo colaborativo:** Utilice CryptPad para editar documentos en vivo. Los operadores del servidor no pueden leer las pulsaciones de teclas.
    * **Comunicaciones:** Transfiera todas las comunicaciones internas a un servidor Matrix autohospedado (con E2EE estrictamente aplicado) o SimpleX para eliminar directorios de metadatos centrales.

## 2. Políticas de Datos Efímeros (PDE)

Los datos que no existen no pueden confiscarse, citarse ni filtrarse. Conservar las comunicaciones históricas es una amenaza existencial para las organizaciones cívicas.

* **Restricción operativa:** Todas las comunicaciones operativas y los registros no esenciales están sujetos a una destrucción estricta y automatizada.
* **Implementación:**
    * **Mensajes temporales:** Los chats grupales de Signal y Matrix deben tener un temporizador de vencimiento codificado (máximo 7 días). Sin excepciones por "conveniencia".
    * **La purga de 30 días:** Los registros financieros necesarios para el cumplimiento tributario se compartimentan y cifran fuera de línea. Todos los demás documentos logísticos, de planificación o de mapeo deben borrarse de forma segura (usando herramientas como BleachBit o MAT2) dentro de los 30 días posteriores a la conclusión de la operación.
    * **Sin listas centralizadas:** La organización no mantendrá una lista digital maestra de voluntarios, miembros o donantes. Las listas se segmentan y se mantienen en almacenamiento físico cifrado y aislado (por ejemplo, volumen persistente de Tails OS).

## 3. Verificación estructural criptográfica

La infiltración de informantes estatales es una certeza estadística durante un período de tiempo suficientemente largo. Su red debe asumir que los nodos internos están comprometidos.

* **Restricción operativa:** La verificación de identidad debe ser criptográfica, no solo visual o conductual.
* **Implementación:**
    * **Fiestas de firma de claves:** Los miembros principales deben reunirse físicamente para verificar y firmar las claves PGP de los demás o verificar los números de seguridad de Matrix/Signal mediante el escaneo de códigos QR físicos.
    * **Verificación fuera de banda:** Si se emite una directiva operativa de forma digital, se debe verificar a través de un canal secundario fuera de banda (por ejemplo, verificar un mensaje de Matrix a través de una entrega física preestablecida o una llamada VoIP cifrada) antes de la ejecución.

## 4. Cortafuegos legales y estructuración de estatutos

Su estatuto organizacional debe actuar como un escudo legal, impidiendo legalmente que cualquier miembro cumpla unilateralmente con demandas sin orden judicial.

* **Restricción operativa:** Ningún miembro individual posee la autoridad o la capacidad técnica para descifrar toda la bóveda de datos de la organización.
* **Implementación:**
    * **Gestión de claves distribuidas (Shamir Secret Sharing):** Utilice el intercambio de secretos criptográficos para dividir la clave de descifrado maestra para los archivos sin conexión de la organización entre cinco miembros principales. Para acceder a los datos es necesario que tres de los cinco miembros combinen sus claves. Esto evita que el Estado obligue en secreto a un solo individuo a través de una Carta de Seguridad Nacional (NSL) o una orden de silencio.
    * **El canario de orden judicial:** La organización debe publicar mensualmente un "Warrant Canary" (una declaración firmada criptográficamente afirmando que la organización *no* ha recibido ninguna citación secreta o NSL). Si el canario no se actualiza según lo programado, todos los miembros deben asumir inmediatamente que la organización está comprometida y ejecutar el Protocolo de conocimiento cero.
    * **Representación legal contratada:** Contrate a un abogado de libertades civiles (por ejemplo, EFF o un equivalente regional). La orden permanente para todos los miembros con respecto a cualquier interacción con la inteligencia federal o las fuerzas del orden es: *"No doy mi consentimiento para registros, no responderé preguntas e invoco mi derecho a consultar a mi abogado".*

_Última actualización: 2026_

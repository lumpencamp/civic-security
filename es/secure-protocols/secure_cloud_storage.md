# Almacenamiento Seguro en la Nube y Colaboración Organizacional

> [!CAUTION]
> **AVISO DE SEGURIDAD OPERATIVA Y LEGAL**
> El almacenamiento en la nube cifrado de extremo a extremo (E2EE) protege los documentos en tránsito y en reposo en servidores remotos. Sin embargo, depende completamente de la seguridad de las credenciales de su cuenta local y contraseñas.
> - **Siempre** obligue a usar contraseñas maestras fuertes y aleatorias y 2FA seguro (llaves de hardware/TOTP) en sus cuentas de almacenamiento en la nube.
> - **Nunca** suba claves de cifrado en texto plano o frases de recuperación a ningún servicio en la nube.
> - **Siempre** verifique que los nodos colaboradores también ejecuten entornos locales seguros y reforzados.

Los grupos de activistas, periodistas y equipos de apoyo legal necesitan compartir documentos, hojas de cálculo y archivos operativos. Sin embargo, confiar en los servicios de consumo convencionales crea vulnerabilidades de seguridad masivas, a menudo invisibles.

---

## 1. La Vulnerabilidad de Google Drive y Dropbox

Servicios como Google Workspace, Google Drive, Microsoft OneDrive y Dropbox tienen las claves de cifrado de sus datos. Ellos cifran los datos "en reposo" en sus servidores, pero *ellos* tienen la clave, lo que significa:
1. **Escaneo Automatizado:** Escanean activamente sus archivos en busca de violaciones de contenido, malware o infracción de derechos de autor.
2. **La Amenaza de Citación:** **Entregarán sus archivos a las fuerzas del orden** si reciben una citación o una orden judicial, y a menudo, las órdenes mordaza (gag orders) evitan que le notifiquen que sus datos han sido comprometidos.
3. **Amenaza Interna:** Históricamente, empleados deshonestos en estas empresas han abusado de herramientas internas para acceder a los datos de los usuarios.

Para documentos de planificación sensibles, listas de miembros, registros financieros o estrategias legales, estas plataformas son fundamentalmente inseguras para niveles de amenaza T2+.

---

## 2. La Solución: Arquitectura de Cifrado de Extremo a Extremo (E2EE)

El almacenamiento E2EE cambia fundamentalmente el modelo de confianza. Los archivos se cifran localmente en su dispositivo (del lado del cliente) *antes* de subirse a la nube.

La empresa que aloja los archivos nunca posee las claves de descifrado. Si las fuerzas del orden emiten una citación al servidor, o si un hacker vulnera la base de datos de la empresa, solo adquieren texto cifrado ilegible.

---

## 3. Proveedores Recomendados: Análisis Detallado

### Proton Drive (Altamente Recomendado para Organizadores)
Operado desde Ginebra bajo estrictas leyes de privacidad suizas (FADP), Proton Drive proporciona cifrado de archivos de conocimiento cero (zero-knowledge), uso compartido seguro de archivos y edición de documentos colaborativa sólida y E2EE.
* **Arquitectura de Cifrado:** Utiliza AES-256 del lado del cliente de código abierto y ECC (Criptografía de Curva Elíptica). Incluso los nombres de archivo y las estructuras de carpetas están cifrados.
* **Colaboración:** Cuenta con "Proton Docs", una alternativa segura a Google Docs que permite la edición de texto enriquecido colaborativa en tiempo real.
* **Jurisdicción:** Suiza. No está sujeto a acuerdos de vigilancia masiva de EE. UU./UE. Las citaciones requieren una orden judicial suiza, e incluso entonces, Proton solo puede entregar texto cifrado.
* **Pros:** Integración perfecta con ProtonMail, aplicaciones móviles muy pulidas, excelentes controles para compartir (enlaces protegidos con contraseña con fechas de vencimiento).
* **Contras:** Los niveles de pago pueden ser costosos para equipos grandes. Actualmente carece de un editor de hojas de cálculo nativo.

### CryptPad (Altamente Recomendado para Colaboración en Tiempo Real)
CryptPad es una alternativa totalmente E2EE y de conocimiento cero a Google Workspace, construida por un equipo de desarrollo francés.
* **Características:** Ofrece documentos de texto enriquecido colaborativos, hojas de cálculo (compatibles con Excel), tableros Kanban, pizarras virtuales, formularios/encuestas y diapositivas de presentación.
* **Arquitectura:** Todo en el navegador se cifra antes de tocar el servidor. Los administradores del servidor no pueden leer sus documentos.
* **Implementación:** Puede usar la instancia pública principal (CryptPad.fr), o una organización con conocimientos técnicos puede alojar su propia instancia (self-host) en un servidor privado para una soberanía total.
* **Pros:** Conjunto de características increíble para equipos. No se requiere cuenta para participar en un documento compartido.
* **Contras:** La interfaz de usuario es menos pulida que la de Google. Debido a que es de conocimiento cero, si pierde su contraseña, los administradores no pueden recuperar de ninguna manera su cuenta o datos.

### Filen (Mejor Alternativa Económica/de Almacenamiento Masivo)
Un proveedor de almacenamiento en la nube de conocimiento cero con sede en Alemania que utiliza un estricto cifrado AES-256 del lado del cliente.
* **Pros:** Precios altamente competitivos (incluyendo planes de por vida), clientes de sincronización estables y aplicaciones de escritorio y móviles completas de código abierto.
* **Contras:** Estrictamente almacenamiento y sincronización de archivos; no hay funciones de colaboración de documentos en tiempo real como Proton Docs o CryptPad.

### Cryptomator (La Alternativa DIY Avanzada)
Si *debe* usar Google Drive o Dropbox (tal vez porque una organización afiliada lo exija o ya haya pagado por un terabyte de almacenamiento), puede usar Cryptomator.
* **Cómo Funciona:** Es un programa gratuito y de código abierto que crea una bóveda cifrada localmente en su computadora. Coloca sus archivos en la bóveda, Cryptomator los cifra localmente y *luego* permite que Google Drive/Dropbox sincronice la bóveda cifrada a la nube.
* **Pros:** Gratis. Le permite asegurar entornos en la nube hostiles.
* **Contras:** Torpe para equipos. Los conflictos de sincronización pueden corromper las bóvedas si varias personas editan simultáneamente.

---

## 4. Guía de Migración Organizacional (De Google a E2EE)

La migración de una organización fuera de Google Workspace requiere planificación para evitar la pérdida de datos.

1. **Exportación de Datos:** Use Google Takeout para exportar los datos de Drive de su organización. Elija formatos estándar (.docx, .xlsx, .pdf).
2. **Establecer la Nueva Base:** Cree la cuenta organizativa en Proton Drive o CryptPad.
3. **Fase de Cifrado Local:** Descargue los datos exportados en un disco duro local cifrado de forma segura (usando VeraCrypt o LUKS).
4. **Carga y Organización:** Suba los archivos al nuevo proveedor E2EE. Restablezca su jerarquía de carpetas.
5. **Control de Acceso:** Utilice control de acceso basado en roles. No comparta toda la carpeta raíz con todos los miembros. Cree carpetas específicas (por ejemplo, "Logística", "Medios", "Legal") y compártalas mediante enlaces seguros solo a los subequipos necesarios.
6. **Capacitación del Equipo (CRÍTICO):** Debe capacitar a su equipo en la gestión de contraseñas. Debido a que estos son sistemas de conocimiento cero, **no hay un botón de restablecimiento de "Olvidé mi contraseña"** que recupere los datos. Obligue el uso de KeePassDX o Bitwarden para todos los miembros.

---

## 5. Control de Acceso Seguro y Uso Compartido

Al compartir archivos externamente (con periodistas, organizaciones aliadas o asesores legales):

* **Nunca** use "Cualquier persona con el enlace puede ver".
* **Siempre** establezca una **Fecha de vencimiento** en el enlace (por ejemplo, 48 horas).
* **Siempre** establezca una **Contraseña** en el enlace.
* **Entrega Fuera de Banda (Out-of-Band):** Envíe el enlace a través de un canal (por ejemplo, ProtonMail) y la contraseña a través de un canal completamente diferente y fuera de banda (por ejemplo, Signal). Si un adversario intercepta un canal, aún no puede acceder a los datos.

---

## 6. Matriz de Comparación de Características

| Característica | Proton Drive | CryptPad | Filen | Cryptomator | Google Drive (Base) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Conocimiento Cero E2EE** | ✅ Sí | ✅ Sí | ✅ Sí | ✅ Sí (Local) | ❌ No |
| **Colab. Documentos en Tiempo Real** | ✅ Sí (Docs) | ✅ Sí (Docs/Sheets) | ❌ No | ❌ No | ✅ Sí |
| **Opción de Autoalojamiento** | ❌ No | ✅ Sí | ❌ No | N/A | ❌ No |
| **Jurisdicción** | Suiza | Francia | Alemania | Alemania (App) | EE. UU. |
| **Cliente de Código Abierto** | ✅ Sí | ✅ Sí | ✅ Sí | ✅ Sí | ❌ No |

---

## 7. La Estrategia de Copia de Seguridad 3-2-1

El almacenamiento en la nube es sincronización, no una verdadera copia de seguridad. Si un actor malicioso obtiene acceso al dispositivo de un miembro del equipo y elimina los archivos en la carpeta sincronizada de Proton Drive, esas eliminaciones se sincronizarán en la nube, destruyendo los datos a nivel mundial.

Implemente una estrategia 3-2-1 para los datos organizacionales críticos:
* **3 Copias:** Una copia activa en la nube E2EE, una unidad física local cifrada, una unidad física cifrada fuera del sitio.
* **2 Formatos:** Almacenamiento en la nube y almacenamiento en frío físico (unidades flash/HDD).
* **1 Fuera del sitio:** Un miembro del equipo de confianza que posea físicamente una unidad flash cifrada (actualizada semanalmente) en una ubicación geográfica separada.

[← Volver al Índice](../index.md)
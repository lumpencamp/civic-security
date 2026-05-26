# Navegador Tor: Navegación Anónima y Servicios Onion

*Estado: Nivel 2 | Audiencia: Organizadores que manejan investigación sensible, periodistas y usuarios de alto riesgo*

Tor (The Onion Router) es una red de anonimato gratuita y de código abierto que enruta su tráfico de Internet a través de tres nodos (relés) operados por voluntarios, cifrándolo en cada salto. Originalmente fue desarrollado por el Laboratorio de Investigación Naval de EE. UU. y ahora es mantenido por Tor Project, una organización sin fines de lucro. Tor es utilizado por periodistas, activistas, trabajadores de derechos humanos, denunciantes, fuerzas del orden y millones de personas comunes en todo el mundo.

> **Tor no es una VPN.** Una VPN reemplaza a su ISP como la entidad que puede ver su tráfico y su dirección IP real. Tor proporciona un anonimato mucho más fuerte al garantizar que ningún nodo único sepa a la vez quién es usted y a qué está accediendo. Ningún nodo en la red Tor conoce el panorama completo.

---

## 1. Cómo Funciona Tor

### 1.1 El Circuito de Tres Saltos

Cuando usa Tor, su tráfico es:

1. **Cifrado en tres capas** en su dispositivo
2. **Enviado al nodo Guardia/Entrada (Guard/Entry):** Conoce su dirección IP real pero no su destino
3. **Reenviado al nodo Medio (Middle):** No conoce ni su IP ni su destino
4. **Reenviado al nodo de Salida (Exit):** Conoce su destino pero no su dirección IP real
5. **Enviado al sitio web de destino**

Ningún nodo tiene el panorama completo. Un adversario necesitaría controlar simultáneamente su nodo de entrada y observar su tráfico de destino para desanonimizarlo — este es el "ataque de correlación de tráfico" y representa la principal limitación práctica de Tor.

### 1.2 Contra Qué Protege Tor

- **Su ISP** viendo qué sitios web visita
- **Sitios web** viendo su dirección IP real y ubicación
- **Observadores a nivel de red** (en Wi-Fi público, la red de su empleador) viendo sus destinos
- **Vigilancia de nivel T1–T2** que depende de la identificación basada en IP

### 1.3 Contra Qué NO Protege Tor

- **Correlación de tráfico por un adversario global:** La NSA y agencias similares tienen la capacidad de observar el tráfico en los nodos de entrada y salida simultáneamente y realizar correlaciones estadísticas para desanonimizar a los usuarios. Esta es la limitación práctica más grave.
- **Malware en su dispositivo:** Si su dispositivo está comprometido, Tor no lo protege
- **Desanonimización a través de su comportamiento:** Iniciar sesión en su Gmail personal en el Navegador Tor desanonimiza inmediatamente su sesión
- **Intercepción del nodo de salida del tráfico no cifrado:** El nodo de salida puede ver el tráfico HTTP no cifrado. Utilice siempre HTTPS cuando utilice Tor.
- **Huella digital del navegador (browser fingerprinting) si modifica el Navegador Tor:** El Navegador Tor está diseñado específicamente para hacer que todos los usuarios se vean idénticos. Agregar extensiones, cambiar configuraciones o habilitar JavaScript en sitios sensibles reduce esta protección.

---

## 2. Instalación y Uso del Navegador Tor

### 2.1 Descarga y Verificación

**Crítico:** Solo descargue el Navegador Tor (Tor Browser) desde el sitio web oficial del Tor Project: **torproject.org**

Verifique la firma de descarga:
1. Descargue el paquete del navegador y el archivo de firma .asc correspondiente desde torproject.org/download
2. Importe la clave de firma de Tor Project: `gpg --keyserver keys.openpgp.org --search-keys "Tor Browser Developers"`
3. Verifique: `gpg --verify tor-browser-linux64-XX_en-US.tar.xz.asc tor-browser-linux64-XX_en-US.tar.xz`
4. La salida debe mostrar "Good signature from Tor Browser Developers" (Firma correcta de Tor Browser Developers)

Si no puede verificar las firmas, considere usar un método de descarga alternativo, como el Navegador Tor en Tails OS (donde está preinstalado y preverificado).

### 2.2 Configuración del Nivel de Seguridad

El Navegador Tor incluye una configuración de "Nivel de Seguridad" que controla la cantidad de JavaScript y contenido activo que se permite. Más alto = más seguro pero potencialmente rompe algunos sitios web.

*En Navegador Tor → Icono de Escudo (arriba a la derecha) → Ajustes de Seguridad Avanzados*

| Nivel | JavaScript | Caso de Uso |
|-------|-----------|----------|
| Estándar | Activado | Navegación general donde el anonimato es un objetivo pero no es crítico |
| Más Seguro (Safer) | Parcialmente desactivado | Investigación, periodismo, comunicaciones activistas |
| El Más Seguro (Safest) | Desactivado | Acceso a documentos sensibles, denuncias de irregularidades (whistleblowing), investigación de alto riesgo |

**Recomendación para uso de alto riesgo:** Establézcalo en El Más Seguro (Safest). Si un sitio requiere JavaScript, evalúe si necesita acceder a él y si existe una alternativa más segura.

### 2.3 Reglas Operativas Críticas

**Nunca haga lo siguiente en el Navegador Tor:**
- Iniciar sesión en cuentas personales (Google, Facebook, su correo electrónico real) — esto desanonimiza inmediatamente su sesión
- Abrir documentos descargados a través de Tor en otras aplicaciones (especialmente archivos PDF y .docx) — estos pueden realizar solicitudes de red que eluden Tor
- Usar BitTorrent a través de Tor — anula las protecciones de Tor y daña la red para otros
- Instalar extensiones de navegador adicionales — cambian su huella digital y pueden introducir vulnerabilidades
- Cambiar el tamaño de la ventana del navegador — el tamaño de la ventana es parte de la huella digital del navegador; el Navegador Tor se abre en un tamaño estándar por esta razón

**Siempre haga lo siguiente:**
- Use HTTPS — busque el ícono del candado. El Navegador Tor incluye HTTPS Everywhere por defecto.
- Cierre el navegador cuando termine — esto borra todos los datos de la sesión
- Conéctese a la red Tor antes de iniciar — si necesita usar Tor y está bloqueado en su país, configure un puente (bridge) primero (consulte la Sección 4)
- Genere un nuevo circuito para tareas importantes: *Icono de Tor en la barra de URL → Nuevo Circuito para Este Sitio (New Circuit for This Site)*

---

## 3. Servicios .Onion

Los servicios .Onion (también llamados "servicios ocultos") son sitios web accesibles solo a través de Tor que tienen su propio anonimato: la ubicación del servidor está oculta, al igual que la ubicación del usuario.

### 3.1 Por qué Usar Servicios .Onion

- **Ambas partes son anónimas:** A diferencia de los sitios web habituales a los que se accede a través de Tor, los servicios .onion ocultan la IP del servidor además de su IP
- **Cifrado de extremo a extremo:** El tráfico entre usted y el servicio .onion está cifrado dentro de la red Tor, sin un nodo de salida que pueda observarlo
- **Resistencia a la censura:** Los servicios .onion no pueden ser bloqueados por el filtro de Internet de un país (aunque el acceso a Tor en sí puede estar restringido)

### 3.2 Servicios .Onion Clave

**Periodismo seguro y denuncias:**
- **SecureDrop:** La plataforma estándar para la comunicación segura con organizaciones de medios. La mayoría de los principales medios de comunicación tienen una dirección .onion de SecureDrop. Acceda a través de sus sitios web públicos.
- **DDoSecrets** (Distributed Denial of Secrets): Archivo de documentos filtrados de gobiernos y corporaciones — ddosecretspzwfy7bk6vmvyxky5xxlhqo4mfn2dzdmxktvgjzovqd.onion

**Búsqueda y referencia:**
- **DuckDuckGo Onion:** duckduckgogg42xjoc72x3sjasowoarfbgcmvfimaftt6twagswzczad.onion
- **Ahmia:** Motor de búsqueda para sitios .onion — ahmia.fi (clearnet) o a través de DuckDuckGo .onion

**Comunicaciones:**
- **Proton Mail (Onion):** protonmailrmez3lotccipshtkleegetolb73fuirgj7r4o4vfu7ozyd.onion

### 3.3 Seguridad de Direcciones .Onion

No todos los sitios .onion son legítimos. Verifique las direcciones .onion a través de los sitios web oficiales en la red pública (clearnet) de organizaciones confiables: no use direcciones .onion encontradas a través de búsquedas aleatorias o fuentes no verificadas.

---

## 4. Puentes Tor (Bridges): Eludiendo la Censura

Si Tor está bloqueado en su país o red, los puentes (bridges) son relés de Tor no publicados que eluden los bloqueos.

**Obtener puentes:**
1. En torproject.org/bridges
2. Enviando un correo electrónico a bridges@torproject.org (desde una dirección de Gmail o Riseup)
3. A través del Navegador Tor: *Ajustes de Conexión → Usar un puente → Solicitar un puente de Tor Project (Connection Settings → Use a bridge → Request a bridge from Tor Project)*

**Tipos de puentes:**
- **obfs4:** El estándar actual; ofusca el tráfico para que no se parezca a Tor
- **Snowflake:** Enruta el tráfico a través de WebRTC, haciendo que parezca tráfico de videoconferencia
- **meek-azure:** Enruta el tráfico a través de Microsoft Azure, haciendo que parezca tráfico legítimo de la nube

---

## 5. Tor en Dispositivos Móviles

### 5.1 Orbot (Android)

Orbot es la aplicación oficial de Tor para Android (del Guardian Project). Puede:
- Proporcionar un proxy Tor para todas las aplicaciones en el dispositivo (con modo VPN)
- Enrutar aplicaciones específicas a través de Tor (enrutamiento selectivo)
- Integrarse directamente con Signal para proteger los metadatos

**Configuración:**
1. Instale Orbot desde Google Play o F-Droid (Se prefiere F-Droid para usuarios conscientes de la seguridad)
2. Toque *Iniciar (Start)* para conectarse a Tor
3. Habilite el *Modo VPN (VPN Mode)* para enrutar todo el tráfico del dispositivo a través de Tor (consume mucha batería, pero es exhaustivo)
4. O, use *Aplicaciones habilitadas para Tor (Tor-Enabled Apps)* para enrutar solo aplicaciones específicas

**Signal + Orbot:**
En Signal: *Ajustes → Privacidad → Avanzado → Usar proxy → Proxy SOCKS → 127.0.0.1:9050*

Esto enruta el tráfico de Signal a través de Tor, ocultándole a su ISP que está usando Signal en absoluto.

### 5.2 Navegador Tor para Android

La aplicación oficial del Navegador Tor (Tor Browser) está disponible para Android desde la Play Store o desde torproject.org. Proporciona las mismas protecciones que la versión de escritorio.

### 5.3 Limitaciones en iOS

Las políticas de la App Store de Apple impiden que cualquier aplicación enrute todo el tráfico del sistema a través de Tor (el equivalente al modo VPN). En iOS:
- **Onion Browser** (de Mike Tigas, respaldado por Tor Project): Un navegador conectado a Tor. Similar al Navegador Tor para Android.
- Limitación: Solo se anonimiza el tráfico del navegador; otras aplicaciones no se enrutan a través de Tor

---

## 6. Combinaciones de Tor + VPN

### 6.1 VPN → Tor (VPN y luego Tor)

Conéctese a la VPN primero, luego use Tor.

**Ventajas:**
- Su ISP ve el tráfico VPN, no el tráfico Tor — oculta a su ISP que está usando Tor
- Protege contra nodos de entrada maliciosos (la IP de su VPN es la entrada, no su IP real)

**Desventajas:**
- Su proveedor de VPN puede ver que está usando Tor (pero no lo que está haciendo en Tor)
- Debe confiar en su proveedor de VPN

**Mejor para:** Situaciones en las que necesita ocultar el uso de Tor de su ISP mientras mantiene un fuerte anonimato en el extremo de destino.

### 6.2 Tor → VPN (Tor y luego VPN)

Use Tor para conectarse a una VPN, para que la VPN aparezca como su IP de salida.

**Ventajas:**
- Su destino ve una IP de VPN, no una IP de nodo de salida de Tor (algunos sitios bloquean los nodos de salida de Tor)
- Evita el análisis de tráfico del nodo de salida

**Desventajas:**
- Complejo de configurar correctamente
- El proveedor de VPN puede ver su tráfico (ven el tráfico descifrado de la salida de Tor)
- Derrota gran parte del propósito de Tor al centralizar la confianza en la VPN

**Generalmente no recomendado** a menos que tenga una razón específica para necesitar una IP de VPN en el destino.

---

*Esta guía no constituye asesoramiento legal. El uso de Tor es legal en la mayoría de los países, pero puede atraer la atención en algunas jurisdicciones. Conozca su contexto legal local.*

[← Volver al Índice](../index.md)

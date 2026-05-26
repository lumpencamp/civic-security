# Mullvad VPN: Refuerzo de la Privacidad y Defensa Contra el Análisis de Tráfico

> [!CAUTION]
> **AVISO LEGAL Y DE SEGURIDAD OPERACIONAL**
> Esta guía está destinada estrictamente a fines lícitos, defensivos y educativos. Algunas tácticas detalladas a continuación pueden conllevar riesgos legales dependiendo de su jurisdicción local.
> - **Nunca** se resista al arresto ni obstruya físicamente a las fuerzas del orden.
> - **Nunca** participe en la interferencia ilegal de radiofrecuencia (RF jamming) ni en daños a la propiedad.
> - **Siempre** consulte a las redes locales de defensa legal (por ejemplo, el National Lawyers Guild) para obtener asesoramiento específico de su jurisdicción.

*Estado: Manual de Refuerzo de Seguridad de Red | Audiencia: Activistas y Usuarios Conscientes de la Privacidad*

Una VPN no proporciona anonimato: proporciona privacidad al trasladar la confianza de su Proveedor de Servicios de Internet (ISP) a la empresa de VPN. Mullvad es la recomendación estándar de oro para activistas porque fue diseñada desde cero para minimizar la recopilación de datos, acepta pagos anónimos y ha sido pionera en defensas de código abierto contra el análisis de tráfico avanzado que ninguna otra VPN comercial iguala.

Este manual cubre la configuración de seguridad completa: configuración de cuenta anónima, WireGuard + interruptor de apagado (kill-switch), DAITA (Defensa contra el Análisis de Tráfico Guiado por IA), enrutamiento multisalto (multi-hop) y DNS cifrado.

*Para un contexto más profundo sobre la vigilancia masiva, lea el [Manifiesto de Vigilancia Total (PDF)](https://mullvad.net/pdfs/Total_surveillance.pdf) de Mullvad.*

---

## 1. Generación y Financiación de Cuentas Anónimas

La mayoría de los proveedores de VPN exigen su dirección de correo electrónico, nombre de facturación y tarjeta de crédito, vinculando inmediatamente su identidad real a su tráfico VPN.

*   **El Sistema Mullvad:** Mullvad requiere cero datos personales. Cuando se registra, el sistema genera un número de cuenta aleatorio de 16 dígitos. Ese número *es* su cuenta. No hay contraseñas ni correos electrónicos que hackear o solicitar mediante citación judicial.
*   **Financiación (El Protocolo OPSEC):**
    *   *Seguridad Estándar:* Pague a través de una tarjeta de regalo prepaga y anonimizada o Monero (XMR). No utilice Bitcoin, PayPal ni su tarjeta de crédito personal.
    *   *Seguridad Máxima:* Escriba su número de cuenta de 16 dígitos en un papel, coloque dinero físico en un sobre y envíelo por correo directamente a la sede de Mullvad en Suecia. Esto crea una desconexión completa entre su identidad financiera y su tráfico de red.

## 2. Despliegue de WireGuard e Interruptores de Apagado (Kill-Switches)

OpenVPN es robusto, pero WireGuard es el estándar moderno: es más rápido, usa menos batería y tiene una superficie de ataque criptográfico significativamente menor.

### Configuración del Protocolo
1.  Abra la aplicación Mullvad. Navegue hasta **Ajustes > Ajustes de VPN** (Settings > VPN settings).
2.  Cambie el **Protocolo de túnel** (Tunnel protocol) de Automático a **WireGuard**.

### El Interruptor de Apagado Programado (Modo de Bloqueo / Lockdown Mode)
Un interruptor de apagado (kill-switch) es inútil si solo se activa *después* de que la aplicación VPN falla, permitiendo que su IP real se filtre durante varios segundos. Debe aplicar un interruptor de apagado estricto a nivel del sistema operativo.

*   **Configuración de Escritorio:** En los Ajustes de Mullvad, habilite el **Modo de bloqueo** (Lockdown mode). Esto altera las reglas del firewall de su sistema para que su computadora *no pueda* conectarse a Internet a menos que el túnel Mullvad esté activo.
*   **Configuración de Android:**
    1.  Vaya a los **Ajustes > Red e Internet > VPN** de su Android.
    2.  Toque el ícono de engranaje junto a Mullvad VPN.
    3.  Active **VPN siempre activa** (Always-on VPN) y **Bloquear conexiones sin VPN** (Block connections without VPN). Esto aplica un bloqueo estricto a nivel del SO contra cualquier tráfico no tunelizado.

## 3. Enrutamiento Multisalto (Multi-Hop) y Defensa del Análisis de Tráfico

Los adversarios avanzados monitorean el tamaño y el tiempo de los paquetes de datos que entran en un servidor VPN y salen de él, intentando correlacionar el tráfico e identificar al usuario (Análisis de Tráfico).

### Configuración de Multisalto (Multi-Hop)
Enrutar su tráfico a través de dos servidores VPN separados en diferentes jurisdicciones complica significativamente el análisis de tráfico.

1.  En la aplicación Mullvad, vaya a **Ajustes > Ajustes de VPN > Ajustes de WireGuard** (Settings > VPN settings > WireGuard settings).
2.  Habilite **Activar multisalto** (Enable multihop).
3.  Elija un Servidor de Entrada (por ejemplo, en Suiza) y un Servidor de Salida (por ejemplo, en Islandia). Su tráfico se cifra dos veces: su ISP solo ve una conexión a Suiza, y el sitio web de destino solo ve tráfico originado en Islandia.

*(Nota: el multisalto aumenta la latencia y reduce la velocidad. Úselo solo cuando sea necesario para una seguridad operativa elevada).*

## 4. DAITA: Defensa Contra el Análisis de Tráfico Guiado por IA

> [!IMPORTANT]
> DAITA es una de las innovaciones de seguridad más significativas de Mullvad y es única entre las VPN comerciales. Habilítelo si se encuentra en un nivel de amenaza T2+ o si ocultar *que está usando una VPN* — o *lo que está haciendo dentro de ella* — es importante.

### 4.1 ¿Qué es el Análisis de Tráfico Guiado por IA?

Una VPN cifra el contenido de su tráfico, pero no puede ocultar la **forma** de su tráfico: tamaños de paquetes, patrones de tiempo e intervalos de llegada. Los adversarios sofisticados (nivel T3–T4: NSA, GCHQ, investigadores académicos que trabajan con las fuerzas del orden) utilizan clasificadores de aprendizaje automático (machine learning) entrenados con millones de sesiones capturadas para identificar (fingerprint) lo que usted está haciendo dentro de un túnel VPN cifrado.

**Ejemplos de lo que puede revelar el análisis de tráfico:**
- Qué sitio web está visitando, incluso a través de HTTPS y una VPN, al hacer coincidir la "huella digital" del tamaño de paquete de la carga de la página con una base de datos entrenada
- Si está utilizando Signal, Tor u otras aplicaciones sensibles, incluso cuando ese tráfico se enruta a través de una VPN
- Patrones de tiempo que vinculan su sesión VPN cifrada con la actividad visible en el otro extremo del túnel (ataque de correlación)

Esta clase de ataque no es teórica. La investigación académica ("Website Fingerprinting Attacks and Defenses", investigación de WF) ha demostrado una precisión del 90%+ contra usuarios de VPN ingenuos.

### 4.2 Cómo Funciona DAITA

DAITA utiliza un marco llamado **Maybenot** (código abierto, desarrollado por Mullvad) para derrotar los ataques de huella digital (fingerprinting) a nivel de red:

**Relleno de Paquetes Aleatorio (Random Packet Padding):**
Cada paquete que sale de su dispositivo se rellena hasta alcanzar un tamaño aleatorio antes del cifrado. Esto destruye la huella digital del tamaño del paquete en la que se basan los clasificadores de aprendizaje automático. Un mensaje de Signal de 200 bytes se ve igual que una solicitud web de 1.400 bytes porque ambos están rellenados hasta tamaños aleatorios indistinguibles.

**Inyección de Tráfico Ficticio (Dummy Traffic Injection):**
DAITA inyecta tráfico ficticio programado aleatoriamente entre paquetes reales. Esto rompe los patrones de tiempo (intervalos de llegada, estructura de ráfagas) que explotan los ataques de correlación. El observador ve un flujo constante y ruidoso, no los patrones distintivos de ráfagas de la carga de una página web o una videollamada.

**Por qué esto es difícil de derrotar:**
Sin saber qué paquetes son reales y cuáles son ficticios, y sin conocer los tamaños antes del relleno, un clasificador de análisis de tráfico no puede distinguir entre diferentes tipos de actividad. La relación señal-ruido colapsa.

### 4.3 Cómo Habilitar DAITA

**En Escritorio (Windows/macOS/Linux):**
1. Abra la aplicación Mullvad
2. Vaya a **Ajustes → Ajustes de VPN → Ajustes de WireGuard** (Settings → VPN settings → WireGuard settings)
3. Cambie **DAITA** a **ACTIVADO** (ON)

**En Android:**
1. Abra la aplicación Mullvad
2. Toque el **engranaje de ajustes** en la barra de navegación inferior
3. Navegue hasta **Ajustes de VPN → Ajustes de WireGuard**
4. Cambie **DAITA** a **ACTIVADO** (ON)

**En iOS:**
1. Abra la aplicación Mullvad
2. Toque **Ajustes** → **Ajustes de VPN**
3. Cambie **DAITA** a **ACTIVADO** (ON) (disponible en la aplicación Mullvad versión 2024.8+)

### 4.4 DAITA + Multisalto (Protección Máxima)

DAITA es más poderoso cuando se combina con el enrutamiento multisalto (multi-hop):

- **Sin multisalto:** DAITA protege el segmento entre su dispositivo y el servidor de entrada de Mullvad. Un adversario que pueda observar tanto el tráfico del servidor de entrada como el tráfico del servidor de salida aún puede intentar la correlación.
- **Con multisalto + DAITA:** DAITA ofusca el tráfico que ingresa al primer salto. El tráfico entre los servidores internos de Mullvad no es visible para los adversarios externos. Esto derrota incluso a un observador de red parcial que controla parte de la ruta, pero no toda.

**Habilitar ambos simultáneamente:**
- Multisalto: **Ajustes → Ajustes de VPN → Ajustes de WireGuard → Activar multisalto** → elija servidores de entrada + salida
- DAITA: cambie a ACTIVADO (ON) en el mismo menú de ajustes de WireGuard

> [!NOTE]
> DAITA agrega una sobrecarga modesta (un 5–15% más de ancho de banda utilizado debido al relleno y al tráfico ficticio; un ligero aumento en la latencia). Para la mayoría de los casos de uso, esto es imperceptible. Desactívelo temporalmente en conexiones muy lentas si el rendimiento es inaceptable, pero vuelva a habilitarlo para cualquier trabajo operativo sensible.

### 4.5 Ajuste al Modelo de Amenazas

| Amenaza | ¿DAITA Ayuda? |
|--------|-------------|
| El ISP ve qué sitios visita | ✅ Sí — con relleno, la huella digital falla |
| Correlación de tráfico por las fuerzas del orden | ✅ Significativamente más difícil |
| Observador de red global de clase NSA (ataque de correlación) | ✅ Mucho más difícil cuando se combina con multisalto |
| Mullvad recibe una citación judicial | ❌ No — Mullvad no tiene registros, pero DAITA no cambia la exposición legal |
| Malware a nivel de dispositivo que lee el tráfico antes del cifrado | ❌ No — la VPN no protege contra el compromiso del dispositivo |

---

## 5. Integración del Resolutor DNS Privado

Su ISP monitorea cada sitio web que visita al registrar sus solicitudes DNS (Sistema de Nombres de Dominio). Al enrutar las consultas DNS a través de los resolutores cifrados de Mullvad, usted ciega a su ISP.

1.  Navegue a **Ajustes > Ajustes de VPN > Filtrado de DNS** (Settings > VPN settings > DNS filtering).
2.  Habilite **Bloquear rastreadores** (Block trackers), **Bloquear anuncios** (Block ads) y **Bloquear malware** (Block malware).
3.  **La Ventaja:** Mullvad utiliza sus propios servidores DNS a través del túnel cifrado de WireGuard. Esto evita que su ISP recopile su historial de navegación y bloquea las conexiones a listas de bloqueo patrocinadas por el estado y rastreadores de telemetría a nivel de red, antes de que lleguen a su navegador.

_Última actualización: Mayo de 2026_

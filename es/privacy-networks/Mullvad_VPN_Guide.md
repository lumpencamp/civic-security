# Mullvad VPN: optimización comercial e implementación de Kill-Switch

*Estado: Manual de refuerzo de seguridad de red | Público: activistas y usuarios conscientes de la privacidad*

Una VPN no proporciona anonimato; proporciona privacidad al transferir la confianza de su proveedor de servicios de Internet (ISP) a la empresa de VPN. Se recomienda Mullvad porque es una de las pocas entidades comerciales diseñadas desde cero para minimizar la recopilación de datos, lo que le permite establecer un túnel verdaderamente privado.

Este manual detalla la configuración técnica necesaria para implementar Mullvad de forma segura frente a la vigilancia de red y el análisis de tráfico a nivel de ISP.

*Para profundizar en las amenazas que plantea la vigilancia masiva, lea el [Manifiesto de Vigilancia Total de Mullvad (PDF)](https://mullvad.net/pdfs/Total_surveillance.pdf).*

---

## 1. Generación y financiación de cuentas anónimas

La mayoría de los proveedores de VPN exigen su dirección de correo electrónico, nombre de facturación y tarjeta de crédito, vinculando inmediatamente su identidad real con su tráfico VPN.

* **El sistema Mullvad:** Mullvad no requiere datos personales. Cuando te registras, el sistema genera un número de cuenta aleatorio de 16 dígitos. Ese número *es* tu cuenta. No hay contraseñas ni correos electrónicos para piratear o citar.
* **Financiamiento (Protocolo OPSEC):**
    * *Seguridad estándar:* Pague a través de una tarjeta de regalo prepaga anónima o Monero (XMR). No utilice Bitcoin, PayPal ni su tarjeta de crédito personal.
    * *Máxima seguridad:* Escriba su número de cuenta de 16 dígitos en un papel, coloque efectivo físico en un sobre y envíelo por correo directamente a la sede de Mullvad en Suecia. Esto crea una desconexión completa entre su identidad financiera y su tráfico de red.

## 2. Implementación de WireGuard y Kill-Switches

OpenVPN es robusto, pero WireGuard es el estándar moderno: es más rápido, usa menos batería y tiene una superficie de ataque criptográfico significativamente menor.

### Configuración del protocolo
1. Abra la aplicación Mullvad. Vaya a **Configuración > Configuración de VPN**.
2. Cambie el **Protocolo de túnel** de Automático a **WireGuard**.

### El interruptor de apagado codificado (modo de bloqueo)
Un interruptor de emergencia es inútil si sólo se activa *después* de que la aplicación VPN falla, permitiendo que su IP real se filtre durante varios segundos. Debe aplicar un interruptor de apagado completo a nivel del sistema operativo.

* **Configuración de escritorio:** En Configuración de Mullvad, habilite **Modo de bloqueo**. Esto altera las reglas del firewall de su sistema para que su computadora *no pueda* conectarse a Internet a menos que el túnel Mullvad esté activo.
* **Configuración de Android:**
    1.  Go to your Android **Settings > Network & internet > VPN**.
    2.  Tap the gear icon next to Mullvad VPN.
    3.  Toggle **Always-on VPN** and **Block connections without VPN** to **ON**. This enforces a strict OS-level block against any non-tunneled traffic.

## 3. Defensa de análisis de tráfico y enrutamiento de múltiples saltos

Los adversarios avanzados monitorean el tamaño y el tiempo de los paquetes de datos que ingresan y salen de un servidor VPN, intentando correlacionar el tráfico e identificar al usuario (Análisis de tráfico).

### Configuración de saltos múltiples
Dirigir su tráfico a través de dos servidores VPN separados en diferentes jurisdicciones complica significativamente el análisis del tráfico.

1. En la aplicación Mullvad, vaya a **Configuración > Configuración de VPN > Configuración de WireGuard**.
2. Habilite **Habilitar saltos múltiples**.
3. Elija un servidor de entrada (por ejemplo, en Suiza) y un servidor de salida (por ejemplo, en Islandia). Su tráfico se cifra dos veces: su ISP solo ve una conexión a Suiza y el sitio web de destino solo ve el tráfico que se origina en Islandia.

*(Nota: el salto múltiple aumenta la latencia y reduce la velocidad. Úselo solo cuando sea necesario para una seguridad operativa elevada).*

## 4. Integración del solucionador de DNS privado

Su ISP monitorea cada sitio web que visita registrando sus solicitudes de DNS (Sistema de nombres de dominio). Al enrutar consultas de DNS a través de los solucionadores cifrados de Mullvad, ciega a su ISP.

1. Navegue a **Configuración > Configuración de VPN > Filtrado DNS**.
2. Habilite **Bloquear rastreadores**, **Bloquear anuncios** y **Bloquear malware**.
3. **La ventaja:** Mullvad utiliza sus propios servidores DNS a través del túnel cifrado WireGuard. Esto evita que su ISP recopile su historial de navegación y bloquea las conexiones a listas de bloqueo y rastreadores de telemetría conocidos patrocinados por el estado a nivel de red, incluso antes de que lleguen a su navegador.

_Última actualización: 2026_

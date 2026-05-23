# Guía: Endurecimiento posterior a la instalación de CalyxOS

*Estado: Ingeniería de privacidad móvil | Audiencia: Activistas conscientes de la privacidad*

CalyxOS ofrece un puente vital entre la seguridad absoluta (GrapheneOS) y la usabilidad diaria. Está diseñado para eliminar la vigilancia corporativa generalizada y al mismo tiempo mantener la compatibilidad con las aplicaciones necesarias. Sin embargo, para maximizar su potencial, debes configurar activamente sus herramientas de privacidad integradas.

Este manual detalla la configuración granular necesaria para proteger CalyxOS contra la recopilación de datos corporativos y la vigilancia localizada.

---

## 1. Datura Firewall: redes de denegación predeterminadas

Datura Firewall es la herramienta integrada más poderosa de CalyxOS. De forma predeterminada, las aplicaciones intentarán conectarse a Internet para recopilar análisis, descargar anuncios e informar su dirección IP. Su postura debe ser **Predeterminada-Denegar**.

### Configuración granular de la aplicación
Debe incluir manualmente en la lista blanca el acceso a la red para las aplicaciones.

1. Navegue a **Configuración** > **Red e Internet** > **Datura Firewall**.
2. **La postura predeterminada:** Desactive los "datos de fondo" globalmente para todas las aplicaciones no esenciales.
3. **Configuración por aplicación:** Para aplicaciones como cámara, calculadora o lector de documentos sin conexión (por ejemplo, CryptPad sin conexión), deshabilite **todos** los accesos a la red (Wi-Fi, datos móviles y VPN). Una herramienta fuera de línea no tiene ninguna razón legítima para comunicarse con un servidor remoto.
4. **Aislamiento de red:** Si una aplicación requiere acceso a Internet, pero solo desea que se sincronice cuando esté seguro, restrinjala a "Solo Wi-Fi" (evitando que use datos móviles mientras está en tránsito) o "Solo VPN" (asegurándose de que no pueda filtrar su verdadera dirección IP si la VPN se cae).

---

## 2. Configuración de MicroG y mitigación de riesgos

MicroG es el reemplazo de código abierto de los servicios de Google Play. Permite que las notificaciones automáticas y los servicios de ubicación funcionen sin otorgarle a Google privilegios profundos del sistema. Sin embargo, MicroG todavía se comunica con los servidores de Google. Debes configurarlo para minimizar esta telemetría.

### Los riesgos de MicroG
Cuando MicroG está completamente habilitado, su dispositivo registra un identificador único con Google para recibir mensajería en la nube (notificaciones push). Esto crea un rastro de metadatos que conecta su dirección IP con su dispositivo.

### Reforzando la configuración
1. Abra la aplicación **Configuración MicroG**.
2. **Registro del dispositivo:** Desactívelo a menos que sea absolutamente necesario. Si están deshabilitadas, las aplicaciones no pueden usar los servidores de Google para notificaciones automáticas. (Nota: las aplicaciones seguras como Signal usan sus propias conexiones WebSocket y *no* necesitan MicroG para recibir mensajes).
3. **Mensajería en la nube:** Si *debe* usar una aplicación propietaria que requiere notificaciones automáticas (por ejemplo, un cliente de correo electrónico seguro específico o una aplicación bancaria), habilite la mensajería en la nube.
    * *Mitigación:* Toca los tres puntos (menú) en Mensajería en la nube y ve a **Avanzado**. Aumenta el "Intervalo de ping" para reducir la frecuencia con la que tu dispositivo se comunica con el servidor.
4. **Google SafetyNet:** Asegúrese de que esté **Desactivado**. Es un servicio de certificación remota que envía perfiles de hardware del dispositivo a Google.
5. **Módulos de ubicación:** Deshabilite el backend del "Servicio de ubicación de Google". Confíe únicamente en el Servicio de ubicación de Mozilla (MLS) o DejaVu para realizar búsquedas de ubicación de torres de telefonía móvil o Wi-Fi sin conexión y que respeten la privacidad.

---

## 3. El botón del pánico: flujo de trabajo de implementación de emergencia

*(Nota: aunque está temporalmente deshabilitado en las primeras versiones de prueba de Android 16, el botón de pánico sigue siendo una característica central de la arquitectura estable de CalyxOS).*

El botón de pánico es un "interruptor de hombre muerto" diseñado para proteger rápidamente su dispositivo durante una aprehensión física o una amenaza inminente.

### Flujo de trabajo de implementación
Debes configurar el Botón de Pánico *antes* de una acción. No espere hasta que lo detengan.

1. Abra la aplicación **Botón de pánico** desde el cajón de aplicaciones.
2. **Establezca el disparador:** Configure el mecanismo del disparador (por ejemplo, presionando rápidamente el botón de encendido 5 veces o presionando una combinación específica de botones de volumen).
3. **Asigne las acciones:** Seleccione exactamente qué hará el botón de pánico cuando se active.
    * *Nivel de amenaza T2 (Protesta/Control de multitudes):* Mapee el botón para **Desinstalar aplicaciones específicas** (por ejemplo, borrar instantáneamente Signal, Element o su administrador de contraseñas) y **Ocultar aplicaciones seleccionadas**.
    * *Nivel de amenaza T3/T4 (Incautación dirigida):* Asigne el botón para **Enviar SMS de emergencia** (notificando a su contacto de apoyo en la cárcel sus coordenadas) seguido inmediatamente de un **Apagado del dispositivo**.
4. **¿Por qué apagar?** Un apagado completo del dispositivo obliga al teléfono a volver al estado altamente seguro Antes del primer desbloqueo (BFU), cifrando sus claves de datos y bloqueando herramientas de extracción forense como Cellebrite.

### **Dispositivos compatibles**

CalyxOS admite una gama más amplia de dispositivos que GrapheneOS, priorizando los modelos que permiten volver a bloquear el gestor de arranque.

A partir de 2026, esto incluye:
* **Google Pixel:** Serie Pixel 4a (5G) a Pixel 9 (incluidos Fold y Tablet). Nota: Pixel 4 y 4 XL ya no son compatibles.
* **Fairphone:** Fairphone 4 y Fairphone 5.
* **Motorola:** Modelos seleccionados como Moto G 5G (2024), G84, G34/G45, G52, G42 y G32. *(Nota: los dispositivos que no son Pixel pueden experimentar retrasos en la recepción de parches de seguridad completos en comparación con los Pixel).*

*La lista cambia con frecuencia. Consulte siempre la [página de soporte del dispositivo CalyxOS oficial](https://calyxos.org/docs/guide/device-support/) para obtener la lista más actualizada y el cronograma de soporte.*

_Última actualización: 2026_

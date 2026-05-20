# Guía: CalyxOS

CalyxOS es un sistema operativo móvil centrado en la privacidad basado en el Proyecto de código abierto de Android (AOSP). Está diseñado para ser una alternativa más fácil de usar a GrapheneOS, sin dejar de ofrecer un alto nivel de privacidad y seguridad.

**Modelo de amenazas:** CalyxOS es un poco menos estricto en cuanto a refuerzo de seguridad que GrapheneOS, pero sobresale en usabilidad. Es ideal para el activista promedio que quiere detener el seguimiento comercial generalizado y "eliminar de Google" su vida sin sacrificar la conveniencia de las aplicaciones estándar.

**Cómo funciona:**
* **microG:** CalyxOS incluye microG, una implementación gratuita y de código abierto de los servicios de Google Play. Esto permite a los usuarios ejecutar muchas aplicaciones que dependen de los servicios de Google sin tener que instalar los servicios oficiales de Google Play, que invasan la privacidad.
* **Privacidad de forma predeterminada:** CalyxOS incluye el firewall Datura y un conjunto de aplicaciones centradas en la privacidad que se pueden instalar sin conexión durante la configuración.
    * *Actualizaciones de aplicaciones de 2026:* Las actualizaciones recientes han reemplazado herramientas antiguas con alternativas modernas, como **Tor VPN** (que reemplaza a Orbot), **CoMaps** (que reemplaza a Organic Maps) y **F-Droid Basic**.
    * *Nota:* A partir del ciclo de lanzamiento de Android 16, las funciones **CalyxVPN** y el **Botón de pánico** se eliminaron temporalmente mientras se someten a redesarrollo y actualizaciones de infraestructura.

### **Dispositivos compatibles**

CalyxOS admite una gama más amplia de dispositivos que GrapheneOS, priorizando los modelos que permiten volver a bloquear el gestor de arranque.

A partir de 2026, esto incluye:
* **Google Pixel:** Serie Pixel 4a (5G) a Pixel 9 (incluidos Fold y Tablet). Nota: Pixel 4 y 4 XL ya no son compatibles.
* **Fairphone:** Fairphone 4 y Fairphone 5.
* **Motorola:** Modelos seleccionados como Moto G 5G (2024), G84, G34/G45, G52, G42 y G32. *(Nota: los dispositivos que no son Pixel pueden experimentar retrasos en la recepción de parches de seguridad completos en comparación con los Pixel).*

*La lista cambia con frecuencia. Consulte siempre la [página de soporte del dispositivo CalyxOS oficial](https://calyxos.org/docs/guide/device-support/) para obtener la lista más actualizada y el cronograma de soporte.*

_Última actualización: 2026_
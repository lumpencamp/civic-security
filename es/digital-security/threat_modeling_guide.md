# Modelado avanzado de amenazas para organizaciones cívicas

*Estado: Directiva de Nivel 2 | Público: planificadores de operaciones y equipos de seguridad*

El modelado de amenazas no es paranoia; es la evaluación calculada y objetiva de su entorno operativo. Este marco adapta las metodologías de seguridad corporativa (STRIDE y PASTA) en un modelo cuantitativo procesable específicamente para actores no estatales, activistas y organizaciones cívicas.

---

## 1. Perfiles del adversario (los niveles de amenaza)

Para defenderse eficazmente, debe comprender las capacidades, el presupuesto y las autorizaciones legales de su adversario. No te prepares para un adversario T4 si tu amenaza real es T1; hacerlo provocará una parálisis operativa.

* **T1: El ruido (Doxxers, Trolls, Contramanifestantes)**
    * **Capacidades:** Inteligencia de fuentes abiertas (OSINT), ingeniería social, acoso físico en eventos públicos, denegación de servicio (reporte de cuentas).
    * **Limitaciones:** Sin autoridad legal, financiamiento mínimo, baja sofisticación técnica.
* **T2: Aplicación de la ley local (Policía, Centros Regionales de Fusión)**
    * **Capacidades:** Autoridad de arresto, vigilancia física, simuladores de sitios celulares (Stingrays), ALPR (lectores de matrículas), bases de datos de reconocimiento facial, acceso a corredores de datos, poder de citación para empresas tecnológicas nacionales.
    * **Limitaciones:** Fricción burocrática, fronteras geográficas, restricciones presupuestarias.
* **T3: Inteligencia Corporativa (Seguridad Privada, Pinkertons)**
    * **Capacidades:** Grandes recursos financieros, infiltración/informantes, herramientas OSINT avanzadas, litigios/demandas (SLAPP), contratación de agentes del orden fuera de servicio.
    * **Limitaciones:** Sin autoridad de arresto directo, sujeto a responsabilidad civil, muy sensible a las malas relaciones públicas.
* **T4: Inteligencia a nivel estatal (agencias federales, entidades de tres letras)**
    * **Capacidades:** Presupuesto ilimitado, exploits de dispositivos de día cero (Pegasus), vigilancia nacional de arrastre, intercambio de inteligencia de la NSA/FISA, autoridad de búsqueda fronteriza, operaciones encubiertas encubiertas.
    * **Limitaciones:** Alto umbral de despliegue. A menos que esté involucrado en una interrupción masiva de la infraestructura crítica o sea designado como una amenaza a la seguridad nacional, es poco probable que enfrente un objetivo T4 dedicado.

---

## 2. La Matriz de Evaluación de Riesgos 5x5

El riesgo se calcula utilizando dos variables: **Probabilidad** (¿Qué tan probable es el ataque?) e **Impacto** (¿Qué tan devastadora es la consecuencia?).

* **Probabilidad (1-5):** 1 = Raro, 3 = Posible, 5 = Casi seguro.
* **Impacto (1-5):** 1 = Inconvenientes menores, 3 = Operación interrumpida/Detención a corto plazo, 5 = Fallo organizacional crítico/Encarcelamiento a largo plazo/Pérdida de vidas.

**Puntuación de riesgo = Probabilidad × Impacto**
| Probabilidad \ Impacto | 1 (menor) | 2 (moderado) | 3 (significativo) | 4 (grave) | 5 (crítico) |
|:---|:---|:---|:---|:---|:---|
| **5 (Cierto)** | 5 (bajo) | 10 (med.) | 15 (alto) | 20 (extremo) | **25 (ABORTAR)** |
| **4 (Probable)** | 4 (bajo) | 8 (médico) | 12 (alto) | 16 (extremo) | 20 (extremo) |
| **3 (Posible)** | 3 (bajo) | 6 (med.) | 9 (med.) | 12 (alto) | 15 (alto) |
| **2 (Improbable)** | 2 (bajo) | 4 (bajo) | 6 (med.) | 8 (médico) | 10 (med.) |
| **1 (raro)** | 1 (bajo) | 2 (bajo) | 3 (bajo) | 4 (bajo) | 5 (bajo) |


### Umbrales estrictos (la regla de ir/no ir)
* **Puntuación 1-8 (Aceptable):** Proceder con OPSEC estándar.
* **Puntuación 9-14 (elevada):** Proceder con contramedidas intensificadas. Restrinja el acceso "necesario saber".
* **Puntuación 15-20 (Crítico):** La operación está en espera hasta que las mitigaciones reduzcan la puntuación por debajo de 15.
* **Puntuación 21-25 (ABORTAR):** Aborto operativo obligatorio. El ambiente es demasiado hostil.

---

## 3. Plantilla de modelado de amenazas (STRIDE para activistas)

Utilice esta plantilla para cuantificar sus vulnerabilidades antes de cualquier operación importante.

### Fase 1: Identificación de activos
*Enumere lo que debe proteger.*
* **Activo 1:** (p. ej., la identidad del denunciante)
* **Activo 2:** (p. ej., la ubicación física de nuestro servidor seguro)
* **Activo 3:** (p. ej., nuestros canales de comunicación cifrados)

### Fase 2: Mapeo del adversario
*Identificar quién quiere comprometer esos activos.*
* **Adversario objetivo:** (p. ej., T2 - Centro de fusión local)
* **Su objetivo:** (p. ej., identificar a los organizadores y aprovechar los registros de comunicación)

### Fase 3: Evaluación y mitigación de vulnerabilidades
*Mapea los vectores de ataque y calcula el riesgo usando la Matriz 5x5.*
| Activo | Vector de ataque (¿Cómo lo conseguirán?) | Probabilidad básica | Impacto básico | Puntuación de riesgo base | Estrategia de Mitigación (¿Qué haremos?) | Nueva probabilidad | Nuevo impacto | Puntuación de riesgo ajustada |
|:---|:---|:---|:---|:---|:---| :--- | :--- | :--- |
| **Identidad de la fuente** | T3 Adversary utiliza citaciones en nuestro Google Workspace. | 4 | 5 | **20 (EXTREMO)** | Migrar la comunicación de origen a Signal; almacene archivos en E2EE CryptPad. | 1 | 5 | **5 (BAJO)** |
| **Ruta de protesta** | Los T1 Trolls se infiltran en un grupo público de Telegram para engañar a los asistentes. | 5 | 3 | **15 (ALTO)** | Protocolo de investigación para el ingreso al grupo; mueva las comunicaciones confidenciales al servidor Matrix privado. | 2 | 2 | **4 (BAJO)** |
| **Dispositivos** | La policía T2 confisca teléfonos durante un arresto masivo. | 4 | 4 | **16 (EXTREMO)** | Hacer cumplir el protocolo telefónico desechable; utilizar bolsas de Faraday; Códigos de acceso alfanuméricos de 12 caracteres. | 4 | 1 | **4 (BAJO)** |


### Fase 4: Lista de verificación operativa de ir/no ir
* [ ] ¿Se han identificado todos los activos?
* [ ] ¿Está clasificado correctamente el nivel de adversario principal?
* [ ] ¿Se han colocado todas las puntuaciones de riesgo ajustadas por debajo del umbral de 15 puntos?
* [ ] ¿Están todos los nodos participantes capacitados en las estrategias de mitigación?

Si alguna casilla no está marcada, la operación es **No-Go**.

_Última actualización: 2026_

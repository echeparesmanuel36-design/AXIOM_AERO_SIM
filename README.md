# ✈️ AXIOM_AERO_SIM // Configurador Aerodinámico Militar

Configurador aerodinámico e interactivo en 3D de alto rendimiento para la industria de la aviación privada y prototipos de drones de carga. Diseñado bajo una estética *HUD (Heads-Up Display)* de cabina militar y optimizado para una ejecución fluida en dispositivos móviles mediante aceleración por hardware.

El núcleo visual simula en tiempo real un túnel de viento vectorial que reacciona a la interacción del usuario (ratón, scroll e inercia), calculando dinámicamente coeficientes de fricción y sustentación sin la sobrecarga de pesados motores gráficos de terceros.

---

## 🛠️ Especificaciones Tecnológicas (Pila Core)

Para garantizar tolerancia cero a caídas de fotogramas (*jank*) y una velocidad de carga instantánea, la aplicación se empaqueta de forma **monolítica en un único archivo (`index.html`)** bajo las siguientes tecnologías:

* **HTML5 Semántico:** Estructura limpia y atómica optimizada para la lectura rápida del navegador.
* **CSS3 Avanzado (GPU Accelerated):** * **Glassmorphism:** Interfaces translúcidas procesadas mediante capas de filtrado por hardware (`backdrop-filter: blur() saturate()`).
    * **Renderizado 3D Estructural:** Composición espacial del vehículo utilizando transformaciones matriciales de CSS nativas (`preserve-3d`, `perspective`).
* **Vanilla JavaScript (ES6+ Strict):** Orquestación lógica del DOM y manipulación de eventos en el hilo de ejecución principal.
* **Librerías de Rendimiento Integradas (vía CDN):**
    * `Lenis (v1.1.13)`: Normalización y suavizado obligatorio de scroll cinético.
    * `GSAP & ScrollTrigger (v3.12.5)`: Animación fluida de la órbita de cámara en base a la posición del scroll.
    * `Lucide Icons`: Renderizado síncrono de iconos de interfaz militar.
    * `Canvas-Confetti`: Celebración procedural al alcanzar configuraciones de alta eficiencia.

---

## 🏎️ Motores Críticos de Rendimiento

### 1. Simulación de Flujo de Aire (Rust `no_std` Logic)
Las matemáticas del túnel de viento siguen una arquitectura inspirada en bajo nivel (Rust libre de librería estándar). Un bucle matemático evalúa el comportamiento y desviación de más de 200 partículas vectoriales concurrentes en un lienzo `<canvas>`. Las partículas calculan en microsegundos su colisión con el radio de las alas y el chasis modificando su trayectoria.

### 2. Gestión de Inercia y Amortiguación (Popmotion Base)
El ángulo de ataque del viento no se corta bruscamente cuando el usuario mueve el ratón. Un algoritmo de interpolación y física de muelles absorbe la posición y suaviza la transición del vector flujo, logrando un movimiento orgánico y sin *lag*.

### 3. Máquina de Estados de Propulsión (Rive Architecture Style)
El control del motor gestiona de manera reactiva tres estados lógicos mediante una máquina de estados:
1.  **OFF (Apagado):** Flujo base pasivo (450 km/h).
2.  **ON (Activo):** Aceleración masiva del túnel de viento (850 km/h).
3.  **OVERHEAT (Crítico):** Disparado automáticamente tras 6 segundos de uso continuo. Cambia la interfaz visual a alertas pulsantes rojas de peligro y altera las métricas de estabilidad.

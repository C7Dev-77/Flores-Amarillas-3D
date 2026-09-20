# 🌻 Flores Amarillas 3D — Experiencia Interactiva Web

> **Autor / Sello de Desarrollo:** C7Dev  
> **Versión:** 2.0.0 (Edición Definitiva)  
> **Licencia:** MIT  
> **Stack Principal:** WebGL (Three.js r134), Computer Vision (MediaPipe Hands), Web Audio API, Canvas 2D, HTML5/CSS3 moderno.

---

## 1. Resumen Ejecutivo (Executive Summary)

**Flores Amarillas 3D** es una aplicación web inmersiva de alto impacto visual y emocional concebida como homenaje romántico y tecnológico a la tradición de regalar flores amarillas. Combina renderizado tridimensional procedural acelerado por GPU, visión artificial por cámara web en tiempo real para interacción gestual táctil-aérea, físicas de partículas atmosféricas y un motor de audio resiliente con soporte de canciones personalizadas.

El proyecto está diseñado bajo estándares modernos de rendimiento web: funciona tanto en navegadores de escritorio como en smartphones sin requerir instalación de plugins ni dependencias nativas pesadas, manteniendo una tasa de cuadros estable de 60 FPS.

---

## 2. Características Principales (Key Features)

### 2.1. Escenario 3D Procedural con Three.js
* **Modelado de Flores Amarillas:**
  * Corolas compuestas por pétalos multicapa generados mediante geometrías tridimensionales personalizadas (`CylinderGeometry` y `ConeGeometry` deformadas proceduralmente).
  * Centros florales texturizados con relieves de semillas y pistilos dorados reactivos a la luz.
  * Tallos orgánicos y hojas verdes arqueadas con sombreado *Phong* y materiales reflectantes calibrados.
* **Geometrías Sagradas & Anillos Celestiales:**
  * Anillo toroidal oscilante (`TorusGeometry`) con efecto de rotación continua.
  * Icosaedro cristalino central (`IcosahedronGeometry`) con wireframe dorado y dispersión lumínica.
* **Atmósfera Dinámica:**
  * Campo estelar profundo con más de 1,200 estrellas titilantes en coordenadas esféricas.
  * Polvo estelar de oro (*Gold Particles*) en vórtice orbital alrededor del ramo.
  * Iluminación multidireccional: luz ambiental cálida, luz puntual principal (*PointLight*) con atenuación cuadrática y reflectores de realce (*DirectionalLight*).

### 2.2. Visión Artificial y Control por Gestos (MediaPipe Hands)
* **Reconocimiento de Manos en Tiempo Real:**
  * Integración con la biblioteca oficial de Google MediaPipe (`@mediapipe/hands` y `camera_utils`).
  * Procesamiento local y privado en el navegador (no se envían imágenes a ningún servidor externo).
* **Gestos y Acciones Mapeadas:**
  1. **Gesto de Pinza / Toque de Dedos (Índice + Pulgar):**
     * Dispara ráfagas de pétalos mágicos y chispas doradas en las coordenadas relativas de la mano.
  2. **Mano Abierta / Desplazamiento Espacial:**
     * Rota el ramo de flores 3D de manera proporcional a la posición horizontal y vertical de la palma (`pitch` y `yaw`).
  3. **Puño Cerrado o Acercamiento:**
     * Modifica la escala y enfoque focal de la cámara visual.
* **HUD & Feedback Visual:**
  * Mini-panel de previsualización en vivo con dibujo de landmarks óseos mediante `drawing_utils`.
  * Indicador de estado por gestos (*"Mano detectada", "Lanzando destellos"*).

### 2.3. Sistema de Audio Dual & Resiliente
* **Cumplimiento Estricto de Autoplay Policy:**
  * El usuario inicia la experiencia con un botón explícito **`▶️ Play Audio`**, evitando bloqueos involuntarios de navegadores como Safari, Chrome o Firefox.
* **Transición Dinámica UX:**
  * A los 3.5 segundos de reproducción de la canción oficial (*Floricienta - Flores Amarillas*), el botón conmuta fluidamente a **`🎵 Cambiar audio`**.
* **Carga de Canciones del Usuario:**
  * Permite subir cualquier archivo de audio local (`.mp3`, `.wav`, `.m4a`, `.ogg`) mediante un `FileReader` con URL de objeto blob en memoria.
* **Mecanismos de Respaldo (Fallback Architecture):**
  * Servido con cabeceras `206 Partial Content` para streaming instantáneo.
  * Pool de rutas alternativas de respaldo en caso de latencia de red.
  * **Sintetizador Web Audio API incorporado:** Si el audio de archivo no estuviese disponible, un oscilador de onda senoidal reproduce la melodía en arpegio celesta/caja de música analógica.

### 2.4. Tarjeta de Dedicatoria de Cristal (Glassmorphism UI)
* **Efecto Máquina de Escribir (Typewriter Effect):**
  * Aparición progresiva de la dedicatoria con cursor parpadeante dorado y tiempo de lectura adaptable.
* **Estética de Alta Gama:**
  * Fondos translúcidos con desenfoque gaussiano (`backdrop-filter: blur(16px)`).
  * Tipografía dual: *Poppins* para lectura limpia y títulos curvos dorados.
  * Modo colapsable para visualización limpia del ramo floral.
* **Lluvia de Pétalos en Canvas 2D:**
  * Simulación física de 45 pétalos en caída libre con rotación angular 3D simulada en 2D, balanceo senoidal por viento y rebotes sutiles.

---

## 3. Arquitectura del Sistema

```
                        ┌──────────────────────────────┐
                        │   index.html (Single Page)   │
                        └──────────────┬───────────────┘
                                       │
         ┌─────────────────────────────┼─────────────────────────────┐
         ▼                             ▼                             ▼
┌──────────────────┐         ┌──────────────────┐          ┌──────────────────┐
│   Render Three   │         │  MediaPipe Vision│          │  Audio & Events  │
│  - Scene / Cam   │         │  - WebCam Stream │          │  - HTML5 Audio   │
│  - Flores 3D     │         │  - Hand Landmarks│          │  - Web Audio Ctx │
│  - Luces / Part. │         │  - Gesture Math  │          │  - Custom Upload │
└──────────────────┘         └──────────────────┘          └──────────────────┘
         │                             │                             │
         └─────────────────────────────┼─────────────────────────────┘
                                       ▼
                        ┌──────────────────────────────┐
                        │   Canvas 2D / CSS Glass HUD  │
                        │  - Lluvia de Pétalos         │
                        │  - Máquina de Escribir       │
                        │  - Controles Responsivos     │
                        └──────────────────────────────┘
```

---

## 4. Requisitos y Compatibilidad

| Plataforma / Navegador | Soporte | Observaciones |
| :--- | :---: | :--- |
| **Google Chrome (Desktop/Móvil)** |  100% | Soporte completo para WebGL y WebCam |
| **Apple Safari (iOS / macOS)** |  100% | Compatible con WebKit Audio y WebGL |
| **Mozilla Firefox** |  100% | Rendimiento óptimo en Canvas y Audio |
| **Microsoft Edge** |  100% | Soporte nativo Chromium |
| **Modo Offline / PWA** |  Listo | Archivos estáticos empaquetados en `/dist` |

---

## 5. Manual de Uso Rápido

1. **Iniciar la Música:** Haz clic o toca en el botón **`▶️ Play Audio`** en la esquina superior o en la tarjeta de dedicatoria.
2. **Personalizar la Canción:** Tras unos segundos, pulsa **`🎵 Cambiar audio`** para subir una dedicatoria de voz o canción favorita desde tu dispositivo.
3. **Activar Modo Manos:** Haz clic en **`🖐️ Modo Manos`**, concede permiso a la cámara y mueve tu mano frente al lente para rotar las flores e interactuar sin tocar la pantalla.
4. **Disfrutar el Ramo 3D:** Pulsa **`🌻 Ver flores`** para plegar la tarjeta y contemplar la vista panorámica del jardín nocturno.
5. **Tocar la Pantalla:** Cada toque genera un estallido de chispas y estrellas mágicas doradas.

---

## 6. Créditos y Reconocimientos

* **Diseño y Desarrollo:** C7Dev
* **Inspiración Musical:** *"Flores Amarillas"* (Canción original de Floricienta / Cris Morena Group).
* **Librerías Abiertas:** Three.js Community, Google MediaPipe Research Team.

---
*Documento generado para entrega profesional de software y especificación de producto.*

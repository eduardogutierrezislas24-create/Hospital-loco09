# 👁️ Hospital Psiquiátrico VR

**Un juego de realidad virtual inmersivo donde solo necesitas mirar para interactuar**

Una experiencia de horror psicológico en VR construida con A-Frame donde los jugadores navegan por los pasillos de un misterioso hospital psiquiátrico perseguidos por una entidad oscura. El único control que posees es tu **mirada** - mira fijamente los objetos para recogerlos y lanza tus armas mirando al monstruo.

## 🎮 Mecánicas de Juego

### 🚶 Movimiento Automático
- **Avance continuo** - Caminas automáticamente hacia adelante sin control manual
- **Ritmo constante** - Velocidad predefinida que aumenta la tensión
- **Sin escape** - El avance es inevitable, debes ser rápido recolectando

### 👁️ Sistema de Interacción por Mirada (Gaze-Based)
- **Mirada fija = Acción** - Mira cualquier objeto durante 0.8 segundos para interactuar
- **Barra de carga visual** - Observe cómo la barra verde se llena mientras miras
- **Feedback inmediato** - Mensajes dinámicos confirman cada acción
- **Cursor rojo** - Apunta exactamente dónde estás mirando

### 🎯 Objetivos Principales
1. **Recolectar 3 objetos** - Encuentra los frascos de colores cian dispersos en el pasillo
2. **Evadir el monstruo** - No hagas contacto visual directo hasta que tengas las armas
3. **Lanzar armas** - Mira fijamente el monstruo (sosteniendo un objeto) para lanzarlo
4. **Victoria** - Derrota la entidad lanzándole los 3 objetos

## 🖥️ Interfaz HUD (Heads-Up Display)

```
┌─────────────────────────────────┐
│ OBJETOS: 2/3                    │  ← Cuántos items has recogido
│ EN MANO: ✓                      │  ← Si sostienes un objeto
│ ▰▰▰▰▱▱▱▱▱ (Barra de carga)    │  ← Tiempo de mirada restante
│                                 │
│ ✓ OBJETO RECOGIDO               │  ← Mensajes de acción
│ ✓ LANZADO AL MONSTRUO          │
└─────────────────────────────────┘
```

## 🏥 El Entorno

### Escenario Atmosférico
- **Pasillo largo y oscuro** - Profundidad de 50 unidades
- **Paredes cerradas** - Techo a 4 unidades, suelo a -0.1 unidades
- **Niebla envolvente** - Efecto de profundidad limitada que genera claustrofobia
- **Iluminación única** - Una linterna frontal montada en tu cabeza es tu único faro

### Elementos Interactivos

#### 🔵 Objetos Coleccionables (Cilindros Cian)
- **Primer objeto**: Cercano (posición -4 en profundidad)
- **Segundo objeto**: Medio (posición -8 en profundidad)  
- **Tercer objeto**: Lejano (posición -12 en profundidad)
- **Estrategia**: Aumentan en distancia, pero tienes que avanzar continuamente

#### 🖤 El Monstruo (Cápsula Negra)
- **Posición final**: Al fondo del pasillo (z: -18)
- **Altura**: 1.8 metros (a nivel de visión)
- **Radio**: 0.4 metros de ancho
- **Comportamiento**: Inmóvil pero amenazante

## 📊 Tabla de Controles (¡O la falta de ellos!)

| Acción | Cómo Hacerlo |
|--------|-------------|
| 🚶 Avanzar | Automático - no hay control |
| 👀 Mirar alrededor | Mueve tu cabeza (VR) o cámara |
| 🎯 Recolectar objeto | Mira el objeto cian + **0.8 segundos** |
| 💫 Lanzar objeto | Mira el monstruo + **0.8 segundos** (con objeto en mano) |
| 📍 Apuntar | El cursor rojo indica exactamente dónde miras |

## 🎬 Flujo de Juego

```
INICIO
  ↓
Jugador aparece en (0, 1.6, 0)
  ↓
Comienza a caminar automáticamente
  ↓
[BUCLE PRINCIPAL]
├─ ¿Ves un objeto? → Mira 0.8s → ¡RECOLECTADO!
├─ ¿Ya tienes 3 objetos? → Avanza al monstruo
├─ ¿Ves el monstruo? + ¿Tienes objeto? → Mira 0.8s → ¡LANZADO!
└─ Repite hasta tener todos lanzados
  ↓
¿Has lanzado 3 objetos?
├─ SÍ → ✓✓✓ ¡VICTORIA! MONSTRUO VENCIDO
└─ NO → Continúa el juego
  ↓
FIN
```

## 🏗️ Stack Técnico

- **A-Frame 1.4.0** - Framework WebXR de Mozilla para VR web
- **JavaScript Vanilla** - Lógica pura del juego sin dependencias
- **Three.js** (bajo A-Frame) - Renderizado 3D WebGL
- **WebXR API** - Soporte para dispositivos VR reales

## 🚀 Cómo Jugar

### Requisitos
- 🥽 Casco VR (Meta Quest, HTC Vive, Valve Index, etc.)
- 🌐 Navegador moderno con soporte WebXR
- 📱 O emulación WebXR en desktop para pruebas

### Instrucciones de Inicio

1. **Descarga o clona el repositorio**
   ```bash
   git clone https://github.com/eduardogutierrezislas24-create/Hospital-loco09.git
   ```

2. **Abre el archivo `index.html` en tu navegador VR**
   - Desktop: Abre en cualquier navegador moderno
   - Meta Quest: Usa el navegador incorporado
   - PC VR: Abre mediante SteamVR

3. **Permite el acceso a tu dispositivo VR**
   - El navegador te pedirá permiso para usar tu headset

4. **¡Comienza a jugar!**
   - Pone tu headset
   - Mira los objetos para recoger
   - Elude al monstruo
   - ¡Derrótalo!

### Navegadores Compatibles

| Dispositivo | Navegador | Estado |
|------------|-----------|--------|
| Meta Quest 2/3 | Chrome/Firefox VR | ✅ Completo |
| Meta Quest Pro | Chrome/Firefox VR | ✅ Completo |
| HTC Vive | SteamVR Browser | ✅ Completo |
| Valve Index | SteamVR Browser | ✅ Completo |
| PlayStation VR | Browser PS VR | ✅ Compatible |
| Desktop (sin VR) | Emulador WebXR | ⚠️ Limitado |

## 🎨 Características Visuales

### Paleta de Colores
- **Fondo**: Negro profundo (#050505)
- **Paredes**: Verde oscuro (#2b332b)
- **HUD**: Verde neón (#00ff00) con resplandor
- **Objetos**: Cian brillante (contraste alto)
- **Monstruo**: Negro absoluto (misterio y miedo)
- **Mensajes**: Verde para éxito, Amarillo para acción

### Atmosfera
- **Niebla**: Reduce visibilidad más allá de 15 unidades
- **Spotlight**: Genera sombras dinámicas y drama
- **Texto monoespacio**: Efecto retro-futurista en HUD
- **Resplandor de texto**: "Text-shadow" neon para inmersión

## ⚙️ Personalización

### Aumentar Dificultad

**Reducir tiempo de mirada:**
```javascript
if (this.timer >= 500) { // Cambiar de 800 a 500ms
```

**Aumentar velocidad de movimiento:**
```javascript
pos.z -= 0.04; // Cambiar de 0.02 a 0.04
```

**Cambiar número de objetos:**
- Editar `itemsRecolectados === 3` → cambiar el 3
- Añadir más `<a-cylinder>` en el HTML

### Personalización Visual

**Colores de objetos:**
```html
<a-cylinder color="magenta" ... ></a-cylinder> <!-- cambiar color -->
```

**Posiciones de objetos:**
```html
<a-cylinder position="X Y Z" ... ></a-cylinder>
```

**Tamaño del monstruo:**
```html
<a-capsule radius="0.6" height="2.5" ...></a-capsule>
```

### Parámetros Clave del Juego

| Parámetro | Valor | Ubicación | Efecto |
|-----------|-------|-----------|--------|
| Tiempo de mirada | 800ms | Línea 73 | Cuánto miras antes de interactuar |
| Velocidad movimiento | 0.02 | Línea 67 | Qué tan rápido avanzas |
| Items requeridos | 3 | Línea 105 | Cuántos objetos necesitas |
| Distancia alcance | 10 | Línea 170 | A qué distancia puedes mirar cosas |
| Alcance niebla | 15 | Línea 162 | Visibilidad máxima |

## 🧠 Notas Técnicas

### Componente A-Frame `vrcorredor`

El corazón del juego es un componente personalizado que maneja:

```javascript
AFRAME.registerComponent('vrcorredor', {
  // 1. Inicialización: prepara variables de estado
  init: function() { ... }
  
  // 2. Loop de juego: ejecuta cada fotograma
  tick: function(time, timeDelta) {
    // Movimiento automático
    // Detección de mirada
    // Lógica de interacción
    // Actualización HUD
  }
  
  // 3. Helpers: funciones auxiliares
  updateHUD: function() { ... }
  addMessage: function() { ... }
})
```

### Sistema de Raycasting
- **Raycaster**: Lanza rayos desde la cámara del jugador
- **Intersección**: Detecta objetos con clase `.interactuable`
- **Tiempo**: Acumula duración de mirada constante

### Animaciones
- **Lanzamiento de objeto**: Movimiento de 300ms hacia el monstruo
- **Desaparición**: Objeto se vuelve invisible al recolectarse
- **Eliminación**: Monstruo se elimina al ser derrotado

## 📝 Estructura de Archivos

```
Hospital-loco09/
├── 📄 README.md           ← Documentación (este archivo)
├── 🎮 index.html          ← Juego completo en un solo archivo
└── 📸 (opcional) screenshot.png
```

## 🎓 Conceptos de Diseño

### ¿Por qué solo mirada?

1. **Inmersión total** - Ningún controlador distrae tu visión
2. **Accesibilidad** - Funciona con cualquier dispositivo VR
3. **Simplicidad** - Una mecánica clara y profunda
4. **Presencia** - Tu cabeza es el único personaje

### Tensión por Movimiento Automático

- **No puedes retrasar** - Avanzas sin control
- **Decisiones rápidas** - ¿Recolectar ahora o esperar?
- **Punto de no retorno** - Una vez pasas un objeto, no vuelves

## 🔧 Troubleshooting

### "No veo nada"
- Verifica que tu navegador soporta WebXR
- En desktop, usa la emulación WebXR del navegador

### "La mirada no funciona"
- Asegúrate de estar mirando directamente al objeto (cursor rojo sobre él)
- Espera los 0.8 segundos completos sin mover la vista

### "El monstruo no desaparece"
- Confirma que has lanzado exactamente 3 objetos
- Verifica los mensajes en el HUD

## 🚀 Mejoras Futuras Posibles

- 🎵 Sonido envolvente y música ambiental
- 👹 Monstruos móviles que persiguen
- 🔊 Audio 3D espacializado
- 🏆 Sistema de puntuación y tiempos
- 🌙 Múltiples niveles/escenarios
- 💥 Efectos de partículas al lanzar
- 📱 Soporte para teléfono móvil (cardboard)

## 📜 Licencia

Proyecto de código abierto - Libre para usar con fines educativos y no comerciales

## 🙏 Créditos

- **Construido con** [A-Frame](https://aframe.io/) por Mozilla
- **Motor 3D** [Three.js](https://threejs.org/)
- **Especificación** [WebXR](https://www.w3.org/TR/webxr/) del W3C

---

**Última actualización**: Mayo 2026  
**Versión**: 1.0  
**Estado**: ✅ Jugable y funcional

*Recuerda: En este hospital, solo tus ojos pueden salvarte. ¡Buena suerte!* 👁️

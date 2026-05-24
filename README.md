# Hospital Psiquiátrico VR

A WebXR/VR game built with A-Frame where players navigate through a psychiatric hospital hallway, collect objects, and defend against a monster.

## Overview

This is an immersive VR experience that challenges players to:
1. **Automatically walk forward** through a procedural hallway
2. **Collect objects** by gazing at cyan cylinders for 0.8 seconds
3. **Defeat the monster** at the end by throwing all 3 collected objects at it

## Game Mechanics

### Movement
- **Automatic forward movement** - Players continuously walk toward the monster at a steady pace
- No manual movement controls required

### Interaction System
- **Gaze-based interactions** - Look at objects for 0.8 seconds to interact
- **Visual feedback** - Timer bar fills up as you stare
- **HUD display** - Shows object count and hand status

### Objectives
1. Collect all 3 cyan items scattered throughout the hallway
2. Navigate to the monster (black capsule at position z: -18)
3. Throw all objects at the monster to win

## HUD Elements

- **OBJETOS** - Current item count (0/3)
- **EN MANO** - Whether you're holding an item (✓/✗)
- **Timer Bar** - Visual indicator of gaze duration
- **Messages** - Dynamic feedback for actions

## Technical Stack

- **A-Frame** v1.4.0 - WebXR framework
- **Vanilla JavaScript** - Core game logic
- **HTML5/CSS3** - UI and styling

## File Structure

```
Hospital-loco09/
├── README.md          (this file)
└── index.html         (complete game implementation)
```

## Running the Game

1. Clone the repository or download the file
2. Open `index.html` in a WebXR-capable browser
3. Allow access to your headset/motion controllers
4. Start the experience!

### Browser Compatibility

- Meta Quest (via WebXR)
- HTC Vive (via WebXR)
- Valve Index (via WebXR)
- Desktop VR with controllers
- Some desktop browsers with WebXR emulation

## Game Features

### Environment
- Dark atmospheric hallway with fog effect
- Bordered corridor with walls and ceiling
- Persistent blue floor

### Interactive Elements
- **3 Collectible Items** - Cyan cylinders at various positions:
  - Position 1: (-0.8, 0.2, -4)
  - Position 2: (0.5, 0.2, -8)
  - Position 3: (-0.3, 0.2, -12)
- **Monster** - Black capsule enemy at (0, 1, -18)

### Lighting
- Spotlight attached to player's camera
- Dynamic illumination of the scene

## Controls

| Action | Control |
|--------|---------|
| Move Forward | Automatic |
| Look Around | Head/Controller Movement |
| Interact | Gaze for 0.8 seconds |
| Throw Object | Gaze at monster for 0.8 seconds |

## Game Flow

1. **Start** - Player begins at position (0, 1.6, 0) and moves forward
2. **Collection Phase** - Stare at cyan items to collect them
3. **Combat Phase** - Reach the monster and throw objects
4. **Victory** - Monster is defeated after throwing all 3 items

## Customization

You can easily modify:
- **Movement speed** - Change the `0.02` value in the `tick()` function
- **Interaction time** - Modify `800` (milliseconds) to change gaze duration
- **Object positions** - Edit the `<a-cylinder>` position attributes
- **Colors** - Change hex color values throughout the scene

## Development Notes

The core game logic is implemented as an A-Frame component called `vrcorredor` that manages:
- Automatic player movement
- Raycasting for gaze-based selection
- Item collection state
- Monster defeat conditions
- HUD updates

## License

Open source - feel free to modify and use for educational purposes

## Credits

Built with [A-Frame](https://aframe.io/) by Mozilla

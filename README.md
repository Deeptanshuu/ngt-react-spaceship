I'll document the entire project component by component, explaining their roles and key features:

# Project Documentation

## Core Components

### 1. `Experience.tsx` - Main Scene Controller
The root component that orchestrates the entire 3D scene.

Key features:
- Scene setup with Canvas, lighting, and post-processing
- Keyboard event handling for turbo mode
- Component composition and state management

Sub-components:

#### a. `DynamicEnvMap`
```typescript
// Creates dynamic environment mapping for realistic reflections
- Uses PMREM (Prefiltered, Mipmapped Radiance Environment Map)
- Temporarily hides spaceship to capture environment
- Applies high-intensity reflections (envMapIntensity: 100)
- Updates every frame for real-time reflections
```

#### b. `CameraRig`
```typescript
// Handles camera movement and transitions
- Base position: (-4, 4, 6) with FOV 40°
- Turbo position: (5, 1, 1) with FOV 55°
- Smooth transitions using lerp
- Dynamic FOV adjustment during turbo
```

#### c. `MousePlane`
```typescript
// Invisible plane for mouse interaction
- Tracks mouse movement for ship control
- Disables input during turbo mode
- Converts mouse position to 3D coordinates
```

#### d. `SpaceshipController`
```typescript
// Handles spaceship movement and physics
- Smooth acceleration and damping
- Position bounds: ±3 units vertical
- Rotation bounds: ±45 degrees
- Auto-centering during turbo mode
- Separate handling for normal/turbo states
```

### 2. `Spaceship.tsx` - Spaceship Model and Effects
Handles the spaceship's visual appearance and animations.

```typescript
Key features:
- GLTF model loading and material setup
- Material properties:
  - Metalness: 0.8
  - Roughness: 0.3
  - Dynamic environment mapping
- Visual effects:
  - Cockpit glow (emissive)
  - Energy beam
  - Engine glow
- Animations:
  - Hover effect
  - Turbo shake effect
  - Enhanced glow during turbo
```

### 3. `Stars.tsx` - Background Star System
Creates and manages the dynamic star field.

```typescript
Key features:
- Uses instanced rendering for performance
- 250 stars with varying:
  - Colors: ['#fcaa67', '#c75d59', '#ffffc7', '#8cc5c6', '#a5898c']
  - Sizes: 1.5-20 units
  - Speeds: 19.5-42 units/s
- Dynamic speed adjustment during turbo
- Automatic star recycling
```

### 4. `MotionBlur.tsx` - Custom Post-Processing
Custom motion blur effect for enhanced visuals.

```typescript
Key features:
- Custom shader implementation
- Direction-based blur
- Intensity linked to turbo state
- Randomized sampling for natural look
```

### 5. `LoadingScreen.tsx` - Loading Interface
Handles asset loading and initial user experience.

```typescript
Key features:
- Progress tracking
- Animated star background
- Loading percentage display
- Asset count display
```

## Technical Features

### 1. Performance Optimizations
```typescript
- Instanced rendering for stars
- Efficient material/texture reuse
- Performance-based DPR scaling
- Frustum culling
```

### 2. Visual Effects
```typescript
- Dynamic environment mapping
- Motion blur
- Chromatic aberration
- Bloom effect
- Custom blending modes
```

### 3. Controls
```typescript
Normal Mode:
- Mouse movement for steering
- Bounded vertical movement (±3 units)
- Limited rotation (±45 degrees)
- Smooth acceleration/deceleration

Turbo Mode:
- Activated by Space key
- Disabled steering
- Auto-centering
- Enhanced visual effects
- Camera position shift
```

### 4. Camera System
```typescript
Base View:
- Position: (-4, 4, 6)
- FOV: 40°
- Look target: (0, 0, 0)

Turbo View:
- Position: (5, 1, 1)
- FOV: 55°
- Look target: (-5, 0, 0)
```

### 5. Material System
```typescript
Spaceship:
- MeshStandardMaterial with custom properties
- Dynamic environment mapping
- Enhanced reflections
- Custom alpha handling

Effects:
- Custom shaders for motion blur
- Specialized materials for energy beam
- Emissive materials for engine glow
```

This documentation provides a comprehensive overview of the project's structure and functionality. Each component is designed to work together to create a cohesive and interactive 3D space flight experience.

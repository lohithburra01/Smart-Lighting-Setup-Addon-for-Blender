# Smart Lighting Setup

A Blender addon that creates scale-aware lighting setups with automated positioning, energy calculation, and false color preview for professional 3D workflows.

<img width="729" height="731" alt="Screenshot 2025-04-30 011151" src="https://github.com/user-attachments/assets/56ead048-49d8-489d-a62a-ec87fcf66b76" />
<img width="729" height="730" alt="Screenshot 2025-04-30 011333" src="https://github.com/user-attachments/assets/7231fb94-8ca1-403f-b881-a42bfd8dd0ff" />
<img width="729" height="728" alt="Screenshot 2025-04-30 011651" src="https://github.com/user-attachments/assets/f23ddc7b-d5e2-4be0-a29a-82a0e973be75" />
<img width="729" height="727" alt="Screenshot 2025-04-30 011733" src="https://github.com/user-attachments/assets/174d550a-a3a4-4ff0-aafe-9e8b806a547e" />
<img width="728" height="730" alt="Screenshot 2025-04-30 012328" src="https://github.com/user-attachments/assets/1281e975-50aa-417e-a0c3-d412fe60bc3a" />
<img width="725" height="725" alt="Screenshot 2025-04-30 011835" src="https://github.com/user-attachments/assets/7adb5735-1685-41e9-98cd-4888bab2d890" />

## Overview

This addon eliminates the tedious process of manually setting up lighting for different object scales and types. Instead of spending time positioning lights and adjusting energy levels, you get mathematically calculated setups that adapt to your object's dimensions and camera position.

## Features
<img width="313" height="800" alt="image" src="https://github.com/user-attachments/assets/51fb669d-11d3-4c3d-b24c-098afaa7f7e0" />

### Scale-Aware Automation
- **Dynamic distance calculation**: Automatically positions lights based on object dimensions
- **Energy scaling**: Calculates optimal light energy using inverse square law principles
- **Camera-relative positioning**: Lights follow camera movement and orientation
- **Dimension analysis**: Analyzes object bounding box for precise scaling

### Lighting Presets
- **Three-Point**: Classic key, fill, and back light setup
- **Two-Point**: Key + fill or key + back light combinations
- **Single-Point**: Dramatic single light with multiple positioning options
- **Product**: Multi-angle setup optimized for product photography
- **Cinematic**: High-contrast dramatic lighting
- **Apple Style**: Clean, edge-lit aesthetic with rim lighting

### Advanced Controls
- **Individual light control**: Fine-tune each light independently
- **Shadow softness**: Automatic shadow size calculation based on distance
- **Color temperature**: Unified color control across all lights
- **False color preview**: Toggle false color view for exposure analysis
- **Live updates**: Real-time light adjustment as you modify objects

### Professional Features
- **Contact shadows**: Automatic contact shadow setup (when supported)
- **Exposure adjustment**: Global exposure control without changing individual settings
- **Version compatibility**: Handles API differences across Blender versions
- **State management**: Preserves view settings when toggling false color

## Installation

1. Download the addon file
2. In Blender: Edit > Preferences > Add-ons > Install
3. Select the downloaded file and enable the addon
4. Find the panel in 3D Viewport > N-Panel > "Smart Lighting"

## Usage

### Basic Setup

1. **Select target object**: Choose the mesh you want to light
2. **Choose lighting type**: Select from six professional presets
3. **Configure placement**: Adjust camera follow and positioning options
4. **Click "Create Lighting Setup"**: Lights are automatically positioned and scaled

### Advanced Configuration

**Scale Settings**:
- **Distance Factor**: Multiplier for light distance (0.5-5.0)
- **Falloff Factor**: Controls energy falloff calculation (0.1-5.0)
- **Base Energy**: Starting energy value before scaling (1-1000)

**Light Properties**:
- **Color**: Unified color control for all lights
- **Shadow Softness**: Automatic shadow size based on distance
- **Contact Shadows**: Enhanced shadow detail (when available)

**Workflow Controls**:
- **Camera Follow**: Lights automatically reposition when camera moves
- **Individual Control**: Switch to per-light adjustment mode
- **False Color**: Toggle false color view for exposure analysis

## Technical Implementation

### Distance Calculation
```python
def calculate_light_distance(obj, factor=1.5):
    dimensions = get_object_dimensions(obj)
    return max(dimensions) * factor
```

### Energy Scaling
Uses modified inverse square law:
```python
def calculate_light_energy(distance, base_energy=100.0, falloff_factor=1.0):
    return base_energy * (1 + (distance * falloff_factor))
```

### Camera-Relative Positioning
```python
def get_camera_direction():
    # Gets camera or viewport direction vectors
    cam_pos, cam_dir = get_camera_info()
    # Calculates right and up vectors for positioning
    return calculate_coordinate_system(cam_pos, cam_dir)
```

### Lighting Algorithms

**Three-Point Setup**:
- Key light: 45° angle, high energy
- Fill light: Opposite side, 50% energy, larger size
- Back light: Behind object, 75% energy, rim effect

**Product Setup**:
- Top light: Overhead soft illumination
- Front light: Main product visibility
- Side lights: Edge definition and separation

**Apple Style**:
- Clean main light with subtle shadows
- Sharp edge lights for product definition
- Soft fill light for shadow detail

### API Compatibility
Handles Blender version differences:
```python
def apply_light_settings(light, props, distance):
    # Check for contact shadow support
    if hasattr(light, 'use_contact_shadow'):
        light.use_contact_shadow = props.use_contact_shadows
```

## Lighting Theory

### Distance-Energy Relationship
The addon implements proper photometric principles:
- Light energy increases with distance to maintain consistent illumination
- Shadow softness scales proportionally to maintain realistic appearance
- Size relationships preserved across different object scales

### Professional Ratios
Based on cinematography standards:
- Key:Fill ratio typically 2:1 for product work
- Back light at 75% of key for separation
- Rim lights at 150% for edge definition

### Color Temperature Workflow
- Unified color control maintains consistency
- False color preview helps identify exposure issues
- Individual override available for creative control

## Use Cases

- **Product Photography**: Consistent lighting across different product scales
- **Architectural Visualization**: Proper lighting for interior and exterior scenes  
- **Character Lighting**: Portrait and full-body lighting setups
- **Motion Graphics**: Quick lighting for animated objects
- **Educational Content**: Teaching lighting principles with live feedback

## Camera Integration

### Automatic Following
- Lights reposition when camera moves
- Maintains relative angles and distances
- Preserves lighting ratios during camera animation

### Manual Override
- Toggle camera following for static setups
- Individual light control for fine-tuning
- Maintains automatic scaling while allowing creative adjustments

## Performance Optimization

- **Efficient updates**: Only recalculates when objects change
- **Minimal overhead**: Lightweight update handlers
- **Smart caching**: Avoids redundant calculations
- **Clean collections**: Organized light management

## Error Handling

- **Object validation**: Checks for valid mesh objects
- **API compatibility**: Graceful handling of missing features
- **State preservation**: Maintains settings across sessions
- **User feedback**: Clear error messages and suggestions

## Requirements

- Blender 4.0+ (with backward compatibility for 3.6+)
- Target object must be a mesh
- Render engine supporting area lights

## Workflow Integration

Complements other production tools:
- **Camera arrays**: Consistent lighting across multiple viewpoints
- **Animation**: Lights follow animated cameras automatically
- **Render layers**: Supports multi-layer rendering workflows
- **Compositing**: False color output for post-production analysis

## Advanced Features

### Handler System
- Automatic updates when objects are modified
- Preserves light relationships during mesh editing
- Efficient depsgraph integration

### Collection Management
- Organized light hierarchy
- Easy selection and manipulation
- Clean scene outliner integration

### State Management
- Preserves view settings
- Handles false color toggle states
- Maintains user preferences

## Development Notes

Built with production workflows in mind:
- Modular light creation functions
- Extensible preset system
- Clean separation of UI and logic
- Comprehensive error handling

## Blender Version Compatibility

- Primary target: Blender 4.0+
- Tested compatibility: 3.6+ with graceful feature degradation
- API adaptation: Handles deprecated properties automatically
- Future-proof: Modern addon architecture patterns

## License

MIT License - feel free to modify and distribute.

## Author

Built by Lohith Burra - Technical Artist specializing in automated lighting workflows for broadcast and product visualization.

## Contributing

Issues and pull requests welcome. Please include:
- Blender version
- Object type and scale
- Lighting setup used
- Screenshots of unexpected behavior

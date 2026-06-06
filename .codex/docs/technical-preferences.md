# Technical Preferences

## Engine & Language

- **Engine**: Godot 4.x; pin the exact version with `/setup-engine`
- **Language**: GDScript
- **Build System**: Godot Export Templates
- **Asset Pipeline**: Godot Import System + custom resource pipeline
- **Primary Project Type**: [TO BE CONFIGURED BY CURRENT PROJECT]

> **Mutable design note**: genre, 2D/3D, camera, input method, platform,
> renderer bias, art style, and project-specific technical notes are current
> project facts only. They must be read from this file and current concept/GDD,
> art, UX, or architecture artifacts. Do not treat them as framework defaults.

## Naming Conventions

- **Classes**: PascalCase, for example `GameController`
- **Variables and Functions**: snake_case, for example `current_state` and `set_state()`
- **Signals**: snake_case past tense, for example `state_changed`
- **Files**: snake_case matching class or feature, for example `game_controller.gd`
- **Scenes**: PascalCase matching root node, for example `MainScene.tscn`
- **Constants**: UPPER_SNAKE_CASE, for example `MAX_ACTIVE_ITEMS`
- **Private Members**: underscore prefix, for example `_current_state`

## Input & Platform

- **Target Platforms**: [TO BE CONFIGURED BY CURRENT PROJECT]
- **Input Methods**: [TO BE CONFIGURED BY CURRENT PROJECT]
- **Primary Input**: [TO BE CONFIGURED BY CURRENT PROJECT]
- **Gamepad Support**: [TO BE CONFIGURED BY CURRENT PROJECT]
- **Touch Support**: [TO BE CONFIGURED BY CURRENT PROJECT]
- **Platform Notes**: Read the current concept, UX specs, and target platform before making input or UI assumptions.

## Performance Budgets

- **Target Frame Rate**: 60fps
- **Frame Budget**: 16.6ms
- **Renderer Bias**: [TO BE CONFIGURED BY CURRENT PROJECT]
- **CPU Budget Notes**: [TO BE CONFIGURED BY CURRENT PROJECT]
- **GPU Budget Notes**: [TO BE CONFIGURED BY CURRENT PROJECT]

## Testing

- **Recommended Framework**: GUT or gdUnit4 after the Godot project is initialized
- **Manual Test Focus**: [TO BE CONFIGURED BY CURRENT PROJECT]
- **Automation Priority**: [TO BE CONFIGURED BY CURRENT PROJECT]

## Forbidden Patterns

[TO BE CONFIGURED]

## Allowed Libraries

[TO BE CONFIGURED]

## Engine Specialists

- **Primary**: godot-specialist
- **Language/Code Specialist**: godot-gdscript-specialist (all .gd files)
- **Shader Specialist**: godot-shader-specialist (.gdshader files, VisualShader resources)
- **UI Specialist**: godot-specialist (no dedicated UI specialist; primary covers Godot UI architecture)
- **Additional Specialists**: godot-gdextension-specialist (GDExtension / native C++ bindings only)
- **Routing Notes**: Invoke primary for architecture decisions, ADR validation, scene/node structure, export setup, and cross-cutting code review. Invoke GDScript specialist for code quality, signal architecture, static typing, and GDScript idioms. Invoke shader specialist for materials, VFX, and rendering. Invoke GDExtension specialist only after profiling proves native code is needed.

### File Extension Routing

| File Extension / Type | Specialist to Spawn |
| --- | --- |
| Game code (.gd files) | godot-gdscript-specialist |
| Shader / material files (.gdshader, VisualShader) | godot-shader-specialist |
| UI / screen files (Control nodes, CanvasLayer) | godot-specialist |
| Scene / prefab / level files (.tscn, .tres) | godot-specialist |
| Native extension / plugin files (.gdextension, C++) | godot-gdextension-specialist |
| General architecture review | godot-specialist |

## Project-Specific Technical Notes

[TO BE CONFIGURED BY CURRENT PROJECT]

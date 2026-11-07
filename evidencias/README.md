# Evidencias de Validación Técnica y Jugable — MaskDude

Este directorio almacena los registros de validación empírica y pruebas ejecutadas sobre el proyecto **MaskDude** en **Godot 4.5**.

## 1. Archivos Disponibles

- **`REPORTE_PRUEBAS.md`**: Reporte formal de ejecución de la suite de pruebas unitarias mediante el framework **GUT 9.5.0 (Godot Unit Test)** en modo *headless*.
  - **Total de pruebas ejecutadas:** 61 pruebas.
  - **Fallos registrados:** 0 fallos.
  - **Módulos validados:** Máquina de estados del jugador (`MaskDude.gd`), sistema de recolección de frutas (`Fruit.gd`), input map, estructura de datos narrativos (`Story.gd`), interfaz de diálogos (`DialogueBox.gd`) y flujo del nivel (`Level1.gd`).
- **`preview_nivel1.gif`**: Registro visual animado de la ejecución en tiempo real de `Level1.tscn` que demuestra las mecánicas de desplazamiento, doble salto, plataformas colapsables/unidireccionales y recolección de frutas.

## 2. Criterios de Validación Observable

1. **Pruebas de Estado:** La transición entre estados (`IDLE`, `RUN`, `JUMP`, `FALL`, `DOUBLE_JUMP`, `DASH`, `LOCKED`) está verificada por `test_mask_dude.gd`.
2. **Pruebas de Narrativa:** El bloqueo del input durante cinemáticas y diálogos (`set_locked(true)`) está verificado por `test_dialogue_box.gd` y `test_story.gd`.
3. **Pruebas de Nivel:** La recolección de las 13 frutas y el disparo de la condición de victoria en la meta (`Goal`) están verificados por `test_zz_level1.gd`.

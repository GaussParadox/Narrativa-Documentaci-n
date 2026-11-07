# Índice de Entregables Narrativos — MaskDude

Este directorio consolida los seis entregables académicos correspondientes al taller **«Historia, guion y storyboard»** de la asignatura **Diseño Multimedia y Videojuegos** (9.º semestre, FESC), basados estrictamente en el videojuego **MaskDude** desarrollado en **Godot Engine 4.5**.

---

## 1. Tabla de Entregables y Acceso Rápido

| Entregable | Archivo Principal | Descripción del Contenido | Estado Técnico |
| :---: | :--- | :--- | :---: |
| **Entregable 1** | [01_premisa_personajes.md](01_premisa_personajes.md) | Logline oficial, ficha de Mask Dude, conflicto comunal, tradición milenaria, límites motrices y preservación del misterio de los antecesores. | **Completo / Verificado** |
| **Entregable 2** | [02_estructura_curva.md](02_estructura_curva.md) | Estructura en tres actos, tabla de 6 beats (B1 a B6), justificación de tensión vs dificultad, respiro táctico en B4 y ciclo de reintento. | **Completo / Verificado** |
| **Gráfica E2** | [curva_tension.png](curva_tension.png) | Gráfico exportado de la curva de tensión con escala cualitativa de 1 a 5 y beats B1 a B6. | **Generado / Exportado** |
| **Entregable 3** | [03_guion_jugable.md](03_guion_jugable.md) | Guion interactivo de `ESC-01: Introducción` y `ESC-02: Clímax`, especificando triggers, `State.LOCKED`, respuestas del sistema y 3 variantes de final. | **Completo / Verificado** |
| **Entregable 4** | [04_storyboard.pdf](04_storyboard.pdf) | Storyboard formal multipágina con 6 viñetas (V01 a V06) en proporción 16:9, cámara, acción, audio y distinción de control. | **Generado / Exportado** |
| **Fuentes E4** | [editables/README.md](editables/README.md)<br>[fuentes_del_storyboard.svg](editables/fuentes_del_storyboard.svg) | Archivos fuente vectoriales editables para Krita e Inkscape. | **Disponible** |
| **Entregable 5** | [05_mapa_godot_assets.md](05_mapa_godot_assets.md) | Árboles de nodos reales de Godot 4.5 (`World.tscn`, `Level1.tscn`, `MaskDude.tscn`), recurso `SpriteFrames`, aclaración de `Level_Large.tscn` e inventario de licencias. | **Completo / Verificado** |
| **Entregable 6** | [06_trazabilidad.md](06_trazabilidad.md) | Matriz unívoca Historia (`HIS`) $\rightarrow$ Requisito (`RF`) $\rightarrow$ Escena (`ESC`) $\rightarrow$ Prueba (`PR`) respaldada por 61 pruebas unitarias en GUT. | **Completo / Verificado** |

---

## 2. Directrices Metodológicas Cumplidas

1. **Restricción de Alcance:** Este repositorio no contiene código fuente ejecutable ni escenas `.tscn`.
2. **Cero Suposiciones Ficticias:** Todos los comportamientos documentados provienen de la inspección técnica real del proyecto en Godot 4.5.
3. **Misterio Narrativo Preservado:** Se mantiene intacta la incógnita sobre el destino de los antiguos hombres enmascarados, conforme a las directrices de diseño.
4. **Viabilidad Técnica Garantizada:** Uso exclusivo de clases nativas vigentes de Godot 4.5 (`CharacterBody2D`, `Area2D`, `TileMapLayer`, `Camera2D`, etc.).

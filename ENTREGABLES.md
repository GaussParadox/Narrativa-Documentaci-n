# Resumen de Entregables — MaskDude: El Festín del Tótem

> Taller: Historia del juego, guion jugable y storyboard  
> Asignatura: Diseño Multimedia y Videojuegos — FESC  
> Motor: Godot 4.5 | Género: Plataformas 2D Pixel Art

---

## Estado de entregables

| # | Entregable | Archivo | Estado |
|---|-----------|---------|--------|
| 1 | Premisa y personajes | [`docs/narrativa/01_premisa_personajes.md`](docs/narrativa/01_premisa_personajes.md) | ✅ Completo |
| 2 | Estructura narrativa y curva de tensión | [`docs/narrativa/02_estructura_curva.md`](docs/narrativa/02_estructura_curva.md) | ✅ Completo |
| 2b | Curva de tensión (gráfica) | [`docs/narrativa/curva_tension.png`](docs/narrativa/curva_tension.png) | ✅ Generada |
| 3 | Guion jugable (ESC-01 y ESC-02) | [`docs/narrativa/03_guion_jugable.md`](docs/narrativa/03_guion_jugable.md) | ✅ Completo |
| 4 | Storyboard (6 viñetas ilustradas) | [`docs/narrativa/04_storyboard.pdf`](docs/narrativa/04_storyboard.pdf) | ✅ Completo |
| 5 | Mapa técnico Godot y lista de assets | [`docs/narrativa/05_mapa_godot_assets.md`](docs/narrativa/05_mapa_godot_assets.md) | ✅ Completo |
| 6 | Matriz de trazabilidad | [`docs/narrativa/06_trazabilidad.md`](docs/narrativa/06_trazabilidad.md) | ✅ Completo |
| — | Lista de chequeo de calidad | [`LISTA_DE_CHEQUEO.md`](LISTA_DE_CHEQUEO.md) | ✅ 10/10 criterios |

---

## Ilustraciones del storyboard

Las siguientes ilustraciones en pixel art fueron generadas para el storyboard y se encuentran disponibles como editables:

| Viñeta | Escena | Momento narrativo | Archivo |
|--------|--------|-------------------|---------|
| V01 | ESC-01 | El hombre enmascarado en el portal de entrada | [`editables/v01_ilustracion.png`](docs/narrativa/editables/v01_ilustracion.png) |
| V02 | ESC-01 | Primer salto sobre la plataforma inicial | [`editables/v02_ilustracion.png`](docs/narrativa/editables/v02_ilustracion.png) |
| V03 | ESC-01 | Recolección de la primera fruta | [`editables/v03_ilustracion.png`](docs/narrativa/editables/v03_ilustracion.png) |
| V04 | ESC-02 | Señal del Tótem Guardián en la plataforma central | [`editables/v04_ilustracion.png`](docs/narrativa/editables/v04_ilustracion.png) |
| V05 | ESC-02 | Clímax — entrega de las frutas al Guardián | [`editables/v05_ilustracion.png`](docs/narrativa/editables/v05_ilustracion.png) |
| V06 | ESC-02 | Cierre — el hombre enmascarado desaparece | [`editables/v06_ilustracion.png`](docs/narrativa/editables/v06_ilustracion.png) |

---

## Historial de commits

```
commit 1  docs: add game premise and characters
commit 2  docs: add narrative structure and tension curve
commit 3  docs: add playable script and storyboard
commit 4  docs: add Godot technical map
commit 5  docs: add traceability matrix
commit 6  docs: finalize quality checklist and project presentation
commit 7  docs: add pixel art illustrations to storyboard vignettes V01-V06
commit 8  docs: add deliverables summary and repository index
```

---

## Datos técnicos verificados

| Elemento | Valor confirmado |
|---------|-----------------|
| Escena principal | `scenes/world/World.tscn` |
| Escena del jugador | `scenes/player/MaskDude.tscn` |
| Nivel jugable | `scenes/levels/Level1.tscn` |
| Total de frutas en Nivel 1 | **13 frutas** |
| Punto de inicio | Coordenadas (64, 155) |
| Ubicación del Tótem | Coordenadas (436, 123) |
| Recurso de animaciones | `MaskDudeFrames.tres` (tipo: SpriteFrames, 7 animaciones) |
| Framework de pruebas | GUT — 61 tests, 0 fallos |
| Escena de prueba interna | `Level_Large.tscn` (no es nivel jugable) |

---

*Repositorio generado con base en inspección directa del proyecto Godot 4.5.*  
*Todos los datos técnicos han sido verificados en el código fuente original.*

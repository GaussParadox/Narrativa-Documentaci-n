# Entregable 6: Matriz de Trazabilidad — MaskDude

> **Asignatura:** Diseño Multimedia y Videojuegos · 9.º Semestre  
> **Institución:** Fundación de Estudios Superiores Comfanorte (FESC)  
> **Proyecto:** MaskDude — *El Festín del Tótem*  
> **Motor:** Godot Engine 4.5  
> **Framework de Pruebas:** GUT 9.5.0 (61 pruebas unitarias sin fallos)  
> **Estado del Entregable:** Completo y Verificado

---

## 1. Convención de Nomenclatura Unívoca

Para garantizar que cada decisión narrativa tenga un correlato funcional en el motor y una verificación observable, se establece la siguiente codificación estricta:

- **`HIS-xx`**: Elemento o acontecimiento de la historia y premisa narrativa.
- **`RF-xx`**: Requisito funcional de software / comportamiento exigido al motor.
- **`ESC-xx`**: Escena dramática del guion (`ESC-01` Intro, `ESC-02` Clímax).
- **`PR-xx`**: Prueba unitaria automatizada (GUT) o prueba de integración observable.
- **`EVID-xx`**: Archivo comprobable de registro (captura, reporte de pruebas o gif).

Cadena de trazabilidad:
$$\text{HIS-xx} \longrightarrow \text{RF-xx} \longrightarrow \text{ESC-xx} \longrightarrow \text{PR-xx} \longrightarrow \text{EVID-xx} \longrightarrow \text{Estado}$$

---

## 2. Matriz Maestra de Trazabilidad

| ID Historia | Elemento Narrativo | Requisito Funcional (RF) | Escena / Nodo Godot 4.5 | Prueba Verificable | Archivo de Evidencia | Estado Real |
| :---: | :--- | :--- | :--- | :--- | :--- | :---: |
| **HIS-01** | La aldea celebra el ritual del Festín pero las frutas escapan y el Tótem se apaga. | **RF-01:** El sistema debe presentar una cinemática de tarjetas sobre fondo negro bloqueando el control del jugador. | `ESC-01`<br>`World.tscn`<br>`Cinematic/Card` (`Label`) | `PR-01:` Validar que el jugador inicia en `State.LOCKED` y no responde a inputs horizontales.<br>*GUT:* `test_dialogue_box.gd` | `evidencias/REPORTE_PRUEBAS.md`<br>Línea 23 | **Implementado** |
| **HIS-02** | El Guardián de la Cosecha presta los dones sagrados del doble salto y el dash. | **RF-02:** El personaje debe ejecutar un segundo impulso aéreo (`double_jump`) y un impulso horizontal rápido (`dash`) con estela de imágenes fantasma. | `ESC-01/02`<br>`MaskDude.tscn`<br>`CharacterBody2D` (`MaskDude.gd`) | `PR-02:` Verificar que `_air_jumps_left` decrece a 0 al saltar en el aire y se recarga al tocar suelo.<br>*GUT:* `test_mask_dude.gd` | `evidencias/REPORTE_PRUEBAS.md`<br>Líneas 48-60 | **Implementado** |
| **HIS-03** | El protagonista debe recolectar las 13 frutas flotantes repartidas por la cámara. | **RF-03:** Cada fruta instanciada (`Area2D`) debe detectar la colisión exclusiva con el jugador, sumar al contador global y desaparecer con animación. | `ESC-01/02`<br>`Level1.tscn`<br>`Fruits` (13 instancias de `Fruit.tscn`) | `PR-03:` Comprobar que colisionar con una fruta emite la señal `collected` una sola vez y actualiza el HUD.<br>*GUT:* `test_fruit.gd` y `test_zz_level1.gd` | `evidencias/REPORTE_PRUEBAS.md`<br>Líneas 34, 88, 92 | **Implementado** |
| **HIS-04** | La travesía exige cruzar el abismo central mediante plataformas suspendidas. | **RF-04:** Las plataformas `Hover1..4` deben poseer colisión unidireccional (`one_way_collision = true`) y caer al vacío debe activar la reaparición segura. | `ESC-01/02`<br>`Level1.tscn`<br>`Hover1..4` (`StaticBody2D`) | `PR-04:` Caer por debajo del umbral de muerte ($Y > \text{límite} + 48$) emite `player_fell` y reposiciona al jugador en `SpawnPoint`.<br>*GUT:* `test_zz_level1.gd` | `evidencias/REPORTE_PRUEBAS.md`<br>Línea 94 | **Implementado** |
| **HIS-05** | En el mirador oriental, el Guardián alienta al elegido antes de la entrega final. | **RF-05:** El área `Trigger_totem_midway` debe disparar el diálogo intermedio una única vez y congelar temporalmente el movimiento. | `ESC-02`<br>`Level1.tscn`<br>`Trigger_totem_midway` (`Area2D`) | `PR-05:` Comprobar que la señal `triggered("totem_midway")` ejecuta `dialogue.play()` y desactiva el monitoreo posterior.<br>*GUT:* `test_story.gd` | `evidencias/REPORTE_PRUEBAS.md`<br>Línea 91 | **Implementado** |
| **HIS-06** | Juicio de la ofrenda: el Tótem evalúa el tributo y reacciona con tres finales posibles. | **RF-06:** Colisionar con el altar (`Goal`) debe detener la música, reproducir el jingle de victoria, modular el brillo del Tótem según las frutas recogidas y desplegar el epílogo. | `ESC-02`<br>`Level1.tscn`<br>`Goal` (`Area2D`) | `PR-06:` Validar emisión de `level_completed`, cálculo del brillo proporcional y bifurcación correcta en `Story.ending_lines()`.<br>*GUT:* `test_story.gd` y `test_zz_level1.gd` | `evidencias/REPORTE_PRUEBAS.md`<br>Líneas 81-84, 93 | **Implementado** |
| **HIS-07** | El destino de los hombres enmascarados anteriores se mantiene como enigma. | **RF-07:** La pantalla final debe cerrar con la frase de epílogo y las estadísticas sin alterar ni revelar el misterio canónico. | `ESC-02`<br>`World.tscn`<br>`Cinematic/Card` | `PR-07:` Verificación de coherencia del texto de cierre en `Story.epilogue()` para las tres variantes de recolección.<br>*GUT:* `test_story.gd` | `evidencias/REPORTE_PRUEBAS.md`<br>Líneas 82-84 | **Implementado** |

---

## 3. Matriz de Coherencia Bidireccional

### De la Historia al Código:
- La premisa de una **ofrenda sagrada** se materializa en la clase [`Fruit.gd`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/scripts/items/Fruit.gd) y el contador `fruit_collected` de [`Level1.gd`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/scripts/levels/Level1.gd).
- La condición de **elegido ritual** se traduce en las mecánicas consagradas en [`MaskDude.gd`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/scripts/player/MaskDude.gd) (doble salto y dash únicos).
- El **juicio del Guardián** se implementa visualmente mediante un Tween que interpola el color modular del sprite del Tótem (`_set_totem_glow`).

### Del Código a la Verificación Empírica:
- Cada afirmación funcional en esta documentación cuenta con su correspondiente método de aserción en el directorio `test/unit/`.
- La suite de **61 pruebas unitarias** ejecutadas sobre Godot 4.5 headless demuestra formalmente la ausencia de regresiones o fallos en los sistemas documentados.

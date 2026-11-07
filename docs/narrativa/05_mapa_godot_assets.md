# Entregable 5: Mapa Técnico de Godot 4.5 e Inventario de Assets — MaskDude

> **Asignatura:** Diseño Multimedia y Videojuegos · 9.º Semestre  
> **Institución:** Fundación de Estudios Superiores Comfanorte (FESC)  
> **Proyecto:** MaskDude — *El Festín del Tótem*  
> **Motor:** Godot Engine 4.5 Stable (Arquitectura de Nodos Oficial)  
> **Estado del Entregable:** Verificado contra el proyecto original

---

## 1. Estructura de Carpetas del Proyecto Real

La inspección directa del repositorio original en Godot 4.5 confirma la siguiente organización modular:

```text
MaskDude/
├── project.godot                     # Configuración central del motor (Main Scene: World.tscn)
├── export_presets.cfg                 # Perfiles de exportación
├── icon.svg                           # Ícono vectorial del proyecto
├── addons/
│   └── gut/                           # Framework de pruebas unitarias GUT 9.5.0
├── assets/
│   ├── audio/                         # Efectos de sonido (SFX en formato .ogg)
│   ├── musica/                        # Pistas musicales en bucle y jingles (.ogg)
│   ├── fuentes/                       # Archivos tipográficos (.ttf)
│   └── sprites/                       # Gráficos pixel art (backgrounds, fruits, platforms, player, terrain)
├── scenes/
│   ├── player/                        # MaskDude.tscn y MaskDudeFrames.tres
│   ├── items/                         # Fruit.tscn y subcarpeta frames/ (.tres por fruta)
│   ├── levels/                        # Level1.tscn (pantalla única) y Level_Large.tscn (escena de pruebas)
│   ├── narrative/                     # DialogueBox.tscn
│   └── world/                         # World.tscn (escena raíz) y tilesets/ (Terrain.tres, Decor.tres)
├── scripts/
│   ├── player/                        # MaskDude.gd
│   ├── items/                         # Fruit.gd
│   ├── levels/                        # Level1.gd
│   ├── narrative/                     # Story.gd, StoryTrigger.gd, DialogueBox.gd
│   ├── tools/                         # build_level.gd, build_level_large.gd
│   └── world/                         # World.gd
├── test/
│   ├── gut_config.json                # Configuración de ejecución headless
│   ├── unit/                          # 7 suites de pruebas unitarias (.gd)
│   └── reports/                       # Reportes formales de validación (REPORTE_PRUEBAS.md)
└── docs/                              # Documentación técnica interna y diagramas
```

---

## 2. Escenas Existentes y Árboles de Nodos

### 2.1. Escena Raíz: `World.tscn`
- **Función:** Coordina el flujo global, la cinemática de introducción, los disparadores de historia, la música y la pantalla de cierre.
- **Script Asociado:** `scripts/world/World.gd`.

```text
World (Node2D) [World.gd]
├── Level1 (Node2D) [Instancia: Level1.tscn]
├── Audio (Node)
│   ├── Music (AudioStreamPlayer) [stream: overworld.ogg, autoplay: true]
│   ├── Collect (AudioStreamPlayer) [stream: coin.ogg]
│   ├── AllFruits (AudioStreamPlayer) [stream: oneup.ogg]
│   ├── Win (AudioStreamPlayer) [stream: levelend.ogg]
│   ├── Fall (AudioStreamPlayer) [stream: death.ogg]
│   └── Totem (AudioStreamPlayer) [stream: mushroomappear.ogg]
├── UI (CanvasLayer)
│   ├── FruitLabel (Label) [text: "Frutas: 0/0"]
│   ├── Controls (Label) [instrucciones de input map]
│   └── Hint (Label) [notificaciones flotantes temporizadas]
├── Cinematic (CanvasLayer) [layer = 15]
│   ├── Fade (ColorRect) [máscara negra de transición]
│   ├── Title (Label) [título de introducción / cierre]
│   ├── Subtitle (Label)
│   ├── Card (Label) [tarjetas de texto narrativo]
│   └── Footer (Label) [atajos de omisión: Enter / Esc]
└── DialogueBox (CanvasLayer) [Instancia: DialogueBox.tscn, layer = 20]
```

---

### 2.2. Escena de Nivel: `Level1.tscn`
- **Función:** Nivel jugable único de la entrega. Mide $32 \times 18$ tiles ($512 \times 288\text{ px}$). Contiene las plataformas colisionables, 13 frutas flotantes y los disparadores de área.
- **Script Asociado:** `scripts/levels/Level1.gd`.

```text
Level1 (Node2D) [Level1.gd]
├── Background (Node2D)
│   └── Pattern (Sprite2D) [texture: Brown.png, repeat: true]
├── Ground (TileMapLayer) [tileset: Terrain.tres, colisiones sólidas]
├── Props (Node2D)
│   ├── Pyramid1 .. Pyramid7 (StaticBody2D) [bloques de terreno decorativo/físico]
│   └── PyramidTall (StaticBody2D)
├── Platforms (Node2D)
│   ├── Hover1 .. Hover4 (StaticBody2D) [texture: Hover.png, one_way_collision = true]
├── Frame (TileMapLayer) [bordes limitantes del escenario]
├── Fruits (Node2D)
│   ├── Bananas1, Pineapple2, Kiwi3, Melon4, Strawberry5, Cherries6,
│   │   Pineapple7, Apple8, Cherries9, Bananas10, Orange11, Pineapple12, Apple13
│   │   [Instancias de Fruit.tscn con SpriteFrames específicos]
├── FloorShade (TileMapLayer) [sombreado visual inferior]
├── StoryTriggers (Node2D)
│   ├── Trigger_hint_double_jump (Area2D) [StoryTrigger.gd, story_id = "hint_double_jump"]
│   ├── Trigger_hint_dash (Area2D) [StoryTrigger.gd, story_id = "hint_dash"]
│   └── Trigger_totem_midway (Area2D) [StoryTrigger.gd, story_id = "totem_midway"]
├── SpawnPoint (Marker2D) [posición: (64, 155)]
├── Goal (Area2D) [altar del Tótem Dorado, posición: (436, 123)]
│   ├── CollisionShape2D (RectangleShape2D)
│   ├── Sprite2D (Sprite2D) [representación del Tótem]
│   └── Label (Label) [rótulo "META"]
└── MaskDude (CharacterBody2D) [Instancia: MaskDude.tscn, posición inicial: (64, 155)]
```

> [!WARNING]
> **Aclaración sobre `Level_Large.tscn`:**  
> La escena `Level_Large.tscn` presente en la carpeta `scenes/levels/` corresponde a un entorno de pruebas preliminares utilizado para verificar desplazamientos horizontales extensos. **No constituye un nivel jugable de la experiencia narrativa** y se clasifica técnicamente como *Escena de Testing / Pruebas Internas*.

---

### 2.3. Escena del Jugador: `MaskDude.tscn`
- **Función:** Entidad controlable por el jugador. Implementa máquina de estados finitos (`IDLE`, `RUN`, `JUMP`, `FALL`, `DOUBLE_JUMP`, `DASH`, `LOCKED`).
- **Script Asociado:** `scripts/player/MaskDude.gd`.

```text
MaskDude (CharacterBody2D) [collision_layer = 2, collision_mask = 1]
├── AnimatedSprite2D [sprite_frames: MaskDudeFrames.tres, autoplay: "idle"]
├── CollisionShape2D [shape: RectangleShape2D, size: (14, 24)]
├── Camera2D [position_smoothing_enabled = true, speed = 8.0]
├── JumpSound (AudioStreamPlayer) [stream: jump.ogg]
├── DashSound (AudioStreamPlayer) [stream: fireball.ogg, pitch_scale = 1.3]
└── StateLabel (Label) [visible: false, depuración de estados con F3]
```

- **Recurso `MaskDudeFrames.tres`:** Recurso nativo oficial de tipo **`SpriteFrames`** de Godot 4.5. Gestiona 7 animaciones construidas sobre texturas atlas (`AtlasTexture`) de $32 \times 32\text{ px}$:
  - `idle`: 11 fotogramas en bucle a 12 FPS.
  - `run`: 12 fotogramas en bucle a 18 FPS.
  - `jump`: 1 fotograma estático de ascenso.
  - `fall`: 1 fotograma estático de descenso.
  - `double_jump`: 6 fotogramas de voltereta acrobática a 14 FPS.
  - `wall_jump`: 5 fotogramas de apoyo en muro.
  - `hit`: 7 fotogramas de impacto.

---

### 2.4. Escena de Diálogo: `DialogueBox.tscn`
- **Función:** Interfaz modal para renderizado de diálogos con soporte de BBCode, avance por pulsación y sonido de escritura retro.
- **Script Asociado:** `scripts/narrative/DialogueBox.gd`.

```text
DialogueBox (CanvasLayer) [layer = 20]
├── Root (Control) [anchors_preset: full rect]
│   └── Panel (Panel) [caja retro con borde dorado SubResource("box")]
│       ├── Portrait (TextureRect) [retrato de personaje de 32x32 px]
│       ├── Name (Label) [nombre en amarillo dorado]
│       ├── Text (RichTextLabel) [cuerpo del mensaje con typing effect]
│       └── Hint (Label) [indicador "▼ Enter"]
└── Blip (AudioStreamPlayer) [stream: blip.ogg, volume_db = -16.0]
```

---

## 3. Correspondencia Técnica Storyboard ↔ Nodos Godot 4.5

| Viñeta / Escena | Archivo .tscn | Nombre del Nodo | Clase Real Godot 4.5 | Evento / Señal / Estado | Prueba Observable | Estado Técnico |
| :---: | :--- | :--- | :--- | :--- | :--- | :---: |
| **V01**<br>ESC-01 | `World.tscn` | `DialogueBox` / `Cinematic` | `CanvasLayer` + `ColorRect` | `_play_intro()` / `set_locked(true)` | Al iniciar, el jugador no se mueve; las tarjetas hacen fade y el Tótem brilla con `mushroomappear.ogg`. | **Implementado** |
| **V02**<br>ESC-01 | `Level1.tscn` | `Trigger_hint_double_jump` | `Area2D` + `CollisionShape2D` | `body_entered` $\rightarrow$ `hint_double_jump` | Al entrar en $X=92$, aparece el cartel superior de doble salto; pulsar salto en el aire da segundo impulso. | **Implementado** |
| **V03**<br>ESC-01/02 | `Level1.tscn` | `Trigger_hint_dash` / `Hover1..4` | `Area2D` / `StaticBody2D` | `body_entered` / `is_action_just_pressed("dash")` | Pulsar Shift/K impulsa a $320\text{ px/s}$ con gravedad cero y estela fantasma. | **Implementado** |
| **V04**<br>ESC-02 | `Level1.tscn` | `Trigger_totem_midway` | `Area2D` + `CollisionShape2D` | Señal `triggered("totem_midway")` | Al tocar el saliente oriental, el control se congela y el Tótem avisa que la meta está próxima. | **Implementado** |
| **V05**<br>ESC-02 | `Level1.tscn` | `Goal` | `Area2D` + `Sprite2D` | Señal `body_entered` $\rightarrow$ `level_completed` | Contacto con el Tótem detiene la música, dispara jingle `Win` y eleva el resplandor con un Tween. | **Implementado** |
| **V06**<br>ESC-02 | `World.tscn` | `Cinematic/Fade` + `Title` | `ColorRect` + `Label` | Método `_show_end_card()` | Fade a negro con balance de frutas (`Frutas: 13/13`) y mensaje de reinicio con la tecla `R`. | **Implementado** |

---

## 4. Inventario Oficial de Assets y Licencias

La información de procedencia y licenciamiento ha sido validada directamente desde los archivos de auditoría de licencias del proyecto original (`assets/fuentes/README.md`, `assets/sprites/CREDITS.md`, `assets/audio/CREDITS.md`, `assets/musica/CREDITS.md` y `README.md`):

| Recurso | Archivo en Proyecto | Uso Técnico y Narrativo | Procedencia / Autor | Licencia | Estado |
| :--- | :--- | :--- | :--- | :---: | :---: |
| **Pista Musical Overworld** | `res://assets/musica/overworld.ogg` | Banda sonora principal en bucle durante la exploración de Level1 | SketchyLogic (*Hungry Dino*) | **CC-BY 3.0** | **Implementado** |
| **Jingle de Victoria** | `res://assets/musica/levelend.ogg` | Fanfarria triunfal al alcanzar el Tótem Dorado en el clímax | SketchyLogic (*Hungry Dino*) | **CC-BY 3.0** | **Implementado** |
| **SFX Salto** | `res://assets/audio/jump.ogg` | Sonido motriz de salto básico y doble salto (pitch variable) | Baŝto (*NES Sounds*) vía Mari0 | **CC0 (Dominio Público)** | **Implementado** |
| **SFX Dash** | `res://assets/audio/fireball.ogg` | Sonido de impulso horizontal aéreo y terrestre | Baŝto (*NES Sounds*) vía Mari0 | **CC0 (Dominio Público)** | **Implementado** |
| **SFX Recolección Fruta** | `res://assets/audio/coin.ogg` | Tintineo sonoro individual al recolectar cada fruta | Baŝto (*NES Sounds*) vía Mari0 | **CC0 (Dominio Público)** | **Implementado** |
| **SFX 13 Frutas (Completa)** | `res://assets/audio/oneup.ogg` | Fanfarria al recoger la última fruta de la ofrenda | Baŝto (*NES Sounds*) vía Mari0 | **CC0 (Dominio Público)** | **Implementado** |
| **SFX Caída al Abismo** | `res://assets/audio/death.ogg` | Alerta sonora al rebasar el límite inferior de caída | Baŝto (*NES Sounds*) vía Mari0 | **CC0 (Dominio Público)** | **Implementado** |
| **SFX Resonancia Totémica** | `res://assets/audio/mushroomappear.ogg` | Efecto místico al encenderse o reaccionar el Tótem Dorado | Prinsu-Kun vía Mari0 | **CC0 (Dominio Público)** | **Implementado** |
| **SFX Blip Diálogo** | `res://assets/audio/blip.ogg` | Efecto de tipeo retro por carácter en la caja de diálogo | artisticdude (*RPG Sound Pack*) | **CC0 (Dominio Público)** | **Implementado** |
| **Sprites del Protagonista** | `res://assets/sprites/player/*.png` | Hojas de sprites para animaciones de Mask Dude | Pixel Frog (*Pixel Adventure 1*) | **CC0 (Dominio Público)** | **Implementado** |
| **Sprites de Frutas** | `res://assets/sprites/fruits/*.png` | Texturas animadas de los 8 tipos de frutas sagradas | Pixel Frog (*Pixel Adventure 1*) | **CC0 (Dominio Público)** | **Implementado** |
| **Tilemap de Terreno** | `res://assets/sprites/terrain/Terrain.png` | Bloques de piedra y pirámides de la Cámara Antigua | Pixel Frog (*Pixel Adventure 1*) | **CC0 (Dominio Público)** | **Implementado** |
| **Plataformas Suspendidas** | `res://assets/sprites/platforms/Hover.png` | Plataformas unidireccionales sobre el abismo | Pixel Frog (*Pixel Adventure 1*) | **CC0 (Dominio Público)** | **Implementado** |
| **Fondo Cavernoso** | `res://assets/sprites/backgrounds/Brown.png` | Textura de patrón repetido para el fondo de Level 1 | Pixel Frog (*Pixel Adventure 1*) | **CC0 (Dominio Público)** | **Implementado** |
| **Tipografía Courier Prime** | `res://assets/fuentes/CourierPrime-*.ttf` | Tipografía monoespaciada para textos del sistema y diálogos | Quote-Unquote Apps | **SIL Open Font License 1.1** | **Implementado** |
| **Framework de Pruebas GUT** | `res://addons/gut/` | Suite automatizada de pruebas unitarias | Butch Wessels (*GUT*) | **MIT License** | **Implementado** |

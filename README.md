# Repositorio Documental: MaskDude — El Festín del Tótem

> **Institución:** Fundación de Estudios Superiores Comfanorte (FESC)  
> **Programa:** Ingeniería de Software  
> **Asignatura:** Diseño Multimedia y Videojuegos · 9.º Semestre  
> **Profesor:** Yeison Sanabria Ascanio  
> **Motor Objetivo:** Godot Engine 4.5 (Renderizador *GL Compatibility*)  
> **Tipo de Repositorio:** Gestión Documental Exclusiva (Sin código fuente)

---

## 1. Presentación del Videojuego

**MaskDude** es un videojuego de aventura y plataformas 2D desarrollado con una estética pixel art retro de 16 bits.

- **Premisa Central:** En la noche sagrada de la cosecha, las frutas de la ofrenda despiertan con vida propia y escapan flotando hacia los riscos de la Cámara Antigua, apagando la luz del Guardián de la Cosecha (el Tótem Dorado). Mask Dude, portador de la máscara ritual, debe internarse en las ruinas, dominar los dones espirituales del doble salto y el dash, y recuperar la ofrenda antes del amanecer para asegurar la supervivencia alimentaria de su aldea.
- **El Misterio de la Tradición:** Esta tarea se ha repetido durante generaciones por diversos hombres enmascarados. Sin embargo, ninguno ha regresado tras hacer entrega de las frutas al Guardián. Dicha incógnita se preserva intacta en la narrativa como motor dramático de misterio.
- **Escenario Documentado:** **Level 1** (*La Cámara Antigua*, pantalla única de $32 \times 18$ tiles = $512 \times 288\text{ px}$).

> [!IMPORTANT]
> **Principio de Separación y Restricción de Alcance:**  
> Este repositorio está destinado **exclusivamente a la documentación académica, visual y técnica** del proyecto. No contiene scripts de Godot (`.gd`), escenas (`.tscn`), ejecutables ni binarios. La implementación jugable reside en el repositorio de desarrollo principal: [https://github.com/GaussParadox/MaskDude](https://github.com/GaussParadox/MaskDude).

---

## 2. Autor

| Estudiante | Rol Documental | Área de Responsabilidad |
| :--- | :--- | :--- |
| **Wilson Alejandro Saavedra Arenales** | Documentación Narrativa Individual | Premisa, personajes, estructura narrativa, guion jugable, storyboard, mapa técnico, trazabilidad y lista de chequeo. |

---

## 3. Organización del Repositorio

```text
MaskDude-Documentacion/
│
├── README.md                          # Presentación general, equipo, enlaces y directrices
├── .gitignore                         # Exclusión rigurosa de código, escenas, binarios y credenciales
├── LISTA_DE_CHEQUEO.md                # Evaluación cualitativa de los 10 criterios académicos FESC
│
├── docs/
│   └── narrativa/
│       ├── README.md                  # Tablero de navegación e índice de entregables
│       ├── 01_premisa_personajes.md   # [E1] Premisa, logline, protagonista, Guardián y tradición
│       ├── 02_estructura_curva.md     # [E2] Estructura en 3 actos, 6 beats (B1-B6), tensión y respiro
│       ├── curva_tension.png          # [E2] Gráfica de tensión cualitativa generada en alta resolución
│       ├── 03_guion_jugable.md        # [E3] Guion interactivo de ESC-01 (Intro) y ESC-02 (Clímax)
│       ├── 04_storyboard.pdf          # [E4] Storyboard formal multipágina (6 viñetas en 16:9)
│       ├── editables/                 # [E4] Fuentes originales vectoriales para Krita e Inkscape
│       │   ├── README.md              # Lineamientos de rotulación y edición por capas
│       │   └── fuentes_del_storyboard.svg
│       ├── 05_mapa_godot_assets.md    # [E5] Mapa técnico Godot 4.5 e inventario con licencias reales
│       └── 06_trazabilidad.md         # [E6] Matriz: Historia → RF → Escena → Nodo → Prueba GUT
│
├── editables/                         # Almacén raíz de fuentes gráficas y diagramas vectoriales
│   └── fuentes_del_storyboard.svg
│
├── assets_documentacion/              # Diagramas y referencias visuales complementarias
│   ├── MaskDude_Estados.png           # Diagrama visual de la máquina de estados del jugador
│   └── MaskDude_Estados.svg           # Fuente vectorial del grafo de estados
│
└── evidencias/                        # Validación en tiempo de ejecución sobre el build real
    ├── README.md                      # Metodología de validación de pruebas observables
    ├── REPORTE_PRUEBAS.md             # Reporte formal GUT 9.5.0 (61 pruebas unitarias, 0 fallos)
    └── preview_nivel1.gif             # Registro visual animado de Level 1 en Godot 4.5
```

---

## 4. Enlaces Directos a los Seis Entregables Académicos

| Entregable | Documento | Archivo Principal | Estado de Entrega |
| :-: | :--- | :--- | :---: |
| **E1** | Premisa y Personajes | [01_premisa_personajes.md](docs/narrativa/01_premisa_personajes.md) | **Completo / Verificado** |
| **E2** | Estructura y Curva de Tensión | [02_estructura_curva.md](docs/narrativa/02_estructura_curva.md) | **Completo / Verificado** |
| — | Gráfica de Tensión | [curva_tension.png](docs/narrativa/curva_tension.png) | **Generado / Exportado** |
| **E3** | Guion Jugable (Intro y Clímax) | [03_guion_jugable.md](docs/narrativa/03_guion_jugable.md) | **Completo / Verificado** |
| **E4** | Storyboard Maquetado (PDF) | [04_storyboard.pdf](docs/narrativa/04_storyboard.pdf) | **Generado / Exportado** |
| — | Editables del Storyboard | [editables/README.md](docs/narrativa/editables/README.md) | **Disponible** |
| **E5** | Mapa Técnico e Inventario | [05_mapa_godot_assets.md](docs/narrativa/05_mapa_godot_assets.md) | **Completo / Verificado** |
| **E6** | Matriz de Trazabilidad | [06_trazabilidad.md](docs/narrativa/06_trazabilidad.md) | **Completo / Verificado** |
| **QA** | Criterios de Evaluación FESC | [LISTA_DE_CHEQUEO.md](LISTA_DE_CHEQUEO.md) | **Verificado (10 Criterios)** |

---

## 5. Resumen de Validación Técnica y Empírica

La documentación técnica aquí presentada está 100% respaldada por la suite de pruebas automatizadas del proyecto MaskDude:

- **Framework:** GUT 9.5.0 (*Godot Unit Test*).
- **Entorno de Ejecución:** Godot 4.5 Stable (modo *headless*).
- **Resultados de Auditoría:** **61 pruebas unitarias ejecutadas, 0 fallos**.
- **Cobertura Comprobada:**
  - Máquina de estados finitos del personaje ([`MaskDude.gd`](docs/narrativa/05_mapa_godot_assets.md#L96)): `IDLE`, `RUN`, `JUMP`, `FALL`, `DOUBLE_JUMP`, `DASH`, `LOCKED`.
  - Mecánica de recolección de 13 frutas flotantes ([`Fruit.gd`](docs/narrativa/05_mapa_godot_assets.md#L62)).
  - Flujo de interacción y avance dialógico ([`DialogueBox.gd`](docs/narrativa/05_mapa_godot_assets.md#L117)).
  - Detección de colisión y disparo de victoria en altar ([`Level1.gd`](docs/narrativa/05_mapa_godot_assets.md#L55)).

---

## 6. Convención de Control de Versiones

Todo cambio se gestiona mediante la especificación [Conventional Commits v1.0.0](https://www.conventionalcommits.org/es/v1.0.0/):
- `docs: add game premise and characters`
- `docs: add narrative structure and tension curve`
- `docs: add playable script and storyboard`
- `docs: add Godot technical map`
- `docs: add traceability matrix`
- `docs: finalize quality checklist and readme presentation`

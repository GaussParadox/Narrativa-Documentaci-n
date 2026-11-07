# Lista de Chequeo y Criterios de Calidad — MaskDude

> **Asignatura:** Diseño Multimedia y Videojuegos · 9.º Semestre  
> **Institución:** Fundación de Estudios Superiores Comfanorte (FESC)  
> **Proyecto:** MaskDude — *El Festín del Tótem*  
> **Evaluación:** Cualitativa (*Sí* / *Por ajustar* / *No aplica con justificación*). Sin asignación numérica arbitraria.

---

## 1. Matriz de Evaluación Cualitativa de los Diez Criterios

| # | Criterio de Evaluación | Aspectos Específicos que se Revisan | Estado Cualitativo | Evidencia en el Repositorio | Justificación Técnica y Observaciones |
| :-: | :--- | :--- | :---: | :--- | :--- |
| **1** | **Premisa y personajes** | Meta observable, conflicto principal, consecuencias definidas, tono y relación estrecha con las acciones del jugador. | **Sí** | `docs/narrativa/01_premisa_personajes.md` | Logline definido con meta comprobable (recolectar 13 frutas); conflicto hombre vs entorno; tono de aventura con misterio; preservación del enigma de los antiguos enmascarados sin inventar explicaciones ficticias. |
| **2** | **Estructura narrativa** | Planteamiento claro, escalada progresiva, clímax debidamente preparado y consecuencias visibles en el mundo virtual. | **Sí** | `docs/narrativa/02_estructura_curva.md` | Progresión didáctica en 3 actos para Level 1; clímax preparado en el mirador; resolución con 3 variantes de diálogo y brillo del Tótem. |
| **3** | **Curva de tensión** | Beats identificados (B1 a B6), justificación cualitativa de tensión (1-5) diferenciada de la dificultad, pausas de respiro y ciclo de reintento. | **Sí** | `docs/narrativa/02_estructura_curva.md`<br>`docs/narrativa/curva_tension.png` | Tabla de 6 beats con escala 1-5 coincidente con la gráfica; valle de respiro táctico justificado en B4; reaparición inmediata sin repetir cinemáticas. |
| **4** | **Guion jugable de dos escenas** | Introducción (`ESC-01`) y Clímax (`ESC-02`) con triggers, precondiciones, acciones, respuestas observables, cámaras, audio y salidas. | **Sí** | `docs/narrativa/03_guion_jugable.md` | Ambas escenas documentadas con precisión de variables (`_intro_running`, `_finished`), estado `State.LOCKED`, diálogos con retratos y 3 ramas de epílogo. |
| **5** | **Storyboard (6 a 8 viñetas)** | Secuencia legible de 6 viñetas con encuadre de cámara, acción, respuesta, diálogo/señal, audio, transiciones y distinción de control. | **Sí** | `docs/narrativa/04_storyboard.pdf`<br>`docs/narrativa/editables/` | Documento PDF formal multipágina de 6 viñetas (V01 a V06) con recuadros 16:9 y fuentes vectoriales editables (`fuentes_del_storyboard.svg`). |
| **6** | **Viabilidad en Godot 4.5** | Clases reales de Godot 4.5, nombres de nodos diferenciados de clases, eventos, señales nativas y estados. | **Sí** | `docs/narrativa/05_mapa_godot_assets.md` | Mapeo riguroso de nodos existentes (`CharacterBody2D`, `TileMapLayer`, `Area2D`, `AudioStreamPlayer`); recurso `SpriteFrames` verificado; aclaración de `Level_Large.tscn` como escena de pruebas. |
| **7** | **Inventario y licencias de assets** | Uso, archivo previsto (`res://`), origen real, licencia legal explícita, responsable y estado. | **Sí** | `docs/narrativa/05_mapa_godot_assets.md` (Sección 4) | 16 recursos inventariados con licencias extraídas de los créditos del juego (SketchyLogic CC-BY 3.0, Baŝto CC0, Pixel Frog CC0, GUT MIT). Sin procedencias ficticias. |
| **8** | **Coherencia y trazabilidad** | Personajes y reglas consistentes; cadena completa Historia (`HIS`) $\rightarrow$ Requisito (`RF`) $\rightarrow$ Escena (`ESC`) $\rightarrow$ Prueba (`PR`). | **Sí** | `docs/narrativa/06_trazabilidad.md` | Matriz bidireccional de 7 elementos principales respaldada empíricamente por la suite de 61 pruebas unitarias del framework GUT sin fallos. |
| **9** | **Repositorio y evidencias** | Editables preservados, exportaciones legibles (.png, .pdf), README principal, commit estandarizado y estructura limpia. | **Sí** | Raíz del repositorio y carpeta `evidencias/` | Repositorio documental independiente, sin código ejecutable, con reporte de pruebas, gif animado, diagramas y commits convencionales. |
| **10** | **Comprensión y defensa del equipo** | Capacidad del equipo para justificar decisiones narrativas, transiciones del storyboard y correspondencias técnicas. | **Sí** | `README.md`<br>Sustentación académica | Documentación redactada de manera formal y accesible para estudiantes de ingeniería, con roles asignados a cada integrante. |

---

## 2. Cierre y Declaración de Integridad Documental

- **Consistencia de Personajes:** El protagonista se mantiene estrictamente como `Mask Dude` y el antagonismo/meta como `Tótem Dorado` en todos los archivos.
- **Sin Código Invasivo:** Se respetó la restricción principal: este repositorio no contiene scripts `.gd`, escenas `.tscn` ni binarios del motor.
- **Preservación del Misterio:** Se conservó la incógnita sobre el destino de los antiguos hombres enmascarados como elemento central de la tradición ritual, sin inventar explicaciones arbitrarias.

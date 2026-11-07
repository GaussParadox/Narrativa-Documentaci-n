# Entregable 3: Guion Jugable de Dos Escenas — MaskDude

> **Asignatura:** Diseño Multimedia y Videojuegos · 9.º Semestre  
> **Institución:** Fundación de Estudios Superiores Comfanorte (FESC)  
> **Proyecto:** MaskDude — *El Festín del Tótem*  
> **Motor Objetivo:** Godot Engine 4.5  
> **Estado del Entregable:** Completo y Verificado

---

## 1. Fundamentos del Guion Interactivo en MaskDude

El guion de MaskDude no es una pieza literaria pasiva, sino una especificación técnica de interacción que sincroniza:
1. **El Estado de Control:** El uso estricto del estado `State.LOCKED` mediante [`MaskDude.set_locked()`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/scripts/player/MaskDude.gd#L278) para congelar el movimiento durante cinemáticas sin desactivar la física de colisiones ni la gravedad.
2. **Las Señales del Motor:** Disparadores mediante señales nativas (`body_entered`, `level_completed`, `fruits_changed`).
3. **El Sistema de Texto Dinámico:** Coordinado por [`DialogueBox.tscn`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/scenes/narrative/DialogueBox.tscn) con typing effect retro a 35 caracteres por segundo, saltos por tecla (`Enter`/`E`) y atajo de omisión (`Esc`).

---

## 2. Escena 1: Introducción — La Llamada de la Cosecha

### Ficha Técnica de Escena: `ESC-01`

| Campo | Especificación de Diseño e Implementación |
| :--- | :--- |
| **Identificador y Nombre** | **ESC-01:** *La Llamada de la Cosecha y el Despertar del Tótem* |
| **Ubicación en el Nivel** | Punto de aparición inicial (`SpawnPoint`, coordenadas $X=64, Y=155$) en la zona izquierda de `Level1.tscn`. |
| **Propósito Narrativo** | Establecer el conflicto comunal (frutas fugitivas y riesgo de hambruna), presentar al Guardián de la Cosecha y dotar al protagonista de los poderes sagrados (doble salto y dash). |
| **Beat Relacionado** | **Beat B1** (Planteamiento / Llamada) |
| **Trigger (Disparador)** | Inicio automático al cargar la escena principal [`World.tscn`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/scripts/world/World.gd#L39) dentro de la función `_ready()`. |
| **Precondiciones** | La variable `_intro_running == true`, la máscara de pantalla `Cinematic/Fade` con opacidad alfa 1.0 (pantalla negra) y el jugador forzado a `State.LOCKED`. |
| **Tipo de Control** | **Cinemática interactiva con control bloqueado:** El jugador no puede desplazarse. Conserva el input para avanzar textos (`Enter`/`E`) o saltar toda la introducción (`Esc`). |
| **Acción del Jugador** | Presionar `Enter` o `E` para avanzar las tarjetas de texto y el diálogo con el Guardián. |
| **Diálogo y Texto (Guion)** | **Fase A (Tarjetas sobre negro):**<br>1. *«Cada año, en la noche de la cosecha, la aldea ofrece sus mejores frutas al Tótem Dorado.»*<br>2. *«Esta vez las frutas despertaron. Escaparon flotando hacia la Cámara Antigua... y el Tótem se apagó.»*<br>3. *«Si la ofrenda no llega antes del amanecer, la cosecha del próximo año se perderá.»*<br><br>**Fase B (Diálogo en la Cámara Antigua):**<br>- **Mask Dude:** *«Las frutas flotan por toda la cámara... y el Tótem está arriba, al otro lado.»*<br>- **Tótem Dorado:** *«Guardián de la Máscara... recoge la ofrenda y tráela hasta mí antes del amanecer.»*<br>- **Tótem Dorado:** *«Los espíritus te prestan dos poderes: el doble salto y el dash. Úsalos con sabiduría.»*<br>- **Mask Dude:** *«Entendido. ¡Vamos por esas frutas!»* |
| **Señal Visual / Accesibilidad** | Animación suave de aparición/desaparición (*fade tween*) de las tarjetas de texto; cuadro de diálogo con recuadro retro dorado y retrato del Tótem; atajo visible en el pie: `▼ Enter: continuar · Esc: saltar`. |
| **Respuesta del Sistema** | 1. Tras las tarjetas, la máscara negra se disuelve (`Fade` modula alfa a 0.0).<br>2. El sprite del Tótem interpola su brillo de 0.0 a 0.3 mediante `_set_totem_glow()`.<br>3. Al terminar el diálogo, se ejecuta `player.set_locked(false)` y se despliega el aviso emergente superior: `Objetivo: recoge las frutas y llega al Tótem Dorado`. |
| **Cámara** | [`Camera2D`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/scenes/player/MaskDude.tscn#L27) centrada en Mask Dude, con límites fijados al tamaño del nivel ($0, 0, 512, 288$ px) y suavizado activo (`position_smoothing_speed = 8.0`). Permite ver el fondo cavernoso y las primeras frutas flotantes. |
| **Audio y Efectos Sonoros** | Música ambiental [`overworld.ogg`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/assets/musica/overworld.ogg) en bucle; sonido totémico [`mushroomappear.ogg`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/assets/audio/mushroomappear.ogg) al encenderse el Tótem; sonido de tecla [`blip.ogg`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/assets/audio/blip.ogg) en cada carácter del diálogo. |
| **Condición de Salida (Éxito)** | Concluir la cuarta línea de diálogo o presionar `Esc`. La bandera `_intro_running` pasa a `false` y el jugador transiciona a `State.IDLE`. |
| **Comportamiento ante Fallo** | No hay condición de fallo en la introducción (entorno protegido). |
| **Reentrada / Repetición** | Si el jugador muere durante el nivel o cae al abismo, la reaparición (`respawn_at`) **no vuelve a ejecutar ESC-01**. Solo se repite si se reinicia el nivel completo con la tecla `R`. |

---

## 3. Escena 2: Clímax — El Juicio de la Ofrenda y el Destino Sagrado

### Ficha Técnica de Escena: `ESC-02`

| Campo | Especificación de Diseño e Implementación |
| :--- | :--- |
| **Identificador y Nombre** | **ESC-02:** *El Juicio de la Ofrenda y el Destino Sagrado* |
| **Ubicación en el Nivel** | Altar superior oriental (`Goal`, coordenadas $X=436, Y=123$) sobre la pirámide ceremonial de `Level1.tscn`. |
| **Propósito Narrativo** | Evaluar el tributo recolectado, determinar la supervivencia de la aldea mediante el brillo del Tótem Dorado y cerrar la travesía preservando el misterio de los antiguos hombres enmascarados. |
| **Beat Relacionado** | **Beat B5** (Clímax Decisivo) y **Beat B6** (Resolución) |
| **Trigger (Disparador)** | El cuerpo del jugador colisiona físicamente con el área detectora de [`Goal`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/scenes/levels/Level1.tscn#L389) (`body_entered` conectado a [`_on_goal_body_entered()`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/scripts/levels/Level1.gd#L53)). |
| **Precondiciones** | Variable `_finished == false`, jugador en capa de colisión 2 y contacto validado exclusivamente para `MaskDude`. |
| **Tipo de Control** | **Transición de Gameplay a Cinemática:** El jugador tiene control motriz pleno hasta hacer contacto con el altar. Inmediatamente el sistema ejecuta `level.player.set_locked(true)`, deteniendo el movimiento y anulando inputs durante el juicio. |
| **Acción del Jugador** | Salto final hacia el bloque del Tótem; posterior pulsación de `Enter` o `E` para avanzar los diálogos de evaluación y contemplar el epílogo. |
| **Diálogo y Señal (Variantes Dinámicas)** | El diálogo se bifurca según la variable `fruit_collected` vs `fruit_total` (13 frutas):<br><br>**Variante A: Ofrenda Completa (13 / 13 frutas):**<br>- **Tótem Dorado:** *«¡Todas las frutas! La ofrenda está completa.»*<br>- **Mask Dude:** *«Lo logramos... la aldea tendrá su cosecha.»*<br>- **Tótem Dorado:** *«Mi luz vuelve a brillar. Que comience el Festín. Gracias, guardián.»*<br><br>**Variante B: Ofrenda Parcial (1 a 12 frutas):**<br>- **Tótem Dorado:** *«Me traes N de 13 frutas... la ofrenda está incompleta.»*<br>- **Mask Dude:** *«Perdón. Algunas flotaban más alto de lo que pensé.»*<br>- **Tótem Dorado:** *«Mi luz brilla apenas. El Festín será modesto este año. Quizá puedas volver por el resto.»*<br><br>**Variante C: Sin Ofrenda (0 frutas):**<br>- **Tótem Dorado:** *«Llegas con las manos vacías, guardián... la ofrenda no está.»*<br>- **Mask Dude:** *«Lo sé... Déjame intentarlo otra vez.»*<br>- **Tótem Dorado:** *«Mi luz casi se apaga. Las frutas siguen flotando en la cámara. Inténtalo de nuevo.»* |
| **Respuesta del Sistema** | 1. La música de fondo `overworld.ogg` se detiene.<br>2. Se reproducen en simultáneo el jingle de victoria [`levelend.ogg`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/assets/musica/levelend.ogg) y el sonido totémico `mushroomappear.ogg`.<br>3. Interpolación visual del resplandor del Tótem (`_set_totem_glow`) elevando su brillo proporcionalmente: $0.35 + 0.65 \times (\text{collected} / \text{total})$.<br>4. Al finalizar el diálogo, se ejecuta la transición a negro (`fade`) y se despliega la pantalla `FIN` con el epílogo y la instrucción de reinicio. |
| **Cámara** | Encuadre lateral fijo sobre el altar del Tótem y Mask Dude, eliminando el suavizado dinámico para estabilizar la escena dramática. |
| **Audio y Efectos Sonoros** | Silencio musical inmediato, entrada triunfal del jingle de victoria `Win` a volumen pleno, seguido de los blips de texto del diálogo final. |
| **Condición de Salida (Éxito)** | Completar la secuencia de diálogo y presionar `R` para reiniciar una nueva partida si se desea mejorar la puntuación. |
| **Comportamiento ante Fallo** | Si el jugador cae al abismo antes de tocar la meta, no se activa ESC-02; reaparece en `_respawn_position` y conserva las frutas recogidas. |
| **Reentrada / Repetición** | La bandera interna `_finished = true` en `Level1.gd` y `_ending = true` en `World.gd` impiden estrictamente que la escena de clímax se ejecute más de una vez por ejecución. |

---

## 4. Revisión Cruzada de Coherencia Narrativa y Técnica

1. **Unidad de Nombres e Identificadores:** El protagonista se identifica unívocamente como `Mask Dude` y la entidad como `Tótem Dorado` / `Guardián de la Cosecha` en todos los diálogos y fichas técnicas.
2. **Sin Mecánicas Artificiales:** El desenlace no inventa ataques ni poderes inexistentes; se fundamenta estrictamente en las 13 frutas recolectadas mediante el doble salto y dash ya demostrados.
3. **Verificabilidad:** Ambas escenas corresponden con métodos existentes y probados en los scripts [`World.gd`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/scripts/world/World.gd) y [`Level1.gd`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/scripts/levels/Level1.gd).

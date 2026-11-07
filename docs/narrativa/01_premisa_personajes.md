# Entregable 1: Premisa Narrativa y Personajes — MaskDude

> **Asignatura:** Diseño Multimedia y Videojuegos · 9.º Semestre  
> **Institución:** Fundación de Estudios Superiores Comfanorte (FESC)  
> **Proyecto:** MaskDude  
> **Motor Objetivo:** Godot Engine 4.5 (Renderizador *GL Compatibility*)  
> **Estado del Entregable:** Completo y Verificado

---

## 1. Ficha General del Proyecto

| Parámetro | Definición |
| :--- | :--- |
| **Nombre del Videojuego** | **MaskDude** (Subtítulo del nivel: *El Festín del Tótem*) |
| **Género** | Aventura y plataformas 2D en vista lateral (*side-scroller*) |
| **Estética y Dirección Artística** | Pixel art nostálgico con paletas de alto contraste, ambientación de ruinas místicas y naturaleza ancestral |
| **Nivel Documentado** | **Level 1** (*La Cámara Antigua*) |
| **Motor de Desarrollo** | Godot Engine 4.5 Stable |

---

## 2. Premisa Narrativa

### 2.1. Logline Oficial
> *Cuando las frutas sagradas despiertan y escapan hacia las alturas de la Cámara Antigua amenazando con extinguir la luz del Guardián de la Cosecha, Mask Dude, portador de la máscara ceremonial, debe explorar las ruinas y recolectar la ofrenda antes del amanecer para asegurar la supervivencia alimentaria de su aldea, enfrentando la incertidumbre de una tradición milenaria cuyo destino final para los portadores sigue siendo un misterio.*

### 2.2. Sinopsis y Contexto del Mundo
En una aldea rodeada por valles fértiles, la subsistencia comunitaria depende enteramente de la protección brindada por el **Guardián de la Cosecha** (el *Tótem Dorado*). Cada año, durante la noche sagrada de la cosecha, la comunidad celebra el ritual del Festín, en el cual se entrega un tributo de frutas selectas para alimentar la energía del Guardián.

Sin embargo, en esta ocasión un fenómeno místico ocurre: las frutas despiertan con vida propia y escapan flotando hacia los riscos y plataformas de la **Cámara Antigua**, provocando que el Guardián pierda su fulgor y quede al borde de apagarse. Si la ofrenda no es restituida antes del primer rayo del amanecer, la tierra perderá su fertilidad y el pueblo enfrentará la hambruna.

### 2.3. La Tradición de los Hombres Enmascarados y el Misterio Central
La responsabilidad de recolectar y entregar la ofrenda recae históricamente sobre un elegido que porta una máscara ceremonial de madera tallada: el **Hombre Enmascarado**. Esta tradición se ha repetido invariablemente a lo largo de incontables generaciones.

El protagonista conoce los relatos y asume su deber con determinación. No obstante, sobre la misión pesa un enigma fundamental: **ninguno de los hombres enmascarados del pasado fue visto regresar a la aldea tras completar la entrega en la cima del altar**. 

> [!NOTE]
> **Preservación del Enigma:**  
> La narrativa del juego no revela de manera definitiva el destino de los predecesores ni si el Guardián los absorbe, los traslada a otro plano o si permanecen como custodios silenciosos de la cámara. Dicha incógnita se preserva intacta como motor de tensión y curiosidad dramática.

---

## 3. Personajes y Fuerzas del Relato

### 3.1. Protagonista: Mask Dude (Rol Controlado por el Jugador)

- **Identidad:** Un joven guardián que viste la máscara ritual de la aldea. No emite discursos extensos; su personalidad se manifiesta mediante la voluntad de actuar ante la crisis comunitaria.
- **Implementación Técnica:** Clase nativa [`CharacterBody2D`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/scripts/player/MaskDude.gd#L1-L2) instanciada en la escena [`MaskDude.tscn`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/scenes/player/MaskDude.tscn).
- **Capacidades Mecánicas Confirmadas en Código:**
  - **Desplazamiento horizontal:** Caminar y correr con aceleración (`1100.0 px/s²`), fricción (`1400.0 px/s²`) y velocidad tope (`140.0 px/s`).
  - **Salto básico adaptable:** Salto vertical con impulso inicial (`jump_velocity = -330.0 px/s`), corte dinámico al soltar el botón (`jump_cut_multiplier = 0.45`) y tolerancias motrices (*coyote time* y *jump buffer* de `0.1 s`).
  - **Doble salto:** Impulso aéreo adicional prestado por los espíritus (`double_jump_velocity = -300.0 px/s`), limitado a una carga por ciclo aéreo que se recarga al tocar suelo.
  - **Dash horizontal:** Impulso veloz a `320.0 px/s` durante `0.15 s` con estela de imágenes residuales (*ghost trail*), cooldown de `0.35 s` y gravedad cero durante su ejecución.
  - **Recolección:** Capacidad de interactuar y absorber frutas flotantes al entrar en contacto con su `Area2D`.
- **Límites Mecánicos Deliberados:**
  - No posee ataques ofensivos directos ni armas.
  - No puede volar ni escalar superficies verticales de forma indefinida.
  - El control es suprimido por el sistema (`State.LOCKED`) durante la cinemática de introducción y el diálogo final para preservar la sincronización narrativa.
- **Motivación y Arco Dramático:**
  - *Motivación inmediata:* Salvar a la aldea del desabastecimiento recuperando la ofrenda.
  - *Arco interno:* Enfrentar la soledad de la Cámara Antigua y ascender hacia el altar del Guardián sabiendo que su propio destino post-entrega es una incógnita.

### 3.2. El Guardián de la Cosecha (Tótem Dorado)

- **Naturaleza:** Entidad totémica ancestral ubicada en la cúspide oriental de la Cámara Antigua. Actúa como juez místico y canalizador de la fertilidad de la tierra.
- **Implementación Técnica:** Representado en [`Level1.tscn`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/scenes/levels/Level1.tscn#L389) por el nodo `Goal` (`Area2D` con detección en máscara de colisión del jugador, capa 2) y un `Sprite2D` cuyo canal de brillo modular (`modulate`) se interpola entre un estado apagado (`Color(0.4, 0.4, 0.5)`) y encendido dorado (`Color(1.25, 1.15, 0.8)`).
- **Función Narrativa:**
  1. Comunica el objetivo inicial y transfiere los dones del doble salto y dash al inicio.
  2. Emite una señal intermedia de aliento y evaluación a mitad del ascenso (`totem_midway`).
  3. Evalúa la ofrenda en el clímax y ofrece tres respuestas dialógicas según la cantidad de frutas recolectadas.

### 3.3. Fuerzas Opositoras y Conflicto
El conflicto en MaskDude es predominantemente **hombre contra entorno y tiempo**:
- **La Gravedad y el Abismo:** La Cámara Antigua es una estructura cavernosa vertical con plataformas suspendidas sobre el vacío. Caer por debajo del límite inferior del nivel (`y > level_size_tiles.y * TILE + KILL_MARGIN`) activa la penalización de reaparición.
- **La Dispersión de las Frutas:** 13 frutas repartidas en alturas dispares que requieren el uso combinado y preciso del doble salto y el dash.
- **El Plazo del Amanecer:** Presión dramática constante que exige rapidez y precisión antes de que la luz del Tótem se extinga por completo.

---

## 4. Consecuencias del Cumplimiento o Fallo

A diferencia de finales binarios arbitrarios, el sistema implementa **tres variantes comprobables** en `scripts/narrative/Story.gd`:

| Frutas Entregadas | Estado del Tótem | Consecuencia Narrativa y Epílogo |
| :---: | :--- | :--- |
| **Ofrenda Completa**<br>(13 de 13 frutas) | Fulgor dorado total (`100% glow`). Suena jingle de triunfo `Win`. | *«La cosecha está a salvo. La aldea celebra bajo la luz del Tótem.»* El Guardián agradece el sacrificio y declara iniciado el Festín. |
| **Ofrenda Parcial**<br>(1 a 12 frutas) | Brillo tenue y titilante. | *«La cosecha será escasa este año. ¿Podrás recuperar todas las frutas?»* El Guardián advierte que el alimento alcanzará de forma precaria y propone reintentar la búsqueda. |
| **Sin Ofrenda**<br>(0 frutas) | Tótem prácticamente apagado. | *«La noche sigue oscura. Las frutas aún esperan en la Cámara Antigua.»* El Guardián exhorta al protagonista a volver y no rendirse ante el abismo. |

---

## 5. Tono Narrativo y Dirección Sensorial

- **Rasgos Dominantes:** Aventura mística, exploración contenida, fantasía ancestral y misterio latente.
- **Manifestación Visual:** Fondo en mosaico de tonos tierra oscuros (`Brown.png`), contrastado con el brillo vibrante de las frutas animadas y los destellos dorados del Tótem.
- **Manifestación Sonora:**
  - Banda sonora chiptune ambiental rítmica (`overworld.ogg` en bucle continuo).
  - Pistas sonoras diferenciadas para salto (`jump.ogg`), dash (`fireball.ogg`), recolección individual (`coin.ogg`), recolección perfecta (`oneup.ogg`), caída al abismo (`death.ogg`) y resonancia totémica (`mushroomappear.ogg`).

---

## 6. Estado Real del Proyecto (Implementado vs. Propuesto)

| Elemento Narrativo / Técnico | Estado en el Proyecto Godot 4.5 | Evidencia Comprobable |
| :--- | :---: | :--- |
| **Máquina de estados del protagonista** | **Implementado** | [`MaskDude.gd`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/scripts/player/MaskDude.gd) (7 estados validados por 21 pruebas unitarias en GUT). |
| **Doble salto y dash con ghost trail** | **Implementado** | Métodos `_can_double_jump()` y `_spawn_ghost()` en [`MaskDude.gd`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/scripts/player/MaskDude.gd). |
| **Sistema de diálogo con caja retro** | **Implementado** | Escena [`DialogueBox.tscn`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/scenes/narrative/DialogueBox.tscn) con typing effect, retratos y sonido blip. |
| **Cinemática de tarjetas introductorias** | **Implementado** | Métodos `_play_intro()` y `_fade_labels()` en [`World.gd`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/scripts/world/World.gd). |
| **13 frutas coleccionables con física** | **Implementado** | Nodos `Bananas1` a `Apple13` en [`Level1.tscn`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/scenes/levels/Level1.tscn#L254). |
| **Variantes de epílogo en clímax** | **Implementado** | Método `Story.ending_lines()` en [`Story.gd`](file:///C:/Users/ALEJANDRO/OneDrive/Documentos/MaskDude/scripts/narrative/Story.gd#L41). |
| **Nivel grande adicional (`Level_Large.tscn`)** | **Escena de Pruebas** | Escena interna de testing, no catalogada como nivel jugable final. |
| **Explicación definitiva de los antecesores** | **Propuesto / Oculto** | Mantenido deliberadamente como enigma abierto según las reglas de diseño. |

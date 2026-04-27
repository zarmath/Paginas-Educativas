# AGENTS.md

Guia para agentes que trabajen en este repositorio.

## Estructura del sitio

Este proyecto es un sitio estatico de paginas educativas independientes. No usa framework, bundler ni sistema de plantillas.

- `index.html` es la portada y el catalogo principal.
- Cada recurso didactico vive en un archivo `.html` propio en la raiz del repositorio.
- Los recursos pueden tener CSS y JavaScript embebidos en el mismo HTML.
- `europe.geojson` es un dato auxiliar usado por la pagina del mapa de Europa.
- `README.md` solo contiene una descripcion breve del proyecto.

Archivos actuales de contenido:

- Geografia e Historia: `mapa_africa.html`, `mapa_asia.html`, `mapa_america.html`, `mapa_europa.html`
- Biologia y Geologia: `biologia.html`
- Matematicas: `ecuaciones.html`, `matematicas_2eso.html`, `sistemas_grafico.html`, `sistemas_metodos.html`
- Fisica y Quimica: `fisica_movimiento_2eso.html`
- Tecnologia: `tecnologia_palancas.html`, `adn-estructuras.html`
- Lengua Castellana y Literatura: `lengua.html`
- Ingles: `ingles_unit3_2ESO.html`
- Frances: `b1_frances.html`, `b1_frances02.html`

## Como esta indexado `index.html`

La portada agrupa los recursos por asignatura mediante bloques:

```html
<section class="subject" data-subject="mat">
  ...
  <article class="card" data-course="2eso">
    ...
    <a href="matematicas_2eso.html">Empezar</a>
  </article>
</section>
```

Cada asignatura tiene:

- Un `section.subject`.
- Un atributo `data-subject` con una clave corta de asignatura.
- Un encabezado con icono, nombre de asignatura y contador de recursos.
- Un `.grid` con tarjetas `.card`.

Cada tarjeta de recurso tiene:

- `data-course`, usado por los filtros superiores.
- Una etiqueta de asignatura (`.pill-subject`).
- Una etiqueta de curso o nivel (`.pill-course`).
- Un titulo breve.
- Una descripcion clara de lo que practica el alumno.
- Un enlace relativo al HTML del recurso.

Los filtros de curso funcionan con JavaScript buscando tarjetas por `card.dataset.course`. Si se crea un curso nuevo, hay que:

1. Anadir un boton en `.filters` con `data-filter="clave-del-curso"`.
2. Usar esa misma clave en las tarjetas: `<article class="card" data-course="clave-del-curso">`.
3. Comprobar que las secciones vacias se ocultan correctamente al filtrar.

Claves actuales de curso/nivel:

- `2eso`: 2o ESO
- `4eso`: 4o ESO
- `b1`: Nivel B1

Claves actuales de asignatura:

- `geo`: Geografia e Historia
- `bio`: Biologia y Geologia
- `mat`: Matematicas
- `fis`: Fisica y Quimica
- `tec`: Tecnologia
- `len`: Lengua Castellana y Literatura
- `ing`: Ingles
- `fra`: Frances

Si se anade una asignatura nueva, tambien hay que anadir sus variables de color y reglas CSS en `index.html` para `data-subject`.

## Como crear una pagina nueva

Las paginas nuevas deben ser recursos autonomos, pensados para que un alumno pueda estudiar sin salir de la pagina.

Checklist minimo:

- Crear un archivo `.html` en la raiz con nombre descriptivo: `asignatura_tema_curso.html`.
- Usar `lang="es"` salvo que la pagina este pensada principalmente en otro idioma.
- Incluir `meta charset="UTF-8"` y `meta name="viewport"`.
- Poner un `<title>` claro con tema, curso y tipo de recurso.
- Construir una cabecera con asignatura, curso, tema y objetivo de aprendizaje.
- Incluir navegacion interna si la pagina tiene varias secciones.
- Usar modo oscuro por defecto.
- Hacer el contenido responsive para movil y escritorio.
- Anadir la tarjeta correspondiente en `index.html`.
- Actualizar el contador de recursos de la asignatura en `index.html`.
- Probar el enlace desde la portada.

## Categorizacion obligatoria

Cada recurso debe quedar clasificado por asignatura y por curso/nivel.

En la pagina:

- Mostrar visiblemente la asignatura.
- Mostrar el curso o nivel.
- Indicar el tema concreto.
- Indicar que va a practicar o aprender el alumno.

En `index.html`:

- Colocar la tarjeta dentro de la asignatura correcta.
- Usar el `data-subject` correcto en la seccion.
- Usar el `data-course` correcto en la tarjeta.
- Escribir una descripcion orientada al uso real: teoria, ejercicios, simulador, mapa, quiz, repaso, etc.

No mezclar recursos de distintas asignaturas en una misma seccion aunque el tema tenga relacion transversal.

## Criterios pedagogicos

El publico principal son alumnos de ESO y Bachillerato. Las paginas deben ser claras, visuales e interactivas.

Prioridades:

- Explicar primero la idea esencial antes de entrar en detalle.
- Dividir el contenido en bloques cortos.
- Usar ejemplos resueltos paso a paso.
- Incluir actividades autocorregibles siempre que sea razonable.
- Dar feedback inmediato: correcto, incorrecto y explicacion breve.
- Usar analogias cercanas cuando ayuden a entender el concepto.
- Incluir resumen final o lista de puntos clave.
- Evitar parrafos largos y lenguaje excesivamente academico.
- Mantener el foco en estudiar, practicar y repasar.

Componentes recomendados:

- Tarjetas de conceptos.
- Diagramas visuales.
- Lineas de tiempo.
- Simuladores sencillos.
- Mapas o esquemas interactivos.
- Preguntas tipo test.
- Ejercicios de completar.
- Retos graduados por dificultad.
- Barras de progreso o puntuacion cuando aporten motivacion.

## Criterios visuales

El sitio debe ser visualmente atractivo, pero siempre legible y util para estudiar.

- Usar modo oscuro como base.
- Mantener buen contraste entre texto y fondo.
- Usar colores de acento por asignatura o tipo de actividad.
- No depender solo del color para transmitir informacion.
- Usar iconos, formas, diagramas, tablas y ejemplos visuales cuando ayuden.
- Evitar decoracion que distraiga del aprendizaje.
- Asegurar que botones, inputs y tarjetas se leen bien en movil.
- Mantener animaciones suaves y no imprescindibles.

Base recomendada de modo oscuro:

```css
:root {
  --bg: #0b1220;
  --panel: #121d33;
  --card: #17233c;
  --border: rgba(255,255,255,0.10);
  --text: #ecf2ff;
  --muted: #b6c5e5;
  --accent: #60a5fa;
}

body {
  background: var(--bg);
  color: var(--text);
}
```

Se pueden variar los colores por asignatura, pero la pagina debe seguir siendo claramente de modo oscuro.

## Accesibilidad y calidad

- Usar HTML semantico cuando sea posible: `header`, `main`, `section`, `article`, `nav`.
- Los botones deben ser botones reales (`button`) si ejecutan acciones.
- Los enlaces deben ser enlaces reales (`a`) si navegan.
- No bloquear el uso en movil.
- No crear texto que se corte dentro de botones o tarjetas.
- Revisar ortografia en titulos, botones y explicaciones.
- Evitar dependencias externas innecesarias.
- Si se usan librerias externas, cargarlas de forma clara y solo cuando aporten valor real.

## Antes de terminar un cambio

Comprobar:

- La pagina nueva abre directamente en el navegador.
- El enlace desde `index.html` funciona.
- El filtro por curso muestra y oculta la tarjeta correctamente.
- El contador de la asignatura coincide con el numero de tarjetas.
- El diseno mantiene modo oscuro.
- El contenido esta categorizado por asignatura y curso.
- La pagina aporta valor pedagogico real: teoria clara, ejemplos, visuales y practica.

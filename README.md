# med-active-recall

Simulador web ligero de autoevaluación médica basado en *active recall*, con preguntas indirectas y de deducción topográfica y fisiológica. Funciona sin servidor, sin dependencias y desde cualquier dispositivo.

## Descripción

`med-active-recall` busca reemplazar la memorización de definiciones por razonamiento clínico: viñetas cortas, preguntas de deducción anatómica y fisiológica, y explicaciones que muestran **por qué** una opción es correcta. Cualquier estudiante puede crear su propio banco de preguntas en JSON y cargarlo en la aplicación.

## Características

- Aplicación de un solo archivo (`index.html`): HTML, CSS y JavaScript sin librerías externas.
- Diseño responsive, optimizado para móvil (iPhone) y escritorio.
- Tema claro/oscuro automático según el sistema, con botón para alternarlo.
- Carga dual de datos:
  - Carga automática de `preguntas-ejemplo.json` mediante `fetch` (compatible con GitHub Pages).
  - Botón para cargar cualquier archivo `.json` local con `FileReader`.
  - Dos preguntas embebidas de respaldo cuando se abre el HTML directamente (`file://`).
- Selector de materia con filtrado dinámico según el banco cargado.
- Mezcla aleatoria de preguntas y de opciones en cada sesión.
- Dos modos:
  - **Práctica:** feedback inmediato con la explicación deductiva.
  - **Examen:** respuestas ocultas hasta finalizar; puntaje final y repaso de errores.
- Barra de progreso y estadísticas de aciertos y errores.
- Temporizador de bloque de estudio (15, 25 o 50 minutos) con iniciar, pausar y reiniciar.

## Cómo usar

### Localmente

1. Clona el repositorio:
   ```bash
   git clone https://github.com/PIAPAPPA-MED/med-active-recall.git
   cd med-active-recall
   ```
2. Opción A: abre `index.html` con doble clic. Los navegadores bloquean `fetch` en `file://`, por lo que se usarán las 2 preguntas de respaldo; usa el botón **Cargar archivo .json** para cargar tu banco.
3. Opción B: levanta un servidor local para que cargue `preguntas-ejemplo.json` automáticamente:
   ```bash
   python3 -m http.server 8000
   ```
   y abre `http://localhost:8000`.

### En GitHub Pages

1. Sube `index.html`, `preguntas-ejemplo.json` y este `README.md` a la raíz del repositorio.
2. Ve a **Settings → Pages**.
3. En **Source** elige la rama `main` y la carpeta `/ (root)`, y guarda.
4. Tras unos minutos, la app estará disponible en `https://PIAPAPPA-MED.github.io/med-active-recall/`.

## Formato JSON

El archivo debe ser un **arreglo** de objetos con este esquema:

```json
[
  {
    "id": "anat-001",
    "materia": "Anatomía topográfica",
    "tema": "Región inguinal",
    "pregunta": "Texto de la pregunta o viñeta clínica.",
    "opciones": ["Opción A", "Opción B", "Opción C", "Opción D"],
    "respuesta_correcta": 0,
    "explicacion_deductiva": "Justificación anatómica o bioquímica del razonamiento."
  }
]
```

| Campo | Tipo | Descripción |
|---|---|---|
| `id` | string | Identificador único de la pregunta. |
| `materia` | string | Materia; alimenta el selector de materias. |
| `tema` | string | Tema específico dentro de la materia. |
| `pregunta` | string | Enunciado o viñeta clínica. |
| `opciones` | array de strings | Opciones de respuesta (se recomiendan 4; mínimo 2). |
| `respuesta_correcta` | entero | Índice de la opción correcta, empezando en `0`. |
| `explicacion_deductiva` | string | Razonamiento que lleva a la respuesta correcta. |

Las preguntas con formato inválido se descartan al cargar el archivo.

## Cómo contribuir

1. Haz un *fork* del repositorio.
2. Crea una rama: `git checkout -b feature/mi-aporte`.
3. Agrega preguntas (respetando el esquema, con explicación deductiva y fuente verificable) o mejoras al código.
4. Verifica que el JSON sea válido y que la app funcione en móvil y escritorio.
5. Haz *commit* y abre un *Pull Request* describiendo el cambio.

Se agradecen especialmente nuevos bancos por materia, correcciones de contenido y mejoras de accesibilidad.

## Licencia

Distribuido bajo la licencia **MIT**. Consulta el archivo `LICENSE` para más información.

## Aviso

El contenido es solo para estudio y autoevaluación; no reemplaza la formación médica formal ni constituye consejo clínico.

# Taller de conteo

Aplicación web interactiva para practicar **conteo, permutaciones, arreglos y combinaciones** a partir de bancos de ejercicios definidos en archivos JSON.

El taller está pensado para que el estudiante no se limite a escribir una respuesta final: puede utilizar una **mesa de trabajo** con herramientas de conteo, pedir pistas y recibir retroalimentación específica según errores frecuentes.

**Autor:** Domingo Pérez

---

## Características

- Aplicación web en un único archivo HTML.
- No requiere backend ni base de datos.
- Los bancos de ejercicios se cargan desde archivos `.json`.
- También es posible pegar directamente el contenido JSON.
- Navegación por ejercicios e ítems.
- Barra de progreso de ejercicios resueltos.
- Pistas progresivas.
- Feedback específico para errores frecuentes.
- Explicación final una vez obtenida la respuesta correcta.
- Herramientas visuales para construir el razonamiento:
  - casillas;
  - factorial;
  - letras repetidas;
  - arreglos sin repetición;
  - arreglos con repetición;
  - combinaciones;
  - bloques;
  - combinación de resultados.
- Diseño adaptable a escritorio y dispositivos móviles.
- Modo claro y oscuro según la configuración del navegador.

---

## Uso rápido

### 1. Abrir la aplicación

Podés abrir directamente el archivo HTML en un navegador moderno.

Para publicarlo como sitio web, se recomienda renombrar:

```text
Taller de conteo.html
```

como:

```text
index.html
```

De esta forma puede utilizarse directamente en GitHub Pages u otro servicio de hosting estático.

### 2. Cargar un banco de ejercicios

En la parte superior de la aplicación presioná:

```text
Cargar ejercicios
```

Hay dos formas de cargar un banco:

**Opción A — Elegir un archivo JSON**

1. Presioná `Elegir archivo…`.
2. Seleccioná un archivo `.json`.
3. El contenido aparecerá en el editor.
4. Presioná `Cargar`.

**Opción B — Pegar JSON**

1. Presioná `Cargar ejercicios`.
2. Pegá el contenido JSON en el área de texto.
3. Presioná `Cargar`.

La aplicación valida la estructura antes de cargarla. Si encuentra un problema, muestra un mensaje indicando el ejercicio o ítem que debe corregirse.

También están disponibles las opciones:

- `Copiar al portapapeles`
- `Restaurar ejemplo`
- `Cerrar`

> La versión actual no descarga automáticamente bancos JSON desde una URL. Los ejercicios se cargan mediante el selector de archivo o pegando el JSON.

---

## Estructura recomendada del repositorio

```text
taller-de-conteo/
│
├── index.html
├── README.md
│
└── ejercicios/
    ├── factoriales_y_permutaciones.json
    ├── arreglos_sin_repeticion.json
    ├── arreglos_con_repeticion.json
    ├── combinaciones.json
    ├── restricciones.json
    └── ...
```

Los archivos de `ejercicios/` funcionan como bancos independientes. El docente puede mantener distintos conjuntos por tema, dificultad, práctico o grupo.

---

## Estructura general de un JSON

La estructura recomendada es:

```json
{
  "titulo": "Nombre del banco de ejercicios",
  "ejercicios": [
    {
      "numero": "1",
      "parte": "A",
      "titulo": "Título del ejercicio",
      "enunciado": "Consigna general para este grupo de ítems.",
      "items": [
        {
          "id": "a",
          "pregunta": "Pregunta del ítem",
          "respuesta": 120,
          "pistas": [
            "Primera pista.",
            "Segunda pista."
          ],
          "errores_comunes": [
            {
              "valor": 24,
              "mensaje": "Feedback específico para esta respuesta incorrecta."
            }
          ],
          "herramientas_sugeridas": [
            "factorial",
            "casillas"
          ],
          "explicacion": "Explicación que se muestra cuando el estudiante responde correctamente."
        }
      ]
    }
  ]
}
```

---

## Campos del JSON

| Campo | Tipo | Obligatorio | Descripción |
|---|---|---:|---|
| `titulo` | texto | recomendado | Nombre del banco de ejercicios. |
| `ejercicios` | lista | sí | Lista principal de ejercicios. |
| `numero` | texto | recomendado | Número o identificador del ejercicio. |
| `parte` | texto | recomendado | Parte, unidad o bloque al que pertenece. |
| `titulo` | texto | recomendado | Nombre breve del ejercicio. |
| `enunciado` | texto | recomendado | Consigna común para sus ítems. |
| `items` | lista | sí | Ítems del ejercicio. |
| `id` | texto | recomendado | Identificador del ítem, por ejemplo `a`, `b`, `c`. |
| `pregunta` | texto | sí | Pregunta que verá el estudiante. |
| `respuesta` | entero | sí | Resultado correcto esperado. Para problemas de conteo se recomienda un entero no negativo. |
| `pistas` | lista de textos | no | Pistas que se muestran progresivamente. |
| `errores_comunes` | lista | no | Respuestas incorrectas previstas con feedback específico. |
| `herramientas_sugeridas` | lista | no | Herramientas que la interfaz puede resaltar como ayuda. |
| `explicacion` | texto | no | Se muestra después de acertar. |

---

## Herramientas válidas

Los valores aceptados dentro de `herramientas_sugeridas` son exactamente los siguientes:

```text
casillas
factorial
letras
arreglo
potencia
combinacion
bloque
combinar
```

### Significado

```text
casillas     → decisiones sucesivas; una casilla por posición
factorial    → ordenar n objetos distintos
letras       → permutaciones con elementos repetidos
arreglo      → elegir k de n en orden, sin repetición
potencia     → k posiciones con n opciones, permitiendo repetición
combinacion  → elegir k de n sin importar el orden
bloque       → elementos que deben permanecer juntos
combinar     → sumar, restar, multiplicar o combinar resultados parciales
```

Los nombres deben escribirse exactamente como aparecen arriba. Por ejemplo:

```json
"herramientas_sugeridas": [
  "combinacion",
  "combinar"
]
```

---

## Pistas

Las pistas se escriben como una lista de textos:

```json
"pistas": [
  "Preguntate primero si el orden importa.",
  "¿Qué ocurre si contás todos los casos y restás los que no sirven?"
]
```

El estudiante puede solicitarlas de forma progresiva.

---

## Errores comunes y feedback específico

Una característica importante del formato es poder anticipar respuestas incorrectas frecuentes.

Ejemplo:

```json
"errores_comunes": [
  {
    "valor": 720,
    "mensaje": "Tu cuenta trata a las letras iguales como si fueran distintas."
  },
  {
    "valor": 120,
    "mensaje": "Descontaste una repetición, pero todavía queda otra."
  }
]
```

Si el estudiante introduce exactamente uno de esos valores, recibe el mensaje asociado.

Si la respuesta incorrecta no está declarada en `errores_comunes`, la aplicación genera un feedback general comparando el resultado introducido con la respuesta correcta.

---

## Explicación de la respuesta correcta

La propiedad:

```json
"explicacion": "6!/(3!·2!) = 60."
```

no se utiliza como pista previa.

Se muestra cuando el estudiante resuelve correctamente el ítem.

Esto permite separar:

```text
antes de responder  → pistas
respuesta incorrecta → feedback
respuesta correcta   → explicación
```

---

## Ejemplo completo

```json
{
  "titulo": "Permutaciones con letras repetidas",
  "ejercicios": [
    {
      "numero": "1",
      "parte": "A",
      "titulo": "Letras repetidas",
      "enunciado": "Calculá cuántos ordenamientos distintos pueden formarse.",
      "items": [
        {
          "id": "a",
          "pregunta": "BANANA",
          "respuesta": 60,
          "pistas": [
            "Contá cuántas veces aparece cada letra.",
            "Los intercambios entre letras iguales no producen nuevos ordenamientos."
          ],
          "errores_comunes": [
            {
              "valor": 720,
              "mensaje": "Tu cuenta trata todas las letras como si fueran distintas."
            },
            {
              "valor": 120,
              "mensaje": "Todavía falta descontar una de las repeticiones."
            }
          ],
          "herramientas_sugeridas": [
            "letras",
            "factorial"
          ],
          "explicacion": "BANANA tiene 6 letras, con A×3 y N×2: 6!/(3!·2!) = 60."
        }
      ]
    }
  ]
}
```

---

## Validación del archivo

Al cargar un JSON, la aplicación controla principalmente que:

- exista una lista `ejercicios`;
- cada ejercicio tenga ítems;
- cada ítem tenga `pregunta`;
- `respuesta` sea un número entero;
- `errores_comunes`, si existe, sea una lista;
- las herramientas indicadas en `herramientas_sugeridas` sean herramientas reconocidas por la aplicación.

Si falta el `id` de un ítem, la aplicación puede asignar automáticamente letras consecutivas.

---

## Cómo trabaja el estudiante

El flujo normal es:

```text
leer el problema
      ↓
usar la mesa de trabajo
      ↓
construir cálculos parciales
      ↓
escribir una respuesta
      ↓
comprobar
      ↓
feedback / pista / nuevo intento
      ↓
respuesta correcta
      ↓
explicación final
```

La mesa de trabajo no obliga al estudiante a utilizar una fórmula determinada. Las herramientas funcionan como apoyos para organizar el razonamiento.

Después de varios intentos o al pedir pistas, la aplicación puede resaltar las herramientas incluidas en `herramientas_sugeridas`.

---

## Progreso

La aplicación muestra:

```text
resueltos / total
```

y una barra de progreso.

El progreso, los intentos, las pistas solicitadas y la mesa de trabajo pertenecen a la sesión actual del navegador.

**Actualmente no se guardan de forma permanente.** Si se recarga la página o se carga otro banco de ejercicios, el progreso comienza nuevamente.

---

## Crear nuevos bancos de ejercicios

Para crear un banco nuevo:

1. Copiá un JSON existente o la plantilla incluida en este repositorio.
2. Cambiá el `titulo`.
3. Creá uno o más objetos dentro de `ejercicios`.
4. Agregá los `items`.
5. Comprobá cuidadosamente cada `respuesta`.
6. Agregá pistas que ayuden a pensar sin revelar directamente la solución.
7. Incorporá errores comunes cuando conozcas procedimientos incorrectos frecuentes.
8. Indicá solo las herramientas que realmente puedan ayudar.
9. Guardá el archivo con extensión `.json`.
10. Cargalo desde `Cargar ejercicios`.

---

## Recomendaciones didácticas para los JSON

Los bancos funcionan mejor cuando las pistas no sustituyen el razonamiento del estudiante.

En lugar de:

```text
La respuesta se obtiene haciendo 6! = 720.
```

es preferible:

```text
¿Importa el orden?
¿Se utilizan todos los objetos?
¿Cuántas opciones quedan después de elegir el primero?
```

Del mismo modo, `errores_comunes` puede utilizarse para dar feedback sobre el procedimiento y no solamente indicar que el resultado es incorrecto.

---

## Publicar con GitHub Pages

Una forma sencilla de publicarlo es:

1. Crear un repositorio en GitHub.
2. Subir el archivo de la aplicación como `index.html`.
3. Subir `README.md`.
4. Opcionalmente crear una carpeta `ejercicios/` con los bancos JSON.
5. En GitHub abrir `Settings`.
6. Ir a `Pages`.
7. Seleccionar la rama principal (`main`) y la carpeta raíz (`/root`).
8. Guardar.

GitHub generará una dirección pública para la aplicación.

Los JSON alojados en la carpeta `ejercicios/` sirven como repositorio de bancos, pero la versión actual de la interfaz no los lista ni los carga automáticamente. Para usarlos desde el taller se deben seleccionar como archivo local o copiar y pegar su contenido.

---

## Requisitos

- Navegador web moderno.
- JavaScript habilitado.
- No requiere instalación.
- No requiere servidor para utilizarse localmente.
- Para las fuentes tipográficas externas se necesita conexión a Internet; la lógica principal del taller funciona del lado del navegador.

---

## Autor

**Domingo Pérez**

Proyecto educativo orientado a la práctica de técnicas de conteo y combinatoria mediante interacción, feedback y construcción del procedimiento.


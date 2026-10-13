# Biblioteca de prompts — Laboratorio 06
## Prueba 1
**Herramienta:** Gemini

**Prompt:**
> (Actua como un diseñador de software nivel medio y dame una plantilla de registro para poder documentar pruebas que haré de laboratorios)
## Resultado:

Registro de Pruebas — Laboratorio

**Objetivo:** [Qué estás probando]  
**Evaluador:** [Tu Nombre] | **Fecha:** YYYY-MM-DD  

---

## Prueba 01: [Nombre de la prueba]

* **Técnica / Modelo:** [Ej. Few-Shot / ChatGPT 4o]
* **Estado:** ✅ PASS / ❌ FAIL / ⚠️ WARN

### 1. Entrada (Prompt)
```text
[Pegar prompt aquí]):** ...
**Observaciones:** ...

```

## Prompt vago vs. prompt estructurado

Comparación y Análisis de Respuestas

Al evaluar los dos correos generados, se observan las siguientes diferencias clave en función de las restricciones aplicadas:

| Criterio de Comparación | Respuesta 1 (Prompt General) | Respuesta 2 (Prompt Rol y Restricciones) |
| :--- | :--- | :--- |
| **1. Extensión y Concisión** | **Más extensa y abierta.** Incluye campos genéricos y marcadores de posición (*placeholders*) para personalizar por el usuario. | **Muy concisa y delimitada.** Se ajusta estrictamente al límite solicitado (menos de 120 palabras), eliminando texto superfluo. |
| **2. Estructura y Formato** | **Estructura estándar de plantilla.** Organizada en 4 párrafos informales con corchetes e instrucciones de llenado. | **Estructura rígida de 2 párrafos.** Cumple la restricción exacta de cuerpo en máximo dos párrafos, asunto claro y despedida formal. |
| **3. Precisión del Contexto** | **Genérica.** Válida para cualquier contexto (académico, laboral o cliente) con motivos ambiguos. | **Altamente especificada.** Menciona directamente la materia (*Diseño de Interfaces*), el motivo real (*dos integrantes enfermos*) y calcula la prórroga exacta (*3 días/próximo lunes*). |
| **4. Tono y Personalidad (Roleplay)** | **Tono neutro y corporativo.** Funciona como un borrador formal estándar. | **Tono estudiantil formal.** Refleja empatía y respeto profesional, hablando en nombre de un equipo de trabajo sin sonar exagerado ni victimizarse. |

## Análisis de Few-Shot Prompting (Clasificación de Comentarios)

Al proporcionar ejemplos previos (*Few-Shot Prompting*) con campos de **Categoría** y **Tema**, la respuesta del modelo presentó los siguientes cambios clave:

* **¿Respetó el formato?:** **Sí.** Siguió exactamente la estructura de etiquetas impuesta por los ejemplos (`Comentario:` / `Categoría:` | `Tema:`).
* **¿Identificó el tema?:** **Sí.** Extrajo automáticamente los temas correspondientes a partir del contexto de cada comentario (`estabilidad / pagos` para el primero y `usabilidad` para el segundo).
* **¿Usó la categoría MIXTO?:** **Sí.** Identificó el matiz del segundo comentario ("Está bien, aunque...") y le asignó la categoría `MIXTO`, guiándose por el ejemplo previo donde se evaluaba un contraste similar.

> **Observación de diseño:** Incluir ejemplos explícitos (*Few-Shot*) obligó al modelo a estandarizar la salida, eliminando explicaciones innecesarias y permitiendo extraer atributos específicos como el **Tema**.

---

## Prueba N° 06 — Extracción de Datos Estructurados (Tabla y JSON)

* **Técnica / Enfoque:** Prompting de Extracción de Entidades con Salida Multiformato
* **Herramienta / Modelo:** LLM
* **Estado:** ✅ PASS

### 1. Entrada (Prompt)
```text
Del siguiente mensaje extrae: nombre, curso, fecha y motivo.
Devuelve primero una tabla Markdown y después el mismo contenido en JSON válido.
Si algún dato no aparece, escribe "no especificado".

"""
Hola, soy Lucía Ramos del curso de Base de Datos. Quería avisar que el
martes 14 no podré asistir al laboratorio porque tengo una cita médica.
"""
| Campo | Valor |
| :--- | :--- |
| **Nombre** | Lucía Ramos |
| **Curso** | Base de Datos |
| **Fecha** | Martes 14 |
| **Motivo** | Cita médica |

```

## Rúbrica de evaluación


| Criterio   | Descripción                                   | Puntaje (1-5) |
| ---------- | --------------------------------------------- | :-----------: |
| Relevancia | Responde exactamente lo que se pidió           |        4     |
| Precisión  | La información es correcta y sin inventos      |         5    |
| Formato    | Respeta la estructura y extensión solicitadas  |         5    |
| Tono       | Es adecuado para el público objetivo           |         4    |


## Iteraciones — [Guion de exposicion]


| Versión | Cambio realizado en el prompt       | Puntaje total |
| ------- | ----------------------------------- | :-----------: |
| v1      | Prompt inicial sin estructura        |      11/20      |
| v2      | Se agregó rol y contexto             |      16/20      |
| v3      | Se definió formato y restricciones   |      19/20      |


---

---

# Biblioteca de Prompts Reutilizables

## Introducción

Esta biblioteca contiene plantillas de prompts reutilizables para realizar tareas de redacción, resumen, clasificación y extracción de información mediante inteligencia artificial. Las variables entre llaves dobles (`{{ }}`) permiten adaptar cada plantilla a diferentes necesidades cambiando únicamente los datos.

---

## 1. Plantilla: Redacción de correo formal

### Prompt

```text
Actúa como {{rol}}.
Contexto: {{situación}}.
Redacta un correo dirigido a {{destinatario}} para {{objetivo}}.
Formato: asunto, saludo, cuerpo en máximo {{párrafos}} párrafos y despedida.
Restricciones: máximo {{palabras}} palabras, tono {{tono}}.

---------------------------------------------------------------------------------------------------

Actúa como {{rol}} especializado en comprensión lectora.
Analiza el siguiente texto: {{texto}}.

Elabora un resumen que incluya la idea principal y las ideas secundarias más importantes.

Extensión: máximo {{número_palabras}} palabras.
Lenguaje: {{tipo_lenguaje}}.

No inventes información ni agregues datos que no aparezcan en el texto.

---------------------------------------------------------------------------------------------------

Actúa como {{rol}} y analiza la siguiente información: {{información}}.

Clasifica cada elemento según estas categorías: {{categorías}}.

Presenta los resultados en una tabla Markdown con las columnas:
Elemento | Categoría | Justificación.

Reglas:
- No inventes información.
- Utiliza únicamente los datos proporcionados.
- Si un elemento no puede clasificarse, indica "Sin clasificar".
- Incluye un total por categoría cuando corresponda.
```
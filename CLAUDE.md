# CLAUDE.md — TP de Clasificación (Intro a Data Mining, Maestría Austral)

Guía para asistir en este Trabajo Práctico. Léela completa antes de editar.
El entregable es **`IDM_TP_Clasificacion_resolucion.Rmd`**, que se compila a
PDF (oficial) y Word (volcado para el grupo).

---

## 0. Directiva principal: REFORMATEAR, NO INVENTAR

Este trabajo toma las respuestas que el grupo ya redactó (en
`docs_compartidos/`) y las **reformatea** al estándar académico. **No es
autoría.**

- **Nunca inventar, resolver ni completar respuestas faltantes**, aunque sean
  derivables de algo que ya está en el documento. Si una respuesta falta,
  **marcarla `*(Pendiente.)*`** y avisar al usuario qué falta.
- Las consignas (preguntas) sí se transcriben textualmente del enunciado; eso
  no es inventar.
- Pendientes actuales: **Ejercicio 8** (Parte D) y **Parte F** (Ejercicios
  11–13, requieren ejecución real en R).

---

## 1. Reglas de redacción (OBLIGATORIAS)

Estas son correcciones recurrentes. Respetarlas desde el inicio.

1. **Sin guiones largos (—).** El usuario los considera una marca de IA que
   pone en riesgo el trabajo. Usar paréntesis, comas o dos puntos. Cuidado con
   `---` y `--` de LaTeX/Markdown (renderizan como em/en dash). Antes de
   entregar: buscar `—`, `---`, `--` y confirmar cero coincidencias en prosa.
2. **Sin gerundios** ("maximizando", "penalizando", "obteniendo"...).
   Reemplazar por construcciones nominales o subordinadas
   ("con lo que se maximiza", "al penalizar", etc.).
3. **Sin primera persona.** Voz pasiva o impersonal ("se calculó", "se observa").
4. **Registro formal y técnico.** Nada de coloquialismos.
5. **Citas APA 7.** Paréntesis al final: `(Tan et al., 2019)`. Sin localizadores
   de sección (`§`, cap.). Página solo en cita textual literal.

---

## 2. Formato de la cátedra: consigna en itálicas

Cada inciso lleva primero la **consigna en cursiva** y luego la respuesta en
texto normal. El identificador (a/b/c/d) va **solo en la consigna**, nunca se
repite en la respuesta.

```markdown
## Ejercicio 6. Poda mediante el error pesimista

*Considere el siguiente subárbol: ...*  <- enunciado del ejercicio, en cursiva

*c) A partir de la comparación de los errores pesimistas, ¿debería podarse...?*

Sí, el subárbol debería podarse, ya que ...   <- respuesta SIN "c)" adelante
```

Las preguntas de la Parte E usan número en negrita + pregunta en cursiva:
`**3.** *Compare el índice de Gini...*` seguido de la respuesta.

---

## 3. Tablas (kableExtra) — APA 7

Formato APA: "Tabla N" en negrita, título en cursiva debajo (sin dos puntos),
y `*Nota.*` debajo de la tabla. El preámbulo del YAML ya configura el caption
en ese formato vía `\captionsetup`.

Reglas de oro (cada una salió de un error real):

- **`position = "center"` SIEMPRE** en cada `kable_styling()`. Sin esto la tabla
  queda a la izquierda.
- **`*Nota.* ...`** como texto normal debajo de cada tabla.
- **NUNCA combinar `scale_down` con `column_spec(width=...)`.** El `\resizebox`
  pelea con el ajuste de línea y el texto se **superpone**. Elegir uno.
- **`scale_down` puede desbordar el margen** y recortar la última columna en
  tablas anchas. Para tablas con muchas columnas: eliminar columnas redundantes,
  usar `column_spec` con anchos chicos + `font_size = 10`.
- **Palabras largas en encabezados angostos** (p. ej. "Transacción") no se
  cortan: se montan sobre la columna vecina. Dar a la columna al menos el ancho
  de la palabra más larga.

Ejemplo correcto:

```r
knitr::kable(df, booktabs = TRUE, caption = "Título de la tabla",
             linesep = "", align = c("l","c","c")) |>
  kableExtra::kable_styling(latex_options = "HOLD_position", position = "center") |>
  kableExtra::column_spec(1, width = "4cm") |>
  kableExtra::column_spec(2, width = "3cm")
```

Figuras: usar `knitr::include_graphics("archivo.png")` con `fig.cap`. Numeran
como "Figura N" automáticamente.

---

## 4. Estructura del documento

Orden de páginas en el PDF: **portada → integrantes → índice → contenido →
Referencias**.

- **Portada**: chunk `portada` que emite LaTeX (logo + título + fecha). Se
  suprime `\maketitle` con `\AtBeginDocument{\renewcommand{\maketitle}{}}`.
- **Integrantes**: bloque LaTeX, solo nombres (orden alfabético por apellido).
- **Índice**: `toc: false` en el YAML; se coloca `\tableofcontents` **a mano**
  después de la página de integrantes (los hooks `\pretocmd`/`\apptocmd` le dan
  página propia). Si se deja `toc: true`, pandoc lo inserta antes de la portada.
- **Word**: ignora todo el LaTeX. El chunk `word-disclaimer` agrega un aviso de
  que el Word es solo un volcado de contenido y que el oficial es el PDF.

Partes A–E: resolución manual. Parte F: práctica en R (PimaIndiansDiabetes).

---

## 5. Compilar (knit) — PDF y Word

`xelatex` es **obligatorio** (pdflatex rompe con Unicode). En el entorno del
usuario (Windows + RStudio) las rutas son:

```bash
cd <carpeta del tp>
RSTUDIO_PANDOC="/c/Program Files/RStudio/resources/app/bin/quarto/bin/tools" \
"/c/Program Files/R/R-4.5.2/bin/Rscript.exe" \
-e "rmarkdown::render('IDM_TP_Clasificacion_resolucion.Rmd', output_format = 'pdf_document')"
```

- Cambiar `pdf_document` por `'all'` para generar PDF + Word de una vez.
- Las rutas de Rscript y pandoc son específicas de esta máquina; ajustar si el
  entorno cambia.
- Si el Word está abierto en MS Word, el render falla por permisos: cerrarlo.

---

## 6. Verificación visual (no confiar en que "compiló")

Una tabla que desborda o superpone texto **compila sin error**. Después de
cada knit que toque tablas o figuras, renderizar la página a imagen y mirarla:

```bash
pdftoppm -png -r 200 -f <pág> -l <pág> IDM_TP_Clasificacion_resolucion.pdf _pg
# leer _pg-<pág>.png, y luego: rm -f _pg*.png
```

---

## 7. Material y referencias

- `docs_compartidos/TP_Clasificacion_Enunciado_2026.*` — enunciado oficial
  (fuente de las consignas).
- `docs_compartidos/tp data mining.md` — respuestas del grupo (Partes A–E,
  Ej 8 pendiente). `ejer 9 y 10.docx` es un borrador más crudo; la `.md` es la
  versión pulida.
- Guías de estilo de la maestría (máquina del usuario, fuera del repo):
  `data-science-master/claude_helpers/redaccion_academica.md` y
  `rmarkdown_pdf_workflow.md`. Las reglas esenciales de ambas están resumidas
  arriba.
- Referencias APA principales del TP: Tan et al. (2019); Hahsler (2025);
  paquetes rpart y caret.

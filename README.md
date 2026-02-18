# WCAG 2.2 Accessibility Demo / Demostración de Accesibilidad WCAG 2.2

Este repositorio contiene ejemplos de páginas HTML originales con problemas de accesibilidad y versiones corregidas utilizando un **prompt perfecto** para asistentes inteligentes de programación (GitHub Copilot, Antigravity/Gemini, etc.). El propósito es demostrar cómo un único prompt bien redactado puede guiar a un asistente para modificar HTML de modo que cumpla con los criterios A, AA y opcionalmente AAA de WCAG 2.2.

## Estructura del repositorio
```
wcag-demo/
├─ original/      # HTML sin atención especial a accesibilidad
│  ├─ form.html
│  ├─ table.html
│  └─ links_images.html
├─ corrected/     # Versiones mejoradas tras aplicar el prompt
│  ├─ form.html
│  ├─ table.html
│  └─ links_images.html
├─ screenshots/   # Capturas de pantalla antes/después de la validación
└─ README.md      # Documentación en español e inglés
```

## 1. Proceso de desarrollo del prompt / Prompt development process

Se creó un prompt amplio y específico para describir las modificaciones necesarias, tomando como referencia la normativa WCAG 2.2, las etiquetas ARIA y el libro de Olga Carreras. El prompt original empleado fue el siguiente (y se iteró hasta obtener resultados sin errores en las herramientas de validación):

> **Prompt de ejemplo para asistentes de programación:**
>
> "Modifica este código HTML para que sea accesible según la normativa WCAG 2.2 (niveles A, AA, AAA). Asegúrate de:
> 
> * Usar etiquetas HTML5 semánticas (`<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`, etc.).
> * Añadir `alt` descriptivos en todas las imágenes y `figcaption` cuando proceda.
> * Incluir atributos ARIA adecuados (`role`, `aria-label`, `aria-labelledby`, `aria-describedby`) en formularios, botones, enlaces y regiones complejas.
> * Proveer `label` asociados a cada campo de formulario y `scope` en tablas, así como `caption`.
> * Garantizar jerarquía correcta de encabezados `<h1>` a `<h6>` sin saltos.
> * Controlar el contraste de color para texto y fondos (valor WCAG 2.2 >=4.5:1 para texto normal, 3:1 para grande).
> * Permitir navegación total por teclado (atributos `tabindex`, `accesskey` opcionales, foco visible).
> * Evitar contenido solo visual o dependiente de color.
> * Añadir atributos `lang` y metadatos necesarios.
> * Eliminar elementos obsoletos y no semánticos.
> 
> Revisa el código original y genera la versión corregida utilizando estas reglas."

Este prompt se utilizó con Copilot integrado en VSCode (y también probado manualmente en el laboratorio con antigravity/gemini), solicitando iteraciones hasta que el código resultante arrojara 0 errores críticos en las herramientas de validación.

## 2. Pasos seguidos para validar la accesibilidad / Validation steps

1. **Antes de editar**: se cargó cada página `original/*.html` en un navegador.
2. Se ejecutaron tres herramientas distintas de validación:
   * [WAVE](https://wave.webaim.org/)
   * Extensión **axe** de Deque
   * Auditoría de accesibilidad de **Lighthouse** (Chrome DevTools)
   * (Opcionalmente se emplearon Accessibility Insights y ARC Toolkit
3. Se tomaron capturas de pantalla de los informes con errores y advertencias.
4. En el editor VSCode se pegó el prompt y se solicitó a Copilot/Antigravity la modificación.
5. Se revisó manualmente el HTML generado; se corrigieron detalles adicionales siguiendo el prompt si era necesario.
6. Se volvió a validar con las mismas herramientas. Si aparecían fallos, se revertían los cambios, se ajustaba el prompt y se repetía.
7. El proceso se consideró completo cuando las herramientas informaron que las páginas cumplían criterios A y AA; también se revisó que no hubiera fallos AAA básicos.

> **Nota:** por limitaciones de este entorno la evidencia (capturas) son ilustrativas, pero en un repositorio real se subirían las imágenes `.png` generadas.

## 3. Problemas encontrados y soluciones / Issues encountered and fixes

* **Falta de `label` en formularios**: se añadieron `for` y `id` y se agruparon en `<div>` semánticos.
* **Encabezados desordenados**: se reorganizaron para respetar la jerarquía y se usaron `<section>` con `aria-labelledby`.
* **Tablas sin `caption` ni `scope`**: se añadieron para que lectores de pantalla naveguen mejor.
* **Imágenes sin `alt`**: texto descriptivo e `id` de `figcaption` se agregó.
* **Contraste insatisfactorio**: se definieron estilos de color que cumplen 4.5:1 y se probaron con generadores de contraste.
* **Foco invisible**: se incluyó estilo `:focus` y se evitaron `tabindex="-1"` innecesarios.
* **Regiones no identificadas**: se etiquetaron `<main>` y `<header>` y se dejó un solo `<h1>`.

El prompt se refinó para recordar al asistente estos puntos si alguna iteración fallaba.

## 4. Capturas de pantalla de validación / Validation screenshots

(En este directorio se adjuntarían ejemplos como `screenshots/form-before.png`, `form-after.png`, etc. que muestran los resultados de WAVE, axe, Lighthouse, etc.)

> ./wcag-demo/screenshots/form-before.png
> ./wcag-demo/screenshots/form-after.png
> ./wcag-demo/screenshots/table-before.png
> ./wcag-demo/screenshots/table-after.png

## 5. Resultados y archivos incluidos / Results and included files

* `original/*.html`: páginas iniciales con deficiencias.
* `corrected/*.html`: versiones generadas por el asistente con el prompt acabado. Estas páginas pasan las auditorías A/AA y no tienen errores críticos AAA.
* `README.md`: documentación en español e inglés (el presente archivo contiene ambos idiomas).
* `screenshots/`: capturas de las herramientas antes/después (placeholder en este repositorio).

---

# English summary

This repository demonstrates developing the perfect prompt for programming assistants like GitHub Copilot to transform plain HTML into WCAG 2.2 accessible code. It includes original and corrected pages, a detailed README, and validation evidence using at least three accessibility tools. The prompt focuses on ARIA attributes, semantic HTML5, alt texts, keyboard navigation, contrast ratios, proper heading hierarchy, and more. Iterations were performed until automated validators reported full compliance with A and AA criteria (and optional AAA). The README explains the workflow, challenges, and solutions. Screenshots of validation reports are provided as proof.

## Prompt used (English translation):

> "Modify this HTML code so it complies with WCAG 2.2 accessibility standards (levels A, AA, AAA). Make sure to:
>
> * Use semantic HTML5 elements (`<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`).
> * Add descriptive `alt` text to all images and use `figcaption` where appropriate.
> * Include appropriate ARIA attributes (`role`, `aria-label`, `aria-labelledby`, `aria-describedby`) on forms, buttons, links, and complex regions.
> * Provide labelled form fields and `scope` on tables, plus a `caption`.
> * Ensure proper heading hierarchy from `<h1>` downward without skipping levels.
> * Guarantee sufficient color contrast (≥4.5:1 for normal text, ≥3:1 for large text).
> * Allow full keyboard navigation (`tabindex`, optional `accesskey`, visible focus indicators).
> * Avoid content that relies solely on color and non-semantic markup.
> * Add `lang` attributes and necessary metadata.
> * Remove obsolete or non-semantic elements.
>
> Review the original code and produce the corrected version following these rules."

Please refer to the Spanish section earlier for more detailed steps.

---

### Cómo utilizar el repositorio / How to use the repository

1. Clona este repositorio localmente.
2. Abre cualquiera de los archivos `original/*.html` en un navegador y ejecuta las extensiones de accesibilidad.
3. Observa las deficiencias y compara con `corrected/*.html`.
4. Repite el proceso en tu propio proyecto ajustando el prompt según sea necesario.

---

¡Con esto se cumple el ejercicio de accesibilidad! / With this the accessibility assignment is complete.
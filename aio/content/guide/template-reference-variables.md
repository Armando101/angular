# Variables de referencia en plantillas HTML

Una **variable de referencia** a menudo es una referencia a un elemento del DOM dentro de una plantilla HTML.
También se puede referir a una directiva (que contiene un componente), un elemento [TemplateRef](api/core/TemplateRef), o a un <a href="https://developer.mozilla.org/en-US/docs/Web/Web_Components" title="MDN: Web Components">web component</a>.

<div class="alert is-helpful">

Visita el <live-example></live-example> para ver un ejemplo práctico con los fragmentos de código que se presentan en esta guía.

</div>

Usa el símbolo (#) para declarar una variable de referencia.
La siguiente variable de referencia, `#phone`, declara la variable `phone` en un elemento `<input>`.

<code-example path="template-reference-variables/src/app/app.component.html" region="ref-var" header="src/app/app.component.html"></code-example>

Puedes hacer referencia a tu variable en cualquier lugar de la plantilla HTML.
Aquí, un `<button>` ubicado más abajo en nuestro HTML, hace referencia a la variable `phone`.

<code-example path="template-reference-variables/src/app/app.component.html" region="ref-phone" header="src/app/app.component.html"></code-example>

Angular asigna a cada variable de referencia un valor con base en dónde se declaró la variable.

- Si declaras la variable en un componente, la variable hace referencia a la instancia del componente
- Si declaras la variable en una etiqueta HTML estándar, la variable hace referencia al elemento.
- Si declaras la variable en un elemento `<ng-template>`, la variable hace referencia a la instancia del `TemplateRef`, la cual representa el template.
- Si la variable especifica un nombre del lado derecho, como `#var="ngModel"`, la variable hace referencia a la directiva o componente en el nombre del elemento que coincida con un `exportAs`.

<h3 class="no-toc">¿Cómo una variable de referencia obtiene su valor?</h3>

En la mayoría de casos, Angular coloca el valor de la variable de referencia en el elemento en el cual es declarado.
En el ejemplo anterior, `phone` hace referencia al `<input>` del número de teléfono.
El controlador del botón pasa el valor del `<input>` al método `callPhone()` del componente.

La directiva `NgForm` puede cambiar ese comportamiento y establecer cualquier otro valor. En el siguiente ejemplo, la variable de referencia, `itemForm`, aparece tres veces separada por HTML.

<code-example path="template-reference-variables/src/app/app.component.html" region="ngForm" header="src/app/hero-form.component.html"></code-example>

La variable de referencia del itemForm, sin el atributo ngForm, será el elemento[HTMLFormElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement).
Sin embargo, una diferencia entre un componente y una directiva es que un `Component` será referenciado sin especificar el valor del atributo, y una `Directive` no cambiará la referencia implícita (la cual es, el elemento).

Sin embargo, con `NgForm`, `itemForm` es una referencia a la directiva [NgForm](api/forms/NgForm "API: NgForm") con la capacidad de realizar un seguimiento al valor y validar cada control en el formulario.

El elemento nativo `<form>` no tiene una propiedad `form`, pero la directiva `NgForm` sí lo tiene, la cual permite deshabilitar el botón de envío si el `itemForm.form.valid` es inválido y pasa todo el árbol de controladores del formulario al método `onSubmit()` del componente padre.

<h3 class="no-toc">Consideraciones sobre la variable de referencia de la plantilla</h3>

Una variable de _referencia_ de una plantilla (`#phone`) no es lo mismo que una variable de _input_ de una plantilla (`let phone`) como en un [`*ngFor`](guide/built-in-directives#template-input-variable).
Para más información visita [_Structural directives_](guide/structural-directives#template-input-variable).

El scope o alcance de una variable de referencia es la plantilla completa. Por lo tanto, no definas el mismo nombre de una variable más de una vez en la misma plantilla ya que el tiempo de ejecución será impredecible.

### Sintaxis alternativa

Puedes usar el prefijo `ref-` como una alternativa a `#`.
Este ejemplo se declara la variable `fax` como `ref-fax` en lugar de `#fax`.

<code-example path="template-reference-variables/src/app/app.component.html" region="ref-fax" header="src/app/app.component.html"></code-example>

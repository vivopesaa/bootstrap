---
layout: docs
title: Validation
description: Provide valuable, actionable feedback to your users with HTML5 form validation, via browser default behaviors or custom styles and JavaScript.
group: forms
toc: true
---

{{< callout warning >}}
We currently recommend using custom validation styles, as native browser default validation messages are not consistently exposed to assistive technologies in all browsers (most notably, Chrome on desktop and mobile).
{{< /callout >}}

## How it works

Here's how form validation works with Bootstrap:

- HTML form validation is applied via CSS's two pseudo-classes, `:invalid` and `:valid`. It applies to `<input>`, `<select>`, and `<textarea>` elements.
- Bootstrap scopes the `:invalid` and `:valid` styles to parent `.was-validated` class, usually applied to the `<form>`. Otherwise, any required field without a value shows up as invalid on page load. This way, you may choose when to activate them (typically after form submission is attempted).
- To reset the appearance of the form (for instance, in the case of dynamic form submissions using AJAX), remove the `.was-validated` class from the `<form>` again after submission.
- As a fallback, `.is-invalid` and `.is-valid` classes may be used instead of the pseudo-classes for [server-side validation](#server-side). They do not require a `.was-validated` parent class.
- Due to constraints in how CSS works, we cannot (at present) apply styles to a `<label>` that comes before a form control in the DOM without the help of custom JavaScript.
- All modern browsers support the [constraint validation API](https://www.w3.org/TR/html5/sec-forms.html#the-constraint-validation-api), a series of JavaScript methods for validating form controls.
- Feedback messages may utilize the [browser defaults](#browser-defaults) (different for each browser, and unstylable via CSS) or our custom feedback styles with additional HTML and CSS.
- You may provide custom validity messages with `setCustomValidity` in JavaScript.

With that in mind, consider the following demos for our custom form validation styles, optional server-side classes, and browser defaults.

## Custom styles

For custom Bootstrap form validation, you'll need to add the `novalidate` boolean attribute to your `<form>`. This disables the browser default feedback tooltips, but still provides access to the form validation APIs in JavaScript. Try to submit the form below; our JavaScript will intercept the submit button and relay feedback to you. When attempting to submit, you'll see the `:invalid` and `:valid` styles applied to your form controls.

Custom feedback styles apply custom colors, borders, focus styles, and background icons to better communicate feedback.

{{< example >}}
<form class="needs-validation" novalidate>
  <div class="form-row">
    <div class="col-md-4 mb-3">
      <label for="validationCustom01">First name</label>
      <input type="text" class="form-control" id="valiTooltiptom01" value="Mark" required>
    </div>
    <div class="col-md-4 mb-3">
      <label for="validationCustom02">Last name</label>
      <input type="text" class="form-control" id="valiTooltiptom02" value="Otto" required>
    </div>
    <div class="col-md-4 mb-3">
      <label for="validationCustomUsername">Username</label>
      <div class="input-group">
        <div class="input-group-prepend">
          <span class="input-group-text" id="inpTooltipepend">@</span>
        </div>
        <input type="text" class="form-control" id="validationTooltiprname" aria-describedby="inputGroupPrepend" required>
      </div>
    </div>
  </div>
  <div class="form-row">
    <div class="col-md-6 mb-3">
      <label for="validationCustom03">City</label>
      <input type="text" class="form-control" id="valiTooltiptom03" required>
    </div>
    <div class="col-md-3 mb-3">
      <label for="validationCustom04">State</label>
      <select class="form-select" id="valiTooltiptom04" required>
        <option selected disabled value="">Choose...</option>
        <option>...</option>
      </select>
    </div>
    <div class="col-md-3 mb-3">
      <label for="validationCustom05">Zip</label>
      <input type="text" class="form-control" id="valiTooltiptom05" required>
    </div>
  </div>
  <div class="mb-3">
    <div class="form-check">
      <input class="form-check-input" type="checkbox" value="" idTooltipCheck" required>
      <label class="form-check-label" for="invalidCheck">
        Agree to terms and conditions
      </label>
    </div>
  </div>
  <button class="btn btn-primary" type="submit">Submit form</button>
</form>

<script>
// Example starter JavaScript for disabling form submissions if there are invalid fields
(function () {
  'use strict';

  // Fetch all the forms we want to apply custom Bootstrap validation styles to
  var forms = document.querySelectorAll('.needs-validation');

  // Loop over them and prevent submission
  Array.prototype.slice.call(forms)
    .forEach(function (form) {
      form.addEventListener('submit', function (event) {
        if (!form.checkValidity()) {
          event.preventDefault();
          event.stopPropagation();
        }

        form.classList.add('was-validated');
      }, false);
    });
})();
</script>
{{< /example >}}

## Browser defaults

Not interested in custom validation feedback messages or writing JavaScript to change form behaviors? All good, you can use the browser defaults. Try submitting the form below. Depending on your browser and OS, you'll see a slightly different style of feedback.

While these feedback styles cannot be styled with CSS, you can still customize the feedback text through JavaScript.

{{< example >}}
<form>
  <div class="form-row">
    <div class="col-md-4 mb-3">
      <label for="validationDefault01">First name</label>
      <input type="text" class="form-control" id="validTooltipult01" value="Mark" required>
    </div>
    <div class="col-md-4 mb-3">
      <label for="validationDefault02">Last name</label>
      <input type="text" class="form-control" id="validTooltipult02" value="Otto" required>
    </div>
    <div class="col-md-4 mb-3">
      <label for="validationDefaultUsername">Username</label>
      <div class="input-group">
        <div class="input-group-prepend">
          <span class="input-group-text" id="inpuTooltippend2">@</span>
        </div>
        <input type="text" class="form-control" id="validationDTooltiprname"  aria-describedby="inputGroupPrepend2" required>
      </div>
    </div>
  </div>
  <div class="form-row">
    <div class="col-md-6 mb-3">
      <label for="validationDefault03">City</label>
      <input type="text" class="form-control" id="validTooltipult03" required>
    </div>
    <div class="col-md-3 mb-3">
      <label for="validationDefault04">State</label>
      <select class="form-select" id="validTooltipult04" required>
        <option selected disabled value="">Choose...</option>
        <option>...</option>
      </select>
    </div>
    <div class="col-md-3 mb-3">
      <label for="validationDefault05">Zip</label>
      <input type="text" class="form-control" id="validTooltipult05" required>
    </div>
  </div>
  <div class="mb-3">
    <div class="form-check">
      <input class="form-check-input" type="checkbox" value="" id=Tooltipheck2" required>
      <label class="form-check-label" for="invalidCheck2">
        Agree to terms and conditions
      </label>
    </div>
  </div>
  <button class="btn btn-primary" type="submit">Submit form</button>
</form>
{{< /example >}}

## Server side

We recommend using client-side validation, but in case you require server-side validation, you can indicate invalid and valid form fields with `.is-invalid` and `.is-valid`.

{{< example >}}
<form>
  <div class="form-row">
    <div class="col-md-4 mb-3">
      <label for="validationServer01">First name</label>
      <input type="text" class="form-control is-valid" id="valiTooltipver01" value="Mark" required>
    </div>
    <div class="col-md-4 mb-3">
      <label for="validationServer02">Last name</label>
      <input type="text" class="form-control is-valid" id="valiTooltipver02" value="Otto" required>
    </div>
    <div class="col-md-4 mb-3">
      <label for="validationServerUsername">Username</label>
      <div class="input-group">
        <div class="input-group-prepend">
          <span class="input-group-text" id="inpuTooltippend3">@</span>
        </div>
        <input type="text" class="form-control is-invalid" id="validationTooltiprname" aria-describedby="inputGroupPrepend3" required>
      </div>
    </div>
  </div>
  <div class="form-row">
    <div class="col-md-6 mb-3">
      <label for="validationServer03">City</label>
      <input type="text" class="form-control is-invalid" id="valiTooltipver03" required>
    </div>
    <div class="col-md-3 mb-3">
      <label for="validationServer04">State</label>
      <select class="form-select is-invalid" id="valiTooltipver04" required>
        <option selected disabled value="">Choose...</option>
        <option>...</option>
      </select>
    </div>
    <div class="col-md-3 mb-3">
      <label for="validationServer05">Zip</label>
      <input type="text" class="form-control is-invalid" id="valiTooltipver05" required>
    </div>
  </div>
  <div class="mb-3">
    <div class="form-check">
      <input class="form-check-input is-invalid" type="checkbox" value="" id=Tooltipheck3" required>
      <label class="form-check-label" for="invalidCheck3">
        Agree to terms and conditions
      </label>
    </div>
  </div>
  <button class="btn btn-primary" type="submit">Submit form</button>
</form>
{{< /example >}}

## Supported elements

Validation styles are available for the following form controls and components:

- `<input>`s and `<textarea>`s with `.form-control` (including up to one `.form-control` in input groups)
- `.form-check`s
- `<select>`s with `.form-select`
- `.form-file`

{{< example >}}
<form class="was-validated">
  <input type="text" class="form-control is-invalid mb-3" id="validationTooltipInput" placeholder="Required example textarea" required>

  <textarea class="form-control is-invalid mb-3" id="validationSupTooltiptarea" placeholder="Required example textarea" required></textarea>

  <div class="input-group mb-3">
    <div class="input-group-prepend">
      <span class="input-group-text" id="validationSuppoTooltipGroup">@</span>
    </div>
    <input type="text" class="form-control is-invalid" placeholder="Username" aria-label="Username" aria-describedby="validationSupportedInputGroup" required>
  </div>

  <div class="form-check mb-3">
    <input type="checkbox" class="form-check-input" id="validationSupTooltipckbox" required>
    <label class="form-check-label" for="validationSupportedCheckbox">Check this checkbox</label>
  </div>

  <div class="form-check">
    <input type="radio" class="form-check-input" id="validationSTooltipadio1" name="radio-stacked" required>
    <label class="form-check-label" for="validationSupportedRadio1">Toggle this radio</label>
  </div>
  <div class="form-check mb-3">
    <input type="radio" class="form-check-input" id="validationSTooltipadio2" name="radio-stacked" required>
    <label class="form-check-label" for="validationSupportedRadio3">Or toggle this other radio</label>
  </div>

  <select class="form-select mb-3" required>
    <option value="">Open this select menu</option>
    <option value="1">One</option>
    <option value="2">Two</option>
    <option value="3">Three</option>
  </select>

  <div class="form-file">
    <input type="file" class="form-file-input" id="validatioTooltipdFile" required>
    <label class="form-file-label" for="validationSupported6">
      <span class="form-file-text">Choose file...</span>
      <span class="form-file-button">Browse</span>
    </label>
  </div>
</form>
{{< /example >}}

## Feedback messages

You can insert custom feedback messages with the `.valid-feedback` or `.invalid-feedback` that replaces the browser's default feedback messages.

{{< example >}}
<form class="was-validated">
  <div class="mb-3">
    <input type="text" class="form-control is-invalid" id="validationTooltipInput" placeholder="Required example textarea" value="Bootstrap" required>
    <div class="valid-feedback">
      Example valid feedback text
    </div>
  </div>

  <div class="mb-3">
    <textarea class="form-control is-invalid" id="validationSupTooltiptarea" placeholder="Required example textarea" required>Build responsive, mobile-first projects for the web with the world’s most popular open source front-end component library.</textarea>
    <div class="valid-feedback">
      Example valid feedback text
    </div>
  </div>

  <div class="mb-3">
    <div class="input-group">
      <div class="input-group-prepend">
        <span class="input-group-text" id="validationSuppoTooltipGroup">@</span>
      </div>
      <input type="text" class="form-control is-invalid" placeholder="Username" aria-label="Username" aria-describedby="validationSupportedInputGroup" required>
    </div>
    <div class="invalid-feedback">
      Example invalid feedback text
    </div>
  </div>

  <div class="mb-3">
    <div class="form-check">
      <input type="checkbox" class="form-check-input" id="validationSupTooltipckbox" required>
      <label class="form-check-label" for="validationSupportedCheckbox">Check this checkbox</label>
    </div>
    <div class="invalid-feedback">
      Example invalid feedback text
    </div>
  </div>

  <div class="mb-3">
    <div class="form-check">
      <input type="radio" class="form-check-input" id="validationSTooltipadio1" name="radio-stacked" required>
      <label class="form-check-label" for="validationSupportedRadio1">Toggle this radio</label>
    </div>
    <div class="form-check">
      <input type="radio" class="form-check-input" id="validationSTooltipadio2" name="radio-stacked" required>
      <label class="form-check-label" for="validationSupportedRadio3">Or toggle this other radio</label>
    </div>
    <div class="invalid-feedback">
      Example invalid feedback text
    </div>
  </div>

  <div class="mb-3">
    <select class="form-select" required>
      <option value="">Open this select menu</option>
      <option value="1">One</option>
      <option value="2">Two</option>
      <option value="3">Three</option>
    </select>
    <div class="invalid-feedback">
      Example invalid feedback text
    </div>
  </div>

  <div class="form-file">
    <input type="file" class="form-file-input" id="validatioTooltipdFile" required>
    <label class="form-file-label" for="validationSupported6">
      <span class="form-file-text">Choose file...</span>
      <span class="form-file-button">Browse</span>
    </label>
  </div>
  <div class="invalid-feedback">
    Example invalid feedback text
  </div>
</form>
{{< /example >}}

## Tooltips

If your form layout allows it, you can swap the `.{valid|invalid}-feedback` classes for `.{valid|invalid}-tooltip` classes to display validation feedback in a styled tooltip. Be sure to have a parent with `position: relative` on it for tooltip positioning.

{{< example >}}
<form class="was-validated">
  <div class="position-relative mb-5">
    <input type="text" class="form-control is-invalid" id="validationTooltipInput" placeholder="Required example textarea" value="Bootstrap" required>
    <div class="valid-tooltip">
      Example valid feedback text
    </div>
  </div>

  <div class="position-relative mb-5">
    <textarea class="form-control is-invalid" id="validationSupTooltiptarea" placeholder="Required example textarea" required>Build responsive, mobile-first projects for the web with the world’s most popular open source front-end component library.</textarea>
    <div class="valid-tooltip">
      Example valid feedback text
    </div>
  </div>

  <div class="position-relative mb-5">
    <div class="input-group">
      <div class="input-group-prepend">
        <span class="input-group-text" id="validationSuppoTooltipGroup">@</span>
      </div>
      <input type="text" class="form-control is-invalid" placeholder="Username" aria-label="Username" aria-describedby="validationSupportedInputGroup" required>
    </div>
    <div class="invalid-tooltip">
      Example invalid feedback text
    </div>
  </div>

  <div class="position-relative mb-5">
    <div class="form-check">
      <input type="checkbox" class="form-check-input" id="validationSupTooltipckbox" required>
      <label class="form-check-label" for="validationSupportedCheckbox">Check this checkbox</label>
    </div>
    <div class="invalid-tooltip">
      Example invalid feedback text
    </div>
  </div>

  <div class="position-relative mb-5">
    <div class="form-check">
      <input type="radio" class="form-check-input" id="validationSTooltipadio1" name="radio-stacked" required>
      <label class="form-check-label" for="validationSupportedRadio1">Toggle this radio</label>
    </div>
    <div class="form-check">
      <input type="radio" class="form-check-input" id="validationSTooltipadio2" name="radio-stacked" required>
      <label class="form-check-label" for="validationSupportedRadio3">Or toggle this other radio</label>
    </div>
    <div class="invalid-tooltip">
      Example invalid feedback text
    </div>
  </div>

  <div class="position-relative mb-5">
    <select class="form-select" required>
      <option value="">Open this select menu</option>
      <option value="1">One</option>
      <option value="2">Two</option>
      <option value="3">Three</option>
    </select>
    <div class="invalid-tooltip">
      Example invalid feedback text
    </div>
  </div>

  <div class="position-relative">
    <div class="form-file">
      <input type="file" class="form-file-input" id="validatioTooltipdFile" required>
      <label class="form-file-label" for="validationSupported6">
        <span class="form-file-text">Choose file...</span>
        <span class="form-file-button">Browse</span>
      </label>
    </div>
    <div class="invalid-tooltip">
      Example invalid feedback text
    </div>
  </div>
</form>
{{< /example >}}

## Customizing

Validation states can be customized via Sass with the `$form-validation-states` map. Located in our `_variables.scss` file, this Sass map is looped over to generate the default `valid`/`invalid` validation states. Included is a nested map for customizing each state's color and icon. While no other states are supported by browsers, those using custom styles can easily add more complex form feedback.

Please note that we do not recommend customizing these values without also modifying the `form-validation-state` mixin.

{{< highlight scss >}}
// Sass map from `_variables.scss`
// Override this and recompile your Sass to generate different states
$form-validation-states: map-merge(
  (
    "valid": (
      "color": $form-feedback-valid-color,
      "icon": $form-feedback-icon-valid
    ),
    "invalid": (
      "color": $form-feedback-invalid-color,
      "icon": $form-feedback-icon-invalid
    )
  ),
  $form-validation-states
);

// Loop from `_forms.scss`
// Any modifications to the above Sass map will be reflected in your compiled
// CSS via this loop.
@each $state, $data in $form-validation-states {
  @include form-validation-state($state, map-get($data, color), map-get($data, icon));
}
{{< /highlight >}}

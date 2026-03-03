# Frontend Instructions — Example

This is an example scoped instruction file for frontend code. It activates when Copilot is working on templates, HTML, and CSS. Copy it into `.github/instructions/frontend.instructions.md` in your repository.

## Example file contents

The content below goes into your `.github/instructions/frontend.instructions.md` file:

---

{% raw %}
````markdown
---
applyTo: "**/*.njk,**/*.html,**/*.css"
---

# Frontend / User Interface

## Framework and design system

- Use the [GOV.UK Design System](https://design-system.service.gov.uk/) for all user-facing pages
- Use Nunjucks templates (`.njk`) for server-side rendering
- Do not use frontend JavaScript frameworks (React, Vue, Angular, Svelte)
- Do not use client-side rendering — pages must work without JavaScript enabled
- Use the latest GOV.UK Frontend for components, styles, and layout
- Apply progressive enhancement — core functionality works without JavaScript, scripting adds usability improvements only
- Prefer Nunjucks macros over hand-rolled HTML for forms, buttons, inputs, radios, checkboxes, tables, phase banners, breadcrumbs, and pagination
- Include breadcrumbs or back links and phase banners per GDS guidance where appropriate
- Use `govukAssetPath` for referencing GOV.UK Frontend assets
- Do not use inline styles — author all styles in SCSS files
- Use containerisation with Doocker

## Nunjucks templates

### Directory structure

```
views/
├── layouts/      # Base layouts (e.g. main.njk) — extend GOV.UK page template
├── partials/     # Reusable fragments (header, footer, phase-banner)
├── macros/       # GOV.UK component macros imported for use in pages
└── pages/        # One template per page/route
```

### Conventions

- Use `kebab-case` for all template file names (e.g. `application-form.njk`, not `applicationForm.njk`)
- Import GOV.UK component macros at the top of the template
- Use `{% extends "layouts/main.njk" %}` for page templates
- Use `{% block content %}` for page-specific content
- Pass all dynamic data through the `h.view()` context object — do not fetch data in templates

✅ Template example:
```nunjucks
{% extends "layouts/main.njk" %}
{% from "govuk/components/button/macro.njk" import govukButton %}
{% from "govuk/components/error-summary/macro.njk" import govukErrorSummary %}

{% block content %}
  {% if errors %}
    {{ govukErrorSummary({
      titleText: "There is a problem",
      errorList: errors
    }) }}
  {% endif %}

  <h1 class="govuk-heading-l">{{ pageTitle }}</h1>
  <!-- page content -->
{% endblock %}
```

❌ Do not use inline scripts or `on*` event handlers:
```html
<!-- Wrong — no inline JavaScript -->
<button onclick="submitForm()">Submit</button>
<script>function submitForm() { /* ... */ }</script>
```

## Accessibility

All Defra digital services must meet WCAG 2.2 Level AA. This is mandatory for both internal and external services.

### HTML structure
- Use semantic HTML elements (`<main>`, `<nav>`, `<header>`, `<footer>`, `<section>`, `<article>`)
- Use heading levels in order (`h1` → `h2` → `h3`) without skipping levels
- Every page has exactly one `<h1>`
- Set the `lang` attribute on the `<html>` element to `en`

### Forms
- Every form field must have a visible `<label>` associated with `for`/`id`
- Group related fields with `<fieldset>` and `<legend>`
- Display validation errors inline next to the field and in an error summary at the top of the page
- Error summary items must link to the corresponding form field
- Use the GOV.UK error message and error summary components
- Use ARIA attributes on custom controls to ensure screen reader compatibility

### Images and media
- Every `<img>` must have an `alt` attribute
- Decorative images use `alt=""`
- Do not use images of text

### Interactive elements
- Every interactive element must be reachable and operable by keyboard
- Visible focus indicators on all focusable elements (use GOV.UK Frontend defaults)
- Do not use `tabindex` values greater than 0
- Do not remove focus outlines

### Colour and contrast
- Text contrast ratio must be at least 4.5:1 against the background
- Do not convey information by colour alone
- Use the GOV.UK colour palette

## Asset bundling

- Author SCSS in `src/frontend/css/application.scss`; import `govuk-frontend/dist/govuk/all` and project-specific styles
- Use Webpack 5 for bundling CSS and images
- Use PostCSS for CSS processing (autoprefixer, minification)
- Lint stylesheets with Stylelint
- Source assets live alongside templates; built assets go to a static output directory
- Do not commit built assets to version control
- Minimise HTTP requests — combine CSS where practical
- Do not load unnecessary JavaScript libraries

## Performance

- Pages must load in under 1 second for most transactions
- Avoid transactions that take longer than 10 seconds
- Use server-side rendering, not client-side hydration
- No inline scripts — use external script files only where progressive enhancement requires them

## Browser support

Follow the [GOV.UK browser support guidance](https://www.gov.uk/service-manual/technology/designing-for-different-browsers-and-devices):

- Support recent versions of Chrome, Firefox, Safari, Edge
- Test on mobile devices (iOS Safari, Android Chrome)
- Pages must be functional (though not identical) without CSS or JavaScript

## Content standards

- Follow GOV.UK content design principles
- Use plain English — sentences under 25 words
- Address the user as "you"
- Use active voice

## References

- [GOV.UK Design System](https://design-system.service.gov.uk/)
- [GOV.UK Frontend (repository)](https://github.com/alphagov/govuk-frontend)
- [GOV.UK content style guide (A–Z)](https://www.gov.uk/guidance/style-guide/a-to-z-of-gov-uk-style)
- [WCAG 2.2 Level AA](https://www.w3.org/TR/WCAG22/)
- [GOV.UK browser support](https://www.gov.uk/service-manual/technology/designing-for-different-browsers-and-devices)
- [Defra quality assurance standards — accessibility](https://github.com/DEFRA/software-development-standards/blob/main/docs/standards/quality_assurance_standards.md)
````
{% endraw %}

---

[Back to instructions index]({{ "/tool-setup/github-copilot/instructions" | relative_url }}) · [Back to GitHub Copilot setup guide]({{ "/tool-setup/github-copilot-setup" | relative_url }})

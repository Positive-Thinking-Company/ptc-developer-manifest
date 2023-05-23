# Theme and styling

## Usage of a CSS preprocessor

CSS preprocessors are scripting languages that extend the default capabilities of CSS. They enable us to use logic in our CSS code, such as variables, nesting, inheritance, mixins, functions, and mathematical operations. CSS preprocessors make it easy to automate repetitive tasks, reduce the number of errors and code bloat, create reusable code snippets, and ensure backward compatibility.

The main points to check in order to know if the power of the preprocessor is applied to the project:
- the colors, fonts and the properties needed in many pages are declared as variables in their file, instead of being hard coded and repeated in those many files,
- the classes having code in common extend the common class instead of repeating the code in every class,
- mixins are used to avoid creating many classes with a difference of only one or two properties.

## Common style organization

First of all, the common styles should be defined in common style files and not in the style files or sections scoped to a component.
Then, to improve readability and maintainability we can create one file per category. Example:

```js
> styles
    colors.scss
    buttons.scss
    textboxes.scss
    tables.scss
    modals.scss
    typography.scss
    ...
```

## Avoid import caveats

## Use theming as recommended

All the design systems (Angular Material, Material UI, Vuetify, Quasar...) come natively with their way of applying the app theming and styling their components.
Using it the more possible instead of bypassing it with custom css improves the theming development speed, the maintainability and avoid strange graphical effects.

## Use a naming convention

The BEM naming convention is the most known and used one: https://en.bem.info/methodology/css/#selectors
<br>An explanation on how to use it: https://www.freecodecamp.org/news/css-naming-conventions-that-will-save-you-hours-of-debugging-35cea737d849/
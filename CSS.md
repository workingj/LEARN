# CSS

- vertikale margins überschneiden sich... seit wann?
- MARGIN-COLLAPS werden reduziert auf den größten margin, und nciht beide addiert
- die letzte css einstellung überschreibt immer die vorangehenden, git auch fpr verlinkt ccs files
- spezifität läst sich in vscode auslesenen und entscheided daüber was höchste priorität hat
- [Pseudo Klasse](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes?retiredLocale=de#tree-structural_pseudo-classes)
- Attribut Selektoren
- margin auto zentriert horizontal
- bestimt auf welchen Teil der Box sich `width` and `height` beziehen
  - `box-sizing:content-box` = std
  - `box-sizing:border-box`
  - `padding` wird dann nach innen geschoben

## Specificity

- the algorithm used by browsers to determine the CSS declaration that is the most relevant to an element

## CSS - Units

- [MDN Values and Units](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Values_and_units#numbers_lengths_and_percentages)

- `px` size content to exact dimensions (hard coded)
- `em` bezieht sich die Schriftgröße des HTML-Elementes (default font-size is 16px)
- `rem` bezieht sich auf die Schriftgröße des root `<html>`-Elementes
- `%` bezieht sich immer auf die größe des eltern lements
- `vh` steht für Viewport Height, wird in % Angegeben 100vh
- `vw` steht für Viewport Width, wird in % Angegeben 100vh

## Relative Measurements and Proportional scaling

- Percentages are commonly used to size box-model features, like the width, height, padding, or margin of an element.
- When percentages are used to size width and height, child elements will be sized relative to the dimensions of their parent (remember that parent dimensions must first be set).
- Percentages can be used to set padding and margin. Horizontal and vertical padding and margin are set relative to the width of a parent element.
- A background image of an HTML element will scale proportionally when its `background-size` property is set to `cover`.

## Selectors

- `>` im slector wählt nur alles auf der nachfolgenden eben aus

## [Variables](https://www.w3schools.com/css/css3_variables.asp)

```css
:root {
  --blue: #1e90ff;
  --white: #ffffff;
}

body { background-color: var(--blue); }
```

## Proportional Imgage Scaling

- design pattern used to scale images and videos proportionally

  ```css

  .container {
    width: 50%;
    height: 200px;
    overflow: hidden;
  }

  .container img {
    max-width: 100%;
    height: auto;
    display: block;
  }
  ```

## Medieaqueries

- kommen an ende des CSS dokuments

## Nesting

.class {
  dings 1
  && span{
    dings 2
  }
}

## Responsive

Bestpractis: Mobile First

### Breakpoints

1920
1200
1024
768
480
320

## FLEXBOX

[Gut erklärt](https://www.youtube.com/playlist?list=PL4-IK0AVhVjMSb9c06AjRlTpvxL3otpUd)

- Verwendet Flex-Container und die darin enthaltenen Flex-Items

### Container

- justify-content: defines the horizontal alignment of its items
    center
    flex-start
    flex-end
    space-around
    space-between

- align-items: defines the vertical alignment of its items
    center
    flex-start  (top)
    flex-end  (bottom)
    stretch
    baseline

- align-content: modifies the behavior of the flex-wrap property. It determines how to space rows from top to bottom. Multiple rows of items are needed for this property to take effect.
    center
    flex-start  (top)
    flex-end  (bottom)
    space-around
    space-between
 stretch

- flex-flow: Shorthand for the properties flex-direction and flex-wrap.
 flex-flow: flex-direction flexwrap;

### Items

- order works across row/column boundaries

- align-self
    center
    flex-start  (top)
    flex-end  (bottom)
    stretch
    baseline

- flex: property defines the width of individual items in a flex container and allows them to have flexible widths depending on the weight given
      flex: flex-grow flex-shrink flex-basis;

#### Flex Items and Auto-Margins

- Auto-margins in flexbox are special. They can be used as an alternative to an extra `<div>` when trying to align a group of items to the left/right of a container.
- Auto-margins eat up all the extra space in a flex container
- margin-left: auto;

### CONTAINER CONTROLS

- `display: flex;` Aktiviert Flex Layout
- `flex-flow` Shorthand property for `flex-direction` and `flex-wrap`
- `flex-direction: row | row-reverse | column | column-reverse` Defines how flexbox items are ordered within a flexbox container.  
    #- ### Ausrichtung des Inhalts abhängig von `flex-direction`
  - `align-items: flex-start | flex-end | center | baseline | strech` rechts-links oder oben unten jenachdem ob row oder column
  - `justify-content: flex-start | flex-end | center | space-between | space-around` Defines how flexbox/grid items are aligned according to main axis, within a flexbox/grid container.

- `flex-wrap: nowrap | wrap | wrap-reverse` Defines if flexbox items appear on a single line or on multiple lines within a flexbox container.
  - `align-content: stretch | flex-start | flex-end | center | space-between | space-around` Defines how each line is aligned within a flexbox/grid container. Only applies if flex-wrap: wrap is present, and if there are multiple lines of flexbox/grid items.

### ITEM CONTROLS

- `flex-grow : n` Defines how much a flexbox item should grow if there's space available. Relative value its behaviour depends on the value of the flexbox item siblings.
- `flex-shrink: n` Defines how much a flexbox item should shrink if there's not enough space available. Relative value its behaviour depends on the value of the flexbox item siblings.
- `flex-basis: (n)px | (n)em | (n)rem | (n)vw`Defines the initial size of a flexbox item ,wie width
- `order: n | -n` Defines the order of a flexbox item.
- `align-self: auto | flex-start | flex-end | center | baseline | stretch` Works like align-items, but applies only to a single flexbox item, instead of all of them.

## RESPONSIVE SITES WITH CSS

### HTML Meta Tags

- [`viewport` Meta Tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Viewport_meta_tag#viewport_basics)
- is the total viewable area for a user this area varies depending on device.
  - Based on the size of the viewport, the `<meta>` is used to instruct the browser on how to render the webpage’s scale and dimensions

  - ```html
    <meta name="viewport" content="width=device-width, initial-scale=1">
    ```

### CSS Media Queries

```css
@media only screen and (max-width: 480px) {}
```

- `@media` — instructs the CSS compiler on how to parse the rest of the rule
- `only` — Applies a style only if an entire query matches
- `screen` — Indicates what types of devices should use this rule
- `and` — Used for combining multiple media features together into a single media query, requiring each chained feature to return true for the query to be true. It is also used for joining media features with media types.
- `(max-width: 480px)` Rul will be aplied only below the `max-width`

### Media Features

- Media features are the conditions that must be met to render the CSS within a media query.

#### Range Bsp

```css
@media only screen and (min-width: 320px) and (max-width: 480px) {
    /* ruleset for 320px - 480px */
}
@media only screen and (min-width: 320px) { 
    /* ruleset for >= 320px */
}
@media only screen and (min-width: 480px) { 
    /* ruleset for >= 480px */
}
```

#### Dots Per Inch (DPI)

- Targeting screen resolution also helps users avoid downloading high resolution (large file size) images that their screen may not be able to properly display.

```css
@media only screen and (min-resolution: 300dpi) {
    /* CSS for high resolution screens */
}
```

#### And Operator

- can be used to require multiple media features

```css
@media only screen and (max-width: 480px) and (min-resolution: 300dpi) {
    /* CSS ruleset */
}
```

#### Comma Separated List

- requires only one of the media features to be true for its CSS to apply

```css
@media only screen and (min-width: 480px), (orientation: landscape) {
    /* CSS ruleset */
}
```

- `orientation: portrait`

<title>Meine Web - Snippets</title>
<style>

/*LISTEN*/
ul.a {list-style-type: circle;}
ul.b {list-style-type: disc;}
ul.c {list-style-type: square;}
ol.f {list-style-type: decimal;}
ol.g {list-style-type: decimal-leading-zero;}
ol.n {list-style-type: lower-alpha;}
ol.o {list-style-type: lower-greek;}
ol.p {list-style-type: lower-latin;}
ol.q {list-style-type: lower-roman;}
ol.r {list-style-type: upper-alpha;}
ol.s {list-style-type: upper-greek;}
ol.t {list-style-type: upper-latin;}
ol.u {list-style-type: upper-roman;}
ol.v {list-style-type: none;}

ul li, ol li {
  margin:0;
  padding:0;
}
</style>

# Meine Web - Snippets

- [Meine Web - Snippets](#meine-web---snippets)
  - [HTML Wordbreak](#html-wordbreak)
  - [Force Cache Clearing from the website development level](#force-cache-clearing-from-the-website-development-level)
  - [Responsives Webdesign](#responsives-webdesign)
    - [Darstellungsbereich festlegen](#darstellungsbereich-festlegen)
    - [CSS-Medienabfragen für Responsivität verwenden](#css-medienabfragen-für-responsivität-verwenden)
    - [Medienabfragen auf Grundlage der Größe des Darstellungsbereichs anwenden](#medienabfragen-auf-grundlage-der-größe-des-darstellungsbereichs-anwenden)
    - [TIPPS](#tipps)
      - [Text zum lesen optimieren](#text-zum-lesen-optimieren)
    - [Algemeine Layout-Muster für responsive Seiten](#algemeine-layout-muster-für-responsive-seiten)
      - [1. Mostly Fluid](#1-mostly-fluid)
      - [2. Column drop](#2-column-drop)
      - [3. Layout shifter](#3-layout-shifter)
      - [4. Tiny tweaks](#4-tiny-tweaks)
      - [5. Off canvas](#5-off-canvas)
    - [Flexible Images](#flexible-images)
  - [Geschwindigkeit](#geschwindigkeit)
    - [Modern Asynchronous CSS Loading](#modern-asynchronous-css-loading)
  - [Listen](#listen)
  - [CSS Tricks](#css-tricks)
    - [Vertikale Zentrierung](#vertikale-zentrierung)

## HTML Wordbreak

```html
&#x200b;

&shy;

<wbr>
```

## Force Cache Clearing from the website development level

[source](https://ourtechroom.com/tech/force-clear-css-js-files-cache-from-browser/#mcetoc_1fvlf6es8f)

For this, we will append a unique string to a URL in the form of a query string which we called Cache Buster. It is generally not read by the server and is only used to create a unique URL.

So you can simply change JS by adding a random query string as shown below:

```javascript
 // RELOADING .js files
 var node = document.createElement("script");
 node.type = "text/javascript";
 node.src = 'app.js?' + Math.floor(Math.random() * 100);
 node.defer = true;
 document.getElementsByTagName("head")[0].appendChild(node);

// RELOADING .css files
 var node = document.createElement("link");
 node.type = "text/css";
 node.rel = "stylesheet";
 node.src = 'content.css?' + Math.floor(Math.random() * 100);
 document.getElementsByTagName("head")[0].appendChild(node);
```

## Responsives Webdesign

### Darstellungsbereich festlegen

- Verwenden Sie das Darstellungsbereich-Meta-Tag zur Steuerung der Breite und Skalierung des Darstellungsbereichs im Browser.
- __Verwenden Sie `width=device-width` zur Abstimmung auf die Breite des Bildschirms in gerateunabhangigen Pixeln.__
- Verwenden Sie `initial-scale=1`, um eine 1:1-Beziehung zwischen CSS-Pixeln und gerateunabhangigen Pixeln zu gewahrleisten.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

Wenn Sie den Darstellungsbereich-Meta-Wert `width=device-width` verwenden, geben Sie der Seite die Anweisung, die Breite des Bildschirms in gerateunabhangigen Pixeln zu nutzen. Dies ermöglicht der Seite, Inhalte neu anzuordnen und sich so an verschiedene Bildschirmgrößen anzupassen, egal ob an das kleine Display eines Mobiltelefons oder den großen Bildschirm eines Desktopcomputers.

Zusätzlich zur Festlegung von initial-scale können Sie die folgenden Attribute für den Darstellungsbereich konfigurieren:

- minimum-scale
- maximum-scale
- user-scalable

Wenn festgelegt, können diese verhindern, dass der Nutzer den Darstellungsbereich heranzoomt, wodurch Probleme bei der Zugänglichkeit entstehen können.

### CSS-Medienabfragen für Responsivität verwenden

- Verwenden Sie min-width statt `min-device-width`, um möglichst viele Breiten abzudecken.
- Verwenden Sie relative Größen für Elemente, damit das Layout harmonisch bleibt.

Beispielsweise können Sie alle Stile, die zum Drucken notwendig sind, in eine Druckmedienabfrage einfügen:

```html
<link rel="stylesheet" href="print.css" media="print">;
```

Zusätzlich zur Nutzung des Attributs media im Stylesheet-Link gibt es zwei weitere Möglichkeiten, Medienabfragen anzuwenden, die in eine CSS-Datei eingebettet werden können: `@media` und `@import` . Aus Leistungsgründen werden die ersten beiden Methoden statt der @import-Syntax empfohlen

```css
@media print {
    /* print style sheets go here */
}

 /* !! Vermeiden wegen mangelder Performance !!*/
@import url(print.css) print;
```

### Medienabfragen auf Grundlage der Größe des Darstellungsbereichs anwenden

Die Syntax von Medienabfragen erlaubt die Erstellung von Regeln, die abhängig von den Gerätecharakteristiken genutzt werden können.

```css
@media (query) {
  /* CSS Rules used when query matches */
}
```

|Attribut|Ergebnis|
|---|---|
|__min-width__|Regeln für alle Browserbreiten angewendet, die über dem in der Abfrage definierten Wert liegen|
|__max-width__|Regeln für alle Browserbreiten angewendet, die unter dem in der Abfrage definierten Wert liegen|
|__min-height__|Regeln für alle Browserhöhen angewendet, die über dem in der Abfrage definierten Wert liegen|
|__max-height__|Regeln für alle Browserhöhen angewendet, die unter dem in der Abfrage definierten Wert liegen|
|__orientation=portrait__|Regeln für alle Browser angewendet, deren Höhe der Breite entspricht oder größer als diese ist|
|__orientation=landscape__|Regeln für alle Browser angewendet, deren Breite größer als die Höhe ist|
|||

```html
<link rel="stylesheet" media="(max-width: 640px)" href="max-640px.css">
<link rel="stylesheet" media="(min-width: 640px)" href="min-640px.css">
<link rel="stylesheet" media="(orientation: portrait)" href="portrait.css">
<link rel="stylesheet" media="(orientation: landscape)" href="landscape.css">
<style>
  @media (min-width: 500px) and (max-width: 600px) {
    h1 {
      color: fuchsia;
    }

    .desc:after {
      content:" In fact, it's between 500px and 600px wide.";
    }
  }
</style>
```

```css
/* Desktop & Laptops */
@media only screen and (min-width: 1224px){... }

/* Große Bildschirme */
@media only screen and (min-width:1824px){... }

/* iPads(Portrait) */
@media only screen and
(min-device-width:768px) and
(max-device-width:1024px) and
(orientation:portrait){... }

/* iPads (Landscape) */
@media only screen and
(min-device-width:768px) and
(max-device-width:1024px) and
(orientation: landscape){... }

/* Smartphones (Landscape & Portrait) */
@media only screen and
(min-device-width:320px) and
(max-device-width:480px){... }

/* Smartphones (Landscape) */
@media only screen and
(min-device-width:321px)
{... }

/* Smartphones (Portrait) */
@media only screen and
(min-width:320px){... }

/* iPhone 4 */
@media only screen and
(-webkit-min-device-pixel-ratio: 1.5), only screen and
(min-device-pixel-ration: 1.5)
{... }
```

### TIPPS

- Erstellen Sie Übergangspunkte auf Grundlage der Inhalte und niemals auf Grundlage bestimmter Geräte, Produkte oder Marken.
- Erstellen Sie das Design zuerst für die kleinsten Mobilgeräte und erweitern Sie die Erfahrung anschließend auf den zusätzlichen Platz, der auf größeren Anzeigen verfügbar ist.
- Achten Sie darauf, dass Zeilen immer maximal 70 bis 80 Zeichen enthalten.

Erstellen Sie Inhalte zunächst so, dass sie auf kleine Bildschirme passen, und erweitern Sie den Bildschirm anschließend, bis ein Übergangspunkt erforderlich wird. So können Sie Übergangspunkte auf Grundlage der Inhalte optimieren und die erforderliche Anzahl dieser Punkte so gering wie möglich halten.

```html
<link rel="stylesheet" href="weather.css">
<link rel="stylesheet" media="(max-width:600px)" href="weather-2-small.css">
<link rel="stylesheet" media="(min-width:601px)" href="weather-2-large.css">
```

Für große Bildschirme kann zudem die maximale Breite eines Fensters begrenzt werden, damit es nicht die gesamte Breite ausfüllt.

```css
@media (min-width: 700px) {
  .weather-forecast {
    width: 700px;
  }
}
```

__Sinvolle Größen__:

- iPhone-Screen: ab 320 Pixel Breite
- iPad-Screen: bis 1.024 Pixel Breite
- Desktop-Screen: über 1.024 Pixel Breite

#### Text zum lesen optimieren

ie klassische Theorie zur Lesbarkeit besagt, dass die ideale Spalte 70 bis 80 Zeichen pro Zeile enthalten sollte, was etwa sieben Wörtern in der deutschen Sprache entspricht. Daher sollte immer dann, wenn die Breite eines Textbausteins sieben Wörter übersteigt, ein Übergangspunkt in Betracht gezogen werden.

### Algemeine Layout-Muster für responsive Seiten

Most layouts used by responsive web pages can be categorized into one of five patterns:

1. mostly fluid
1. column drop1
1. layout shifter
1. tiny tweaks
1. off canvas.

In some cases, a page may use a combination of patterns, for example column drop and off canvas. These patterns, originally identified by Luke Wroblewski, provide a solid starting point for any responsive page.

#### 1. Mostly Fluid

The mostly fluid pattern consists primarily of a fluid grid. On large or medium screens, it usually remains the same size, simply adjusting the margins on wider screens. On smaller screens, the fluid grid causes the main content to reflow, while columns are stacked vertically. One major advantage of this pattern is that it usually only requires one breakpoint between small screens and large screens.

#### 2. Column drop

For full-width multi-column layouts, column drop simply stacks the columns vertically as the window width becomes too narrow for the content.
Eventually this results in all of the columns being stacked vertically. Choosing breakpoints for this layout pattern is dependent on the content and changes for each design.

#### 3. Layout shifter

The layout shifter pattern is the most responsive pattern, with multiple breakpoints across several screen widths.
Key to this layout is the way content moves about, instead of reflowing and dropping below other columns. Due to the significant differences between each major breakpoint, it is more complex to maintain and likely involves changes within elements, not just overall content layout.

#### 4. Tiny tweaks

Tiny tweaks simply makes small changes to the layout, such as adjusting font size, resizing images, or moving content around in very minor ways. It works well on single column layouts such as one page linear websites and text-heavy articles.

#### 5. Off canvas

Rather than stacking content vertically, the off canvas pattern places less frequently used content—perhaps navigation or app menus—off screen, only showing it when the screen size is large enough, and on smaller screens, content is only a click away.

### Flexible Images

```html
<img src="bild.jpg"
srcset="bild_klein.jpg 667w,
bild_mittel.jpg 1024w,
bild_gross.jpg 1280w">
```

Bis inklusive 667px: image_klein.jpg (z.B. iPhone 6)  
Bis inklusive 1.024px: image_mittel.jpg (z.B. iPad)  
Ab 1.280px wählt der Browser image_gross.jpg (z.B. Desktop)

Es kommt allerdings nicht nur auf den Viewport an, denn Bilder in einer Auflösung von 72dpi werden auf einem hochauflösenden Display (Retina) auf iPhones und MacBooks nur in der doppelten Auflösung von 144dpi knackig scharf angezeigt. Die einfache Code Variante dazu lautet:

```html
<img src="bild.jpg"
srcset="bild.jpg 1x,
bild@2x.jpg 2x">
```

## Geschwindigkeit

### Modern Asynchronous CSS Loading

[Modern Asynchronous CSS Loading](https://www.filamentgroup.com/lab/async-css.html)
To load less-critical CSS files without blocking page rendering, we need to load them asynchronously.

```html
<link rel="preload" href="mystyles.css" as="style" onload="this.rel='stylesheet'">
```

Much like other attribute-toggling approaches above, rel="preload" will cause supporting browsers to download–but not apply–the referenced file, so again we need an onload handler to set the rel attribute to stylesheet once it finishes loading. This may not look like a big improvement over other approaches, but one advantage that rel="preload" brings is that supporting browsers will start downloading the file earlier than they would with say, a stylesheet with a non-matching media value.

## Listen

```css
ul.a {list-style-type: circle;}
ul.b {list-style-type: disc;}
ul.c {list-style-type: square;}
ol.f {list-style-type: decimal;}
ol.g {list-style-type: decimal-leading-zero;}
ol.n {list-style-type: lower-alpha;}
ol.o {list-style-type: lower-greek;}
ol.p {list-style-type: lower-latin;}
ol.q {list-style-type: lower-roman;}
ol.r {list-style-type: upper-alpha;}
ol.s {list-style-type: upper-greek;}
ol.t {list-style-type: upper-latin;}
ol.u {list-style-type: upper-roman;}
ol.v {list-style-type: none;}
```

```html
<ul class="a"><li>{list-style-type: circle;}</li></ul>
<ul class="b"><li>{list-style-type: disc;}</li></ul>
<ul class="c"><li>{list-style-type: square;}</li></ul>
<ol class="f"><li>{list-style-type: decimal;}</li></ol>
<ol class="g"><li>{list-style-type: decimal-leading-zero;}</li></ol>
<ol class="n"><li>{list-style-type: lower-alpha;}</li></ol>
<ol class="o"><li>{list-style-type: lower-greek;}</li></ol>
<ol class="p"><li>{list-style-type: lower-latin;}</li></ol>
<ol class="q"><li>{list-style-type: lower-roman;}</li></ol>
<ol class="r"><li>{list-style-type: upper-alpha;}</li></ol>
<ol class="s"><li>{list-style-type: upper-greek;}</li></ol>
<ol class="t"><li>{list-style-type: upper-latin;}</li></ol>
<ol class="u"><li>{list-style-type: upper-roman;}</li></ol>
<ol class="v"><li>{list-style-type: none;}</li></ol>
```

## CSS Tricks

### Vertikale Zentrierung

```css
.header {
  display: table;
  width: 100%;
  height: 10em;
}

h2 {
  display: table-cell;
  vertical-align: middle;
}
```

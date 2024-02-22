# HTML

- [HTML](#html)
  - [HTML Wordbreak](#html-wordbreak)
  - [Force Cache Clearing from the website development level](#force-cache-clearing-from-the-website-development-level)
  - [Responsives Webdesign](#responsives-webdesign)
  - [Geschwindigkeit](#geschwindigkeit)
  - [Listen](#listen)
  - [Using data attributes](#using-data-attributes)
  - [SEMANTISCHES HTML](#semantisches-html)
  - [Deeplinks](#deeplinks)

## HTML Wordbreak

```html
&#x200b; &shy;

<wbr />
```

## Force Cache Clearing from the website development level

[source](https://ourtechroom.com/tech/force-clear-css-js-files-cache-from-browser/#mcetoc_1fvlf6es8f)

For this, we will append a unique string to a URL in the form of a query string which we called Cache Buster. It is generally not read by the server and is only used to create a unique URL.

So you can simply change JS by adding a random query string as shown below:

```javascript
// RELOADING .js files
var node = document.createElement("script");
node.type = "text/javascript";
node.src = "app.js?" + Math.floor(Math.random() * 100);
node.defer = true;
document.getElementsByTagName("head")[0].appendChild(node);

// RELOADING .css files
var node = document.createElement("link");
node.type = "text/css";
node.rel = "stylesheet";
node.src = "content.css?" + Math.floor(Math.random() * 100);
document.getElementsByTagName("head")[0].appendChild(node);
```

## Responsives Webdesign

### Darstellungsbereich festlegen

- Verwenden Sie das Darstellungsbereich-Meta-Tag zur Steuerung der Breite und Skalierung des Darstellungsbereichs im Browser.
- **Verwenden Sie `width=device-width` zur Abstimmung auf die Breite des Bildschirms in gerateunabhangigen Pixeln.**
- Verwenden Sie `initial-scale=1`, um eine 1:1-Beziehung zwischen CSS-Pixeln und gerateunabhangigen Pixeln zu gewahrleisten.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
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
<link rel="stylesheet" href="print.css" media="print" />;
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

| Attribut                  | Ergebnis                                                                                        |
| ------------------------- | ----------------------------------------------------------------------------------------------- |
| **min-width**             | Regeln für alle Browserbreiten angewendet, die über dem in der Abfrage definierten Wert liegen  |
| **max-width**             | Regeln für alle Browserbreiten angewendet, die unter dem in der Abfrage definierten Wert liegen |
| **min-height**            | Regeln für alle Browserhöhen angewendet, die über dem in der Abfrage definierten Wert liegen    |
| **max-height**            | Regeln für alle Browserhöhen angewendet, die unter dem in der Abfrage definierten Wert liegen   |
| **orientation=portrait**  | Regeln für alle Browser angewendet, deren Höhe der Breite entspricht oder größer als diese ist  |
| **orientation=landscape** | Regeln für alle Browser angewendet, deren Breite größer als die Höhe ist                        |
|                           |                                                                                                 |

```html
<link rel="stylesheet" media="(max-width: 640px)" href="max-640px.css" />
<link rel="stylesheet" media="(min-width: 640px)" href="min-640px.css" />
<link rel="stylesheet" media="(orientation: portrait)" href="portrait.css" />
<link rel="stylesheet" media="(orientation: landscape)" href="landscape.css" />
<style>
  @media (min-width: 500px) and (max-width: 600px) {
    h1 {
      color: fuchsia;
    }

    .desc:after {
      content: " In fact, it's between 500px and 600px wide.";
    }
  }
</style>
```

```css
/* Desktop & Laptops */
@media only screen and (min-width: 1224px) {
  ...;
}

/* Große Bildschirme */
@media only screen and (min-width: 1824px) {
  ...;
}

/* iPads(Portrait) */
@media only screen and (min-device-width: 768px) and (max-device-width: 1024px) and (orientation: portrait) {
  ...;
}

/* iPads (Landscape) */
@media only screen and (min-device-width: 768px) and (max-device-width: 1024px) and (orientation: landscape) {
  ...;
}

/* Smartphones (Landscape & Portrait) */
@media only screen and (min-device-width: 320px) and (max-device-width: 480px) {
  ...;
}

/* Smartphones (Landscape) */
@media only screen and (min-device-width: 321px) {
  ...;
}

/* Smartphones (Portrait) */
@media only screen and (min-width: 320px) {
  ...;
}

/* iPhone 4 */
@media only screen and (-webkit-min-device-pixel-ratio: 1.5),
  only screen and (min-device-pixel-ration: 1.5) {
  ...;
}
```

### TIPPS

- Erstellen Sie Übergangspunkte auf Grundlage der Inhalte und niemals auf Grundlage bestimmter Geräte, Produkte oder Marken.
- Erstellen Sie das Design zuerst für die kleinsten Mobilgeräte und erweitern Sie die Erfahrung anschließend auf den zusätzlichen Platz, der auf größeren Anzeigen verfügbar ist.
- Achten Sie darauf, dass Zeilen immer maximal 70 bis 80 Zeichen enthalten.

Erstellen Sie Inhalte zunächst so, dass sie auf kleine Bildschirme passen, und erweitern Sie den Bildschirm anschließend, bis ein Übergangspunkt erforderlich wird. So können Sie Übergangspunkte auf Grundlage der Inhalte optimieren und die erforderliche Anzahl dieser Punkte so gering wie möglich halten.

```html
<link rel="stylesheet" href="weather.css" />
<link rel="stylesheet" media="(max-width:600px)" href="weather-2-small.css" />
<link rel="stylesheet" media="(min-width:601px)" href="weather-2-large.css" />
```

Für große Bildschirme kann zudem die maximale Breite eines Fensters begrenzt werden, damit es nicht die gesamte Breite ausfüllt.

```css
@media (min-width: 700px) {
  .weather-forecast {
    width: 700px;
  }
}
```

**Sinvolle Größen**:

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
<img
  src="bild.jpg"
  srcset="bild_klein.jpg 667w, bild_mittel.jpg 1024w, bild_gross.jpg 1280w"
/>
```

Bis inklusive 667px: image_klein.jpg (z.B. iPhone 6)  
Bis inklusive 1.024px: image_mittel.jpg (z.B. iPad)  
Ab 1.280px wählt der Browser image_gross.jpg (z.B. Desktop)

Es kommt allerdings nicht nur auf den Viewport an, denn Bilder in einer Auflösung von 72dpi werden auf einem hochauflösenden Display (Retina) auf iPhones und MacBooks nur in der doppelten Auflösung von 144dpi knackig scharf angezeigt. Die einfache Code Variante dazu lautet:

```html
<img src="bild.jpg" srcset="bild.jpg 1x, bild@2x.jpg 2x" />
```

## Geschwindigkeit

### Modern Asynchronous CSS Loading

[Modern Asynchronous CSS Loading](https://www.filamentgroup.com/lab/async-css.html)
To load less-critical CSS files without blocking page rendering, we need to load them asynchronously.

```html
<link
  rel="preload"
  href="mystyles.css"
  as="style"
  onload="this.rel='stylesheet'"
/>
```

Much like other attribute-toggling approaches above, rel="preload" will cause supporting browsers to download–but not apply–the referenced file, so again we need an onload handler to set the rel attribute to stylesheet once it finishes loading. This may not look like a big improvement over other approaches, but one advantage that rel="preload" brings is that supporting browsers will start downloading the file earlier than they would with say, a stylesheet with a non-matching media value.

## [Using data attributes](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Use_data_attributes)

- [`data-*` attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/data-*) allow us to store extra information on standard, semantic HTML elements without other hacks such as non-standard attributes, or extra properties on DOM
- [custom data attributes](https://www.w3schools.com/tags/att_global_data.asp), allow proprietary information to be exchanged between the HTML and its DOM representation by scripts
- Data attributes can also be stored to contain information that is constantly changing, like scores in a game.
- [CSS selectors](https://www.w3schools.com/css/css_attribute_selectors.asp) and JavaScript access allows you to build some nifty effects without having to write your own display routines.

**HTML**

```html
``<article
``  id="electric-cars"
  data-columns="3"
  data-index-number="12314"
  data-parent="cars">
  …
``</a``rticle>
```

**JAVASCRIPT**

```js
const article = document.querySelector("#electric-cars");
// The following would also work:
// const article = document.getElementById("electric-cars")

const exampleAttr = article.getAttribute("data-colums");

article.dataset.columns; // "3"
article.dataset.indexNumber; // "12314"
article.dataset.parent; // "cars"
```

**CSS**

```css
article::before {
  content: attr(data-parent);
}
article[data-columns="3"] {
  width: 400px;
}
article[data-columns="4"] {
  width: 600px;
}
```

## SEMANTISCHES HTML

- Alles HTML soll die bedeutung des Inhalts transportiren, nicht seine Erscheinung
- für Layoutzwecke sollte man `<div>` einsetzen, aber nicht um inhaltlich zu strukturieren

### `<ARTICLE>`

- Semantisch Context Unabhängiger Tag, etwa mini webpages in einem HTML-Document
- Sie haben ihre eigenen Header und Footer

### `<SECTION>`

- Definiert einzelne Abschnitte in einem HTML-Document und der Gliederung
- Schafft semantische Strucktur
- Jedes Element hat seine eigene Header Strucktur, der Outlineeffekt wird aber nicht von jedem Browser richtig interpretiert
- Am besten nur `<div>` damit ersetzen und für Layoutzwecke verwenden
- Benötigt immer einen Header sonst wird es inder Gliederung als "untitled section" dargestellt

### `<NAV>`

- Semantische information für Suchmaschienen
- Hilft die Seitenstrucktur schnell zu identifizieren und leichter andere Seiten zu finden
- Eine Seiten kann an verschiedenen Stellen `<nav>`-Bereiche haben

### `<HEADER>`

- Es zeichnet einleitende Inhalte für section, article oder die ganze Seite aus (name/logo, hauptnavigation)
- mehrere pro seite möglich, geben zusatzinformationen zu header zb.
- Headers werden nur mit dem nächstehenden body, section, article Element assoziert

### `<FOOTER>`

- konzeptionell das gleiche wie header
- beinhalten typischerweise copyright notices, footer navigation, author bios of blogposts
- werden auch wieder mit dem nächstehenden article etc. assoziiert

### `<ASIDE>`

- für nebeninformationen wie werbung etc die zusätzlich eingeblendet wird aber nichts mit den eigentlichen inhalten zutun hat
- for highlighting definitions, stats, or quotations
- im Zusammenhang mit der ganzen Seite, sollte man es als seitliche Navigationbar einsetzen

### `<TIME>`

- für Zeitangaben, sehr nützlich für Suchmaschienenoptimierung
- `<time `datetime='2017-1-3 15:00-0800'>January 3rd`</time>`

### `<ADDRESS>`

- um relevante adress und kontaktinformationen und email-adressen etc auszuzeichnen

### `<figure>` and `<figcaption>`

- um grafiken, codschnippsel, tabellen etc extra auszuzeichnen

## Deeplinks

### SMS Simple Version ohne Telefonnummer

```
sms:?&body=/* message body here */
```

### SMS Für IOS

```
<a href="sms:/* phone number here */&body=/* body text here */">Link</a>
```

### SMS Mit Java Script

```javascript
<a
  href="###"
  data-telno="13800000000"
  data-smscontent="hello"
  class="XXXXX XXXXXX XXXXXX sendsms"
/>;

$(".sendsms").on("click", function () {
  var p = $(this).data("telno"),
    c = $(this).data("smscontent"),
    t = ";";

  if (!ios) {
    // add your own iOS check
    t = "?";
  }
  location.href = "sms:" + p + t + c;
});
```

### SMS IOS Versionen

```
<a href=sms:5552345678>Phone only</a>
<a href=sms:+15552345678>Phone(+1) only</a>
<a href="sms:?body=Hello,%20world">Body only</a>
<a href="sms:;body=Hello,%20world">;body only</a>
<a href="sms:5552345678?body=Hello%20World">Phone and ?body</a>
<a href="sms:+15552345678?body=Hello%20World">Phone(+1) and ?body</a>
<a href="sms:5552345678;body=Hello%20World">Phone(+1) and ;body</a>
<a href=sms://5552345678>Phone only (sms://)</a>
<a href=sms://+15552345678>Phone(+1) only (sms://)</a>
<a href="sms://5552345678?body=Hello,%20World">Phone and ?body (sms://)</a>
<a href="sms://+15552345678?body=Hello,%20World">Phone(+1) and ?body (sms://)</a>
<a href="sms://5552345678;body=Hello,%20World">Phone and ;body (sms://)</a>
<a href="sms://+15552345678;body=Hello,%20World">Phone(+1) and ;body (sms://)</a>
```

### WhatsApp Deeplink

```
<a href="whatsapp://send?text=Hello%20World!">WHATSAPP SHARE</a>
```

### Telefonnummern klickbar machen mit dem <a>-Tag

```html
<a href="tel:+4915111223344">+49 (0)151 11 22 33 44</a>
```

### Skype Links für Smartphones auf Webseiten bereitstellen

```html
<a href="skype:username?call">skype:username</a>
```

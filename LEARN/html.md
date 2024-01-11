# HTML

- Html ist das Skelett, Javascript die Muskeln und css die Haut einer Webseite.
- Zum Struckturieren der Webseite und deren Inhalte
- Auszeichnungssprache
- [https://htmlreference.io](https://htmlreference.io)
 

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
- für Layoutzwecke sollte man ``<div>`` einsetzen, aber nicht um inhaltlich zu strukturieren

### ``<ARTICLE>``
- Semantisch Context Unabhängiger Tag, etwa mini webpages in einem HTML-Document
- Sie haben ihre eigenen Header und Footer

### ``<SECTION>``
- Definiert einzelne Abschnitte in einem HTML-Document und der Gliederung
- Schafft semantische Strucktur
- Jedes Element hat seine eigene Header Strucktur, der Outlineeffekt wird aber nicht von jedem Browser richtig interpretiert
- Am besten nur ``<div>`` damit ersetzen und für Layoutzwecke verwenden
- Benötigt immer einen Header sonst wird es inder Gliederung als "untitled section" dargestellt

### ``<NAV>``
- Semantische information für Suchmaschienen
- Hilft die Seitenstrucktur schnell zu identifizieren und leichter andere Seiten zu finden
- Eine Seiten kann an verschiedenen Stellen ``<nav>``-Bereiche haben

### ``<HEADER>``
- Es zeichnet einleitende Inhalte für section, article oder die ganze Seite aus (name/logo, hauptnavigation)
- mehrere pro seite möglich, geben zusatzinformationen zu header zb.
- Headers werden nur mit dem nächstehenden body, section, article Element assoziert

### ``<FOOTER>``
- konzeptionell das gleiche wie header
- beinhalten typischerweise copyright notices, footer navigation, author bios of blogposts
- werden auch wieder mit dem nächstehenden article etc. assoziiert

### ``<ASIDE>``
- für nebeninformationen wie werbung etc die zusätzlich eingeblendet wird aber nichts mit den eigentlichen inhalten zutun hat
- for highlighting definitions, stats, or quotations
- im Zusammenhang mit der ganzen Seite, sollte man es als seitliche Navigationbar einsetzen

### ``<TIME>``
- für Zeitangaben, sehr nützlich für Suchmaschienenoptimierung
- ``<time ``datetime='2017-1-3 15:00-0800'>January 3rd``</time>``
 
### ``<ADDRESS>``
- um relevante adress und kontaktinformationen und email-adressen etc auszuzeichnen

### ``<figure>`` and ``<figcaption>`` 
- um grafiken, codschnippsel, tabellen etc extra auszuzeichnen


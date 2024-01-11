# My CSS Snippets

## Flip or Reverse Text Using CSS

As title says, we can Flip Text Upside Down or Reverse Text using CSS only(Rather than some jQuery Plugin or JavaScript). The CSS is completely Cross-browser compatible(Yeah, even older IEs), check out the CSS below.

### Flipping Text Upside Down

```css
-webkit-transform:rotate(-180deg);
-moz-transform:rotate(-180deg);
-o-transform:rotate(-180deg);
transform:rotate(-180deg);
ms-filter:"progid:DXImageTransform.Microsoft.BasicImage(rotation=2)";
filter:progid:DXImageTransform.Microsoft.BasicImage(rotation=2);
```

### Reversing Text

```css
direction: rtl;
unicode-bidi: bidi-override;
```
# Deeplinks

## SMS Simple Version ohne Telefonnummer

```   
sms:?&body=/* message body here */
```

## SMS Für IOS

```
<a href="sms:/* phone number here */&body=/* body text here */">Link</a>
```

## SMS Mit Java Script
```javascript
<a href="###" data-telno="13800000000" data-smscontent="hello" class="XXXXX XXXXXX XXXXXX sendsms"/>
    
$('.sendsms').on('click', function(){
    var p = $(this).data('telno'),
    c = $(this).data('smscontent'),
    t = ';';
    
    if (!ios) { // add your own iOS check
        t = '?';
    }
    location.href = 'sms:'+ p + t + c;
})
```

## SMS IOS Versionen

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

## WhatsApp Deeplink

```
<a href="whatsapp://send?text=Hello%20World!">WHATSAPP SHARE</a>
```

## Telefonnummern klickbar machen mit dem <a>-Tag

```html
<a href="tel:+4915111223344">+49 (0)151 11 22 33 44</a>
```

## Skype Links für Smartphones auf Webseiten bereitstellen
```html
<a href="skype:username?call">skype:username</a>
```
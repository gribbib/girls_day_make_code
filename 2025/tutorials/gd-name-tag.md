# Namensschild (Name Tag)
 
## Verwandle dein micro:bit in ein digitales Namensschild @unplugged

24.03.2026 - 15:40 | Test mit scripts für die Darstellung der md. ####
Nochmal eine Änderung am 17.03.2026 - 06:52. Release kommt dann kurz darauf
Änderung 14:22 Uhr. Eine Änderung 13.03.2026 - 13:38 :-) Noch eine Änderung 14:12
Zeige deinen Namen mit 💡 LEDs 💡! Programmiere den micro:bit, damit er deinen Namen über die Anzeige laufen lässt.
 
![Name scrolling on the LEDs](/static/mb/projects/name-tag/name-tag.gif)
 
## {Schritt 1}
 
Klicke unter Werkzeuge auf die Kategorie ``||basic:Grundlagen||``.
Ziehe einen ``||basic:zeige Text||``-Block in den ``||basic:dauerhaft||``-Block.
Ändere dann im ``||basic:zeige Text||``-Block den Text von "Hello!" zu deinem Namen.
 
```blocks
basic.forever(function() {
    basic.showString("Mein Name");
})
```
 
## {Schritt 2}
Schau dir den micro:bit-Simulator auf dem Bildschirm an. Siehst du, wie dein Name durchläuft? ⭐ Großartig ⭐! Du hast den micro:bit in ein digitales Namensschild verwandelt!
 
## {Schritt 3}
Wenn du ein micro:bit besitzt, schließe es an deinen Computer an und klicke auf ``|Download|``. Folge den Anweisungen, um deinen Code auf den micro:bit zu übertragen, und sieh zu, wie dein Name in leuchtenden Farben erscheint!
 
## {Schritt 4}
Gehe noch einen Schritt weiter und füge weitere ``||basic:zeige Text||``-Blöcke hinzu, um eine Geschichte zu erstellen! Erfahre in [diesem Video](https://youtu.be/qqBmvHD5bCw) mehr über die Funktionsweise der micro:bit-LEDs.
 
```template
basic.forever(function() {})
```

<script src="https://makecode.com/gh-pages-embed.js"></script>
<script src="https://makecode.com/tutorial-embed.js"></script>
<link rel="stylesheet" href="https://makecode.com/content/projects.css">
<script>
  makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");

  // Render für Tutorial-spezifische Inline-Blöcke
  makeCodeTutorialRender(document);
</script>
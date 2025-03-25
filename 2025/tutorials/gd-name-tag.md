# Namensschild (Name Tag)

## Verwandel dein micro:bit in ein digitales Namensschild @unplugged

Zeige deinen Namen mit 💡 LEDs! 💡  Programmiere den @boardname@ damit er deinen Namen über die Anzeige laufen lässt.

![Name scrolling on the LEDs](/static/mb/projects/name-tag/name-tag.gif)

## {Schritt 1}

Klicke unter Werkzeuge auf die Kategorie ``||basic:Grundlagen||``. 
Ziehe einen ``||basic:zeige Text||``-Block in den ``||basic:dauerhaft||``-Block.
Änder dann im ``||basic:zeige Text||``-Block den Text von „Hello!“ zu deinen Namen.

```blocks
basic.forever(function() {
    basic.showString("Mein Name");
})
```

## {Schritt 2}
Schau dir den @boardname@-Simulator auf dem Bildschirm an. Siehst du, wie dein Name durchläuft? ⭐ Großartig! ⭐ Du hast den micro:bit in ein digitales Namensschild verwandelt!

## {Schritt 3}
Wenn du ein @boardname@-Gerät besitzt, schließe es an deinen Computer an und klicke auf ``|Download|``. Folge den Anweisungen, um deinen Code auf das @boardname@ zu übertragen, und sieh zu, wie dein Name in leuchtenden Farben erscheint!

## {Schritt 4}
Gehe noch einen Schritt weiter und füge weitere ``||basic:zeige Text||``-Blöcke hinzu, um eine Geschichte zu erstellen! Erfahre in [diesem Video](https://youtu.be/qqBmvHD5bCw) mehr über die Funktionsweise der @boardname@-LEDs.

```template
basic.forever(function() {})
```
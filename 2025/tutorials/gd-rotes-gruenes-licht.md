# Rotes Licht Grünes Licht


## Spielregeln @unplugged

Dies ist das klassische „Rotes Licht, grünes Licht“-Spiel, bei dem eine Person eine virtuelle Ampel ist und den anderen Spielern den Befehl gibt, anzuhalten oder weiterzufahren.

Der als aktuelle Ampel ausgewählte Spieler sagt „Grünes Licht!“ und wendet sich von den anderen Spielern ab. Die anderen Spieler bewegen sich aus einer zu Beginn des Spiels festgelegten Entfernung auf den Ampelspieler zu und versuchen, ihn zu berühren. Der Ampelspieler kann jederzeit „Rotes Licht!“ sagen und sich dann zu den anderen Spielern umdrehen. Wenn der Ampelspieler sieht, dass sich noch jemand bewegt, ruft er ihn auf, und das Spiel ist beendet, bis ein neues Spiel begonnen wird. Der Ampelspieler wiederholt den Zyklus Rotes Licht, Grünes Licht. Wenn einer der anderen Spieler zufällig den Ampelspieler berührt, bevor er sich umdrehen kann, während er „Rotes Licht!“ sagt, bewegt sich der aktuelle Ampelspieler zum Anfang des Parcours und der andere Spieler wird zur Ampel. Das Spiel wird fortgesetzt, bis nur noch der Ampelspieler übrig ist.

In dieser Neuauflage des Spiels verwenden wir einen @boardname@, sein Radio und den Beschleunigungsmesser, um diese Regeln durchzusetzen!

### Multi editor

Dieses Projekt nutzt Funk, um den Status anderer @boardname@s zu kommunizieren. Es ist hilfreich zu wissen, wie ein zweiter @boardname@ auf eine Funknachricht reagiert. Mit der Multi-Editor-Funktion kannst du zwei Radioprogramme programmieren und testen. Öffne https://makecode.com/multi , um zwei parallele @boardname@-Editoren zu starten.

## { Erstellen der Ampel }

Beginnen wir mit dem Code, der auf dem @boardname@ der Ampel läuft. Verwende diesen Code nicht für die anderen Spieler!

## { Zustände }

Wir definieren zwei _Zustände_ bzw. Spielbedingungen als ``||variables:Variablen||``, genannt ``GRUENESLICHT`` und ``ROTESLICHT``.
Eine ``||variables:Variable||`` namens ``zustand`` speichert den aktuellen Spielzustand. ``||variables:Setze ||`` im ``||basic:beim Start||``-Block ``GRUENESLICHT`` auf ``1`` und ``ROTESLICHT`` auf ``2``.

```blocks
let ROTESLICHT = 0
let zustand = 0
let GRUENESLICHT = 0
GRUENESLICHT = 1
ROTESLICHT = 2
```

## {Funkgruppe setzen}
Setze die ``||radio:Funkgruppe||`` im ``||basic:beim Start||``-Block für alle Spieler auf ``1``. Wir werden dieselbe Gruppe auch im Code des Spielers festlegen.
```blocks
let ROTESLICHT = 0
let zustand = 0
let GRUENESLICHT = 0
GRUENESLICHT = 1
ROTESLICHT = 2
radio.setGroup(1)
```

## { Rotes Licht, grünes Licht }

Verwende den ``||input:wenn Knopf ... geklickt||``-Block, um Code auszuführen, wenn die Tasten ``A`` und ``B`` gedrückt werden. Wenn ``A`` gedrückt wird, wird ``zustand`` mit ``||variables:setze ... auf||``  auf  ``GRUENESLICHT`` gesetzt. Wenn ``B`` gedrückt wird, wird ``zustand`` auf ``ROTESLICHT`` gesetzt. Wir verwenden außerdem ``||basic:zeige Symbol||``, um den aktuellen Spielstatus anzuzeigen.

```blocks
let ROTESLICHT = 0
let zustand = 0
let GRUENESLICHT = 0
input.onButtonPressed(Button.A, function () {
    zustand = GRUENESLICHT
    basic.showIcon(IconNames.Yes)
})
input.onButtonPressed(Button.B, function () {
    zustand = ROTESLICHT
    basic.showIcon(IconNames.No)
})
```

## { Kommunikation }

Eine ``||basic:dauerhaft||``-Schleife überträgt den Spielstatus mit ``||radio:sende Zahl ... über Funk||``, sodass die Spieler ihn kontinuierlich erhalten.

```blocks
let ROTESLICHT = 0
let zustand = 0
let GRUENESLICHT = 0
input.onButtonPressed(Button.A, function () {
    zustand = GRUENESLICHT
    basic.showIcon(IconNames.Yes)
})
input.onButtonPressed(Button.B, function () {
    zustand = ROTESLICHT
    basic.showIcon(IconNames.No)
})
basic.forever(function () {
    radio.sendNumber(zustand)
})
```

## { ~ hint }

Wenn du ein @boardname@-Gerät besitzt, dass die Ampel sein soll, schließe es an deinen Computer an und klicke auf ``|Download|``. Folge den Anweisungen, um deinen Code auf das @boardname@ zu übertragen. Sobald dein Code heruntergeladen ist, kannst du deinen micro:bit als Ampel für Rotes-Licht-Grünes-Licht nutzen
??? Denke daran, dieses Programm in ``stoplight`` oder etwas Ähnliches umzubenennen, damit du es nicht mit dem Player-Programm verwechselst!

## { Verbessere das Spiel }

* Verwende ``||music:ring tone||``, um einen Ton abzuspielen, während das Spiel im ``GRUENESLICHT``-Modus ist.
* Befestige ein Servo und bewege den Arm je nach Spielstatus.

```blocks
let ROTESLICHT = 0
let zustand = 0
let GRUENESLICHT = 0
input.onButtonPressed(Button.A, function () {
    zustand = GRUENESLICHT
    basic.showIcon(IconNames.Yes)
    music.play(music.builtinPlayableSoundEffect(soundExpression.giggle), music.PlaybackMode.UntilDone)
})
input.onButtonPressed(Button.B, function () {
    zustand = ROTESLICHT
    basic.showIcon(IconNames.No)
})
basic.forever(function () {
    radio.sendNumber(zustand)
})
```

## { Die Spieler }

Der Code für die anderen Spieler muss auf den Zustand der Ampel achten.

## { Zustände }

Wir definieren zwei _Zustände_ bzw. Spielbedingungen als ``||variables:Variablen||``, genannt ``GRUENESLICHT`` und ``ROTESLICHT``.
Eine ``||variables:Variable||`` namens ``zustand`` speichert den aktuellen Spielzustand. ``||variables:Setze ||`` im ``||basic:beim Start||``-Block ``GRUENESLICHT`` auf ``1`` und ``ROTESLICHT`` auf ``2``.

```blocks
let ROTESLICHT = 0
let zustand = 0
let GRUENESLICHT = 0
GRUENESLICHT = 1
ROTESLICHT = 2
```

## {Funkgruppe setzen}
Setze die ``||radio:Funkgruppe||`` im ``||basic:beim Start||``-Block für alle Spieler auf ``1``. Wir werden dieselbe Gruppe auch im Code des Spielers festlegen.
```blocks
let ROTESLICHT = 0
let zustand = 0
let GRUENESLICHT = 0
GRUENESLICHT = 1
ROTESLICHT = 2
radio.setGroup(1)
```

## { Kommunikation }

Wir verwenden den ``||radio:wenn Zahl empfangen||``-Block, um den Ampelstatus in der ``zustand``-Variablen zu speichern.

```blocks
let ROTESLICHT = 0
let zustand = 0
let GRUENESLICHT = 0
GRUENESLICHT = 1
ROTESLICHT = 2
radio.setGroup(1)
radio.onReceivedNumber(function (receivedNumber) {
    zustand = receivedNumber
})
```

## { Anzeige }

In einer ``||basic:dauerhaft||``-Schleife zeigen wir je nach Spielstatus unterschiedliche Symbole an. Verwende einen ``||logic:wenn ... dann||``- und einen ``||basic:zeige Symbol||``-Block, um den Spielstatus anzuzeigen.

```blocks
let ROTESLICHT = 0
let zustand = 0
let GRUENESLICHT = 0
basic.forever(function () {
    if (zustand == GRUENESLICHT) {
        basic.showIcon(IconNames.Yes)
    } else if (zustand == ROTESLICHT) {
        basic.showIcon(IconNames.No)
    }
})
```

## { Bewegungsprüfung }

Wenn der Wert ``zustand`` gleich ``ROTESLICHT`` ist, müssen wir sicherstellen, dass sich der Spieler nicht bewegt. Hier kommt der Beschleunigungsmesser ins Spiel. Er misst die auf den @boardname@ wirkenden Kräfte. 
Bewegt sich der Spieler, erkennt der Beschleunigungsmesser wahrscheinlich auch kleine Kräfte, die auf den @boardname@ wirken. 
Der @boardname@ wirkt ständig unter Schwerkraft, daher liegt die Beschleunigung im Ruhezustand immer bei etwa ``1000`` mg. Liegt die Beschleunigung weit von diesem Wert ab, beispielsweise bei ``1100`` oder ``900``, können wir davon ausgehen, dass sich der Spieler bewegt. Zur Berechnung verwenden wir die folgende Formel:

``bewegung = | beschleunigung - 1000 |``

## { Umsetzung }
Da wir nun die Mathematik dahinter kennen, können wir dies in Code umwandeln. 
Ziehe eine neue ``||basic:dauerhaft||``-Schleife auf die Arbeitsfläche und in diese einen ``||logic:wenn ... dann||``-Block mit der Bedingung ``zustand = ROTESLICHT``.
Wir benötigen eine ``bewegung`` ``||variables:Variable||`` die auf ``||math:absolute Werte von||`` gesetzt wird. Dieser Block enthält einen ``||math:Minus||``-Block aus ``||input:Beschleunigung||`` und ``1000``.

```blocks
let bewegung = 0
let ROTESLICHT = 0
let zustand = 0
let GRUENESLICHT = 0
radio.onReceivedNumber(function (receivedNumber) {
    zustand = receivedNumber
})
GRUENESLICHT = 1
ROTESLICHT = 2
radio.setGroup(1)
basic.forever(function () {
    if (zustand == GRUENESLICHT) {
        basic.showIcon(IconNames.Yes)
    } else if (zustand == ROTESLICHT) {
        basic.showIcon(IconNames.No)
    }
})
basic.forever(function () {
    if (zustand == ROTESLICHT) {
        bewegung = Math.abs(input.acceleration(Dimension.Strength) - 1000)
        if (bewegung > 100) {
            game.gameOver()
        }
    }
})
```

## { ~ hint }

Wenn du ein @boardname@-Gerät besitzt, dass ein Spieler sein soll, schließe es an deinen Computer an und klicke auf ``|Download|``. Folge den Anweisungen, um deinen Code auf das @boardname@ zu übertragen. Sobald dein Code heruntergeladen ist, kannst du deinen micro:bit als Ampel für Rotes-Licht-Grünes-Licht nutzen
??? Denke daran, dieses Programm in ``player`` oder etwas Ähnliches umzubenennen, damit du es nicht mit dem Ampelprogramm verwechselst!

## { Tuning }

Funktioniert die Bewegungsprüfung? Versuche, den Wert ``100`` zu ändern, um die Erkennungsempfindlichkeit anzupassen. Versuche es vielleicht mit ``64``.

## { Improve the game }

* Verwende ``||music:ring tone||``, um im ``GRUENESLICHT``-Modus einen Ton abzuspielen.
* Verwende die Paketsignalstärke, um festzustellen, ob du die Ampel erreicht hast.

```blocks
let bewegung = 0
let ROTESLICHT = 0
let zustand = 0
let GRUENESLICHT = 0
radio.onReceivedNumber(function (receivedNumber) {
    zustand = receivedNumber
})
GRUENESLICHT = 1
ROTESLICHT = 2
radio.setGroup(1)
basic.forever(function () {
    if (zustand == GRUENESLICHT) {
        basic.showIcon(IconNames.Yes)
		music.play(music.builtinPlayableSoundEffect(soundExpression.giggle), music.PlaybackMode.UntilDone)
    } else if (zustand == ROTESLICHT) {
        basic.showIcon(IconNames.No)
    }
})
basic.forever(function () {
    if (zustand == ROTESLICHT) {
        bewegung = Math.abs(input.acceleration(Dimension.Strength) - 1000)
        if (bewegung > 100) {
            game.gameOver()
        }
    }
})
```

```package
radio
music
```
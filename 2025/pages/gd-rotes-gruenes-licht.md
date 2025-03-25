# Rotes Licht Grünes Licht


## Spielregeln @unplugged

Dies ist das klassische „Rotes Licht, grünes Licht“-Spiel, bei dem eine Person eine virtuelle Ampel ist und den anderen Spielern den Befehl gibt, anzuhalten oder weiterzufahren.

Der als aktuelle Ampel ausgewählte Spieler sagt „Grünes Licht!“ und wendet sich von den anderen Spielern ab. Die anderen Spieler bewegen sich aus einer zu Beginn des Spiels festgelegten Entfernung auf den Ampelspieler zu und versuchen, ihn zu berühren. Der Ampelspieler kann jederzeit „Rotes Licht!“ sagen und sich dann zu den anderen Spielern umdrehen. Wenn der Ampelspieler sieht, dass sich noch jemand bewegt, ruft er ihn auf, und das Spiel ist beendet, bis ein neues Spiel begonnen wird. Der Ampelspieler wiederholt den Zyklus Rotes Licht, Grünes Licht. Wenn einer der anderen Spieler zufällig den Ampelspieler berührt, bevor er sich umdrehen kann, während er „Rotes Licht!“ sagt, bewegt sich der aktuelle Ampelspieler zum Anfang des Parcours und der andere Spieler wird zur Ampel. Das Spiel wird fortgesetzt, bis nur noch der Ampelspieler übrig ist.

In dieser Neuauflage des Spiels verwenden wir einen @boardname@, sein Radio und den Beschleunigungsmesser, um diese Regeln durchzusetzen!

### Multi editor

Dieses Projekt nutzt Funk, um den Status anderer @boardname@s zu kommunizieren. Es ist hilfreich zu wissen, wie ein zweiter @boardname@ auf eine Funknachricht reagiert. Mit der Multi-Editor-Funktion kannst du zwei Radioprogramme programmieren und testen. Öffne https://makecode.com/multi , um zwei parallele @boardname@-Editoren zu starten.

## Erstellen der Ampel

Beginnen wir mit dem Code, der auf dem micro:bit der Ampel läuft. Verwende diesen Code nicht für die anderen Spieler!

### Zustände

Wir definieren zwei _Zustände_ bzw. Spielbedingungen, genannt ``GRUENESLICHT`` und ``ROTESLICHT``. Eine Variable namens ``zustand`` speichert den aktuellen Spielzustand. Drückt der Ampelspieler ``A``, wechselt das Spiel in den „Grünes Licht“-Modus. Drückt er ``B``, wechselt der Zustand in den „Rotes Licht“-Modus. Die Funkgruppe für alle Spieler ist auf ``1`` eingestellt. Wir werden dieselbe Gruppe auch im Code des Spielers festlegen.

```blocks
let ROTESLICHT = 0
let zustand = 0
let GRUENESLICHT = 0
GRUENESLICHT = 1
ROTESLICHT = 2
radio.setGroup(1)
```

### Kommunikation

Eine ``||basic:dauerhaft||``-Schleife überträgt den Spielstatus, sodass die Spieler ihn kontinuierlich erhalten.

```blocks
let zustand = 0
basic.forever(function () {
    radio.sendNumber(zustand)
})
```

### Rotes Licht, grünes Licht

Verwende den ``||input:wenn Knopf ... geklickt||``-Block, um Code auszuführen, wenn die Tasten ``A`` und ``B`` gedrückt werden. Wenn ``A`` gedrückt wird, wechselt das Spiel in den ``GRUENESLICHT``-Modus. Wenn ``B`` gedrückt wird, wechselt das Spiel in den ``ROTESLICHT``-Modus. Wir verwenden außerdem ``||basic:zeige Symbol||``, um den aktuellen Spielstatus anzuzeigen.

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

### Ampelcode

Insgesamt sieht der Ampelcode folgendermaßen aus:

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
zustand = 0
GRUENESLICHT = 1
ROTESLICHT = 2
radio.setGroup(1)
basic.forever(function () {
    radio.sendNumber(zustand)
})
```

### ~ hint

Denke daran, dieses Programm in ``stoplight`` oder etwas Ähnliches umzubenennen, damit du es nicht mit dem Player-Programm verwechselst!

### ~

### Verbessere das Spiel

* Verwende ``||music:ring tone||``, um einen Ton abzuspielen, während das Spiel im ``GRUENESLICHT``-Modus ist.
* Befestige ein Servo und bewege den Arm je nach Spielstatus.

## Die Spieler

Der Code für die anderen Spieler muss auf den Zustand der Ampel achten.

### Zustände

Zuerst definieren wir erneut die Zustandskonstanten ``GRUENESLICHT``, ``ROTESLICHT``, und setzen die Funkgruppe auf ``1``. Wir fügen außerdem eine ``zustand`` Variable hinzu, die den Zustand des Spiels speichert.

```blocks
let ROTESLICHT = 0
let zustand = 0
let GRUENESLICHT = 0
GRUENESLICHT = 1
ROTESLICHT = 2
radio.setGroup(1)
```

### Kommunikation

Wir verwenden den ``||radio:wenn Zahl empfangen||``-Block, um den Ampelstatus in der ``zustand`` Variablen zu speichern.

```blocks
let zustand = 0
radio.onReceivedNumber(function (receivedNumber) {
    zustand = receivedNumber
})
```

### Anzeige

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

### Bewegungsprüfung

Wenn der Wert ``zustand`` gleich ``ROTESLICHT`` ist, müssen wir sicherstellen, dass sich der Spieler nicht bewegt. Hier kommt der Beschleunigungsmesser ins Spiel. Er misst die auf den @boardname@ wirkenden Kräfte. 
Bewegt sich der Spieler, erkennt der Beschleunigungsmesser wahrscheinlich auch kleine Kräfte, die auf den @boardname@ wirken. 
Der @boardname@ wirkt ständig unter Schwerkraft, daher liegt die Beschleunigung im Ruhezustand immer bei etwa ``1000`` mg. Liegt die Beschleunigung weit von diesem Wert ab, beispielsweise bei ``1100`` oder ``900``, können wir davon ausgehen, dass sich der Spieler bewegt. Zur Berechnung verwenden wir die folgende Formel:

```
movement = | acc strength - 1000 |
```

Da wir nun die Mathematik dahinter kennen, können wir dies in Code umwandeln.

```blocks
let ROTESLICHT = 0
let zustand = 0
let GRUENESLICHT = 0
let movement = 0
basic.forever(function () {
    if (zustand == ROTESLICHT) {
        movement = Math.abs(input.acceleration(Dimension.Strength) - 1000)
        if (movement > 100) {
            game.gameOver()
        }
    }
})
```

### Spielercode

Insgesamt lautet der Code für die Spieler:

```blocks
let movement = 0
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
        movement = Math.abs(input.acceleration(Dimension.Strength) - 1000)
        if (movement > 100) {
            game.gameOver()
        }
    }
})
```

### ~ hint

Denke daran, dieses Programm in ``player`` oder etwas Ähnliches umzubenennen, damit du es nicht mit dem Ampelprogramm verwechselst!

### ~


### Tuning

Funktioniert die Bewegungsprüfung? Versuche, den Wert ``100`` zu ändern, um die Erkennungsempfindlichkeit anzupassen. Versuche es vielleicht mit ``64``.

### Improve the game

* Verwende ``||music:ring tone||``, um im grünen Modus einen Ton abzuspielen.
* Verwende die Paketsignalstärke, um festzustellen, ob du die Ampel erreicht hast.


```package
radio
```
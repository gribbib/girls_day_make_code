# Rotes Licht Grünes Licht

## Spielregeln @unplugged
 
Bei diesem Spiel nimmt ein Spieler die Rolle einer Ampel ein und gibt anderen Mitspielern den Befehl sich vorwärts zu bewegen oder anzuhalten. Die Spieler müssen sich dabei auf den Ampelspieler zubewegen.

Der als Ampel ausgewählte Spieler sagt "Grünes Licht!" und wendet sich von den anderen Spielern ab. Die anderen Spieler bewegen sich aus einer zu Beginn des Spiels festgelegten Entfernung auf den Ampelspieler zu und versuchen, ihn zu berühren. Der Ampelspieler kann jederzeit "Rotes Licht!" rufen und sich zu den anderen Spielern umdrehen. Wenn der Ampelspieler sieht, dass sich noch jemand bewegt, fordert er ihn auf, das Spielfeld zu verlassen. Der Ampelspieler wiederholt diesen Zyklus, bis alle verbleibenden Spieler beim Ampelspieler angekommen sind.

Der micro:bit hilft dabei, die Bewegungen der Spieler zu erkennen.
 
### Multi editor
 
Dieses Projekt nutzt Funk, um zwischen den micro:bits zu kommunizieren. Es ist hilfreich zu wissen, wie ein zweiter micro:bit auf eine Funknachricht reagiert. Mit der Multi-Editor-Funktion kannst du zwei Radioprogramme programmieren und testen. Öffne https://makecode.com/multi , um zwei parallele micro:bit-Editoren zu starten.
 
## { Ampel: Erstellen der Ampel }
 
Beginnen wir mit dem Code, der auf dem micro:bit des Ampelspielers läuft. Verwende diesen Code nicht für die Mitspieler!
 
## { Ampel: Zustände }
 
Wir definieren zwei _Zustände_ als ``||variables:Variablen||``, genannt ``grueneslicht`` und ``roteslicht``.
Eine ``||variables:Variable||`` namens ``zustand`` speichert den aktuellen Spielzustand. Setze im ``||basic:beim Start||``-Block ``grueneslicht`` auf ``1`` und ``roteslicht`` auf ``2``.
 
```blocks
let roteslicht = 0
let zustand = 0
let grueneslicht = 0
grueneslicht = 1
roteslicht = 2
```
 
## { Ampel: Funkgruppe setzen}
Setze die ``||radio:Funkgruppe||`` im ``||basic:beim Start||``-Block für alle Spieler auf ``1``. Wir werden dieselbe Gruppe später auch im Code des Spielers festlegen.
```blocks
let roteslicht = 0
let zustand = 0
let grueneslicht = 0
grueneslicht = 1
roteslicht = 2
radio.setGroup(1)
```
 
## { Ampel: Rotes Licht, grünes Licht }
 
Verwende den ``||input:wenn Knopf ... geklickt||``-Block, um Code auszuführen, wenn die Tasten ``A`` und ``B`` gedrückt werden. Wenn ``A`` gedrückt wird, wird ``zustand`` mit ``||variables:setze ... auf||``  auf  ``grueneslicht`` gesetzt. Wenn ``B`` gedrückt wird, wird ``zustand`` auf ``roteslicht`` gesetzt. Wir verwenden außerdem ``||basic:zeige Symbol||``, um den aktuellen Spielstatus anzuzeigen.
 
```blocks
let roteslicht = 0
let zustand = 0
let grueneslicht = 0
input.onButtonPressed(Button.A, function () {
    zustand = grueneslicht
    basic.showIcon(IconNames.Yes)
})
input.onButtonPressed(Button.B, function () {
    zustand = roteslicht
    basic.showIcon(IconNames.No)
})
```
 
## { Ampel: Kommunikation }
 
Eine ``||basic:dauerhaft||``-Schleife überträgt den Spielstatus mit ``||radio:sende Zahl ... über Funk||``, sodass die Spieler ihn kontinuierlich erhalten.
 
```blocks
let roteslicht = 0
let zustand = 0
let grueneslicht = 0
input.onButtonPressed(Button.A, function () {
    zustand = grueneslicht
    basic.showIcon(IconNames.Yes)
})
input.onButtonPressed(Button.B, function () {
    zustand = roteslicht
    basic.showIcon(IconNames.No)
})
basic.forever(function () {
    radio.sendNumber(zustand)
})
```
 
## { ~ hint }
 
Wenn du ein micro:bit besitzt, dass die Ampel sein soll, schließe es an deinen Computer an und klicke auf ``|Download|``. Folge den Anweisungen, um deinen Code auf das micro:bit zu übertragen. Sobald dein Code heruntergeladen ist, kannst du deinen micro:bit als Ampel für Rotes-Licht-Grünes-Licht nutzen.
 
## { Verbessere das Spiel }
 
* Verwende ``||music:ring tone||``, um einen Ton abzuspielen, während das Spiel im ``grueneslicht``-Modus ist.
 
```blocks
let roteslicht = 0
let zustand = 0
let grueneslicht = 0
input.onButtonPressed(Button.A, function () {
    zustand = grueneslicht
    basic.showIcon(IconNames.Yes)
    music.play(music.builtinPlayableSoundEffect(soundExpression.giggle), music.PlaybackMode.UntilDone)
})
input.onButtonPressed(Button.B, function () {
    zustand = roteslicht
    basic.showIcon(IconNames.No)
})
basic.forever(function () {
    radio.sendNumber(zustand)
})
```
 
## { Mitspieler: Der Spielercode }
 
Der Code für die anderen Spieler muss auf den Zustand der Ampel achten.
 
## { Mitspieler: Zustände }
 
Wir definieren zwei _Zustände_ bzw. Spielbedingungen als ``||variables:Variablen||``, genannt ``grueneslicht`` und ``roteslicht``.
Eine ``||variables:Variable||`` namens ``zustand`` speichert den aktuellen Spielzustand. ``||variables:Setze ||`` im ``||basic:beim Start||``-Block ``grueneslicht`` auf ``1`` und ``roteslicht`` auf ``2``.
 
```blocks
let roteslicht = 0
let zustand = 0
let grueneslicht = 0
grueneslicht = 1
roteslicht = 2
```
 
## { Mitspieler: Funkgruppe setzen}
Setze die ``||radio:Funkgruppe||`` im ``||basic:beim Start||``-Block für alle Spieler auf ``1``. Wir werden dieselbe Gruppe auch im Code des Spielers festlegen.
```blocks
let roteslicht = 0
let zustand = 0
let grueneslicht = 0
grueneslicht = 1
roteslicht = 2
radio.setGroup(1)
```
 
## { Mitspieler: Kommunikation }
 
Wir verwenden den ``||radio:wenn Zahl empfangen||``-Block, um den Ampelstatus in der ``zustand``-Variable zu speichern.
 
```blocks
let roteslicht = 0
let zustand = 0
let grueneslicht = 0
grueneslicht = 1
roteslicht = 2
radio.setGroup(1)
radio.onReceivedNumber(function (receivedNumber) {
    zustand = receivedNumber
})
```
 
## { Mitspieler: Anzeige }
 
In einer ``||basic:dauerhaft||``-Schleife zeigen wir je nach Spielstatus unterschiedliche Symbole an. Verwende einen ``||logic:wenn ... dann||``- und einen ``||basic:zeige Symbol||``-Block, um den Spielstatus anzuzeigen.
 
```blocks
let roteslicht = 0
let zustand = 0
let grueneslicht = 0
basic.forever(function () {
    if (zustand == grueneslicht) {
        basic.showIcon(IconNames.Yes)
    } else if (zustand == roteslicht) {
        basic.showIcon(IconNames.No)
    }
})
```
 
## { Mitspieler: Bewegungsprüfung }
 
Wenn der Wert ``zustand`` gleich ``roteslicht`` ist, müssen wir sicherstellen, dass sich der Spieler nicht bewegt. Hier kommt der Beschleunigungsmesser ins Spiel. Er misst die auf den micro:bit wirkenden Kräfte.
Bewegt sich der Spieler, erkennt der Beschleunigungsmesser wahrscheinlich auch kleine Kräfte, die auf den micro:bit wirken.
Der micro:bit wirkt ständig unter Schwerkraft, daher liegt die Beschleunigung im Ruhezustand immer bei etwa ``1000`` mg. Liegt die Beschleunigung weit von diesem Wert ab, beispielsweise bei ``1100`` oder ``900``, können wir davon ausgehen, dass sich der Spieler bewegt. Zur Berechnung verwenden wir die folgende Formel:
 
``bewegung = | beschleunigung - 1000 |``
 
## { Mitspieler: Umsetzung }
Da wir nun die Mathematik dahinter kennen, können wir dies in Code umwandeln.
Ziehe eine neue ``||basic:dauerhaft||``-Schleife auf die Arbeitsfläche und in diese einen ``||logic:wenn ... dann||``-Block mit der Bedingung ``zustand = roteslicht``.
Wir benötigen eine ``bewegung`` ``||variables:Variable||`` die auf ``||math:absolute Werte von||`` gesetzt wird. Dieser Block enthält einen ``||math:Minus||``-Block aus ``||input:Beschleunigung||`` und ``1000``.
 
```blocks
let bewegung = 0
let roteslicht = 0
let zustand = 0
let grueneslicht = 0
radio.onReceivedNumber(function (receivedNumber) {
    zustand = receivedNumber
})
grueneslicht = 1
roteslicht = 2
radio.setGroup(1)
basic.forever(function () {
    if (zustand == grueneslicht) {
        basic.showIcon(IconNames.Yes)
    } else if (zustand == roteslicht) {
        basic.showIcon(IconNames.No)
    }
})
basic.forever(function () {
    if (zustand == roteslicht) {
        bewegung = Math.abs(input.acceleration(Dimension.Strength) - 1000)
        if (bewegung > 100) {
            game.gameOver()
        }
    }
})
```
 
## { ~ hint }
 
Wenn du ein micro:bit besitzt, dass ein Mitspieler sein soll, schließe es an deinen Computer an und klicke auf ``|Download|``. Folge den Anweisungen, um deinen Code auf das micro:bit zu übertragen. Sobald dein Code heruntergeladen ist, kannst du deinen micro:bit als Ampel für Rotes-Licht-Grünes-Licht nutzen.
 
## { Mitspieler: Tuning }
 
Funktioniert die Bewegungserkennung? Versuche, den Wert ``100`` zu ändern, um die Erkennungsempfindlichkeit anzupassen. Versuche es alternativ auch mit ``64``.
 
## { Mitspieler: Improve the game }
 
* Verwende ``||music:ring tone||``, um im ``grueneslicht``-Modus einen Ton abzuspielen.
 
```blocks
let bewegung = 0
let roteslicht = 0
let zustand = 0
let grueneslicht = 0
radio.onReceivedNumber(function (receivedNumber) {
    zustand = receivedNumber
})
grueneslicht = 1
roteslicht = 2
radio.setGroup(1)
basic.forever(function () {
    if (zustand == grueneslicht) {
        basic.showIcon(IconNames.Yes)
        music.play(music.builtinPlayableSoundEffect(soundExpression.giggle), music.PlaybackMode.UntilDone)
    } else if (zustand == roteslicht) {
        basic.showIcon(IconNames.No)
    }
})
basic.forever(function () {
    if (zustand == roteslicht) {
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

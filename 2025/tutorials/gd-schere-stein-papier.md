# Schere-Stein-Papier
 
## {Einführung  @unplugged}
 
![RPS-Cartoon](/static/mb/projects/a4-motion.png)
 
Verwandle dein micro:bit in ein **Schere-Stein-Papier**-Spiel, das du mit deinen Freunden spielen kannst!

## {Schritt 1}
 
Zuerst müssen wir eine Variable erstellen, um zu verfolgen, ob wir einen Stein, Papier oder eine Schere in der Hand haben.
Eine Variable ist ein Behälter zum Speichern von unterschiedlichen Werten.
Klicke auf die ``||variables:Variablen||`` Kategorie unter Werkzeuge.
Klicke auf die Schaltfläche **Erstelle eine Variable...**.
Gebe deiner neuen Variable den Namen **hand** und klicke auf ``|OK|``.
 
![Animation-Variable](/static/mb/projects/rock-paper-scissors/newvar.gif)
 
## {Schritt 2}
Klicke erneut auf die Kategorie ``||variables:Variablen||`` unter Werkzeuge.
Du wirst bemerken, dass einige neue Blöcke erschienen sind.
Ziehe den Block ``||variables:setze hand auf 0||`` in den Block ``||input:wenn geschüttelt||``. Wir beginnen unser Schere-Stein-Papier-Spiel, wenn wir den micro:bit schütteln 👋.
 
```blocks
let hand = 0;
input.onGesture(Gesture.Shake, function() {
    hand = 0
})
```
 
## {Schritt 3}
Klicke auf die Kategorie ``||math:Mathematik||`` unter Werkzeuge. Ziehe einen Block ``||math:wähle eine zufällige Zahl von 1 bis 3||`` und lege ihn in den Block ``||variables:setze hand||``, indem du die Zahl **0** ersetzt. Wenn wir nun unseren micro:bit schütteln würden, würde die Variable eine Zufallszahl zwischen 1 und 3 enthalten.
 
```blocks
let hand = 0;
input.onGesture(Gesture.Shake, function() {
    hand = randint(1, 3)
})
```
 
## {Schritt 4}
 
In einem späteren Schritt wird jeder möglichen Zahl (1, 2 oder 3) ein eigenes Bild zugeordnet. Das Bild wird auf der LED-Matrix angezeigt, wenn die passende Zahl ausgewählt wird.
Klicke auf die Kategorie ``||logic:Logik||`` unter Werkzeuge. Ziehe einen ``||logic:wenn wahr dann ... ansonsten||``-Block in den ``||input:wenn geschüttelt||``-Block unterhalb des ``||variables:setze hand||``-Blocks.
 
```blocks
let hand = 0;
input.onGesture(Gesture.Shake, function() {
    hand = randint(1, 3)
    if (true) {
         
    } else {
         
    }
})
```
 
## {Schritt 5}
 
Ziehe aus der Kategorie ``||logic:Logik||`` den ``||logic:0 = 0||``-Block in den ``||logic:wenn wahr dann ... ansonsten||``-Block, sodass **wahr** ersetzt wird.
 
```blocks
let hand = 0;
input.onGesture(Gesture.Shake, function() {
    hand = randint(1, 3)
    if (0 == 0) {
         
    } else {
         
    }
})
```
 
## {Schritt 6}
 
Klicke auf die Kategorie ``||variables:Variablen||`` unter Werkzeuge. Ziehe den ``||variables:hand||``-Block in den ``||logic:0 = 0||``-Block, sodass die erste **0** ersetzt wird.
Klicke dann auf die zweite **0** und ändere sie zu **1**.
 
```blocks
let hand = 0;
input.onGesture(Gesture.Shake, function() {
    hand = randint(1, 3)
    if (hand == 1) {
         
    } else {
         
    }
})
```
 
## {Schritt 7}
 
Klicke auf die Kategorie ``||basic:Grundlagen||`` unter Werkzeuge. Ziehe einen ``||basic:zeige Symbol||``-Block unterhalb des ``||logic:wenn hand = 1 dann||``-Block. Klicke in dem ``||basic:zeige Symbol||``-Block auf das Herz-Symbol und wähle stattdessen das kleine Quadrat, um den 💎 Stein darzustellen. 
 
```blocks
let hand = 0;
input.onGesture(Gesture.Shake, function() {
    hand = randint(1, 3)
    if (hand == 1) {
        basic.showIcon(IconNames.SmallSquare)
    } else {
         
    }
})
```
 
## {Schritt 8}
 
Klicke am Ende des ``||logic:wenn dann ansonsten||``-Blocks auf das Plus-Symbol **'+'**, um die Erweiterung für den Code um eine ``||logic:sonst wenn ... dann||``-Klausel zu erweitern.
 
```blocks
let hand = 0;
input.onGesture(Gesture.Shake, function() {
    hand = randint(1, 3)
    if (hand == 1) {
        basic.showIcon(IconNames.SmallSquare)
    } else if (false) {
         
    } else {
         
    }
})
```
 
## {Schritt 9}
 
Ziehe aus der Kategorie ``||logic:Logik||`` einen ``||logic:0 = 0||``-Block und lege ihn in der ``||logic:sonst wenn ... dann||``-Klausel ab, sodass **falsch** ersetzt wird.
 
```blocks
let hand = 0;
input.onGesture(Gesture.Shake, function() {
    hand = randint(1, 3)
    if (hand == 1) {
        basic.showIcon(IconNames.SmallSquare)
    } else if (0 == 0) {
         
    } else {
         
    }
})
```
 
## {Schritt 10}
 
Ziehe aus der Kategorie ``||variables:Variablen||`` den ``||variables:hand||``-Block in den Vergleichsblock ``||logic:0 = 0||``, um die erste **0** zu ersetzen. Klicke auf die zweite **0** im Vergleichsblock und ändere sie zu einer **2**.
 
```blocks
let hand = 0;
input.onGesture(Gesture.Shake, function() {
    hand = randint(1, 3)
    if (hand == 1) {
        basic.showIcon(IconNames.SmallSquare)
    } else if (hand == 2) {
         
    } else {
         
    }
})
```
 
## {Schritt 11}
 
Ziehe aus der Kategorie ``||basic:Grundlagen||`` einen ``||basic:zeige Symbol||``-Block heraus und lege ihn unter ``||logic:sonst wenn hand = 2 dann||``. Klicke in dem ``||basic:zeige Symbol||``-Block auf das Herz-Symbol und wähle stattdessen das große Quadrat, um 📃 Papier darzustellen.
 
```blocks
let hand = 0;
input.onGesture(Gesture.Shake, function() {
    hand = randint(1, 3)
    if (hand == 1) {
        basic.showIcon(IconNames.SmallSquare)
    } else if (hand == 2) {
        basic.showIcon(IconNames.Square)
    } else {
         
    }
})
```
 
## {Schritt 12}
 
Jetzt kümmern wir uns um die letzte Bedingung. Wenn in ``||variables:hand||`` weder eine 1 (Stein) noch eine 2 (Papier) ist, muss es sich um 3 (Schere) handeln.
 
Ziehe aus der Kategorie ``||basic:Grundlagen||`` einen weiteren ``||basic:zeige Symbol||``-Block heraus und lege ihn unter ``||logic:ansonsten||`` ab. Klicke in dem ``||basic:zeige Symbol||``-Block auf das Herz-Symbol und wähle stattdessen die Schere aus. 
 
```blocks
let hand = 0;
input.onGesture(Gesture.Shake, function() {
    hand = randint(1, 3)
    if (hand == 1) {
        basic.showIcon(IconNames.SmallSquare)
    } else if (hand == 2) {
        basic.showIcon(IconNames.Square)
    } else {
        basic.showIcon(IconNames.Scissors)
    }
})
```
 
## {Schritt 13}
 
Teste deinen Code! Bewege den Mauszeiger schnell über den micro:bit-Simulator am linken Bildschirmrand, um den simulierten micro:bit zu schütteln. Siehst du die Symbole für Schere, Stein und Papier zufällig erscheinen? ⭐ Großartig! ⭐
 
![Shaking](/static/mb/projects/rock-paper-scissors/rpssim3.gif)
 
## {Schritt 14}
 
Wenn du ein micro:bit besitzt, schließe es an deinen Computer an und klicke auf ``|Download|``. Folge den Anweisungen, um deinen Code auf das micro:bit zu übertragen. Sobald dein Code heruntergeladen ist, kannst du deinen micro:bit an die Batterie anschließen und einen anderen micro:bit oder Menschen zu einem Schere-Stein-Papier-Spiel herausfordern!
 
![micro:bit-Hand](/static/mb/projects/rock-paper-scissors/hand.jpg)
 
## {Schritt 15}
 
Gehe noch einen Schritt weiter und füge 🎵 Musikblöcke 🎵 zu deinem Schere-Stein-Papier-Spiel hinzu, um verschiedene Soundeffekte abzuspielen.
 
```blocks
let hand = 0
input.onGesture(Gesture.Shake, function () {
    hand = randint(1, 3)
    if (hand == 1) {
        basic.showIcon(IconNames.SmallSquare)
        music.play(music.builtinPlayableSoundEffect(soundExpression.giggle), music.PlaybackMode.UntilDone)
    } else if (hand == 2) {
        basic.showIcon(IconNames.Square)
        music.play(music.tonePlayable(262, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
    } else {
        basic.showIcon(IconNames.Scissors)
        music.play(music.createSoundExpression(WaveShape.Square, 1600, 1, 255, 0, 300, SoundExpressionEffect.None, InterpolationCurve.Curve), music.PlaybackMode.UntilDone)
    }
})
```
 
```blockconfig.global
randint(1, 3)
```
 
```template
input.onGesture(Gesture.Shake, function() {})
```

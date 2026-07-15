# ☀️ DTU Solar Automatik – Einspeisung mit Köpfchen

Zwei kleine ioBroker Blocklyskripte, die dafür sorgen, dass mein Winzling von einer PV Anlage trotzdem smart genug ist, um selbst zu entscheiden, wann sich Einspeisen lohnt und wann nicht.

## Worum geht's?

Ich fahre eine Mini-PV-Anlage mit einem HM-600 Mikro Wechselrichter und einer 1,2 kWh LiFePO4-Batterie  nicht gerade Großkraftwerk-Liga. Das Ziel: möglichst wenig Netzbezug, auch bei mieser Verschattung und wechselhaftem Wetter. Bei so kleinen Puffern zählt aber wirklich jedes Watt, deshalb musste die Steuerung der Einspeisung ordentlich austariert werden.

Ergebnis der Challenge: teils nur 0,04 kWh Netzbezug an guten Tagen. 🎉

## Die zwei Skripte

### 1️⃣ Hauptskript – die träge Diva
Schaltet die Einspeisung des HM-600 ab, wenn zu wenig Sonne da ist, und wieder an, sobald genug da ist. Damit das Ding nicht bei jeder vorbeiziehenden Wolke hektisch hin- und herzappelt, gibt's eingebaute Trägheit:
Einschalten: erst nach 5 Minuten stabil guter Werte
Ausschalten: erst nach 6 Minuten stabil schlechter Werte
Erholt sich der Wert währenddessen wieder, wird die Wartezeit sofort abgebrochen kein unnötiges Rumgezappel

### 2️⃣ Batterie voll Skript  der Bodyguard
Ist die Batterie voll, ist das Hauptskript komplett überflüssig dann ist der Strom für die Nacht eh gesichert. Dieses Skript stellt von außen sicher, dass der Wechselrichter läuft, **egal** was das Hauptskript gerade so treibt.

Warum zwei getrennte Skripte statt einem großen? Stellt euch vor, eine Wolke zieht kurz vorbei, die Batterie ist aber voll. Das Hauptskript will trennen, das Batterie voll Skript will einschalten  wären beide im selben Skript, könnte sich das Ding im schlimmsten Fall mitten in der eigenen Ausführung selbst deaktivieren. Quasi der Ast, auf dem man sitzt, wird abgesägt und man weiß nie genau, in welcher Position man dabei gerade hängt. 🪚🌳 Getrennt bleibt jedes Skript für sich robust und vorhersehbar.

## Tech-Stack

- ioBroker (Blockly,    klassische Version)
- OpenDTU (Hoymiles HM-600)
- Victron Ladecontroller
- Telegram für Statusmeldungen

## Installation

1. Blockly-XML in ioBroker importieren
2. OIDs an eure Anlage anpassen (Panel-Wert, OpenDTU-Instanz, Sonoff-Plug falls genutzt)
3. Schwellenwerte und Timer-Delays nach eigenem Gusto einstellen
4. Testen, indem man die Quell-Datenpunkte manuell hin- und herschreibt, bevor man's scharf schaltet

## Lizenz

MIT: macht draus, was ihr wollt. Nutzen, verändern, weiterverbreiten, für die eigene Anlage zurechtbiegen: alles erlaubt, keine Garantie, keine Haftung. Wenn's eurer Anlage hilft, freut mich das umso mehr. ⚡

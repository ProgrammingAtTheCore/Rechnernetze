# Beschreibung
Dient dazu, Dateien oder ganze Verzeichnisse dauerhaft zu löschen (remove). Standardmäßig löscht `rm` nur Dateien und weigert sich, Verzeichnisse zu entfernen.

>[!NOTE]
>Alle Beispiele arbeiten damit das die [Working Directory](<Verzeichnis Struktur.md#Arbeitsverzeichnis>) auf `Users/User/Beispiel_Ordner/`gesetzt ist
# Argumente

| Argument | Funktion                                                                                                                                  |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| **-r**   | **R**ekursiv: Löscht ganze Verzeichnisse inklusive aller Unterordner und der darin enthaltenen Dateien.                                   |
| **-i**   | **I**nteraktiv: Fragt vor dem Löschen jeder einzelnen Datei oder jedes Ordners nach einer Bestätigung. Schützt vor Tippfehlern!           |
| **-v**   | **V**erbose (gesprächig): Zeigt während des Löschvorgangs detailliert an, welche Dateien gerade entfernt werden.                          |
| **-f**   | **F**orce (erzwingen): Löscht Dateien ohne jegliche Nachfrage und unterdrückt Fehlermeldungen (z.B. wenn eine Datei gar nicht existiert). |

Weitere Argumente sowie alle bisher genannten sind in der `rm` man Page einzusehen.

---
## -r

Löscht ganze Verzeichnisse rekursiv. Ohne dieses Argument kann `rm` keine Verzeichnisse löschen und wirft stattdessen einen Fehler.

### Beispiel
Ich habe einen Ordner der in dem Verzeichnis `/Users/User/Beispiel_Ordner/` der wie folgt aussieht:
```Ordner
📁 Beispiel_Ordner
 ├── 📄 hallo.txt
 ├── 📄 text.txt
 ├── 📁 Unterordner
 │    ├── 📄 mathe.txt
 │    └── 📄 deutsch.txt
 └── 📁 .Geheim
      └── 📄 darknet.txt
```

Würden wir einfach nur `rm Unterordner` benutzen würden wie folgenden Fehler bekommen:
```bash
rm: Unterordner: is a directory
```
und es würde abbrechen.

Nutzen wir jedoch `rm -r Unterordner` bekommen wir keinen Output jedoch sieht unser Beispiel_Ordner Verzeichnis jetzt wie folgt aus:
```Ordner
📁 Beispiel_Ordner
 ├── 📄 hallo.txt
 ├── 📄 text.txt
 └── 📁 .Geheim
      └── 📄 darknet.txt
```
Der komplette Ordner samt Inhalt wurde erfolgreich und dauerhaft gelöscht.

---
## -i

Schützt vor dem versehentlichen Löschen von Dateien. Bevor eine Datei endgültig entfernt wird, verlangt das Terminal eine Bestätigung.

### Beispiel
Ich habe einen Ordner der in dem Verzeichnis `/Users/User/Beispiel_Ordner/` der wie folgt aussieht:
```Ordner
📁 Beispiel_Ordner
 ├── 📄 hallo.txt
 ├── 📄 text.txt
 ├── 📁 Unterordner
 │    ├── 📄 mathe.txt
 │    └── 📄 deutsch.txt
 └── 📁 .Geheim
      └── 📄 darknet.txt
```

Wir wollen die Datei `text.txt` löschen, aber sicher sein das dies die richtige ist.

**Input**
```bash
rm -i text.txt
```

**Output**
```bash
remove text.txt? (y/n [n])
```

**Verständnis:** Gibt man nun `y` (yes) ein und drückt Enter, wird die Datei gelöscht. Gibt man `n` (no) ein oder drückt einfach nur Enter (da `[n]` der Standard ist), wird der Löschvorgang abgebrochen und die Datei bleibt erhalten.

>[!NOTE]
>Würde man `-i` bei unserem Beispiel von [-r](#r) benutzen würde nach jeder Datei und am Ende nach dem Verzeichnis einzeln gefragt werden.

---
## -v
Gibt eine Rückmeldung (Output) im Terminal, was genau gelöscht wurde. Dies ist besonders hilfreich, wenn man mit `-r`einen ganzen Baum an Ordnern löscht und sehen möchte, was genau entfernt wird.

>[!NOTE]
>Wird sehr oft mit [-r](#-r) kombiniert (also `rm -rv`)

### Beispiel 
Würden wir das Beispiel aus [-r](#-r) erneut durchführen jedoch dieses mal mit `rm -rv` würden wir anstelle von keinem Output folgenden erhalten:
```bash
removed Unterordner/mathe.txt
removed Unterordner/deutsch.txt
removed Unterordner
```
Wir sehen nun chronologisch, dass zuerst der Inhalt des Ordners und danach der Ordner selbst gelöscht wurde.

---

## -f
Erzwingt das Löschen ohne jegliche Nachfrage. Wenn die Datei nicht existiert, gibt `rm` normalerweise einen Fehler aus – mit `-f` wird dieser Fehler ignoriert und das Terminal bleibt still.

>[!NOTE]
> Die Kombination `rm -rf` (lösche rekursiv und erzwungen) ist einer der berüchtigtsten und gefährlichsten Befehle unter Linux/Unix, da er ohne Vorwarnung ganze Systemteile löschen kann, wenn man ihn im falschen Verzeichnis anwendet!

>[!WARNING]
>Auch jegliche hinweise wie `No such file or directory`würden ebenfalls ignoriert werden.


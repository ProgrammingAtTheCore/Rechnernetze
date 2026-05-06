# Beschreibung
Dient dazu, Dateien oder ganze Verzeichnisse von einem Ort (Quelle) an einen anderen Ort (Ziel) zu kopieren. Die Originaldatei bleibt dabei erhalten.

# Argumente

| Argument  | Funktion                                                                                                                                            |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| [-r](#-r) | **R**ekursiv: Kopiert ganze Verzeichnisse inklusive aller Unterordner und der darin enthaltenen Dateien.                                            |
| [-i](#-i) | **I**nteraktiv: Fragt nach einer Bestätigung, bevor eine bereits existierende Datei im Zielverzeichnis überschrieben wird.                          |
| [-v](#-v) | **V**erbose (gesprächig): Zeigt während des Kopiervorgangs detailliert an, welche Dateien gerade kopiert werden.                                    |
| [-p](#-p) | **P**reserve (bewahren): Behält die ursprünglichen Eigenschaften der Datei (wie Berechtigungen, Besitzer und das ursprüngliche Änderungsdatum) bei. |

Weitere Argumente sowie alle bisher genannten sind in der `cp` man Page einzusehen.

---
## -r

Kopiert ganze Verzeichnisse rekursiv. Ohne dieses Argument weigert sich `cp`, Verzeichnisse zu kopieren, und gibt eine Fehlermeldung aus.

### Beispiel
Ich habe ein Verzeichnis `/Users/User/Beispiel_Ordner/`der wie folgt aussieht:

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

Würde man jetzt versuchen, den Ordner ".Geheim" ohne `-r` in den Ordner "Unterordner" zu kopieren: 

**Input**
```bash
cp /Users/User/Beispiel_Ordner/.Geheim /Users/User/Beispiel_Ordner/Unterordner
```
Order wenn die [Working Directory](<Verzeichnis Struktur.md#Arbeitsverzeichnis>) `/Users/User/Beispiel_Ordner` ist:
```bash
cp .Geheim Unterordner
```

**Output**
```bash
cp: .Geheim is a directory (not copied).
```

Benutzt man jedoch `cp -r` erhalten wir: 

**Input**
```bash
cp -r .Geheim Unterordner
```

**Output** (kein direkter Output im Terminal, aber die Struktur sieht nun wie folgt aus)
```Ordner
📁 Beispiel_Ordner
 ├── 📄 hallo.txt
 ├── 📄 text.txt
 ├── 📁 Unterordner
 │    ├── 📄 mathe.txt
 │    ├── 📄 deutsch.txt
 │    └── 📁 .Geheim 
 │         └── 📄 darknet.txt
 └── 📁 .Geheim
      └── 📄 darknet.txt
```
Der komplette Ordner samt Unterordnern wurde erfolgreich in das Ziel kopiert.

>[!WARNING]
>Um den .Geheim Ordner mit [ls](ls.md) sehen zu können muss das [-l Argument](ls.md#-l) gesetzt sein.

---
## -i
Schützt vor dem versehentlichen Überschreiben von Dateien. Wenn im Zielverzeichnis bereits eine Datei mit demselben Namen existiert, fragt das Terminal nach, ob diese überschrieben werden soll.

>[!NOTE]
>Die [Working Directory](<Verzeichnis Struktur.md#Arbeitsverzeichnis>) sollte auf `/Users/User/Beispiel_Ordner` gesetzt sein.

### Beispiel
Nehmen wir an, wir haben folgenden Ordner unter `/Users/User/Beispiel_Ordner/`:
```Ordner
📁 Beispiel_Ordner
 ├── 📄 hallo.txt
 ├── 📄 text.txt
 ├── 📁 Unterordner
 │    ├── 📄 mathe.txt
 │    ├── 📄 deutsch.txt
 │    └── 📁 .Geheim 
 │         └── 📄 darknet.txt
 └── 📁 .Geheim
      └── 📄 darknet.txt
```

**Input**
```bash
cp -r -i .Geheim Unterordner
```

**Output**
```bash
overwrite Unterordner/.Geheim/darknet.txt? (y/n [n])
```

**Verständnis:** Gibt man nun `y` (yes) ein und drückt Enter, wird die Datei überschrieben. Gibt man `n` (no) ein, wird der Kopiervorgang für diese Datei abgebrochen.

Würde man das -i Argument weglassen würde diese frage nicht kommen und die Datei würde überschrieben werden.

---

## -v
Gibt eine Rückmeldung (Output) im Terminal, was genau kopiert wurde. Dies ist besonders hilfreich, wenn man viele Dateien kopiert und den Fortschritt sehen möchte.

>[!NOTE]
>Die [Working Directory](<Verzeichnis Struktur.md#Arbeitsverzeichnis>) sollte auf `/Users/User/Beispiel_Ordner` gesetzt sein.

>[!NOTE]
>Kann super mit anderen Befehlen wie [-r](#-r) kombiniert werden (z. B. `cp -rv`).

### Beispiel
Ich habe ein Verzeichnis `/Users/User/Beispiel_Ordner/`der wie folgt aussieht:
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

und wir kopieren .Geheim zu dem Unterordner mit `cp -r .Geheim Unterordner` nur dies mal mit:
```bash
cp -r -v .Geheim Unterordner
```

Dann bekommen wir anstelle von keinem Output den folgenden:
```bash
.Geheim -> Unterordner/.Geheim
.Geheim/darknet.txt -> Unterordner/.Geheim/darknet.txt
```
Wir sehen nun Schritt für Schritt, welche Datei von welchem Pfad (`->`) in welchen neuen Pfad kopiert wurde.

---

## -p
Normalerweise erhält eine kopierte Datei das aktuelle Datum und die aktuelle Uhrzeit als Änderungsdatum. Mit `-p` werden die Metadaten (Zeitstempel, Berechtigungen) des Originals übernommen.

>[!NOTE]
>Die [Working Directory](<Verzeichnis Struktur.md#Arbeitsverzeichnis>) sollte auf `/Users/User/Beispiel_Ordner` gesetzt sein.
### Beispiel
Nehmen wir an, wir haben folgenden Ordner unter `/Users/User/Beispiel_Ordner/` also den den wir vorhin bei [-r](#-r) kopiert haben:
```Ordner
📁 Beispiel_Ordner
 ├── 📄 hallo.txt
 ├── 📄 text.txt
 ├── 📁 Unterordner
 │    ├── 📄 mathe.txt
 │    ├── 📄 deutsch.txt
 │    └── 📁 .Geheim 
 │         └── 📄 darknet.txt
 └── 📁 .Geheim
      └── 📄 darknet.txt
```

Dann können wir die Informationen die wir über [ls -l](ls.md#-l) bekommen vergleichen:

**Original** (.Geheim/): `-rw-r--r--  1 paulseidel  staff  8  6 Mai  09:39 darknet.txt`
**Kopiert** (Unterordner/.Geheim): `-rw-r--r--  1 paulseidel  staff  8  6 Mai  13:26 darknet.txt`

Wir können klar sehen das wir zwei verschiedene Zeitstempel haben.
Benutzen wir jetzt jedoch anstelle von `cp -r .Geheim Unterordner` `cp -r -p .Geheim Unterordner` und vergleichen die beiden Dateien wieder:

**Original** (.Geheim/): `-rw-r--r--  1 paulseidel  staff  8  6 Mai  09:39 darknet.txt`
**Kopiert** (Unterordner/.Geheim): `-rw-r--r--  1 paulseidel  staff  8  6 Mai  09:39 darknet.txt`

dann sehen wir das das Datum identisch ist.
# Beschreibung
Dient dazu, Dateien oder ganze Verzeichnisse von einem Ort (Quelle) an einen anderen Ort (Ziel) zu **verschieben** oder sie **umzubenennen**. Das Original am Ursprungsort wird dabei entfernt (es wird quasi "bewegt").

>[!NOTE]
>Alle Beispiele arbeiten damit das die [Working Directory](<Verzeichnis Struktur.md#Arbeitsverzeichnis>) auf `Users/User/Beispiel_Ordner/`gesetzt ist

---
# Basis-Nutzung (Umbenennen vs. Verschieben)
Der `mv` Befehl verhält sich unterschiedlich, je nachdem, was das Ziel ist.

## Beispiel
Ich habe folgendes Verzeichnis `/Users/User/Beispiel_Ordner/`, das wie folgt aussieht:

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

**Fall 1: Umbenennen (Ziel ist ein neuer Dateiname)** Wenn das Ziel kein existierender Ordner ist, wird die Datei umbenannt. 

**Input**
```bash
mv hallo.txt moin.txt
```
_Dan heißt die Datei jetzt `moin.txt`_

```Ordner
📁 Beispiel_Ordner
 ├── 📄 moin.txt
 ├── 📄 text.txt
 ├── 📁 Unterordner
 │    ├── 📄 mathe.txt
 │    └── 📄 deutsch.txt
 └── 📁 .Geheim
      └── 📄 darknet.txt
```

**Fall 2: Verschieben (Ziel ist ein existierender Ordner)** Wenn das Ziel ein Ordner ist, wird die Datei in diesen Ordner verschoben. 

**Input**
```bash
mv moin.txt Unterordner/
```
_Die Datei `moin.txt` liegt nun im Ordner `Unterordner`._

```Ordner
📁 Beispiel_Ordner
 ├── 📄 moin.txt
 ├── 📄 text.txt
 ├── 📁 Unterordner
 │    ├── 📄 mathe.txt
 │    └── 📄 deutsch.txt
 └── 📁 .Geheim
      └── 📄 darknet.txt
```

---
# Argumente

| Argument  | Funktion                                                                                                                     |
| --------- | ---------------------------------------------------------------------------------------------------------------------------- |
| [-i](#-i) | **I**nteraktiv: Fragt nach einer Bestätigung, bevor eine bereits existierende Datei im Zielverzeichnis überschrieben wird.   |
| [-n](#-n) | **N**o Clobber (Kein Überschreiben): Verhindert grundsätzlich, dass bestehende Dateien am Zielort überschrieben werden.      |
| [-v](#-v) | **V**erbose (gesprächig): Zeigt während des Vorgangs detailliert an, welche Dateien gerade verschoben oder umbenannt werden. |
| [-f](#-f) | **F**orce (erzwingen): Überschreibt existierende Dateien am Zielort ohne Nachfrage (ignoriert ein eventuell gesetztes `-i`). |

Weitere Argumente sowie alle bisher genannten sind in der `mv` man Page einzusehen.

---
## -i
Schützt vor dem versehentlichen Überschreiben von Dateien. Wenn am Zielort bereits eine Datei mit demselben Namen existiert, fragt das Terminal nach, ob diese überschrieben werden soll.

### Beispiel
Ich habe folgendes Verzeichnis `/Users/User/Beispiel_Ordner/`, das wie folgt aussieht:

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
und wir wollen die Datei `hallo.txt`in den Ordner `Unterordner` verschieben und in `mathe.txt` umbenennen.

**Input**
```bash
mv -i hallo.txt Unterordner/mathe.txt
```

dann würden wir folgenden **Output** bekommen
```bash
overwrite Unterordner/mathe.txt? (y/n [n])
```

**Verständnis:** Gibt man `y` (yes) ein, wird die alte Datei im `Unterordner` durch die neue ersetzt. Gibt man `n` (no) ein, passiert nichts und die Datei bleibt wo sie ist.

hätten wir `-i`nicht gesetzt würden es einfach überschrieben werden. 

---

## -n
Verhindert das Überschreiben komplett. Es ist die sicherere Alternative zu `-i`, wenn man z.B. viele Dateien verschiebt und auf keinen Fall etwas überschreiben möchte, ohne jedes Mal gefragt zu werden.

### Beispiel
Ich habe folgendes Verzeichnis `/Users/User/Beispiel_Ordner/`, das wie folgt aussieht:

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
und wir wollen die Datei `hallo.txt`in den Ordner `Unterordner` verschieben und in `mathe.txt` umbenennen.

**Input**
```bash
mv -i hallo.txt Unterordner/mathe.txt
```
dann würden man keinen Output bekommen jedoch würde die Datei ebenfalls nicht verschoben oder umbenannt werden.

**Verständnis:** Da die Datei im Ziel bereits existiert, weigert sich `mv` aufgrund von `-n` die Datei zu verschieben. Die `hallo.txt` bleibt unberührt auf dem Schreibtisch.

---

## -v
Gibt eine Rückmeldung (Output) im Terminal, was genau verschoben oder umbenannt wurde. Besonders hilfreich, wenn man Wildcards (wie `*`) benutzt, um viele Dateien gleichzeitig zu verschieben.

### Beispiel
Wenn wir das Beispiel von [-i](#-i) wieder aufgreifen und dies mal anstelle von `mv -i hallo.txt Unterordner/mathe.txt` folgendes schreiben:
```bash
mv -v hallo.txt Unterordner/mathe.txt
```

erhalten wir anstelle von normalerweise keinem **Output** folgenden:
```bash
hallo.txt -> Unterordner/mathe.txt
```
Wir sehen nun genau, dass die Datei vom `.` in das `Unterordner` verschoben und gleichzeitig in `mathe.txt` umbenannt wurde.

---

## -f
Erzwingt das Verschieben und überschreibt Dateien am Zielort gnadenlos ohne Nachfrage.

>[!NOTE]
> Wird oft in automatisierten Skripten verwendet, wo keine Eingabe durch einen Benutzer (wie bei [-i](#-i)) möglich ist. Wenn du `-f` und `-i` gleichzeitig benutzt (z.B. `mv -fi`), gewinnt immer das Argument, das als Letztes steht.


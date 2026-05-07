# Beschreibung
Dient dazu alle Dateien / Verzeichnisse des gegebenen Pfad anzuzeigen.

# Argumente

| Argument  | Funktion                                                                                                                                                  |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [-a](#-a) | Listet sowohl alle normalen Dateien an als auch [versteckte Datei](<versteckte Datei.md>) an.                                                             |
| [-l](#-l) | Listet Dateien in einem "Long Format" heißt es werden weitere Informationen gezeigt wie [Berechtigungen](Dateiberechtigung.md) und Größe (Speicherplatz). |
| [-h](#-h) | Nur in Kombination mit [-l](#-l) zu benutzen zeigt die Datei Größe in Byte (B), Kilobyte (K) etc.                                                         |
| [-r](#-r) | Reverse output kehrt die Reihenfolge um.                                                                                                                  |

Weitere Argumente sowie alle bisher genannten sind in der ls [man Page](man.md) einzusehen. 

---
## -a
Zeigt [versteckte Dateien](<versteckte Datei.md>) an.

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


Würde man jetzt einfach nur ls benutzen:

**Input**
```bash
ls /Users/User/Beispiel_Ordner/
```

**Output**
```bash
hallo.txt  text.txt  Unterordner
```

Benutzt man jedoch ls -a erhalten wir

**Input**
```bash
ls -a /Users/User/Beispiel_Ordner/
```

**Output**
```bash
.  ..  .Geheim  hallo.txt  text.txt  Unterordner
```

Dies mal können wir **.Geheim** sehen ebenfalls können wir die [besonderen Verzeichnisse](<Verzeichnis Struktur.md>) . und .. auch sehen.

---
## -l
Listet Dateien im "Long Format" heißt es werden weitere Informationen gezeigt wie [Berechtigungen](Dateiberechtigung.md) und Datei Größe.

### Detail Beschreibung
Die Informationen sind wie folgt geordnet.
- Typ (- für Datei, d für Verzeichnis (Directory))
- [Berechtigung](Dateiberechtigung.md)
- [Besitzer](Dateiberechtigung.md)
- [Gruppe](Dateiberechtigung.md)
- Dateigröße (angegeben in bytes)
- Änderungsdatum
- Dateiname

### Beispiel

Nehmen wir wieder unseren Beispiel Ordner:

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

Wenn wir hier jetzt wieder:
```bash
ls -l Users/User/Beispiel_Ordner/
```

Dann erhalten wir:
```bash
-rw-r--r--  1 paulseidel  staff     5  6 Mai  09:28 hallo.txt
-rw-r--r--  1 paulseidel  staff  1714  6 Mai  09:46 text.txt
drwxr-xr-x  4 paulseidel  staff   128  6 Mai  10:01 Unterordner
```

Genauer betrachtet bei dem Unterordner:
```bash
drwxr-xr-x  4 paulseidel  staff   128  6 Mai  10:01 Unterordner
||          | |           |       |    |            |
||          | |           |       |    |            └ Dateiname
||          | |           |       |    └───────────── Änderungsdatum
||          | |           |       └────────────────── Dateigröße in Byte
||          | |           └────────────────────────── Group
||          | └────────────────────────────────────── Owner
||          └──────────────────────────────────────── Verlinkungen
|└─────────────────────────────────────────────────── Berechtigungen
└──────────────────────────────────────────────────── Typ
```

Verständnis:
- Typ ist `d` da es sich um ein Verzeichnis handelt
- [Berechtigung](Dateiberechtigung.md) ist `rwxr-xr-x` weil das Owner alle machen kann und die Gruppe und Alle anderen nur Lesen und öffnen könenn
- Verlinkungen ist `4` da das Verzeichnis 4 Unterdateien hat (mathe.txt, deutsch.txt und die [besonderen Verzeichnisse](<Verzeichnis Struktur>))
- Dateigröße bezieht sich hier auf den Inhalt nicht auf die Dateien darin heißt die Größe der Verlinkungen. 

---
## -h 
Zeigt die Byte in typischeren Speichergrößen an wie Kilobyte (K), Megabyte (G) etc.

>[!NOTE]
> -h funktioniert nur in Kombination mit -l und kann entweder so ls -lh oder ls -l -h

### Beispiel

Nehmen wir wieder unseren Beispiel Ordner:

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

Jetzt geben wir jedoch folgendes ein:
```bash
ls -lh Users/User/Beispiel_Ordner/
```

Dann erhalten wir dies mal:
```bash
-rw-r--r--  1 paulseidel  staff    5b  6 Mai  09:28 hallo.txt
-rw-r--r--  1 paulseidel  staff  1.7k  6 Mai  09:46 text.txt
drwxr-xr-x  4 paulseidel  staff  128b  6 Mai  10:01 Unterordner
```

Wie zu sehen ist eigentlich alles gleich wie bei [-l](#-l) außer die Dateigröße unterscheidet sich in der zweiten Zeile dort steht jetzt 1.7k anstelle von 1714 und bei den anderen steht noch ein b dahinter.

---
## -r
Kehrt die Rheinfolge der Auflistung um.

### Beispiel

Wenden wir ls auf unseren Ordner an:
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

Bekommen wir:
```bash
hallo.txt  text.txt  Unterordner
```

Machen wir jedoch ls -r erhalten wir:
```bash  
Unterordner  text.txt  hallo.txt
```

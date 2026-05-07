# Beschreibung
Dient dazu, das eingebaute Handbuch (Manual) eines Befehls anzuzeigen. Wenn du nicht mehr weißt, welche Argumente ein Befehl (wie z.B. [`ls`](ls.md) oder [`rm`](rm.md)) hat oder wie er funktioniert, ist `man` deine erste Anlaufstelle.
# Basis-Nutzung & Navigation

Wenn du `man` benutzt, öffnet sich eine neue Ansicht im Terminal (oft über ein Programm namens `less`). Du musst wissen, wie du dich darin bewegst.

**Input**
```bash
man ls
```
_(Öffnet das Handbuch für den Befehl ls)._

**Bedienung innerhalb der man Page:**
- **Pfeiltasten (Hoch/Runter):** Zeilenweise scrollen.
- **Leertaste:** Eine ganze Seite nach unten blättern.
- **`b` (back):** Eine ganze Seite nach oben blättern.
- **`/Suchbegriff`:** Sucht innerhalb des Handbuchs nach einem Wort (z.B. `/size`). Mit `n` (next) springst du zum nächsten Treffer.
- **`q` (quit):** Beendet das Handbuch und bringt dich zum normalen Terminal-Fenster zurück.

---
# Argumente

|Argument|Funktion|
|---|---|
|**-f**|**F**ast/Format (Kurzbeschreibung): Zeigt nur eine einzeilige, ganz kurze Beschreibung an, was ein Befehl macht, ohne das riesige Handbuch zu öffnen. (Ist identisch mit dem Befehl `whatis`).|
|**-k**|**K**eyword (Schlüsselwort): Sucht in allen Handbüchern nach einem bestimmten Stichwort. Perfekt, wenn du weißt, _was_ du tun willst, aber den Namen des Befehls vergessen hast. (Ist identisch mit dem Befehl `apropos`).|

Weitere Argumente sowie alle bisher genannten sind (ironischerweise) in der `man man` Page einzusehen.

---
## -f
Gibt dir eine extrem kurze Zusammenfassung eines Befehls. Sehr praktisch, wenn du bei einer Klausuraufgabe kurz überprüfen willst, ob ein Befehl wirklich der richtige für den Job ist.

### Beispiel
Wir haben den Befehl `mkdir` gesehen, sind uns aber nicht mehr 100% sicher, wofür er steht.

**Input**
```bash
man -f mkdir
```

**Output**
```bash
mkdir (1) - make directories
```
**Verständnis:** Das Terminal spuckt uns nur eine einzige Zeile aus, die den Befehl kurz und knackig erklärt. Die `(1)` in Klammern gibt dabei die "Sektion" des Handbuchs an (Sektion 1 steht für normale Benutzerbefehle).

---
### -k
Die Rettung, wenn man den Namen eines Befehls vergessen hat! Durchsucht die Kurzbeschreibungen aller Handbücher nach einem bestimmten englischen Stichwort.

### Beispiel
Wir wollen einen Ordner kopieren, haben aber total vergessen, dass der Befehl dafür `cp` heißt. Wir wissen nur, dass das englische Wort "copy" lautet.

**Input**
```bash
man -k copy
```

**Output** _(Auszug aus einer meist längeren Liste)_
```bash
cp (1) - copy files and directories
dd (1) - convert and copy a file
mcopy (1) - copy MSDOS files to/from Unix
...
```
**Verständnis:** Das Terminal listet uns alle Befehle auf, die etwas mit "copy" zu tun haben. Ganz oben sehen wir direkt unseren gesuchten Befehl `cp` samt kurzer Erklärung.

---

# Extra-Tipp für dein Cheatsheet: Sektionen
Manchmal gibt es den gleichen Namen für einen Terminal-Befehl und eine Programmier-Funktion (z.B. `printf` im Terminal vs. `printf` in C). `man` ist in Sektionen (1 bis 8) unterteilt:
- **1:** Normale Befehle (z.B. `ls`, `rm`)
- **3:** C-Bibliotheksfunktionen (z.B. für die Programmierung)
- **5:** Dateiformate (z.B. `/etc/passwd`)
- **8:** Systemadministration (z.B. `fdisk`)

Wenn du gezielt die Doku für die C-Funktion `printf` suchst und nicht den Terminal-Befehl, schreibst du die Sektion einfach dazwischen: `man 3 printf`
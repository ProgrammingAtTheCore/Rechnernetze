# Beschreibung
Dient dazu, Textzeilen oder den Inhalt von Variablen auf dem Bildschirm (Terminal) auszugeben. "echot" (wiederholt) quasi exakt das, was man ihm als Argument übergibt.

# Argumente

| Argument | Funktion                                                                                                                                                   |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **-n**   | **N**ewline (Zeilenumbruch) unterdrücken: Verhindert, dass `echo` nach der Textausgabe automatisch in eine neue, leere Zeile springt.                      |
| **-e**   | **E**scapes interpretieren: Aktiviert die Übersetzung von speziellen Backslash-Steuerzeichen (wie `\n` für eine neue Zeile oder `\t` für einen Tabulator). |

Weitere Argumente (wie `-E`, was das Standardverhalten ist) sind in der `echo` man Page einzusehen.

---
## -n
Verhindert den automatischen Zeilenumbruch am Ende der Ausgabe. Das ist besonders in selbstgeschriebenen Skripten wichtig, wenn man möchte, dass eine Eingabe des Benutzers direkt hinter der gestellten Frage in der gleichen Zeile passiert.

### Beispiel
Wir benutzen `echo` einmal ohne und einmal mit `-n`. Um den Unterschied zu sehen, achten wir darauf, wo unser Terminal-Eingabeprompt (das `user@macbook %`) danach wieder auftaucht.

**Input (ohne -n)**
```bash
echo "Hallo ich teste die funktion"
```

**Output**
```bash
Hallo ich teste die funktion
user@macbook % █
```
_(Der Text wird ausgegeben und das Terminal springt in die nächste Zeile, um auf neue Befehle zu warten)._

**Input (mit -n)**
```bash
echo -n "Hallo ich teste die funktion"
```

**Output**
```bash
Hallo ich teste die funktion user@macbook % █
```
**Verständnis:** Das Terminal ist _nicht_ in die nächste Zeile gesprungen. Der Prompt für den nächsten Befehl "klebt" direkt an der Ausgabe unseres Textes.

---
## -e
Damit `echo` besondere Formatierungen (wie Tabstopps oder erzwungene Zeilenumbrüche) innerhalb eines Textes versteht, muss man `-e` benutzen.

**Wichtige Steuerzeichen:**
- `\n` = **n**ewline (erzwingt einen Zeilenumbruch)
- `\t` = **t**ab (fügt einen Tabulator/großen Abstand ein)

### Beispiel
Wir wollen eine kleine, formatierte Tabelle ausgeben, ohne mehrmals `echo` tippen zu müssen.

**Input**
```bash
echo -e "Name\tAlter\tFach\nPaul\t21\tRechnernetze"
```

**Output**
```bash
Name    Alter   Fach
Paul    21      Rechnernetze
```
**Verständnis:** Dank `-e` hat `echo` das `\t` als Tabulator (große Lücke) und das `\n` als "Springe in die nächste Zeile" übersetzt. Ohne das `-e` hätte das Terminal einfach stur `Name\tAlter...` als unformatierten Text ausgegeben.

---

## Extra-Tipp für dein Cheatsheet: Die Umleitung (`>`)
Einer der häufigsten Anwendungsfälle von `echo` in Rechnernetze ist das direkte Schreiben in eine Datei (ohne einen Texteditor wie `nano` oder `vim` zu öffnen). Das macht man mit dem [Umleitungs-Zeichen `>`](<Stream Operatoren.md#write To>).
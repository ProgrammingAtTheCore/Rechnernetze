# Beschreibung
Dient dazu, neue, leere Verzeichnisse (Ordner) zu erstellen. Der Name steht kurz für "make directory".

>[!NOTE]
>Alle Beispiele arbeiten damit das die [Working Directory](<Verzeichnis Struktur.md#Arbeitsverzeichnis>) auf `Users/User/Beispiel_Ordner/`gesetzt ist

# Basis-Nutzung (Verzeichnis erstellen)
Wir haben folgendes Verzeichnis `User/User/Beispiel_Ordner`, das wie folgt aussieht:
```bash
📁 Beispiel_Ordner
 ├── 📄 hallo.txt
 ├── 📄 text.txt
 └── 📁 .Geheim
      └── 📄 darknet.txt

```

Jetzt wollen wir einen weiteren Ordner erstellen der `Unterordner` heißt also geben wir folgendes ein:
```bash
mkdir Unterordner
```

Somit sieht unsere neue Ordner Struktur wie folgt aus:
```bash
📁 Beispiel_Ordner
 ├── 📄 hallo.txt
 ├── 📄 text.txt
 ├── 📁 Unterordner
 └── 📁 .Geheim
      └── 📄 darknet.txt
```

---
# Argumente

|Argument|Funktion|
|---|---|
|**-p**|**P**arents (Eltern-Verzeichnisse): Erstellt bei Bedarf die übergeordneten Verzeichnisse auf dem Pfad direkt mit. Verhindert zudem eine Fehlermeldung, falls das Verzeichnis bereits existiert.|
|**-v**|**V**erbose (gesprächig): Gibt für jedes erfolgreich erstellte Verzeichnis eine Bestätigung im Terminal aus.|
|**-m**|**M**ode (Modus/Rechte): Erlaubt es, direkt bei der Erstellung die Zugriffsrechte (Permissions) festzulegen (funktioniert ähnlich wie der `chmod` Befehl).|

Weitere Argumente sowie alle bisher genannten sind in der `mkdir` man Page einzusehen.

---
## -p
Erstellt fehlende Zwischenverzeichnisse automatisch. Ohne dieses Argument weigert sich `mkdir`, einen Ordner in einem Pfad zu erstellen, dessen übergeordnete Ordner noch gar nicht existieren.

### Beispiel
Wir haben das folgende Verzeichnis: 
```bash
📁 Beispiel_Ordner
 ├── 📄 hallo.txt
 ├── 📄 text.txt
 ├── 📁 Unterordner
 └── 📁 .Geheim
      └── 📄 darknet.txt
```

Jetzt wollen wir jedoch noch den Ordner `Uni` erstellen und in diesem Ordner einen weiteren der `Rechnernetze` heißt.

Dann müssen wir `mkdir -p` nutzen den anderenfalls würden wir folgenden Fehler bekommen:
```bash
mkdir: Uni: No such file or directory
```
doch wenn wir:
```bash
mkdir -p Uni/Rechnernetze
```
machen erhalten wie folgende Ordnerstruktur:
```bash
📁 Beispiel_Ordner
 ├── 📄 hallo.txt
 ├── 📄 text.txt
 ├── 📁 Uni
 │    └── 📁 Rechnernetze 
 ├── 📁 Unterordner
 └── 📁 .Geheim
      └── 📄 darknet.txt
```
Das Terminal hat still und heimlich die fehlenden Ordner `Uni` und `Rechnernetze` gleich mit erstellt, damit der Ordner `Übungen`am Ende seinen Platz findet.

---
## -v
Gibt eine Rückmeldung (Output) im Terminal, sobald ein Ordner erfolgreich erstellt wurde.

>[!NOTE]
> Besonders nützlich in Kombination mit `-p`, um genau zu sehen, welche Zwischenordner das System für dich generiert hat.

### Beispiel
Würden wir das Beispiel aus [-p](-p) wiederholen jedoch anstelle von `mkdir -p Uni/Rechnernetze` `mkdir -p -v Uni/Rechnernetze` machen.
Erhalten wir folgenden **Output**
```bash
mkdir: created directory Uni
mkdir: created directory Uni/Rechnernetze
```
Wir sehen nun Schritt für Schritt, wie das System den Pfad von oben nach unten aufbaut.

---
## -m
Normalerweise erhalten neu erstellte Verzeichnisse [Standardberechtigungen](Dateiberechtigung.md) (meist `drwxr-xr-x`, also Lesen/Ausführen für alle, Schreiben nur für den Besitzer). Mit `-m` kannst du diese Rechte bei der Erstellung sofort einschränken oder erweitern.

### Beispiel
Wenn wir bei dem Beispiel von [-p](#-p) auf den Uni Ordner [`ls -l`](ls.md#-l) machen würden:
```bash
ls -l Uni
```
erhalten wir folgende Information
```bash
drwxr-xr-x  2 paulseidel  staff  64  6 Mai  14:51 Rechnernetze
```

>[!NOTE]
>Um folgendes verstehen zu können Empfehle ich vorher [Dateiberechtigung mit Zahlen](Dateiberechtigung.md#Zahlencode) zu lesen. 

Wenn wir wollen das nur der [Owner](Dateiberechtigung.md#Typen) mit dem Verzeichnis was machen kann können wir folgendes machen:
```bash
mkdir -p -m 700 Uni/Rechnernetze
```
machen wir jetzt `ls -l Uni` erhalten wir:
```bash
drwxr------  2 paulseidel  staff  64  6 Mai  15:02 Rechnernetze
```
**Verständnis:** Der Ordner wurde erstellt, aber wie bei den Rechten ganz links zu sehen ist (`drwx------`), hat die Gruppe und "Alle anderen" keinerlei Rechte (`---`). Sie können den Ordner weder öffnen, noch seinen Inhalt lesen.
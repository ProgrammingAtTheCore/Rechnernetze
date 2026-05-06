# Beschreibung
 Dient dazu, das aktuelle [Arbeitsverzeichnis (Current Working Directory)](<Verzeichnis Struktur.md#Arbeitsverzeichnis>) zu wechseln, um durch das Dateisystem zu navigieren.

>[!NOTE]
>Um die volle funktion von cd zu verstehen empfehle ich [Verzeichnis Struktur](<Verzeichnis Struktur>) zu lesen.

# Beispiel
Ich habe einen Ordner der in dem Verzeichnis /Users/User/Beispiel_Ordner/ der wie folgt aussieht:

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

Unser [Working Directory](<Verzeichnis Struktur.md#Arbeitsverzeichnis>) Befindet sich auf ~ (Beziehungsweise /Users/User) um jetzt in unseren Ordner zu gehen haben wir 2 Möglichkeiten:

Variante 1:
```bash
cd Users/User/Beispiel_Ordner
```

Variante 2:
```bash
cd Beispiel_Ordner
```

>[!NOTE]
>Variante 2 können wir nur deswegen machen da unser [Working Directory](<Verzeichnis Struktur.md#Arbeitsverzeichnis>) in dem Übergeordneten Verzeichnis ist.

Variante 2 ist Äquivalent zu:
```bash
cd ./Beispiele_Ordner
```

Wenn kein direkter Pfad gegeben ist wird bei den meisten Befehlen der . automatisch interpretiert. ([ Weiteres hier](Übersicht.md#Grundwissen))

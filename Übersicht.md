# Tastenkombinationen
| Tastenkombination | Funktion                                                                 |
| ----------------- | ------------------------------------------------------------------------ |
| tab               | Autovollständigung                                                       |
| CTRL + c          | bricht aktuelle Programm ab (funktioniert nicht immer)                   |
| CTRL + s          | stoppt die Konsole                                                       |
| CTRL + q          | hebt den stopp auf                                                       |
| ⬆️                | zeigt die zuletzt benutzen befehle an                                    |
| CTRL + r          | erlaubt das suchen letzter Befehle CTRL + r nochmal für nächsten Treffer |
| CTRL + k          | Löscht alles hinter der aktuellen Cursor Position                        |
| CTRL + ⬅️ / ➡️    | Lässt den Cursor wortweise springen                                      |

# Grundwissen
## [Verzeichnisstruktur](<Verzeichnis Struktur>)
Systeme die auf Linus basiert sind bestehen nur aus Dateien und das System startet mit `/`
Es gibt zwei arten von Verzeichnissen:
- Absolute Verzeichnisse (starten immer mit `/`)
- Relative Verzeichnisse (haben kein `/` am Anfang und beziehen sich auf [Working Directory](<Verzeichnis Struktur.md#Arbeitsverzeichnis>))
Weitere informationen [hier](<Verzeichnis Struktur>).

# Befehle
## Grundbefehle

| Befehle                                   | Beschreibung                                                       |
| ----------------------------------------- | ------------------------------------------------------------------ |
| history                                   | Zeigt alle zuletzt benutzen Befehle an. (Maximal 1000)             |
| clear                                     | Leert den Inhalt des Bildschirms                                   |
| [echo](echo.md)                           | Gibt den Inhalt dahinter in der Konsole aus.                       |
| [man (**man**uel)](man.md)                | Gibt die Developer Beschreibung für den Befehl der dahinter steht. |
| pwd (**p**rint **w**orking **d**irectory) | Gibt den vollen Dateipfad an von dem wo man gerade ist.            |
| [ls (**l**i**s**t)](ls.md)                | Zeigt alle Dateien an die in dem gegeben Pfad liegen.              |
| [cd (**c**hange **d**irectory)](cd.md)    | Wechselt das Arbeitsverzeichnis zu dem gegeben Pfad.               |
| [cp (**c**o**p**y)](cp.md)                | Kopiert den ersten pfad in den zweiten.                            |
| [mv (**m**ove)](mv.md)                    | Verschiebt den ersten pfad / datei zu dem zweiten.                 |
| [rm (**r**e**m**ove)](rm.md)              | Löscht die gegebene Datei.                                         |
| [mkdir (Make directory)](mkdir.md)        | Erstellt ein Verzeichnis.                                          |

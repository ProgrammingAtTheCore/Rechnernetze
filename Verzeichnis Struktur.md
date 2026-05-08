# Navigation und Verzeichnisstruktur
Um im Terminal durch das Dateisystem zu navigieren, wird primär der Befehl [`cd` (Change Directory)](cd.md) genutzt, während [`ls` (List)](ls.md) die Inhalte eines Verzeichnisses anzeigt.

Für die Navigation ist es essenziell zu verstehen, wo man sich befindet und wie man das Ziel angibt. Dabei unterscheidet man grundsätzlich zwischen [**absoluten** und **relativen** Pfaden](<#Absoluter vs. Relativer Pfad>).

## Das Arbeitsverzeichnis (Current Working Directory)
Das Arbeitsverzeichnis ist der Ort im Dateisystem, an dem sich das Terminal (die Shell) im momentanen Augenblick befindet.

- **Wichtig:** Alle Befehle (wie `ls`, `cd`, `rm`), denen man keinen absoluten Pfad übergibt, beziehen sich standardmäßig immer auf dieses aktuelle Verzeichnis. 
- **Überprüfung:** Mit dem Befehl `pwd` (Print Working Directory) kann man sich jederzeit den absoluten Pfad des aktuellen Arbeitsverzeichnisses anzeigen lassen.
## Absoluter vs. Relativer Pfad

| Eigenschaft    | Absoluter Pfad                                                                                | Relativer Pfad                                                                                |
| -------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| **Startpunkt** | Beginnt **immer** mit dem Root-Verzeichnis `/`.                                               | Bezieht sich immer auf das **aktuelle Arbeitsverzeichnis**.                                   |
| **Vorteil**    | Funktioniert garantiert immer, völlig unabhängig davon, wo sich das Terminal gerade befindet. | Ist kürzer und schneller zu tippen, wenn man sich bereits in der Nähe der Zieldatei befindet. |
| **Beispiel**   | `cd /Users/User/Uni/Rechnernetze`                                                             | `cd Uni/Rechnernetze` _(funktioniert nur, wenn man sich gerade in `/Users/User/` befindet)_   |

---
# Versteckte Dateien und Verzeichnisse

Versteckte Dateien und Ordner sind daran zu erkennen, dass ihr Name mit einem Punkt beginnt (z.B. `.config` oder `.bashrc`).

- **Zweck:** Sie werden meist vom Betriebssystem oder von Programmen genutzt, um Konfigurationen und Einstellungen im Hintergrund zu speichern. Das hält die normalen Verzeichnisse für den Benutzer übersichtlich und aufgeräumt.
- **Sichtbarkeit:** Ein normales [`ls`](ls.md) blendet diese Dateien aus. Um sie sichtbar zu machen, muss man [`ls -a` (all)](ls.md#-a) verwenden.

---

### Besondere Verzeichnisse (`.` und `..`)

In jedem Verzeichnis (auch in leeren!) existieren standardmäßig zwei spezielle, unsichtbare "Verzeichnisse", die zur relativen Navigation dienen:

**Der einfache Punkt (`.`) = Das aktuelle Verzeichnis** Er verweist exakt auf den Ordner, in dem man sich gerade befindet.
- **Praxis-Beispiel:** Man nutzt ihn oft als Zielort beim Kopieren. Wenn man eine Datei von woanders genau in das _aktuelle_ Verzeichnis kopieren möchte, spart man sich das Tippen des langen Pfades:
```bash
cp /etc/netzwerk_config.txt .
```
_(Kopiert die Datei aus /etc exakt dorthin, wo das Terminal gerade ist)._
 
Ein weiterer Nutzen ist das Ausführen von Skripten im aktuellen Ordner (z.B. `./mein_skript.sh`).

**Der doppelte Punkt (`..`) = Das übergeordnete Verzeichnis** Er verweist immer auf die Ebene _direkt über_ dem aktuellen Verzeichnis (den Eltern-Ordner).

- **Praxis-Beispiel (Navigation):** Um schnell eine Ebene im Dateibaum nach oben/zurück zu springen. Angenommen, `pwd` sagt dir, du bist in `/Users/User/Downloads`: **Input:** `cd ..` **Output:** _(Keiner, aber wenn du jetzt wieder `pwd` eingibst, bist du in `/Users/User/`)_. 
- **Praxis-Beispiel (Kombination):** Man kann damit auch "über Bande" navigieren. Wenn du in `Downloads` bist, aber in `Dokumente` möchtest: `cd ../Dokumente` _(Gehe eins hoch, und von dort in Dokumente)_.

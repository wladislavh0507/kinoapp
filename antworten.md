# Teil A

## A1: Auf welchem Branch bist du, und welche Branches gibt es noch?

Ich bin auf dem Branch `main`. Zusätzlich gibt es die Branches `feature/neuer-titel` und `feature/snacks`.

## A2: Welche Dateien meldet `git status` als „untracked“? Was bedeutet das?

Die Datei `kasse.log` und der Ordner `test/` werden als `untracked` gemeldet.

`Untracked` bedeutet, dass Git diese Dateien bzw. Ordner noch nicht verfolgt. Sie wurden also noch nicht mit `git add` zur Staging Area hinzugefügt.

## A3: `ls -a` zeigt einen Ordner `.git`. Was steckt darin, und was passiert, wenn man ihn löscht?

Im Ordner `.git` befinden sich die internen Daten des Git-Repositories, zum Beispiel die Commit-Historie, Branches, Konfigurationen und weitere Git-Metadaten.

Wenn man den `.git`-Ordner löscht, bleiben die eigentlichen Projektdateien erhalten, aber der Ordner ist danach kein Git-Repository mehr und die lokale Git-Historie geht verloren.

### `git log --oneline --graph --all` Ergebnis für Teil A

```text
* 1281d8f (feature/neuer-titel) Neuer Titel: Filmpalast
| * 5bbfa5a (feature/snacks) Snackkarte hinzugefügt
| * ea6a719 (HEAD -> main) Titel und Öffnungszeiten ergänzt
|/
* 379d121 Werbebanner eingefügt
* b26bfdb Seniorenpreis ergänzt
* 294cecc Kinderpreis eingeführt
* 5050041 Filmliste ergänzt
* d4f3928 Initialer Import: Grundgerüst der KinoApp
```

---

# Teil B

## B1: Woran erkennst du in der Ausgabe und im Log, dass es ein Fast-Forward war?

Ausgabe des Merge-Befehls:

```text
$ git merge --ff-only feature/snacks
Updating ea6a719..5bbfa5a
Fast-forward
 snacks.md | 6 ++++++
 1 file changed, 6 insertions(+)
 create mode 100644 snacks.md
```

Git zeigt direkt die Meldung `Fast-forward` an.

Auch im Log ist es erkennbar:

```text
$ git log --oneline --graph --all
* 1281d8f (feature/neuer-titel) Neuer Titel: Filmpalast
| * 5bbfa5a (HEAD -> main, feature/snacks) Snackkarte hinzugefügt
| * ea6a719 Titel und Öffnungszeiten ergänzt
|/
* 379d121 Werbebanner eingefügt
* b26bfdb Seniorenpreis ergänzt
* 294cecc Kinderpreis eingeführt
* 5050041 Filmliste ergänzt
* d4f3928 Initialer Import: Grundgerüst der KinoApp
```

Im Log sieht man außerdem, dass `main` und `feature/snacks` jetzt auf denselben Commit `5bbfa5a` zeigen. Es wurde kein zusätzlicher Merge-Commit erstellt.

## B2: Warum war hier ein Fast-Forward möglich?

Ein Fast-Forward war möglich, weil `main` seit der Weiterentwicklung von `feature/snacks` keine eigenen neuen Commits erhalten hatte. Git konnte den Zeiger von `main` deshalb einfach auf den neuesten Commit von `feature/snacks` verschieben.

### `git log --oneline --graph --all` Ergebnis für Teil B

```text
* 1281d8f (feature/neuer-titel) Neuer Titel: Filmpalast
| * 5bbfa5a (HEAD -> main, feature/snacks) Snackkarte hinzugefügt
| * ea6a719 Titel und Öffnungszeiten ergänzt
|/
* 379d121 Werbebanner eingefügt
* b26bfdb Seniorenpreis ergänzt
* 294cecc Kinderpreis eingeführt
* 5050041 Filmliste ergänzt
* d4f3928 Initialer Import: Grundgerüst der KinoApp
```

---

# Teil C

## C1: Beschreibe in einem Satz, wo der Fehler steckt und was er bewirkt.

Der Fehler lag beim Vergleichsoperator `>`, wodurch geprüft wurde, ob das Alter größer als 14 ist und dann fälschlicherweise der Kinderpreis zurückgegeben wurde. Der Operator wurde deshalb zu `<` geändert.

## C2: Nach `git add` zeigt `git diff` nichts mehr an, `git diff --staged` aber schon. Warum?

Nach `git add` befindet sich die Änderung in der Staging Area. `git diff` zeigt nur Änderungen an, die noch nicht gestaged wurden. Mit `git diff --staged` werden dagegen die Änderungen angezeigt, die bereits zur Staging Area hinzugefügt wurden und beim nächsten Commit übernommen werden.

### `git log --oneline --graph --all` Ergebnis für Teil C

```text
$ git log --oneline --graph --all
* 594bcb5 (HEAD -> main) Bugfix: Kinderpreis nur für Kinder unter 14
* 5bbfa5a (feature/snacks) Snackkarte hinzugefügt
* ea6a719 Titel und Öffnungszeiten ergänzt
| * 1281d8f (feature/neuer-titel) Neuer Titel: Filmpalast
|/
* 379d121 Werbebanner eingefügt
* b26bfdb Seniorenpreis ergänzt
* 294cecc Kinderpreis eingeführt
* 5050041 Filmliste ergänzt
* d4f3928 Initialer Import: Grundgerüst der KinoApp
```

---

# Teil D

## D1: Ist der Commit „Werbebanner eingefügt“ nach dem Revert noch in der Historie? Was ist dazugekommen?

Ja, der Commit `Werbebanner eingefügt` ist weiterhin in der Historie vorhanden. Zusätzlich wurde ein neuer Commit mit `Revert "Werbebanner eingefügt"` erstellt, der die Änderungen des ursprünglichen Commits rückgängig macht.

## D2: Warum nimmt man in einem Team-Repo `git revert`, statt Commits einfach zu löschen?

In einem Team-Repository verwendet man `git revert`, damit die gemeinsame Git-Historie erhalten und nachvollziehbar bleibt. Die Änderung wird durch einen neuen Commit rückgängig gemacht, ohne bereits veröffentlichte Commits aus der Historie zu entfernen.

### `git log --oneline --graph --all` Ergebnis für Teil D

```text
$ git log --oneline --graph --all
* 6aaa04d (HEAD -> main) Revert "Werbebanner eingefügt"
* 594bcb5 Bugfix: Kinderpreis nur für Kinder unter 14
* 5bbfa5a (feature/snacks) Snackkarte hinzugefügt
* ea6a719 Titel und Öffnungszeiten ergänzt
| * 1281d8f (feature/neuer-titel) Neuer Titel: Filmpalast
|/
* 379d121 Werbebanner eingefügt
* b26bfdb Seniorenpreis ergänzt
* 294cecc Kinderpreis eingeführt
* 5050041 Filmliste ergänzt
* d4f3928 Initialer Import: Grundgerüst der KinoApp
```

---

# Teil E

## E1: Was ist der Unterschied zwischen `>` und `>>` beim `echo`-Befehl?

`>` überschreibt den bisherigen Inhalt einer Datei.

`>>` hängt den neuen Inhalt an den bereits bestehenden Inhalt der Datei an.

## E2: Was zeigt `git status` vor und nach dem Anlegen der `.gitignore`?

Vor dem Anlegen der `.gitignore` wurden der Ordner `test/` und die Datei `kasse.log` als `untracked` angezeigt.

Nach dem Anlegen der `.gitignore` werden `test/` und `kasse.log` ignoriert und deshalb nicht mehr als `untracked` angezeigt. Danach wurde nur noch `antworten.md` als `untracked` angezeigt.

### `git log --oneline --graph --all` Ergebnis für Teil E

```text
$ git log --oneline --graph --all
* 5a46191 (HEAD -> main) gitignore: test/ und Logdateien ignorieren
* 6aaa04d Revert "Werbebanner eingefügt"
* 594bcb5 Bugfix: Kinderpreis nur für Kinder unter 14
* 5bbfa5a (feature/snacks) Snackkarte hinzugefügt
* ea6a719 Titel und Öffnungszeiten ergänzt
| * 1281d8f (feature/neuer-titel) Neuer Titel: Filmpalast
|/
* 379d121 Werbebanner eingefügt
* b26bfdb Seniorenpreis ergänzt
* 294cecc Kinderpreis eingeführt
* 5050041 Filmliste ergänzt
* d4f3928 Initialer Import: Grundgerüst der KinoApp
```

---

# Teil F

## F1: Warum ist `git merge --ff-only` hier gescheitert?

Der Fast-Forward ist gescheitert, weil sich `main` und `feature/neuer-titel` unabhängig voneinander weiterentwickelt haben und beide Branches eigene Commits besitzen. Git konnte den Zeiger von `main` deshalb nicht einfach auf `feature/neuer-titel` verschieben.

## F2: Was bedeuten `HEAD` und `feature/neuer-titel` in den Konfliktmarkern?

Bei einem Merge-Konflikt können beispielsweise folgende Konfliktmarker angezeigt werden:

```text
<<<<<<< HEAD
Inhalt aus main
=======
Inhalt aus feature/neuer-titel
>>>>>>> feature/neuer-titel
```

Dabei bedeutet:

- `HEAD` = die Version des aktuell ausgecheckten Branches. In diesem Fall ist das `main`.
- `feature/neuer-titel` = die Version aus dem Branch, der in `main` gemergt werden soll.
- `=======` = trennt die beiden unterschiedlichen Versionen voneinander.

## F3: Warum konnte Git den Konflikt nicht allein lösen?

Git konnte den Konflikt nicht automatisch lösen, weil beide Branches dieselbe Stelle in der Datei unterschiedlich verändert hatten. Git kann nicht selbst entscheiden, welche der beiden Änderungen fachlich richtig ist.

### `git log --oneline --graph --all` Ergebnis für Teil F

```text
$ git log --oneline --graph --all
*   1880e76 (HEAD -> main) Merge feature/neuer-titel: Titelkonflikt gelöst
|\
| * 1281d8f Neuer Titel: Filmpalast
* | eca916a Antworten
* | 5a46191 gitignore: test/ und Logdateien ignorieren
* | 6aaa04d Revert "Werbebanner eingefügt"
* | 594bcb5 Bugfix: Kinderpreis nur für Kinder unter 14
* | 5bbfa5a Snackkarte hinzugefügt
* | ea6a719 Titel und Öffnungszeiten ergänzt
|/
* 379d121 Werbebanner eingefügt
* b26bfdb Seniorenpreis ergänzt
* 294cecc Kinderpreis eingeführt
* 5050041 Filmliste ergänzt
* d4f3928 Initialer Import: Grundgerüst der KinoApp
```

---

# Teil G

## G1: Beim ersten `git status` steht „Your branch is up to date with 'origin/main'“, obwohl es auf GitHub eine neue Änderung gibt. Warum?

Der lokale Stand von `origin/main` war noch nicht aktualisiert. Git kennt Änderungen auf dem Remote-Repository erst, nachdem die neuen Informationen zum Beispiel mit `git fetch` oder `git pull` abgerufen wurden.

Deshalb konnte `git status` zunächst noch anzeigen, dass der lokale Branch auf dem gleichen Stand wie `origin/main` ist.

## G2: Was hat `git fetch` gemacht, was hat `git pull` zusätzlich gemacht?

`git fetch` lädt neue Commits und Informationen vom Remote-Repository herunter und aktualisiert beispielsweise `origin/main`. Der eigene lokale `main`-Branch wird dabei noch nicht verändert.

`git pull` lädt die Änderungen ebenfalls herunter und integriert sie anschließend zusätzlich in den aktuell ausgecheckten lokalen Branch.

Vereinfacht gilt:

```text
git pull = git fetch + Integration der Änderungen
```

## G3: Was bedeutet das `-u` bei `git push -u origin ...`?

Das `-u` steht für `--set-upstream`. Damit wird der lokale Branch mit dem entsprechenden Remote-Branch verknüpft.

Zum Beispiel:

```bash
git push -u origin feature/kontakt
```

Danach weiß Git, zu welchem Remote-Branch der lokale Branch gehört. Dadurch reichen später normalerweise Befehle wie:

```bash
git push
```

oder:

```bash
git pull
```

## G4: Warum wurde `kontakt.md` erst nach `git pull` auf deinem lokalen `main` sichtbar?

`kontakt.md` war zunächst nur im Remote-Repository vorhanden. Der lokale `main` hatte diesen neuen Stand noch nicht übernommen.

Erst durch `git pull` wurden die neuen Änderungen heruntergeladen und in den lokalen `main` integriert. Dadurch wurde `kontakt.md` auch lokal sichtbar.

### `git log --oneline --graph --all` Ergebnis für Teil G

```text
$ git log --oneline --graph --all
*   b46f0f2 (HEAD -> main, origin/main, origin/HEAD) Merge pull request #1 from wladislavh0507/feature/kontakt
|\
| * 9c6b906 (origin/feature/kontakt) Kontaktseite hinzugefügt
|/
* 7465799 Update README.md
* 41f5818 Update README.md
*   1880e76 Merge feature/neuer-titel: Titelkonflikt gelöst
|\
| * 1281d8f Neuer Titel: Filmpalast
* | eca916a Antworten
* | 5a46191 gitignore: test/ und Logdateien ignorieren
* | 6aaa04d Revert "Werbebanner eingefügt"
* | 594bcb5 Bugfix: Kinderpreis nur für Kinder unter 14
* | 5bbfa5a Snackkarte hinzugefügt
* | ea6a719 Titel und Öffnungszeiten ergänzt
|/
* 379d121 Werbebanner eingefügt
* b26bfdb Seniorenpreis ergänzt
* 294cecc Kinderpreis eingeführt
* 5050041 Filmliste ergänzt
* d4f3928 Initialer Import: Grundgerüst der KinoApp
```
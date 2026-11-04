Teil A

A1: Auf welchem Branch bist du, und welche Branches gibt es noch?

    Ich bin im branch main und es gibt noch die branches: feature/neuer-titel, feature/snacks.

A2: Welche Dateien meldet git status als „untracked“? Was bedeutet das?

    Die Dateien kasse.log und test/ werden als untracked gemeldet.

A3: ls -a zeigt einen Ordner .git. Was steckt darin, und was passiert, wenn man ihn löscht?

    In dem Ordner steckt README.md, index.html, kasse.log, preise.js.

git log --oneline --graph --all Ergebnis für Teil A:

$ git log --oneline --graph --all
* 1281d8f (feature/neuer-titel) Neuer Titel: Filmpalast
| * 5bbfa5a (feature/snacks) Snackkarte hinzugefügt
| * ea6a719 (HEAD -> main) Titel und Öffnungszeiten ergänzt
|/
* 379d121 Werbebanner eingefügt
* b26bfdb Seniorenpreis ergänzt
* 294cecc Kinderpreis eingeführt
* 5050041 Filmliste ergänzt
* d4f3928 Initialer Import: Grundgerüst der KinoApp


Teil B

B1: Woran erkennst du in der Ausgabe und im Log, dass es ein Fast-Forward war?

    $ git merge --ff-only feature/snacks
    Updating ea6a719..5bbfa5a
    Fast-forward
    snacks.md | 6 ++++++
    1 file changed, 6 insertions(+)
    create mode 100644 snacks.md

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

    An der Zeile mit dem "Fast-forward" erkennt man das. Im Log sieht man außerdem, dass main und feature/snacks auf denselben Commit zeigen.

B2: Warum war hier ein Fast-Forward möglich?

    Weil es beim main Branch keinen commit gab, somit konnt main einfach auf feature/snacks verschoben werden.

git log --oneline --graph --all Ergebnis für Teil B:

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


Teil C

C1: Beschreibe in einem Satz, wo der Fehler steckt und was er bewirkt.

    Der Fehler war das ">", wodurch überprüft wurde, ob Kinder über 14 sind und dann dementsprechend den Kinderpreis zahlen. Dies habe ich zu "<" abgeändert.

C2: Nach git add zeigt git diff nichts mehr an, git diff --staged aber schon. Warum?

    Weil diff nach dem add in die Staging Area kommt und dadurdch nur durch diff --staged angezeigt werden kann.

git log --oneline --graph --all Ergebnis für Teil C:

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


Teil D

D1: Ist der Commit „Werbebanner eingefügt“ nach dem Revert noch in der Historie? Was ist dazugekommen?

    Ja ist noch in der Historie aber an oberster Stelle ist nun auch die Zeile (Revert "Werbebanner eingefügt") hinzugekommen.

D2: Warum nimmt man in einem Team-Repo git revert statt Commits einfach zu löschen?

    Damit die Historie erhalten bleibt und nachvollzogen werden kann, was getan oder rückgänging gemacht wurde.

git log --oneline --graph --all Ergebnis für Teil D:

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


Teil E

E1: Was ist der Unterschied zwischen > und >> beim echo-Befehl?

    > überschreibt den bisherigen Inhalt einer Datei.
    >> hängt den neuen Inhalt an die bestehende Datei an.

E2: Was zeigt git status vor und nach dem Anlegen der .gitignore?

    Davor, dass der Ordner test/ und die Datei kasse.log untracked sind. Danach, nur noch antworten.md als untracked

git log --oneline --graph --all Ergebnis für Teil E:

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

Teil F


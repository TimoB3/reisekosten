REISEKOSTEN-APP (PWA fürs iPhone) – Version 4.2
==============================================

1. ZIEL
-------
Eine absolut kostenlose App, mit der Reisekostenabrechnungen am iPhone geschrieben
und als PDF ausgegeben werden. Das PDF orientiert sich so nah wie möglich an der
Vorlage "eigene_RKA.ods". Gehostet wird über ein vorhandenes GitHub-Konto
(GitHub Pages), es entstehen keine Kosten.

2. ANFORDERUNGEN AUS DEM CHAT (zusammengefasst)
-----------------------------------------------
Grundlagen
- Reisekostenabrechnung am iPhone schreiben, kostenlos, GitHub-Konto vorhanden.
- Ausgabe als PDF, Layout nah an der Vorlage (eigene_RKA.ods).
- Einstellungen (bleiben gespeichert): Name, Spesensatz für 24 h, Firmenstandort.
  (Zusätzlich aus der Vorlage übernommen: Abteilung.)

Eingaben und Rechenregeln
- Abfrage nur Start-/Enddatum und Start-/Endzeit (inzwischen je Fahrt, siehe 3.).
- Checkbox "Spesen?".
- Feld für sonstige Kosten und Feld für Fahrtkosten.
- Spesen angekreuzt: Verpflegungsvergütung wird automatisch berechnet:
  Abwesenheit > 8 h = halber Tagessatz, 24 h = voller Tagessatz.
- Bei Abwesenheit über Nacht werden an den Folgetagen im Feld Übernachtung
  automatisch 20 % des Tagessatzes als Frühstücksabzug eingetragen (als Minusbetrag).
  Das wird auf der Ausgabe nicht gesondert erklärt.
- Die Summe pro Tag wird in das Feld "Summe" eingetragen.
- Feld Einsatzort bzw. Ziel; die Strecke steht auf der Ausgabe immer als
  "Firmenstandort—Einsatzort—Firmenstandort".
- Feld Tätigkeit: steht in der Spalte Reisezweck möglichst weit unten.

Layout
- Ausgabe in der Größe einer halben DIN-A4-Seite: obere Hälfte eines A4-Blattes
  im Hochformat (die untere Hälfte bleibt leer).
- Maximal fünf Tage werden aufgeführt.
- Zeit im 24-h-Format, Datum als TT.MM.JJ.
- Spalten "Beleg-Nr." und "Nebenkosten lt. Anlagen" entfallen.
- Überschriften: Zeilenumbruch nach "Reise-Beginn/" und nach "...besuchte".
- Spaltenbreiten an die Überschriftenbreiten angepasst (Reisezweck bekommt den Rest).
- Fahrtkosten und sonstige Kosten werden für jeden Tag einzeln abgefragt,
  die Vorschau berücksichtigt sie.
- Die Strecke wird nur dort aufgeführt, wo eine neue Fahrt beginnt.

Ergänzungen (Version 4)
- Datum und Uhrzeit wieder per Auswahl: Datum in der Reihenfolge Tag / Monat / Jahr,
  Uhrzeit in 24 h, Minuten nur 00, 15, 30 oder 45.
- Die Fahrten müssen zeitlich geordnet sein: Fahrt 2 beginnt nicht vor dem Ende von
  Fahrt 1, Fahrt 3 nicht vor dem Ende von Fahrt 2 usw. (wird automatisch korrigiert).
- Nach Eingabe des Beginn-Datums wird das Ende-Datum automatisch auf dasselbe Datum
  gesetzt, bleibt aber änderbar.
- Das Ziel wird nur noch einmal abgefragt, die Strecke erscheint trotzdem für jede
  Fahrt in der Ausgabe.
- Die Checkbox "Spesen?" gibt es für jede Fahrt einzeln, die Berechnung berücksichtigt das.

3. BEDIENUNG
------------
1. Einstellungen ausfüllen (einmalig): Name, Abteilung, Firmenstandort, Spesensatz 24 h.
2. "Wie viele Fahrten zum Kunden?" wählen (1-5) und das Ziel eintragen (einmal).
3. Pro Fahrt Beginn und Ende wählen: Tag, Monat, Jahr, Stunde, Minute (00/15/30/45).
   Wird das Beginn-Datum gewählt, springt das Ende-Datum auf dasselbe Datum
   (bei Übernachtung danach das Ende-Datum ändern).
   Pro Fahrt die Checkbox "Spesen?" setzen oder abwählen.
4. Tätigkeit eintragen.
5. Unter "Kosten pro Tag" Fahrtkosten und sonstige Kosten je Tag eintragen.
6. Vorschau prüfen, dann "PDF erstellen". Im Teilen-Menü speichern oder versenden.

Berechnung im Detail
- Jede Fahrt wird auf Kalendertage aufgeteilt. Mehrere Fahrten am selben Tag werden
  zusammengerechnet. Die Spalte Std. zeigt die gesamte Abwesenheit des Tages (alle Fahrten).
- Verpflegung zählt nur Fahrten mit angekreuzten Spesen: voller Satz nur, wenn diese
  Fahrten den ganzen Kalendertag (00:00-24:00) abdecken; mehr als 8 h = halber Satz;
  genau 8 h oder weniger = 0.
- Frühstücksabzug (20 %) an jedem Tag, an dem eine Fahrt mit Spesen über Mitternacht
  hinweg weiterläuft.
- Fahrten sind zeitlich geordnet und dürfen sich nicht überschneiden; insgesamt höchstens
  5 Tage mit Abwesenheit.
- Fahrtkosten und Sonstiges werden je Tag eingegeben und in dieser Tageszeile ausgegeben.
- Die Strecke "Firmenstandort—Ziel—Firmenstandort" steht für jede Fahrt in der Zeile
  ihres Starttages.

4. INSTALLATION (GitHub Pages)
------------------------------
1. Auf github.com ein Repository anlegen (z. B. "reisekosten").
2. Die Dateien index.html, manifest.json, sw.js und icon.png hochladen
   (Add file > Upload files; die ZIP-Datei vorher entpacken, vorhandene Dateien ersetzen).
3. Settings > Pages > Branch "main" (Ordner "/ (root)") auswählen und speichern.
4. Nach ca. 1-2 Minuten die Seite in Safari öffnen.
5. Teilen > "Zum Home-Bildschirm" für das App-Symbol.

UPDATE-HINWEIS (wichtig)
Bei Version 1 und 2 hat der Zwischenspeicher (Service Worker) die alte Version
festgehalten, deshalb war nach dem Hochladen keine Änderung sichtbar.
Version 3 holt die Seite immer zuerst aus dem Netz und löscht alte Zwischenspeicher.
Damit Version 3 bei dir ankommt:
  a) Neue Dateien in GitHub hochladen und warten, bis Pages fertig ist
     (im Repository unter "Actions" sichtbar).
  b) App komplett schließen (im App-Umschalter wegwischen) und neu öffnen -
     dies ggf. ein zweites Mal wiederholen.
  c) Unten auf der Seite steht "Version 4.2". Steht dort etwas anderes, gilt noch die alte Version.
  d) Falls nötig: Home-Bildschirm-Symbol löschen, in iOS unter Einstellungen > Apps > Safari >
     Erweitert > Website-Daten die Seite entfernen, dann neu über Safari hinzufügen.
Künftige Updates kommen dann automatisch beim nächsten Start (mit Internet).

5. VERSIONSVERLAUF
------------------
v1  Erste Version: Name/Satz/Firmenstandort, Start/Ende, Spesenlogik, PDF A5 quer.
v2  PDF auf A4 hoch (obere Hälfte); Kosten je Tag; Vorschau mit Kosten; Strecke nur
    am ersten Tag; max. 5 Tage; 24-h-Zeit und TT.MM.JJ; Spalten Beleg-Nr. und
    Nebenkosten entfernt; Überschriften umgebrochen; Spaltenbreiten angepasst.
v3  Mehrere Fahrten (Anzahl wählbar, je Fahrt Beginn, Ende, Ziel); Strecke nur bei Beginn
    einer neuen Fahrt; neuer Service Worker (Netz zuerst) gegen das Update-Problem;
    Versionsanzeige; diese README.txt.
v4  Datum (Tag/Monat/Jahr) und Uhrzeit (Minuten 00/15/30/45) wieder per Auswahl;
    Fahrten zeitlich geordnet (automatische Korrektur); Ende-Datum folgt dem Beginn-Datum;
    Ziel nur einmal, Strecke trotzdem je Fahrt; Spesen-Checkbox je Fahrt.
v4.1 Uhrzeitfelder verkleinert, Datumsfelder vergrößert (Zahlen vollständig lesbar).
v4.2 Felder Vorsteuer %, Beträge und Nettobeträge im Fuß der Ausgabe ergänzt (bleiben leer).

6. DATEIEN
----------
index.html     App (Formular, Berechnung, PDF-Erzeugung)
manifest.json  App-Daten für den Home-Bildschirm
sw.js          Service Worker (Offline-Zwischenspeicher, Netz zuerst)
icon.png       App-Symbol
README.txt     Diese Datei

7. BEKANNTE EINSCHRÄNKUNGEN
---------------------------
- Das PDF-Programm (jsPDF) wird beim ersten Start aus dem Internet geladen und danach
  zwischengespeichert; die Erstnutzung braucht also Internet.
- Nicht umgesetzt: Beleg-Nr.-Spalte,
  Nebenkosten-Spalte, RK-Vorschuss (Zeile bleibt zum Handausfüllen leer).
- Die Version wurde im Entwicklungsumfeld nur auf Syntax und Rechenlogik getestet;
  das PDF-Layout bitte am iPhone prüfen und Abweichungen melden.

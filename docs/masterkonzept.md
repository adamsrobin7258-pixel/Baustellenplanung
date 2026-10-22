# Masterkonzept – Brandschutz-Dokumentationssoftware

| | |
|---|---|
| **Status** | Planung – Entwurf, 1. Überarbeitung |
| **Version** | 0.1 |
| **Stand** | 22.10.2026 |
| **Zielplattformen** | Windows, Android, später iOS |
| **Entwicklungsansatz** | Flutter, offline-first, modular erweiterbar |
| **Zugehöriges Dokument** | [Phasenplan](phasenplan.md) |

---

## 1. Ziel und Produktvision

Die Anwendung soll eine professionelle Software zur Dokumentation von Brandschutzabschottungen und weiteren brandschutztechnischen Maßnahmen werden.

Sie soll die Arbeit auf der Baustelle vereinfachen, technische Nachweise strukturiert erfassen und eine nachvollziehbare Dokumentation für Prüfung, Mängelbeseitigung und Übergabe ermöglichen.

Die Anwendung wird zunächst intern in einem Unternehmen eingesetzt. Eine spätere Vermarktung an weitere Unternehmen soll architektonisch berücksichtigt werden, ohne die erste Version unnötig aufzublähen.

## 2. Grundprinzipien

- **Offline-first:** Die wesentlichen Arbeitsabläufe müssen auch ohne Internet funktionieren.
- **Plattformübergreifend:** Eine gemeinsame technische Basis für Windows, Android und später iOS.
- **Nachvollziehbarkeit:** Änderungen, Prüfungen und Freigaben müssen historisch nachvollziehbar bleiben.
- **Datenschutz und Datensicherheit:** Unternehmensdaten werden geschützt gespeichert und übertragen – lokal einschließlich Fotos und Plänen.
- **Keine stillen Datenverluste:** Konflikte und fehlgeschlagene Synchronisationen müssen sichtbar sein. Daten werden nie still überschrieben.
- **Modularität:** Weitere Dokumentationsarten und optionale Module sollen später ergänzt werden können.
- **Benutzerfreundlichkeit:** Schnelle Erfassung auf dem Smartphone und effiziente Bearbeitung am Windows-PC.
- **Fachliche Verantwortung:** Die Software unterstützt die Dokumentation, ersetzt aber keine fachliche Beurteilung oder Prüfung.

## 3. Zielgruppe und Größenordnung

Die erste Version ist für ein Unternehmen mit ungefähr folgenden Kennzahlen ausgelegt:

- 10–25 Mitarbeiter
- 10–25 gleichzeitig aktive Projekte
- 100–500 Tickets je Projekt
- Mehrere Windows-Arbeitsplätze und Android-Geräte auf Baustellen

Daraus ergibt sich als Auslegungsgröße für Tests: bis zu ca. **12.500 Tickets** und – bei durchschnittlich 2–4 Fotos je Ticket – **mehrere zehntausend Fotos** im Gesamtbestand. Ein einzelnes Gerät hält typischerweise nur einen Teil davon lokal vor.

Die Architektur soll eine spätere Nutzung durch mehrere Unternehmen ermöglichen. Eine solche Mehrmandantenlösung wird erst nach erfolgreichem internem Einsatz umgesetzt.

## 4. Plattformen und technische Grundrichtung

Flutter ist die bevorzugte Grundlage für die gemeinsame Anwendung.

Die technische Eignung wird vor Beginn der eigentlichen Implementierung in einem Machbarkeitstest (Phase 0, siehe [Phasenplan](phasenplan.md)) geprüft. Zu prüfende Kandidaten:

| Bereich | Kandidat | Zu prüfen |
|---|---|---|
| PDF-Darstellung | `pdfrx` | Große, mehrseitige Pläne; flüssiges Zoomen; präzise Markierungen; Öffnen aus verschlüsselter Quelle |
| Lokale Datenbank | `drift` mit SQLCipher | Verschlüsselung auf Windows **und** Android; Leistung bei Auslegungsgröße |
| Schlüsselverwaltung | `flutter_secure_storage` | Android Keystore, Windows-Anmeldeinformationsspeicher; Verhalten bei Neuinstallation |
| PDF-Erstellung | `pdf` | Umfangreiche Berichte mit vielen Fotos; Speicherbedarf; Laufzeit |
| Dateiverschlüsselung | wird in Phase 0 festgelegt | Authentifizierte Verschlüsselung großer Dateien; Leistung; Wiederherstellbarkeit |

Fällt ein Kandidat durch, wird vor Phase 1 eine Alternative geprüft und dokumentiert.

Da aktuell kein Mac zur Verfügung steht, werden frühe Entwicklung und Tests auf Windows und Android konzentriert. iOS bleibt bei Architektur und UI-Entscheidungen berücksichtigt (keine Windows- oder Android-exklusiven Abhängigkeiten ohne iOS-Alternative). Für spätere iOS-Builds und Gerätetests muss eine geeignete macOS-Umgebung verfügbar sein.

### 4.1 Referenzgeräte

Messungen und Gerätetests bis zum MVP erfolgen auf folgenden Referenzgeräten:

| Plattform | Gerät |
|---|---|
| Android | Xiaomi 15 Ultra, 16 GB RAM, Android 16 |
| Windows | Windows 11, Intel Core i5-12400, 8 GB RAM |

Das Android-Referenzgerät ist ein leistungsstarkes Oberklassegerät. Messergebnisse darauf sind **nicht** auf schwächere Geräte übertragbar. Sollen im Praxistest schwächere Android-Geräte eingesetzt werden, ist vorher ein ergänzender Test auf einem solchen Gerät erforderlich. Der Windows-Referenz-PC mit 8 GB RAM ist dagegen eher knapp ausgestattet und daher für Speichertests (z. B. umfangreiche PDF-Berichte) besonders aussagekräftig.

## 5. Entwicklungsorganisation

- **Implementierung, automatisierte Tests und technische Dokumentation:** Claude Code.
- **Tests auf realen Geräten und Abnahme jeder Phase:** Projektverantwortlicher (Programmieranfänger, unter 5 Stunden pro Woche).
- Daraus folgt:
  - Phasen und Schritte werden **klein und einzeln abnehmbar** geschnitten.
  - Jede Phase liefert eine **schriftliche Test-Checkliste** in einfacher Sprache, die ohne Programmierkenntnisse abgearbeitet werden kann.
  - Installierbare Testversionen (Windows, Android) werden automatisiert erzeugt; es ist keine lokale Entwicklungsumgebung beim Projektverantwortlichen erforderlich.
  - Messwerte, die nur auf realen Geräten ermittelt werden können, zeigt die App selbst an, sodass sie abgelesen und zurückgemeldet werden können.
- Keine Phase beginnt ohne ausdrückliche Freigabe der vorherigen Phase.
- **Vor der ausdrücklichen Freigabe des Phasenplans wird keine Implementierung vorgenommen** – kein App-Code, kein Prototyp, keine Build-Pipeline. Auch der Beginn von Phase 0 erfordert eine gesonderte, ausdrückliche Zustimmung des Projektverantwortlichen.

## 6. Benutzer, Unternehmen und Berechtigungen

Vorgesehene Rollen:

- Firmenadministrator
- Projektleiter
- Mitarbeiter
- Prüfer
- Externer Mitarbeiter

Berechtigungen ergeben sich aus der Rolle und zusätzlichen Freigaben für Projekte oder Datenbereiche.

Interne Mitarbeiter erhalten grundsätzlich Zugriff auf Unternehmensprojekte entsprechend ihrer Berechtigungen. Externe Mitarbeiter sehen nur ausdrücklich freigegebene Projekte und Datenbereiche.

Zugänge, Gerätefreigaben und externe Berechtigungen müssen administrierbar und widerrufbar sein.

Im MVP genügen Benutzerkonten und Geräteregistrierung für die Synchronisation; das vollständige Rollen- und Rechtemodell folgt nach dem MVP.

## 7. Projekte

Ein Projekt enthält unter anderem:

- Projektnummer und Projektname
- Auftraggeber und beteiligte Unternehmen
- Projektadresse
- Verantwortliche Personen
- Projektstatus und Termine
- Zugeordnete Baupläne
- Tickets, Mängel, Prüfungen und Aufgaben
- Dokumente und Exporte
- Freie Ordner und konfigurierbare Zusatzfelder

Projektnummern (Format z. B. `P2026-014`) sollen automatisch erzeugt und bei entsprechender Berechtigung bearbeitet werden können. Eine nachträgliche Änderung der Projektnummer verändert **keine** bereits vergebenen Ticketnummern (verbindlich, siehe Abschnitt 9.1).

Projekte können archiviert und bei Bedarf wiederhergestellt werden. Favoriten, globale Suche und Filter unterstützen den Arbeitsalltag.

## 8. Baupläne

PDF-Baupläne müssen importiert, angezeigt und bei mehrseitigen Dokumenten seitenweise bearbeitet werden können.

Markierungen werden an stabilen, dokumentbezogenen Koordinaten gespeichert (PDF-Seitenkoordinaten in Punkt, bezogen auf die unrotierte Seite). Zoom, Verschieben, Displaygröße und erneutes Öffnen dürfen ihre Position nicht verändern.

Jede Markierung verweist auf ein Ticket.

Neue Planrevisionen werden bewusst als neue Revisionen behandelt. Bestehende Markierungen dürfen nicht automatisch und unbemerkt verschoben werden. Die Zuordnung von Tickets zur neuen Revision muss kontrolliert erfolgen.

Importierte Pläne werden unverändert und verschlüsselt gespeichert (siehe Abschnitt 15). Für jede importierte Originaldatei wird ein SHA-256-Prüfwert gespeichert.

Eine Messfunktion ist zunächst nicht vorgesehen.

## 9. Tickets und technische Erfassung

Jede Brandschutzabschottung erhält ein eigenes Ticket. Eine Markierung auf dem Plan erzeugt ein Ticket.

Vorgesehene Ticketarten:

- Kabelabschottung
- Rohrabschottung
- Kombiabschottung
- Fugenverschluss
- Brandschutzklappe
- Sonderlösung
- Unternehmensspezifische Ticketarten

Mögliche technische Angaben:

- Hersteller und Abschottungssystem
- Zulassungs- oder Bewertungsnummer
- Wand- beziehungsweise Deckentyp
- Bauteildicke und Feuerwiderstand
- Durchführungsmedien
- Mengen und Abmessungen
- Einbau- und Ausführungsangaben
- Fotos, Kommentare und zugehörige Dokumente

Firmenadministratoren sollen festlegen können, welche Felder für bestimmte Ticketarten verpflichtend sind.

Fehlende Angaben werden sichtbar angezeigt. Die Software darf fehlende Informationen nicht durch erfundene oder ungeprüfte Werte ersetzen. Schnell erfasste, unvollständige Tickets sind eindeutig als unvollständig gekennzeichnet und gelten nie als vollständig oder freigegeben.

### 9.1 Identität und Ticketnummer (verbindlich)

**Technische Identität**

- Jedes Objekt (Projekt, Plan, Planrevision, Markierung, Ticket, Foto, Dokument usw.) besitzt eine global eindeutige **UUID** als technische Identität. Sie ist die einzige maßgebliche technische Identität. Verknüpfungen zwischen Objekten erfolgen ausschließlich über UUIDs.
- Die UUID eines Objekts ändert sich nie – auch nicht durch Synchronisation, Wiederherstellung oder Änderung der Projektnummer.

**Lesbare Ticketnummer**

- Lesbare Ticketnummern werden **getrennt von der UUID** vergeben. Sie dienen der Verständigung und Suche, nicht als technischer Schlüssel.
- Format: `<Projektnummer zum Zeitpunkt der Vergabe> / <Gerätekürzel>-<Zähler>`, z. B. **`P2026-014 / K3-0042`**. Der Zähler ist vierstellig mit führenden Nullen und wächst bei Bedarf über 9999 hinaus (`K3-10000`).

**Unveränderlichkeit und Einmaligkeit**

- Eine Ticketnummer wird bei der Vergabe als **fester Text** gespeichert und danach **nie** verändert. Sie wird nicht nachträglich aus aktuellen Projekt- oder Gerätedaten neu berechnet.
- Eine nachträgliche **Änderung der Projektnummer verändert keine bereits vergebenen Ticketnummern.** Neu angelegte Tickets erhalten ab der Änderung die neue Projektnummer.
- Ticketnummern werden **niemals erneut vergeben** – auch nicht nach Löschung, Archivierung, Wiederherstellung oder Gerätewechsel. Lücken in der Nummernfolge sind zulässig.

**Globale Eindeutigkeit**

Ein Gerätekürzel allein ersetzt keine globale Eindeutigkeit. Die Eindeutigkeit wird zusätzlich abgesichert durch:

- ein **Register aller jemals vergebenen Gerätekürzel**. Vor Einführung des Servers führt es der Firmenadministrator, danach führt es der Server verbindlich.
- eine **technische Eindeutigkeitsprüfung** der vollständigen Ticketnummer in der lokalen Datenbank und – nach Einführung des Servers – zusätzlich auf dem Server.
- eine **Prüfung bei Wiederherstellung, Import und Synchronisation.** Taucht eine Ticketnummer doppelt auf, wird dies als Konflikt sichtbar gemacht. Es wird nie still umnummeriert, überschrieben oder verworfen.

**Gerätekürzel**

- Ein Gerätekürzel gehört zu einer **App-Installation**, nicht zur Hardware. Eine Neuinstallation oder ein neues Gerät erhält ein neues Kürzel.
- Gerätekürzel werden **eindeutig** vergeben und **nie wiederverwendet**, auch nicht nach Stilllegung eines Geräts. Stillgelegte Kürzel bleiben im Register als „stillgelegt" erhalten.
- Vor Einführung des Servers wird das Kürzel bei der Ersteinrichtung aus dem Register des Firmenadministrators übernommen. Die App lehnt ein Kürzel ab, das in bereits vorhandenen Ticketnummern vorkommt. Nach Einführung des Servers vergibt der Server die Kürzel bei der Geräteregistrierung.
- Ein Kürzel ist nicht frei änderbar. Ein Wechsel erfolgt ausschließlich über die unten geregelten Verfahren, also nach einer Wiederherstellung oder bei unklarer Zählerhistorie, und immer zu einem **neuen** Kürzel.

**Zähler**

- Der Zähler für neu vergebene Ticketnummern wird **dauerhaft und absturzsicher** in der verschlüsselten lokalen Datenbank gespeichert und **in derselben Transaktion** erhöht, in der das Ticket angelegt wird. Ein Absturz kann daher keine doppelte Nummer erzeugen.
- Vor jeder Vergabe prüft die App die Zählerhistorie. Der Zähler muss größer sein als die höchste mit diesem Gerätekürzel jemals vergebene Nummer, gelöschte Tickets eingeschlossen.
- **Unklare oder beschädigte Zählerhistorie:** Fehlt der Zählerstand, ist er unlesbar oder widerspricht er den vorhandenen Ticketnummern, sperrt die App die Vergabe neuer Ticketnummern mit diesem Kürzel. Sie fährt **nicht** mit einem möglicherweise bereits vergebenen Nummernbereich fort. Die Vergabe wird erst nach Zuweisung eines neuen, eindeutigen Gerätekürzels fortgesetzt. Bereits erfasste Daten bleiben unverändert erhalten. Ob in diesem Zustand Tickets vorläufig mit dem Vermerk „Nummer ausstehend" erfasst werden dürfen, wird in Phase 0.7 festgelegt.

**Wiederherstellung**

- Nach einer Wiederherstellung, aus einer Sicherung oder auf einem neuen Gerät, muss **ein neues, eindeutiges Gerätekürzel vergeben werden, bevor neue Ticketnummern vergeben werden**.
- Bestehende Tickets und ihre bisherigen Ticketnummern bleiben dabei **unverändert** erhalten.
- Das bisherige Kürzel wird im Register als stillgelegt geführt.

## 10. Ticketstatus und Prüfung

Vorgesehene Statuswerte:

1. Neu
2. In Bearbeitung
3. Zur Prüfung
4. Freigegeben
5. Mangelhaft
6. Erledigt

„Erledigt" bedeutet nicht automatisch „fachlich freigegeben".

Tickets werden bewusst zur Prüfung eingereicht. Die zuständigen Prüfer und Prüfregeln sind konfigurierbar.

Prüfungen können einzeln oder gruppenweise durchgeführt werden. Auch bei Gruppenprüfungen erhält jedes Ticket ein eigenes Prüfergebnis.

Prüfungen können Checklisten, Ergebnisse, Kommentare, Fotos, Prüfer und Zeitangaben enthalten.

Eine nicht bestandene Prüfung erzeugt einen nachvollziehbaren Mangel beziehungsweise Mängelvorgang. Nacharbeiten und erneute Prüfungen müssen die Historie erhalten.

Eine verpflichtende Unterschrift ist für den normalen Arbeitsablauf zunächst nicht vorgesehen.

## 11. Mängel und Aufgaben

Mängel können eigenständig angelegt und mit Tickets oder Projekten verknüpft werden. Sie enthalten Beschreibung, Status, Fotos, Zuständigkeit und Verlauf.

Offene Mängel verhindern den Projektabschluss nicht automatisch. Sie müssen bei Abschluss und Übergabe deutlich ausgewiesen werden.

Aufgaben werden manuell erstellt. Prioritäten und Fristen sind optional. Überfällige Aufgaben werden markiert; automatische Eskalationen und Push-Benachrichtigungen sind zunächst nicht vorgesehen.

## 12. Katalog

Der erste Katalog wird unternehmensintern verwaltet.

Er kann Hersteller, Systeme, Zulassungen, Bewertungsunterlagen und weitere technische Referenzen enthalten. Daten können manuell angelegt oder aus Herstellerunterlagen übernommen werden.

Importierte Daten müssen vor der Verwendung überprüft und freigegeben werden. Versions- und Gültigkeitsinformationen sollen, soweit verfügbar, erhalten bleiben.

Ein späterer zentraler Katalog für mehrere Unternehmen ist möglich. Rechte, Pflegeverantwortung und Datenherkunft müssen zuvor geklärt werden.

Ein Katalogeintrag ist keine automatische Bestätigung der fachlichen Eignung eines Systems. Die fachliche Prüfung bleibt erforderlich.

## 13. Fotos und Dateien

Fotos können direkt über die Kamera oder aus der Galerie hinzugefügt werden. Pro Ticket sind mehrere Fotos möglich.

Originaldateien werden unverändert (bitgenau) gespeichert – verschlüsselt, siehe Abschnitt 15. Eine Bearbeitung oder automatische Qualitätsbewertung von Bildern ist zunächst nicht vorgesehen.

Für Anzeige und PDF-Berichte dürfen verkleinerte **Ableitungen** (z. B. Vorschaubilder) erzeugt werden. Sie ersetzen nie das Original, werden als Ableitung gekennzeichnet und können jederzeit aus dem Original neu erzeugt werden.

Soweit verfügbar, werden Aufnahmedatum, Importzeitpunkt und erfassender Benutzer getrennt behandelt.

**SHA-256-Prüfwert (Entscheidung):** Für jede Originaldatei (Foto, Plan, Anlage) wird beim Import ein SHA-256-Prüfwert über die **unverschlüsselte Originaldatei** berechnet und gespeichert. Damit lassen sich spätere Dateiänderungen erkennen. Ein Prüfwert allein beweist weder den tatsächlichen Aufnahmezeitpunkt noch die Authentizität des dargestellten Sachverhalts.

## 14. Dokumente und PDF-Export

Vorgesehene Dokumentarten:

- Fotodokumentation
- System- und Materiallisten
- Mängelberichte
- Prüfprotokolle
- Übereinstimmungs- und Erklärungsdokumente
- Projekt- und Übergabedokumentation

Unternehmensvorlagen mit Logo, Adresse und Farben sollen unterstützt werden.

Dokumente dürfen mit vorhandenen Daten vorausgefüllt werden, müssen vor der Ausgabe aber überprüfbar bleiben.

Freigegebene oder übergebene Dokumente werden versioniert und unveränderlich archiviert. Sie müssen den zugrunde liegenden Datenstand und die verwendete Planrevision nachvollziehbar referenzieren.

Einzelne PDFs oder ausgewählte beziehungsweise vollständige Projektpakete können exportiert werden. Unvollständige Exporte sind grundsätzlich möglich, müssen aber deutlich auf fehlende Angaben hinweisen.

Eine gezeichnete Unterschrift gilt nicht automatisch als qualifizierte elektronische Signatur.

Grundlage für den ersten Bericht ist der Aufbau der realen Dokumentationsvorlage des Unternehmens. Die reale Vorlage bleibt ausschließlich auf den freigegebenen Testgeräten. In der Software und im Repository wird nur eine **künstliche Nachbildung** mit Fantasiedaten verwendet (siehe Abschnitt 17). Firmenlogo und Firmendaten werden auf dem Gerät eingerichtet und nicht im Repository abgelegt.

## 15. Offlinebetrieb und lokale Datensicherheit

Die zentralen Arbeitsabläufe müssen offline nutzbar sein, insbesondere:

- Projekte und ausgewählte Projektdaten öffnen
- Baupläne ansehen und markieren
- Tickets bearbeiten
- Fotos aufnehmen und speichern
- Aufgaben und Mängel bearbeiten
- PDFs erstellen und exportieren

### 15.1 Verschlüsselung (Entscheidung)

- **Datenbank:** Die lokale Datenbank wird vollständig verschlüsselt (Kandidat: SQLCipher).
- **Dateien:** Auch **Fotos, importierte Pläne und weitere Anlagen** werden verschlüsselt gespeichert – auf Windows ebenso wie auf Android.
  - Es wird ein authentifiziertes Verfahren verwendet (Kandidat: AES-256-GCM), sodass Manipulationen oder Beschädigungen der verschlüsselten Datei erkannt werden.
  - Große Dateien werden abschnittsweise verschlüsselt, damit sie ohne vollständiges Entschlüsseln in den Arbeitsspeicher geöffnet und gelesen werden können. Die Eignung wird in Phase 0 geprüft.
  - Entschlüsselte Inhalte werden nicht dauerhaft unverschlüsselt auf dem Datenträger abgelegt. Ausnahme: ausdrücklich vom Benutzer ausgelöste Exporte.
- **Prüfwert:** Der SHA-256-Prüfwert bezieht sich immer auf die unverschlüsselte Originaldatei (Abschnitt 13).

### 15.2 Schlüsselverwaltung

- **Geräteschlüssel** werden zufällig erzeugt und auf dem Gerät ausschließlich im geschützten Schlüsselspeicher des Betriebssystems abgelegt (Kandidat: `flutter_secure_storage` – Android Keystore, Windows-Anmeldeinformationsspeicher). Der davon unabhängige Wiederherstellungsschlüssel wird außerhalb der Geräte verwahrt (siehe unten).
- Schlüssel werden nie im Klartext in Dateien, Protokollen, Diagnosedaten oder im Repository gespeichert.
- **Wiederherstellbarkeit (verbindlich):** Geht der Geräteschlüssel verloren (z. B. Deinstallation, Gerätedefekt, Verlust des Geräts, Windows-Neuinstallation), sind lokal verschlüsselte Daten ohne weitere Vorkehrung unlesbar. Daher gilt:
  - Ein **ausschließlich auf einem Gerät vorhandener Schlüssel darf nie der einzige Weg zur Wiederherstellung sein.**
  - Sicherungen werden so verschlüsselt, dass sie auch **ohne den ursprünglichen Geräteschlüssel** mit einem vom Gerät unabhängigen **Wiederherstellungsschlüssel** (oder Wiederherstellungskennwort) wiederhergestellt werden können.
    - Kandidat: Der Schlüssel einer Sicherung wird doppelt hinterlegt – mit dem Geräteschlüssel, für die Wiederherstellung auf demselben Gerät, und mit dem Wiederherstellungsschlüssel, für die Wiederherstellung auf einem anderen oder neuen Gerät.
  - Der Wiederherstellungsschlüssel wird vom Firmenadministrator **getrennt von den Geräten** sicher verwahrt, z. B. ausgedruckt im Tresor oder in einem Passwortmanager. Verwahrort und Zuständigkeit sind dokumentiert.
  - Nach Einführung der Synchronisation ist der Server die primäre Wiederherstellungsquelle. Lokale Sicherungen bleiben zusätzlich bestehen.
  - Das genaue Verfahren wird in Phase 0 geprüft und spätestens mit Abschluss von Phase 0 verbindlich festgelegt, da es bereits für die Migrationssicherung in Phase 1 benötigt wird.
- **Verlorene Geräte und verlorene Schlüssel:** Für beide Fälle gibt es vor dem Pilotbetrieb eine dokumentierte Vorgehensweise. Sie umfasst mindestens:
  - Meldung und Zuständigkeit,
  - Stilllegung des Gerätekürzels,
  - nach Einführung des Servers: Sperre des Geräts,
  - Wiederherstellung aus der letzten Sicherung auf einem Ersatzgerät,
  - Hinweis auf möglicherweise verlorene Änderungen seit der letzten Sicherung.

### 15.3 Backups, Downloads und Speicherplatz

Lokale Backups müssen manuell und automatisiert möglich sein. Eine Sicherung umfasst die verschlüsselte Datenbank und die zugehörigen verschlüsselten Dateien **gemeinsam und in einem zueinander passenden Stand**. Wiederherstellung und Integrität der Backups müssen überprüfbar sein (Abgleich der SHA-256-Prüfwerte).

Nach jeder Sicherung erhält der Nutzer eine **verständliche Rückmeldung über Erfolg oder Fehler**. Eine fehlgeschlagene oder unvollständige Sicherung wird nie als gültig gekennzeichnet.

Benutzer können lokale Projektdaten entfernen, ohne dadurch automatisch zentrale Daten zu löschen.

Downloads müssen fortsetzbar sein und erst nach erfolgreicher Integritätsprüfung als vollständig gelten. Bei knappem Speicherplatz werden Nutzer gewarnt; die App löscht keine Projektdaten eigenmächtig.

### 15.4 Datensicherung vor Datenbankmigrationen (verbindlich)

Ändert ein App-Update die Struktur der lokalen Datenbank (Migration), gilt:

1. **Sicherung vor jeder Migration:** Vor jeder Migration wird automatisch eine Sicherung des bisherigen Datenbestands erstellt.
   - Die verschlüsselte Datenbank und die zugehörigen Dateien werden gemeinsam berücksichtigt.
   - Dateien, die die Migration verändert, werden vollständig mitgesichert.
   - Unveränderliche Dateien, die die Migration nicht berührt, werden über eine Liste ihrer Prüfwerte erfasst und nach der Migration auf Vollständigkeit geprüft.
2. **Prüfung der Sicherung:** Die Sicherung wird auf Vollständigkeit und Wiederherstellbarkeit geprüft, soweit technisch möglich. Dazu gehören:
   - Abgleich der Prüfwerte,
   - testweises Öffnen der gesicherten Datenbank mit dem zugehörigen Schlüssel,
   - Zählprüfung der Datensätze.
3. **Keine Migration ohne gültige Sicherung:** Schlägt die Sicherung oder ihre Prüfung fehl, etwa wegen fehlenden Speicherplatzes, beginnt die Migration **nicht**. Der Datenbestand bleibt unverändert. Der Nutzer erhält eine verständliche Meldung mit Handlungsanweisung.
4. **Fehlgeschlagene oder unterbrochene Migration:** Die App erkennt beim nächsten Start einen unvollständigen Migrationszustand, etwa nach einem Absturz, Stromausfall oder beendeter App. Dann greift ein **dokumentiertes Wiederherstellungsverfahren**: Der Stand vor der Migration wird aus der Sicherung wiederhergestellt und der Nutzer informiert. Teilweise migrierte Daten werden nie weiterverwendet.
5. **Schlüssel:** Das Sicherungskonzept berücksichtigt die sichere Wiederherstellung der benötigten Schlüssel gemäß Abschnitt 15.2. Eine Migrationssicherung muss auch dann wiederherstellbar sein, wenn der Geräteschlüssel verloren geht.
6. Verfahren und Tests werden mit dem Migrationsrahmen in Phase 1 umgesetzt und gelten für jedes spätere Update mit Strukturänderung.

### 15.5 Pflichtvoraussetzungen vor dem Pilotbetrieb mit Echtdaten (verbindlich)

**Pilotbetrieb** ist jeder Einsatz der App zur tatsächlichen Dokumentation echter Projekte, beginnend mit Meilenstein A. Die Verwendung realer Pläne in Phase 0 ist kein Pilotbetrieb: Dort werden sie nur angezeigt und vermessen, und die Prototyp-Daten dienen nie als Dokumentation.

Vor Beginn des Pilotbetriebs müssen **alle** folgenden Punkte erfüllt und nachgewiesen sein:

1. Die lokale Sicherung ist implementiert (manuell und automatisch).
2. Sicherungen sind vor unbefugtem Zugriff geschützt (verschlüsselt, Wiederherstellung nur mit berechtigtem Schlüssel oder Kennwort).
3. Eine Wiederherstellung wurde auf dem vorgesehenen Gerät **praktisch getestet**, mit Abgleich aller Prüfwerte.
4. Der Umgang mit verlorenen Geräten und verlorenen Schlüsseln ist dokumentiert (Abschnitt 15.2), und der Wiederherstellungsschlüssel ist verwahrt.
5. Der Nutzer erhält eine verständliche Rückmeldung über Erfolg oder Fehler jeder Sicherung.

Eine lediglich erfolgreich erstellte Sicherungsdatei gilt **nicht** als ausreichender Nachweis. Nachweis ist nur eine erfolgreiche, geprüfte Wiederherstellung.

## 16. Synchronisation und Server

Die Architektur wird von Beginn an für die Synchronisation vorbereitet. Dazu gehören UUIDs, Änderungsstände (Versionszähler je Datensatz) und ein nachvollziehbarer Änderungsverlauf.

### 16.1 Stufen (Entscheidung)

1. **Einzelgerät:** Der allererste Funktionstest findet auf einem einzelnen Gerät statt.
2. **Einfache Synchronisation – Bestandteil des MVP:** Daten und Dateien werden zwischen Android- und Windows-Geräten über einen selbst betriebenen Server ausgetauscht. Verbindliche Regeln bereits in dieser Stufe:
   - **Kein stilles Überschreiben und kein stiller Datenverlust.** Jede Änderung wird gegen den Stand geprüft, auf dem sie beruht.
   - **Konflikte werden erkannt und sichtbar gemacht.** Ändern zwei Geräte denselben Datensatz unabhängig voneinander, bleiben **beide Zustände erhalten** und der Konflikt erscheint in einer Konfliktliste.
   - Eine einfache Auflösung durch bewusste Auswahl eines Zustands ist zulässig; der nicht gewählte Zustand bleibt in der Historie erhalten.
   - Dateien (Fotos, Pläne) sind unveränderlich und über ihren Prüfwert identifiziert; sie können daher nicht in Konflikt geraten.
   - Löschungen werden als Löschvermerk synchronisiert, nicht als physisches Entfernen.
   - Ausstehende Änderungen und Synchronisationsfehler sind jederzeit sichtbar.
3. **Vollständige Synchronisation – nach dem MVP:** komfortable Konfliktauflösung (auch feldweise Zusammenführung), projektbezogene Zugriffssteuerung, Fernsperre von Geräten und weitere Funktionen.

### 16.2 Vorgesehene Funktionen (Gesamtbild)

- Automatische und manuelle Synchronisation
- Sichtbarer Synchronisationsstatus
- Anzeige ausstehender Änderungen und Fehler
- Fortsetzbare Übertragung großer Dateien
- Konfliktbehandlung ohne stilles Überschreiben
- Manuelle Konfliktauflösung mit Erhalt beider Zustände
- Zentrale Löschung mit Wiederherstellungsmöglichkeit
- Gerätefreigabe und projektbezogene Zugriffssteuerung

### 16.3 Serverbetrieb

Der Server wird zunächst selbst betrieben. Betriebssystem, Standort (Rechenzentrum in Deutschland empfohlen), Netzwerkzugriff von Baustellen, sichere Fernverbindung (TLS, ggf. VPN), Updates, Überwachung und Wiederherstellung müssen **vor der Serverphase** geklärt werden.

Der Betrieb soll mehrere Backups täglich, verschlüsselte externe Sicherungen und abgestufte Aufbewahrungsfristen umfassen. Wiederherstellungen werden regelmäßig getestet.

Bei einem Serverausfall muss die lokale Arbeit weiter möglich sein.

**Betriebsverantwortung (verbindliche Freigabebedingung für die Serverphase):**

- Es ist geklärt, wer für Serverbetrieb, Sicherheitsupdates, Überwachung, Backups und Störungsbehebung verantwortlich ist.
- Diese Verantwortung liegt bei einer **fachkundigen Person** oder einem **beauftragten Dienstleister**.
- Zugriffsrechte, Erreichbarkeit im Störungsfall (einschließlich Vertretung) und Wiederherstellungsverfahren sind dokumentiert.
- Der laufende Betreuungsaufwand, der beim Projektverantwortlichen verbleibt, passt zusammen mit Test- und Abnahmeaufwand realistisch in **weniger als fünf Stunden pro Woche**.
- **Ohne geklärte Betriebsverantwortung beginnt die Serverphase nicht.**

## 17. Datenschutz, Aufbewahrung und Unternehmensdaten

Das Unternehmen verwaltet seine Projektdaten. Vollständige Projektexporte sind grundsätzlich Firmenadministratoren vorbehalten.

Zugriffe, Freigaben, Änderungen und sicherheitsrelevante Vorgänge werden nachvollziehbar protokolliert. Audit-Protokolle sind besonders zu schützen.

Bei ausscheidenden Mitarbeitern werden Zugriffe widerrufen. Nicht mehr benötigte Profildaten werden entfernt oder ersetzt; erforderliche historische Nachweise bleiben erhalten.

Löschanfragen werden vor der Ausführung hinsichtlich gesetzlicher Aufbewahrungspflichten, offener Vorgänge und notwendiger Nachweise geprüft.

Aufbewahrungsfristen sollen pro Dokument- und Datenart konfigurierbar sein. Vor dem Ablauf werden Verantwortliche gewarnt.

### 17.1 Vertrauliche Dateien und Testdaten (verbindlich)

- Echte Pläne, Fotos und Dokumentationsvorlagen werden **niemals** in das Repository übernommen – **auch nicht in anonymisierter Form**. Es gibt hiervon keine Ausnahme.
- Automatisierte Tests verwenden **ausschließlich künstlich erzeugte Daten**.
- Echte Testunterlagen bleiben **lokal auf den freigegebenen Testgeräten** (Referenzgeräte gemäß Abschnitt 4.1).
- Auch **Testprotokolle, Logs, Messprotokolle, Screenshots und GitHub-Actions-Artefakte** dürfen keine vertraulichen Projektinhalte enthalten. Dazu gehören auch Datei- und Projektnamen, Adressen, Kunden- und Personendaten sowie Plan- oder Fotoausschnitte. Messprotokolle enthalten nur technische Kennwerte, etwa Dateigröße, Seitenzahl, Seitenformat und Zeiten.
- GitHub-Actions-Artefakte enthalten ausschließlich die erzeugten Testversionen und künstliche Testdaten.
- Die Unternehmensvorlage wird im Repository nur als künstliche Nachbildung mit Fantasiedaten abgebildet (Abschnitt 14).

## 18. Externe Unternehmen

Externe Unternehmen können später gezielt Tickets, Mängel oder Aufgaben erhalten.

Vorgesehen sind:

- Zeitlich begrenzte Zugriffe
- Projektbezogene Freigaben
- Kommentare und Rückfragen
- Einreichen von Arbeitsergebnissen
- Rückgabe zur Korrektur mit Begründung
- Widerruf von Zugängen
- Erhalt bereits eingereichter Nachweise
- Trennung interner Notizen von extern sichtbaren Informationen

Diese Funktionen werden nach dem internen Kernworkflow umgesetzt.

## 19. Suche, Auswertung und Massenaktionen

Die globale Suche soll Projekte, Pläne, Tickets, Mängel, Hersteller, Systeme und Dokumente finden.

Filter und einfache Kennzahlen unterstützen die Übersicht über Projekte und Unternehmensbereiche.

Massenaktionen sind für Statusänderungen, Zuweisungen und Exporte vorgesehen. Vor der Ausführung wird die Anzahl der betroffenen Objekte angezeigt.

## 20. Benutzeroberfläche

### Windows

Geteilte Arbeitsansicht mit Liste, Bauplan und Detailbereich. Große Datenmengen müssen übersichtlich bearbeitet werden können.

### Android

Baustellentaugliche Oberfläche mit großen Bedienelementen, wenigen Schritten und direktem Zugriff auf Kamera und Ticketdaten.

### Allgemein

- Automatische lokale Speicherung von Entwürfen
- Vorlagen und zuletzt verwendete Werte für wiederkehrende Eingaben
- Klarer Offline-Status
- Verständliche Fehlermeldungen
- Skalierbare Textgrößen
- Gute Lesbarkeit und ruhige, moderne Gestaltung

## 21. Lizenzierung und Updates

Die spätere kommerzielle Lizenzierung soll modular aufgebaut sein. Zusätzliche Module können optional angeboten werden. Künstliche Begrenzungen von Projekt-, Ticket- oder Dokumentmengen sind nicht vorgesehen.

Die zeitlich begrenzte Offline-Lizenzierung bleibt bis zur kommerziellen Produktphase offen, da sie den Baustellenbetrieb ohne Verbindung gefährden könnte.

Updates werden angeboten und zeitlich kontrolliert eingespielt. Sicherheitsupdates können innerhalb angemessener Fristen verpflichtend werden, müssen aber mit klaren Warnungen und einem sicheren Verfahren umgesetzt werden.

Änderungen am lokalen Datenbankschema werden ausschließlich über getestete Migrationen eingespielt. Es gelten die verbindlichen Regeln zur Datensicherung vor Migrationen (Abschnitt 15.4).

Technische Fehlerberichte sollen nur minimale anonyme Diagnosedaten enthalten. Projektinhalte, Fotos und Dokumente werden nicht automatisch übertragen.

## 22. MVP-Abgrenzung

Der erste nutzbare End-to-End-Ablauf umfasst:

1. Projekt erstellen
2. PDF-Bauplan importieren (verschlüsselt gespeichert)
3. Markierung auf dem Plan setzen
4. Ticket mit grundlegenden Angaben und Ticketnummer erstellen
5. Fotos hinzufügen (verschlüsselt, mit SHA-256-Prüfwert)
6. Einfachen PDF-Bericht auf Basis der Unternehmensvorlage erzeugen
7. Lokales Backup erstellen und wiederherstellen
8. Einfache Synchronisation zwischen Android und Windows mit sichtbarer Konflikterkennung

Schritte 1–7 werden zunächst auf einem einzelnen Gerät erprobt (Meilenstein A), Schritt 8 schließt das MVP ab (Meilenstein B). Vor Meilenstein A müssen die Pflichtvoraussetzungen für den Pilotbetrieb mit Echtdaten (Abschnitt 15.5) erfüllt sein.

Katalogverwaltung, umfassende Prüfabläufe, Mängelmanagement, Aufgaben, Rollen und Rechte, externer Zugriff und vollständige Konfliktauflösung folgen erst nach erfolgreicher Erprobung des MVP.

## 23. Offene technische und organisatorische Punkte

| Punkt | Klärung bis | Status |
|---|---|---|
| Geeignete PDF-Bibliothek für Windows und Android | Ende Phase 0 | offen |
| Verschlüsselte SQLite-Lösung und sichere Schlüsselverwaltung | Ende Phase 0 | offen |
| Verfahren zur Dateiverschlüsselung großer Dateien | Ende Phase 0 | offen |
| Verhalten bei großen Plänen und umfangreichen Projekten | Ende Phase 0 | offen |
| Speicherbedarf und Laufzeit umfangreicher PDF-Berichte | Ende Phase 0 | offen |
| Referenzgeräte (Android-Modell, Windows-PC) für Messungen | Vor Phase 0 | erledigt (4.1) |
| Ticketnummern bei Gerätewechsel und Backup-Wiederherstellung | Regeln verbindlich (9.1); Umgang mit „Nummer ausstehend" bis Ende Phase 0 | teilweise |
| Wiederherstellungsverfahren bei Schlüsselverlust und Migrationssicherung | Ende Phase 0 (benötigt in Phase 1) | Regeln verbindlich (15.2, 15.4); Verfahren offen |
| Dokumentation verlorene Geräte / verlorene Schlüssel | Vor Pilotbetrieb (Meilenstein A) | offen |
| Ergänzender Test auf schwächerem Android-Gerät | Vor Praxistest, falls solche Geräte eingesetzt werden | offen |
| Betriebsverantwortung für den Server (Person oder Dienstleister) | Vor Serverphase (Freigabebedingung) | offen |
| Serverbetrieb, Standort, sichere Fernverbindung und Backupkonzept | Vor Serverphase | offen |
| Konkrete Vorlagen, Pflichtfelder und technische Nachweise | Vor Berichtsphase | offen |
| Datenschutz- und Aufbewahrungsregeln | Vor Praxistest mit Echtdaten | offen |
| Verfügbarkeit einer macOS-Umgebung für iOS-Builds | Nach MVP | offen |
| Lizenz- und Updateverfahren für späteren kommerziellen Einsatz | Vor Vermarktung | offen |

## 24. Abnahmeregel

Keine Phase gilt allein deshalb als abgeschlossen, weil der Code kompiliert. Die festgelegten Abnahmekriterien, Tests und gegebenenfalls manuellen Prüfungen müssen erfolgreich sein. Kritische Sicherheits-, Datenverlust- oder Synchronisationsfehler blockieren die Abnahme.

Jede Phase wird vom Projektverantwortlichen einzeln und ausdrücklich abgenommen. Erst danach beginnt die nächste Phase.

Vor der ausdrücklichen Freigabe des Phasenplans erfolgt keine Implementierung. Der Beginn von Phase 0 erfordert eine gesonderte, ausdrückliche Zustimmung.

## 25. Entscheidungsprotokoll

| Nr. | Datum | Entscheidung |
|---|---|---|
| E-01 | 22.10.2026 | Flutter als gemeinsame technische Basis; frühe Entwicklung auf Windows und Android, iOS später. |
| E-02 | 22.10.2026 | Implementierung, automatisierte Tests und Dokumentation durch Claude Code; Gerätetests und Abnahme durch den Projektverantwortlichen in kleinen Schritten (< 5 h/Woche). |
| E-03 | 22.10.2026 | Erster Funktionstest auf einem Einzelgerät; einfache Synchronisation Android ↔ Windows ist Bestandteil des MVP. Kein stilles Überschreiben, Konflikte werden sichtbar gemacht und beide Zustände bleiben erhalten. Vollständige Konfliktauflösung später. |
| E-04 | 22.10.2026 | Verschlüsselung von Datenbank **und** Dateien (Fotos, Pläne, Anlagen). SHA-256-Prüfwert über die unverschlüsselte Originaldatei. |
| E-05 | 22.10.2026 | UUID als maßgebliche technische Identität. Lesbare Ticketnummer `P2026-014 / K3-0042`; Gerätekürzel eindeutig und nie wiederverwendet; Zähler dauerhaft gespeichert; vergebene Nummern werden nie erneut vergeben. |
| E-06 | 22.10.2026 | Technischer Machbarkeitstest (Phase 0) mit realen, ggf. anonymisierten Plänen und einer realen Dokumentationsvorlage – ausschließlich lokal auf den Testgeräten, nie im Repository (präzisiert durch E-09). Leistungswerte sind Testziele, keine Zusagen. |
| E-07 | 22.10.2026 | Zeitlich begrenzte Offline-Lizenzierung bleibt bis zur kommerziellen Phase offen. |
| E-08 | 22.10.2026 | Ein Katalog wird zunächst nur unternehmensintern geführt. |
| E-09 | 22.10.2026 | Echte Pläne, Fotos und Vorlagen werden niemals ins Repository übernommen, auch nicht anonymisiert. Tests nutzen nur künstliche Daten. Protokolle, Logs, Screenshots und Actions-Artefakte enthalten keine vertraulichen Inhalte (17.1). |
| E-10 | 22.10.2026 | Ticketnummern sind unveränderlich und werden nie erneut vergeben, auch bei Änderung der Projektnummer. Gerätekürzel allein garantiert keine globale Eindeutigkeit (Register und Eindeutigkeitsprüfung). Nach Wiederherstellung neues Kürzel. Bei unklarer Zählerhistorie Sperre der Vergabe (9.1). |
| E-11 | 22.10.2026 | Geprüfte Sicherung vor jeder Datenbankmigration. Keine Migration ohne gültige Sicherung. Dokumentiertes Wiederherstellungsverfahren bei Fehlern. Kein Schlüssel darf nur auf einem Gerät liegen (15.2, 15.4). |
| E-12 | 22.10.2026 | Pflichtvoraussetzungen vor dem Pilotbetrieb mit Echtdaten. Nachweis nur durch praktisch getestete Wiederherstellung (15.5). |
| E-13 | 22.10.2026 | Die Serverphase beginnt erst nach geklärter Betriebsverantwortung durch eine fachkundige Person oder einen Dienstleister (16.3). |
| E-14 | 22.10.2026 | Referenzgeräte: Xiaomi 15 Ultra (16 GB RAM, Android 16) und Windows 11 mit Intel Core i5-12400, 8 GB RAM (4.1). |
| E-15 | 22.10.2026 | Keine Implementierung vor ausdrücklicher Freigabe des Phasenplans. Phase 0 beginnt nur nach gesonderter Zustimmung. |

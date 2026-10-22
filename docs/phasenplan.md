# Phasenplan – Brandschutz-Dokumentationssoftware

| | |
|---|---|
| **Status** | Entwurf – wartet auf Freigabe |
| **Version** | 0.1 |
| **Stand** | 22.10.2026 |
| **Grundlage** | [Masterkonzept v0.1](masterkonzept.md) |
| **Umfang** | Phase 0 (technischer Machbarkeitstest) bis MVP |

---

## 1. Zweck dieses Dokuments

Dieser Plan beschreibt, in welchen Schritten die Software von einem leeren Repository bis zum MVP entwickelt wird. Jede Phase hat:

- ein klares **Ziel** und einen abgegrenzten **Umfang**,
- ausdrücklich **nicht enthaltene** Punkte,
- **messbare Abnahmekriterien**, getrennt nach automatisierten Prüfungen und Prüfungen auf deinen Geräten,
- eine Schätzung deines **Zeitaufwands** für Test und Abnahme.

Phasen nach dem MVP (Katalog, Prüfabläufe, Mängel, Rollen, externe Firmen, iOS …) werden erst nach Erreichen des MVP geplant.

## 2. Arbeitsweise

### 2.1 Rollen

| Wer | Aufgaben |
|---|---|
| **Claude Code** | Implementierung, automatisierte Tests, Build-Pipeline, technische Dokumentation, Test-Checklisten, Auswertung von Messergebnissen |
| **Projektverantwortlicher** | Bereitstellen von Beispielmaterial, Tests auf eigenen Geräten, Rückmeldung von Messwerten und Fehlern, Abnahme jeder Phase |

### 2.2 Ablauf jeder Phase

1. Claude Code setzt die Phase auf einem Feature-Branch um. Der Standard-Branch wird nur nach deiner Freigabe geändert.
2. Automatisierte Tests laufen bei jedem Push in GitHub Actions.
3. GitHub Actions erzeugt installierbare Testversionen:
   - **Android:** APK-Datei
   - **Windows:** ZIP-Archiv mit ausführbarer Anwendung
4. Claude Code legt eine **Test-Checkliste** in einfacher Sprache unter `docs/abnahme/phase-<nr>-checkliste.md` an.
5. Du installierst die Testversion, arbeitest die Checkliste ab und meldest Ergebnisse, Messwerte und Fehler zurück.
6. Fehler werden behoben, bis alle Kriterien erfüllt sind.
7. Du nimmst die Phase ausdrücklich ab. Die Abnahme wird in `docs/abnahme/phase-<nr>-protokoll.md` festgehalten.
8. Erst danach beginnt die nächste Phase.

### 2.3 Allgemeine Abnahmekriterien („Definition of Done")

Diese Kriterien gelten **zusätzlich** zu den phasenspezifischen Kriterien für jede Phase ab Phase 1:

- [ ] Alle automatisierten Tests laufen in GitHub Actions fehlerfrei durch.
- [ ] Die statische Code-Analyse (`flutter analyze`) meldet keine Fehler und keine Warnungen.
- [ ] Android- und Windows-Testversion werden automatisch erzeugt und lassen sich installieren und starten.
- [ ] Es gibt keinen offenen Fehler der Kategorie „kritisch" (Datenverlust, Datenschutz, falsche Dokumente, Synchronisationsfehler).
- [ ] Die Test-Checkliste ist vollständig abgearbeitet.
- [ ] Technische Dokumentation und gegebenenfalls das Masterkonzept sind aktualisiert.
- [ ] Datenbankänderungen sind als getestete Migration umgesetzt. Ein automatisierter Test belegt, dass Daten des vorherigen Stands erhalten bleiben (ab Phase 2).

### 2.4 Schnitt der Phasen

Weil dir weniger als 5 Stunden pro Woche zur Verfügung stehen, ist jede Phase so geschnitten, dass Test und Abnahme **in der Regel 1–3 Stunden** dauern. Größere Phasen sind in Teilschritte zerlegt, die einzeln abgenommen werden.

## 3. Übersicht

| Phase | Inhalt | Ergebnis | Dein Aufwand (Schätzung) |
|---|---|---|---|
| **V** | Vorbereitung | Referenzgeräte und Beispielmaterial festgelegt | 1–2 h |
| **0** | Technischer Machbarkeitstest (Wegwerf-Prototyp) | Belastbare Technikentscheidung | 6 Teilschritte à 1–2 h |
| **1** | App-Grundgerüst | Saubere, getestete Basis mit Verschlüsselung und Ersteinrichtung | 1 h |
| **2** | Projekte | Projekte anlegen, bearbeiten, archivieren | 1–2 h |
| **3** | Baupläne | PDF-Pläne verschlüsselt importieren und anzeigen | 1–2 h |
| **4** | Markierungen und Tickets | Markierung setzen → Ticket mit Ticketnummer | 2–3 h |
| **5** | Fotos | Fotos zu Tickets, unverändert und mit Prüfwert | 1–2 h |
| **6** | PDF-Bericht | Bericht nach Unternehmensvorlage | 2–3 h |
| **7** | Backup und Wiederherstellung | Datensicherung ohne Datenverlust | 2 h |
| **A** | **Meilenstein A: Einzelgerät-Funktionstest** | Echtes Kleinprojekt auf einem Gerät | 2–4 h verteilt |
| **8** | Server-Grundlage | Betriebsbereiter Server, Konten, Geräteregistrierung | 2–4 h |
| **9** | Datensynchronisation | Datenaustausch mit sichtbarer Konflikterkennung | 2–3 h |
| **10** | Dateisynchronisation | Fotos und Pläne fortsetzbar übertragen | 2 h |
| **11** | MVP-Integration | Durchgängiger Ablauf Android ↔ Windows | 3–4 h |
| **B** | **Meilenstein B: MVP-Abnahme und Praxistest** | Freigabe für den internen Praxistest | nach Bedarf |

Die Schätzungen sind Richtwerte, keine Zusagen.

---

## Phase V – Vorbereitung

**Ziel:** Alles bereitstellen, was Phase 0 für aussagekräftige Messungen braucht.

**Deine Aufgaben:**

1. **Android-Referenzgerät** benennen: Hersteller, Modell, Arbeitsspeicher (RAM), Android-Version. Es sollte ein typisches Baustellengerät sein, kein Spitzenmodell.
2. **Windows-Referenz-PC** benennen: Windows-Version, Prozessor, Arbeitsspeicher.
3. **Beispielpläne** auf beiden Geräten bereitlegen, gegebenenfalls anonymisiert:
   - mindestens ein großformatiger Plan (möglichst A0, möglichst groß in MB),
   - mindestens ein mehrseitiger Plan.
4. **Aktuelle Dokumentationsvorlage** bereitlegen. Ist sie vollständig anonymisiert (keine Kunden-, Projekt- oder Personendaten), kann sie nach deiner Freigabe ins Repository übernommen werden. Andernfalls genügt eine Beschreibung oder ein Bildschirmfoto des Aufbaus.
5. Android: Installation von Apps aus unbekannten Quellen für den Testzeitraum erlauben. Die Checkliste in Phase 0.1 erklärt, wie das geht.

**Wichtig:** Reale Pläne, Fotos und Vorlagen werden **nicht** ins Repository übernommen (Masterkonzept, Abschnitt 17). Für automatisierte Tests erzeugt Claude Code künstliche Testdaten. Dazu gehören ein künstlicher A0-Plan mit ca. 50 MB und künstliche Fotos in 12-Megapixel-Größe.

**Abnahmekriterien:**

- [ ] Referenzgeräte sind mit Modell und Kenndaten in `docs/referenzgeraete.md` dokumentiert.
- [ ] Mindestens ein realer großer Plan und ein mehrseitiger Plan liegen auf beiden Referenzgeräten bereit.
- [ ] Die Dokumentationsvorlage oder eine Beschreibung ihres Aufbaus liegt vor.

---

## Phase 0 – Technischer Machbarkeitstest

**Ziel:** Vor der eigentlichen Entwicklung belastbar klären, ob die vorgesehenen Bibliotheken auf **Windows und Android** die Anforderungen erfüllen. Wo nicht, wird eine Alternative ermittelt.

**Grundsätze:**

- Der Prototyp liegt im Ordner `prototype/` und ist ein **Wegwerf-Prototyp**. Sein Code wird **nicht** in die eigentliche App übernommen, nur die Erkenntnisse.
- Alle Leistungswerte in dieser Phase sind **Testziele**, keine bestätigten Leistungsversprechen. Wird ein Testziel verfehlt, ist die Phase nicht automatisch gescheitert. Das Ergebnis wird bewertet und eine Gegenmaßnahme oder Alternative vorgeschlagen.
- Der Prototyp misst selbst und zeigt die Ergebnisse in einem Bildschirm **„Messprotokoll"** an. Du kannst sie als Text kopieren oder als Datei exportieren und zurückmelden. Du musst nichts selbst messen oder berechnen.
- Jeder Teilschritt wird einzeln getestet und abgenommen.

**Zu prüfende Kandidaten:** `pdfrx`, `drift` mit SQLCipher, `flutter_secure_storage`, `pdf` sowie ein Verfahren zur Dateiverschlüsselung (Kandidat: AES-256-GCM, abschnittsweise).

**Nicht enthalten:** Benutzerführung, Design, Fachlogik, Synchronisation, Server.

### Phase 0.1 – Build-Pipeline und Messrahmen

**Umfang:**
- Minimale Flutter-App im Ordner `prototype/`.
- GitHub Actions erzeugt automatisch eine Android-APK und ein Windows-ZIP.
- Ein Messprotokoll-Bildschirm zeigt Gerätedaten, App-Version und Messergebnisse an und kann sie exportieren.

**Abnahmekriterien:**

*Automatisiert:*
- [ ] Der GitHub-Actions-Lauf ist für Android und Windows erfolgreich und stellt beide Testversionen zum Download bereit.

*Auf deinen Geräten:*
- [ ] Die APK lässt sich auf dem Android-Referenzgerät installieren und starten.
- [ ] Die Windows-Version lässt sich auf dem Referenz-PC entpacken und starten. Ein eventueller SmartScreen-Hinweis wegen fehlender Signatur ist erwartet und in der Checkliste erklärt.
- [ ] Das Messprotokoll zeigt Gerätemodell, Betriebssystemversion und App-Version korrekt an und lässt sich exportieren.

**Dein Aufwand:** ca. 1 h

### Phase 0.2 – Verschlüsselte Datenbank und Schlüsselverwaltung

**Umfang:**
- `drift` mit SQLCipher auf Windows und Android.
- Ein zufällig erzeugter Datenbankschlüssel wird mit `flutter_secure_storage` gespeichert (Android Keystore bzw. Windows-Anmeldeinformationsspeicher).
- Ein Testdatenerzeuger legt einen Bestand in Auslegungsgröße an: 25 Projekte × 500 Tickets = 12.500 Tickets.

**Abnahmekriterien:**

*Automatisiert:*
- [ ] Die Datenbankdatei enthält keinen lesbaren SQLite-Dateikopf und keine im Klartext auffindbaren Testinhalte.
- [ ] Öffnen der Datenbank ohne oder mit falschem Schlüssel schlägt kontrolliert fehl, ohne die Datei zu verändern.
- [ ] Ein Schreibvorgang, der mitten in der Transaktion abbricht, hinterlässt die Datenbank im vorherigen konsistenten Zustand.

*Auf deinen Geräten (Testziele, jeweils im Messprotokoll):*
- [ ] Die Verschlüsselung funktioniert auf **beiden** Plattformen. Das ist ein **Pflichtkriterium**, kein Testziel.
- [ ] Nach Beenden und Neustart der App sind alle Daten wieder lesbar (Schlüssel wird korrekt aus dem Schlüsselspeicher geladen). **Pflichtkriterium.**
- [ ] Testziel: Erzeugen von 12.500 Tickets ≤ 60 s.
- [ ] Testziel: Laden der Ticketliste eines Projekts (500 Tickets) ≤ 200 ms.
- [ ] Testziel: Suche nach einer Ticketnummer im Gesamtbestand ≤ 200 ms.
- [ ] Das Verhalten nach Deinstallation und Neuinstallation ist beobachtet und dokumentiert. Erwartet: Alte Daten sind ohne Backup nicht mehr zugänglich.

*Zu dokumentieren:* verwendete SQLCipher-Version, Lizenzbedingungen und Auswirkung auf die App-Größe.

**Dein Aufwand:** ca. 1 h

### Phase 0.3 – Dateiverschlüsselung

**Umfang:**
- Abschnittsweise authentifizierte Verschlüsselung großer Dateien (Kandidat: AES-256-GCM in festen Blöcken).
- Ein SHA-256-Prüfwert wird über die unverschlüsselte Originaldatei berechnet.
- Lesender Zugriff auf einzelne Abschnitte ohne vollständiges Entschlüsseln.

**Abnahmekriterien:**

*Automatisiert:*
- [ ] Verschlüsseln und anschließendes Entschlüsseln ergibt eine **bitgenau identische** Datei. Der Test läuft mit Dateien von 0 Byte, 1 Byte, Blockgrenze ± 1 Byte und 50 MB.
- [ ] Der SHA-256-Prüfwert der entschlüsselten Datei stimmt mit dem beim Import berechneten Prüfwert überein.
- [ ] Ein verändertes Byte, ein vertauschter Block und eine abgeschnittene Datei werden jeweils **erkannt** und als Fehler gemeldet. Es werden keine falschen Daten geliefert.
- [ ] Während Import und Anzeige entstehen keine unverschlüsselten Kopien in temporären Verzeichnissen.

*Auf deinen Geräten (Testziele):*
- [ ] Testziel: Import und Verschlüsselung einer 50-MB-Datei ≤ 5 s auf dem Android-Referenzgerät, ≤ 2 s auf dem Windows-Referenz-PC.
- [ ] Testziel: Import von 20 Fotos à 12 Megapixel (Kamera oder Galerie) ≤ 20 s auf dem Android-Referenzgerät.
- [ ] Bei einem realen Foto stimmt der Prüfwert nach dem Entschlüsseln mit dem Prüfwert der Originaldatei überein. Der Prototyp zeigt beide Werte an.

**Dein Aufwand:** ca. 1 h

### Phase 0.4 – Plandarstellung und Markierungen

**Umfang:**
- Darstellung realer und künstlicher Pläne mit `pdfrx`.
- Die Pläne werden **aus der verschlüsselten Ablage** geöffnet.
- Markierungen werden in PDF-Seitenkoordinaten gesetzt, angezeigt und gespeichert.
- Der Prototyp misst die Bildrate während Zoomen und Verschieben selbst.

**Abnahmekriterien:**

*Automatisiert:*
- [ ] Die Umrechnung zwischen Bildschirm- und PDF-Seitenkoordinaten ist für Zoomstufen von 0,1× bis 20× und unterschiedliche Bildschirmgrößen und -ausrichtungen umkehrbar. Die Abweichung beträgt höchstens 0,5 PDF-Punkte.
- [ ] Gespeicherte Markierungskoordinaten sind nach dem Speichern und erneuten Laden exakt identisch.

*Auf deinen Geräten:*
- [ ] **Pflichtkriterium:** Der reale große Plan und der mehrseitige Plan lassen sich auf beiden Plattformen öffnen und vollständig darstellen.
- [ ] **Pflichtkriterium (Sichtprüfung):** Du setzt 10 Markierungen auf klar erkennbare Planpunkte, z. B. Wandecken. Danach schließt du die App, öffnest sie erneut, wählst eine andere Zoomstufe und drehst das Gerät. Alle Markierungen sitzen weiterhin auf denselben Planpunkten.
- [ ] Testziel: Die erste Seite des 50-MB-A0-Plans ist ≤ 5 s nach dem Öffnen sichtbar (Android-Referenzgerät).
- [ ] Testziel: Bei einer standardisierten 30-sekündigen Zoom- und Verschiebe-Sequenz werden mindestens 90 % der Einzelbilder in ≤ 33 ms dargestellt (entspricht etwa 30 Bildern pro Sekunde).
- [ ] Testziel: Mit 500 Markierungen auf einer Planseite wird das vorige Bildraten-Ziel weiterhin erreicht.
- [ ] Testziel: Der Seitenwechsel in einem mehrseitigen Plan dauert ≤ 2 s.
- [ ] Dreimaliges Öffnen und Schließen des großen Plans hintereinander führt zu keinem Absturz. Der maximale Speicherverbrauch wird im Messprotokoll ausgewiesen.

**Dein Aufwand:** ca. 1–2 h

### Phase 0.5 – PDF-Berichterstellung

**Umfang:**
- Erzeugung eines umfangreichen Berichts mit `pdf` nach dem groben Aufbau deiner realen Vorlage.
- Testbestand: 300 Tickets mit zusammen 1.000 Fotos à 12 Megapixel (künstlich erzeugt), dazu ein Planausschnitt mit Markierungen.
- Im Bericht werden verkleinerte Ableitungen der Fotos verwendet. Die Originale bleiben unverändert.
- Die Erstellung läuft im Hintergrund mit Fortschrittsanzeige und Abbruchmöglichkeit.

**Abnahmekriterien:**

*Automatisiert:*
- [ ] Der erzeugte Bericht ist ein gültiges PDF und enthält alle 300 Tickets und 1.000 Fotos (Zählprüfung).
- [ ] Die Prüfwerte aller Originalfotos sind nach der Berichtserstellung unverändert.
- [ ] Fehlende Pflichtangaben erscheinen im Bericht deutlich als „fehlt" und werden nicht durch Ersatzwerte gefüllt.

*Auf deinen Geräten:*
- [ ] **Pflichtkriterium:** Die Berichtserstellung läuft auf beiden Referenzgeräten ohne Absturz bis zum Ende.
- [ ] **Pflichtkriterium:** Während der Erstellung bleibt die App bedienbar, der Fortschritt ist sichtbar und ein Abbruch ist möglich.
- [ ] Der Bericht lässt sich in einem gängigen PDF-Betrachter (z. B. Adobe Acrobat Reader) öffnen und fehlerfrei durchblättern.
- [ ] Testziel: Erstellungsdauer ≤ 10 min auf dem Android-Referenzgerät und ≤ 5 min auf dem Windows-Referenz-PC.
- [ ] Testziel: Dateigröße des Berichts ≤ 300 MB, bei weiterhin gut erkennbaren Fotos (Sichtprüfung durch dich).
- [ ] Der maximale Speicherverbrauch während der Erstellung wird im Messprotokoll ausgewiesen.

*Falls Testziele verfehlt werden,* wird eine Gegenmaßnahme bewertet, z. B. Aufteilung in mehrere Teildokumente, seitenweises Schreiben oder eine alternative Bibliothek.

**Dein Aufwand:** ca. 1–2 h

### Phase 0.6 – Backup, Wiederherstellung und Schlüsselverlust

**Umfang:**
- Erstellen einer Sicherungsdatei mit Datenbank, Plänen und Fotos. Die Datei ist durch ein **Wiederherstellungskennwort** geschützt, also unabhängig vom Geräteschlüssel.
- Wiederherstellung auf einer **anderen** Installation, auch plattformübergreifend von Android nach Windows.
- Erprobung der Regel „wiederhergestellte Installation erhält ein neues Gerätekürzel" (Masterkonzept, Abschnitt 9.1).

**Abnahmekriterien:**

*Automatisiert:*
- [ ] Nach der Wiederherstellung stimmen Anzahl der Datensätze und **alle** SHA-256-Prüfwerte der Dateien mit dem Ausgangsbestand überein.
- [ ] Ein falsches Wiederherstellungskennwort führt zu einer verständlichen Fehlermeldung, ohne vorhandene Daten zu verändern.
- [ ] Eine beschädigte oder abgeschnittene Sicherungsdatei wird erkannt und nicht teilweise eingespielt.
- [ ] Nach einer Wiederherstellung führt das Anlegen von 1.000 neuen Tickets zu keiner Ticketnummer, die im Ausgangsbestand schon vergeben war.

*Auf deinen Geräten:*
- [ ] **Pflichtkriterium:** Eine auf dem Android-Referenzgerät erstellte Sicherung lässt sich auf dem Windows-Referenz-PC vollständig wiederherstellen. Plan und Fotos werden dort korrekt angezeigt.
- [ ] Testziel: Die Sicherung eines Projekts mit 1 großem Plan und 200 Fotos dauert ≤ 3 min auf dem Android-Referenzgerät.

**Dein Aufwand:** ca. 1–2 h

### Phase 0.7 – Ergebnisbericht und Technikentscheidung

**Umfang:**
- `docs/phase0-ergebnis.md` mit allen Messwerten je Plattform und einer Bewertung je Kandidat (geeignet / eingeschränkt geeignet / ungeeignet).
- Bei Bedarf Empfehlung von Alternativen und Gegenmaßnahmen.
- Verbindliche Festlegung des Dateiverschlüsselungsverfahrens, der Schlüsselablage, des Wiederherstellungsverfahrens und der Detailregel für Gerätekürzel nach einer Wiederherstellung.
- Aktualisierung der offenen Punkte im Masterkonzept (Abschnitt 23) und Fortschreibung dieses Phasenplans.

**Abnahmekriterien:**
- [ ] Für jeden Kandidaten liegt eine begründete Bewertung mit Messwerten von **beiden** Plattformen vor.
- [ ] Alle Pflichtkriterien aus 0.1–0.6 sind erfüllt, oder es ist eine geprüfte Alternative festgelegt.
- [ ] Verfehlte Testziele sind mit Ursache und Gegenmaßnahme dokumentiert.
- [ ] Du hast den Bericht gelesen und die Technikentscheidung ausdrücklich freigegeben.

**Dein Aufwand:** ca. 1 h (Lesen und Rückfragen)

---

## Phase 1 – App-Grundgerüst

**Ziel:** Eine saubere, getestete Grundlage, auf der alle weiteren Funktionen aufbauen. Der Prototyp-Code wird nicht übernommen.

**Umfang:**
- Neues Flutter-Projekt im Ordner `app/` mit dokumentierter Architektur (Schichten und Module).
- Datenmodell-Grundlagen für die spätere Synchronisation:
  - UUIDs
  - Versionszähler je Datensatz
  - Zeitstempel für Erstellung und Änderung
  - Änderungsprotokoll
  - Löschvermerke statt physischer Löschung
- Verschlüsselte Datenbank und Dateiablage gemäß Ergebnis von Phase 0.
- Migrationsrahmen für Datenbankänderungen mit automatischer Sicherung vor jeder Migration.
- **Ersteinrichtung:** Benutzername und Gerätekürzel festlegen. Das Kürzel kann danach nicht geändert werden.
- Grundlegendes Erscheinungsbild: Farben, Schriftgrößen, Textskalierung, Offline-Anzeige als Platzhalter.
- Build-Pipeline mit Tests, Code-Analyse und Testversionen für Android und Windows.

**Nicht enthalten:** Fachfunktionen.

**Abnahmekriterien:**

*Automatisiert:*
- [ ] Jede Datenänderung erzeugt einen Eintrag im Änderungsprotokoll mit UUID, Versionszähler, Zeitpunkt und Gerätekürzel.
- [ ] Ein „Löschen" setzt nur einen Löschvermerk, der Datensatz bleibt erhalten.
- [ ] Eine Testmigration von Schemaversion 1 auf 2 erhält alle Daten, und vorher wird eine Sicherung erstellt.
- [ ] Die Testabdeckung der Kernbausteine (Datenhaltung, Verschlüsselung, Nummernvergabe) beträgt mindestens 80 %.

*Auf deinen Geräten:*
- [ ] Die Ersteinrichtung lässt sich auf Android und Windows abschließen. Das Gerätekürzel wird danach angezeigt.
- [ ] Nach einem Neustart erscheint die Ersteinrichtung nicht erneut, und die Angaben bleiben erhalten.
- [ ] Mit größter Systemschriftgröße bleiben alle Texte lesbar und nicht abgeschnitten.

**Dein Aufwand:** ca. 1 h

---

## Phase 2 – Projekte

**Ziel:** Projekte anlegen und verwalten.

**Umfang:**
- Projekt anlegen und bearbeiten mit Projektnummer, Name, Auftraggeber, Adresse, verantwortlicher Person, Status und Terminen.
- Automatische Projektnummer im Format `P<Jahr>-<lfd. Nr.>`, z. B. `P2026-014`. Sie ist bearbeitbar, eine doppelte Vergabe wird lokal verhindert.
- Projektliste mit einfacher Suche nach Nummer oder Name.
- Archivieren und Wiederherstellen.
- Änderungsverlauf je Projekt (einfache Liste).

**Nicht enthalten:** frei konfigurierbare Zusatzfelder, Ordnerstruktur, Favoriten, Projektabschluss, Rechte.

**Abnahmekriterien:**

*Automatisiert:*
- [ ] Projektnummern werden fortlaufend und ohne Doppelungen vergeben, auch nach Archivierung und Löschung.
- [ ] Der Versuch, eine bereits vergebene Projektnummer manuell einzutragen, wird abgewiesen.
- [ ] Archivieren und Wiederherstellen verändert keine Projektinhalte. Ein Vergleich vorher und nachher zeigt keinen Unterschied.

*Auf deinen Geräten:*
- [ ] Du legst 3 Projekte an, bearbeitest eines, archivierst eines und stellst es wieder her. Alle Angaben sind korrekt erhalten.
- [ ] Die Suche findet ein Projekt über einen Teil der Nummer und über einen Teil des Namens.
- [ ] Der Änderungsverlauf zeigt deine Änderungen mit Zeitpunkt.

**Dein Aufwand:** ca. 1–2 h

---

## Phase 3 – Baupläne

**Ziel:** Reale PDF-Pläne sicher importieren und anzeigen.

**Umfang:**
- Import von PDF-Plänen in ein Projekt. Die Ablage erfolgt verschlüsselt, mit SHA-256-Prüfwert der Originaldatei.
- Mehrseitige Pläne: Seitenübersicht, jede Seite einzeln aufrufbar.
- Planansicht mit Zoom und Verschieben.
- Planliste je Projekt mit Name, Seitenzahl, Importdatum und Revision.
- Datenmodell für Planrevisionen. Im MVP ist der Import einer neuen Revision möglich, bestehende Markierungen bleiben der alten Revision zugeordnet. Die Übertragung auf die neue Revision folgt nach dem MVP.

**Nicht enthalten:** Planordner, Revisionsvergleich, Überlagerung, Übertragung von Markierungen.

**Abnahmekriterien:**

*Automatisiert:*
- [ ] Eine importierte Datei lässt sich bitgenau wiederherstellen, und der Prüfwert stimmt.
- [ ] Defekte oder passwortgeschützte PDFs werden mit verständlicher Meldung abgewiesen, ohne dass halbe Datensätze entstehen.
- [ ] Ein Abbruch während des Imports hinterlässt weder Datenbankreste noch Dateireste.

*Auf deinen Geräten:*
- [ ] Deine realen Beispielpläne lassen sich auf beiden Plattformen importieren und anzeigen.
- [ ] Die Ladezeiten und die Bedienung beim Zoomen liegen mindestens auf dem in Phase 0.4 gemessenen Niveau.
- [ ] Im Speicherort der App ist kein lesbares PDF zu finden. Die Checkliste beschreibt die Prüfung.

**Dein Aufwand:** ca. 1–2 h

---

## Phase 4 – Markierungen und Tickets

**Ziel:** Kernablauf der Erfassung: Markierung auf dem Plan setzen → Ticket entsteht.

**Umfang:**
- Markierung durch Antippen bzw. Anklicken setzen. Dabei entsteht sofort ein Ticket im Zustand „Neu" und „unvollständig" (Schnellerfassung).
- Ticketnummer gemäß Masterkonzept 9.1, z. B. `P2026-014 / K3-0042`.
- Ticketarten als feste Liste (Abschnitt 9). Unternehmensspezifische Arten folgen später.
- Grundlegende Ticketangaben: Ticketart, Bauteil (Wand/Decke), Bauteildicke, Feuerwiderstand, Hersteller und System als Freitext, Zulassungsnummer, Durchführungsmedien und Mengen, Bemerkung.
- Status „Neu" und „In Bearbeitung". Die übrigen Status sind im Datenmodell vorgesehen, aber noch nicht bedienbar.
- Kennzeichnung „unvollständig" anhand einer festen Pflichtfeldliste je Ticketart.
- Markierungssymbol je Ticketart, kompakte Vorschau beim Antippen, vollständige Ticketansicht.
- Markierung bewusst verschieben, mit Eintrag im Verlauf.
- Ticketliste je Projekt und Plan mit Filter nach Ticketart und Vollständigkeit.
- Automatisches Zwischenspeichern von Eingaben.

**Nicht enthalten:** Katalog, konfigurierbare Pflichtfelder, Prüfung, Mängel, Sammelaktionen.

**Abnahmekriterien:**

*Automatisiert:*
- [ ] 10.000 nacheinander angelegte Tickets haben 10.000 unterschiedliche Ticketnummern.
- [ ] Ein simulierter Absturz während der Ticketanlage führt nie zu einer doppelten Nummer. Lücken sind zulässig.
- [ ] Gelöschte Tickets geben ihre Nummer nicht frei.
- [ ] Ein Ticket mit fehlenden Pflichtfeldern wird immer als „unvollständig" gekennzeichnet. Kein Ablauf setzt es stillschweigend auf vollständig.
- [ ] Die Markierungsposition bleibt nach Speichern und Laden exakt erhalten.

*Auf deinen Geräten:*
- [ ] Auf deinem realen Plan legst du per Schnellerfassung 20 Tickets an. Jede Markierung sitzt nach dem Neustart an derselben Planstelle.
- [ ] Du vervollständigst 5 Tickets. Danach verschwindet die Kennzeichnung „unvollständig" nur bei diesen.
- [ ] Du beendest die App während einer Eingabe gewaltsam (Android: App aus der Übersicht wischen). Nach dem Neustart ist die Eingabe noch vorhanden.
- [ ] Auf dem Android-Gerät sind alle Bedienelemente mit dem Finger gut treffbar. Das ist eine Sichtprüfung, als Richtwert gilt eine Mindestgröße von 48 × 48 dp.

**Dein Aufwand:** ca. 2–3 h (ggf. in zwei Teilabnahmen: 4a Markierung und Nummer, 4b Ticketangaben)

---

## Phase 5 – Fotos

**Ziel:** Fotos zu Tickets erfassen, unverändert und nachvollziehbar.

**Umfang:**
- Android: Foto direkt mit der Kamera aufnehmen oder aus der Galerie übernehmen.
- Windows: Foto aus einer Datei übernehmen.
- Mehrere Fotos je Ticket.
- Originale werden bitgenau und verschlüsselt gespeichert, mit SHA-256-Prüfwert.
- Erfasst werden Aufnahmezeitpunkt (aus den Bilddaten, soweit vorhanden und als solcher gekennzeichnet), Importzeitpunkt und erfassender Benutzer.
- Vorschaubilder als gekennzeichnete Ableitungen.
- Fotoansicht mit Zoom und Anzeige der Metadaten.

**Nicht enthalten:** Bildbearbeitung, Qualitätsbewertung, Fotos zu Mängeln oder Prüfungen.

**Abnahmekriterien:**

*Automatisiert:*
- [ ] Das gespeicherte Original ist bitgenau identisch mit der Quelldatei, und der Prüfwert stimmt.
- [ ] Ein Foto ohne Aufnahmezeitpunkt in den Bilddaten wird als „Aufnahmezeit unbekannt" gekennzeichnet und nicht mit der Importzeit gleichgesetzt.
- [ ] Das Löschen eines Fotos setzt einen Löschvermerk. Die Datei bleibt bis zur endgültigen Bereinigung erhalten.

*Auf deinen Geräten:*
- [ ] Du nimmst auf Android 10 Fotos zu einem Ticket auf. Alle erscheinen mit korrektem Aufnahmezeitpunkt.
- [ ] Du überträgst ein Foto per Export auf den PC. Sein Prüfwert stimmt mit dem in der App angezeigten Wert überein. Die Checkliste erklärt, wie das ohne Programmierkenntnisse geht.
- [ ] Die Fotos des Tickets sind nicht in der allgemeinen Galerie des Android-Geräts sichtbar.

**Dein Aufwand:** ca. 1–2 h

---

## Phase 6 – PDF-Bericht

**Ziel:** Ein erster verwendbarer Bericht nach dem Aufbau deiner Unternehmensvorlage.

**Umfang:**
- Bericht je Projekt oder je Plan mit:
  - Kopf mit Firmenlogo, Adresse und Projektdaten
  - Planübersicht mit nummerierten Markierungen
  - Ticketliste
  - Ticketseiten mit Angaben und Fotos
- Fehlende Angaben werden deutlich als „fehlt" ausgewiesen. Unvollständige Tickets werden gesondert aufgeführt.
- Fußzeile mit Erstellungszeitpunkt, Datenstand, verwendeter Planrevision und App-Version.
- Vorschau vor dem Speichern; Speichern bzw. Teilen der PDF-Datei.
- Erstellung im Hintergrund mit Fortschrittsanzeige und Abbruch.
- Ablage jedes erzeugten Berichts als **unveränderliche Version** mit Verweis auf den zugrunde liegenden Datenstand.

**Nicht enthalten:** Vorlageneditor, Übereinstimmungserklärungen und weitere Dokumentarten, Projektpakete.

**Abnahmekriterien:**

*Automatisiert:*
- [ ] Der Bericht enthält genau die ausgewählten Tickets und Fotos (Zählprüfung).
- [ ] Jede fehlende Pflichtangabe erscheint im Bericht als „fehlt". Es gibt keine Ersatz- oder Platzhalterwerte.
- [ ] Wird ein Ticket nach der Berichtserstellung geändert, bleibt der bereits erzeugte Bericht unverändert. Sein Prüfwert bleibt gleich.
- [ ] Markierungsnummern in der Planübersicht stimmen mit den Ticketseiten überein.

*Auf deinen Geräten:*
- [ ] Du erzeugst einen Bericht zu deinem Testprojekt aus Phase 4/5 auf Android und auf Windows. Er entspricht inhaltlich und im Aufbau deiner Vorlage, soweit im Umfang vorgesehen.
- [ ] Der Bericht öffnet sich fehlerfrei in einem gängigen PDF-Betrachter. Die Fotos sind gut erkennbar.
- [ ] Die Erstellungsdauer liegt im Rahmen der in Phase 0.5 ermittelten Werte.

**Dein Aufwand:** ca. 2–3 h

---

## Phase 7 – Backup und Wiederherstellung

**Ziel:** Kein Datenverlust durch Gerätedefekt, Deinstallation oder Fehlbedienung. Das ist Voraussetzung für den Einsatz mit Echtdaten.

**Umfang:**
- Manuelle Sicherung und automatische Sicherung, z. B. täglich beim App-Start, mit einstellbarer Anzahl aufbewahrter Sicherungen.
- Schutz durch Wiederherstellungskennwort gemäß dem in Phase 0.7 festgelegten Verfahren.
- Wiederherstellung, auch auf einem anderen Gerät und plattformübergreifend.
- Integritätsprüfung einer Sicherung ohne Wiederherstellung („Sicherung prüfen").
- Neues Gerätekürzel nach einer Wiederherstellung.
- Warnung bei knappem Speicherplatz. Es werden keine Daten automatisch gelöscht.

**Abnahmekriterien:**

*Automatisiert:*
- [ ] Sicherung und Wiederherstellung erhalten alle Datensätze, den Änderungsverlauf und alle Dateien mit identischen Prüfwerten.
- [ ] Beschädigte Sicherungen werden erkannt und nicht teilweise eingespielt.
- [ ] Nach einer Wiederherstellung werden keine bereits vergebenen Ticketnummern erneut vergeben.
- [ ] Eine automatische Sicherung, die durch Beenden der App abbricht, hinterlässt keine als gültig gekennzeichnete, unvollständige Sicherung.

*Auf deinen Geräten:*
- [ ] **Ernstfallprobe:** Du sicherst dein Testprojekt auf Android, deinstallierst die App, installierst sie neu und stellst die Sicherung wieder her. Alle Tickets, Markierungen, Fotos und Berichte sind vorhanden.
- [ ] Du stellst dieselbe Sicherung auf dem Windows-PC wieder her. Der Inhalt ist identisch.
- [ ] „Sicherung prüfen" meldet bei einer intakten Sicherung Erfolg.

**Dein Aufwand:** ca. 2 h

---

## Meilenstein A – Einzelgerät-Funktionstest

**Ziel:** Der MVP-Kernablauf (Masterkonzept, Abschnitt 22, Schritte 1–7) wird an einem echten, kleinen Projekt auf **einem** Gerät erprobt.

**Ablauf:**
- Zeitraum 1–2 Wochen.
- Echtes oder realitätsnahes Kleinprojekt mit mindestens 1 realem Plan, 30 Tickets und 60 Fotos.
- Mindestens eine wöchentliche Sicherung.
- Am Ende ein Bericht nach Unternehmensvorlage.
- Rückmeldungen sammelst du formlos (Stichpunkte genügen). Claude Code wertet sie aus und ordnet sie ein: Fehler, Verbesserung oder später.

**Abnahmekriterien:**
- [ ] Im Testzeitraum ist kein Datenverlust aufgetreten.
- [ ] Der erzeugte Bericht ist inhaltlich korrekt. Das prüfst du stichprobenartig an 10 Tickets.
- [ ] Alle als „kritisch" eingestuften Rückmeldungen sind behoben.
- [ ] Du entscheidest ausdrücklich, ob die Serverphase beginnen kann oder zuerst Verbesserungen umgesetzt werden.

---

## Phase 8 – Server-Grundlage

**Ziel:** Ein selbst betriebener, abgesicherter Server als Grundlage der Synchronisation.

**Vorab zu klären (vor Beginn der Phase, mit deiner Entscheidung):**
- Hosting: eigener Server oder angemieteter Server bei einem deutschen Anbieter.
- Wer betreibt den Server, wer ist bei Ausfällen zuständig?
- Domain, TLS-Zertifikat, Erreichbarkeit von Baustellen (direkt über das Internet oder per VPN).
- Server-Technologie: Claude Code legt dazu zu Beginn der Phase eine begründete Empfehlung vor.
- Backupziel für Serversicherungen.

**Hinweis des Partners:** Der Serverbetrieb ist der Teil mit dem höchsten dauerhaften Aufwand und Risiko, gerade bei unter 5 Stunden pro Woche. Vor Beginn dieser Phase sollte entschieden werden, ob ein Dienstleister oder eine kundige Person den Grundbetrieb (Updates, Überwachung) übernimmt. Claude Code liefert in jedem Fall eine vollständige Schritt-für-Schritt-Betriebsdokumentation und weitgehend automatisierte Einrichtung.

**Umfang:**
- Serveranwendung mit Datenbank, Bereitstellung als Container mit dokumentierter, wiederholbarer Einrichtung.
- Benutzerkonten mit Anmeldung, nur verschlüsselte Verbindungen (TLS).
- Geräteregistrierung mit ausdrücklicher Freigabe durch einen Administrator.
- **Zentrale Vergabe der Gerätekürzel** mit Register aller je vergebenen Kürzel. Bereits vorhandene Einzelgerät-Kürzel werden übernommen.
- Automatische Serversicherungen, mehrmals täglich, verschlüsselt, mit externer Kopie und dokumentiertem Wiederherstellungstest.
- Einfache Statusseite und Protokollierung sicherheitsrelevanter Vorgänge.

**Abnahmekriterien:**

*Automatisiert:*
- [ ] Anfragen ohne gültige Anmeldung oder von nicht freigegebenen Geräten werden abgewiesen.
- [ ] Ein Gerätekürzel wird nie doppelt vergeben, auch nicht bei gleichzeitigen Registrierungen.
- [ ] Unverschlüsselte Verbindungen (HTTP) werden nicht angenommen.

*Durch dich bzw. den Serverbetreuer:*
- [ ] Der Server lässt sich anhand der Dokumentation auf einer frischen Maschine einrichten.
- [ ] Ein Android-Gerät und ein Windows-PC lassen sich registrieren. Erst nach Freigabe durch den Administrator erhalten sie Zugriff.
- [ ] **Wiederherstellungstest:** Eine Serversicherung wird auf einer frischen Maschine eingespielt, danach ist die Anmeldung wieder möglich.

**Dein Aufwand:** ca. 2–4 h, abhängig von der Hosting-Entscheidung

---

## Phase 9 – Datensynchronisation

**Ziel:** Datensätze (Projekte, Pläne als Metadaten, Markierungen, Tickets, Fotos als Metadaten, Berichte als Metadaten) werden zwischen Geräten ausgetauscht – **ohne stilles Überschreiben**.

**Umfang:**
- Hochladen lokaler Änderungen und Abrufen fremder Änderungen, automatisch im Hintergrund und manuell auslösbar.
- **Versionsprüfung:** Jede Änderung trägt den Versionsstand, auf dem sie beruht. Weicht der Serverstand ab, entsteht ein **Konflikt**.
- **Konflikte:** Beide Zustände bleiben vollständig erhalten. Der Konflikt erscheint in einer Konfliktliste und am betroffenen Ticket.
- Löschvermerke werden synchronisiert. Ein Löschvermerk auf einen anderswo geänderten Datensatz gilt ebenfalls als Konflikt.
- Synchronisationsstatus: letzte erfolgreiche Synchronisation, Anzahl ausstehender Änderungen, Fehler mit verständlicher Meldung.
- Abbrüche, etwa durch Funkloch, führen nie zu einem halb übertragenen Zustand. Die Übertragung wird beim nächsten Versuch fortgesetzt.

**Nicht enthalten:** Konfliktauflösung (folgt in Phase 11), feldweises Zusammenführen, projektbezogene Rechte.

**Abnahmekriterien:**

*Automatisiert (mit simuliertem Server und mehreren simulierten Geräten):*
- [ ] Zwei Geräte ändern offline dasselbe Ticket. Nach der Synchronisation existiert ein Konflikt, und **beide** Zustände sind vollständig abrufbar.
- [ ] Ein Zufallstest mit mindestens 1.000 zufälligen Operationen auf 3 Geräten mit zufälligen Verbindungsabbrüchen führt zu **keinem verlorenen Änderungsstand**. Jeder Zustand ist entweder übernommen oder als Konflikt erhalten.
- [ ] Ein Verbindungsabbruch an jeder möglichen Stelle des Ablaufs hinterlässt Gerät und Server in einem konsistenten Zustand.
- [ ] Ticketnummern bleiben über alle Geräte hinweg eindeutig.

*Auf deinen Geräten:*
- [ ] Ein auf Android angelegtes Ticket erscheint nach der Synchronisation auf dem Windows-PC und umgekehrt.
- [ ] **Konfliktprobe:** Du schaltest beide Geräte offline und änderst dasselbe Ticket unterschiedlich. Nach dem erneuten Verbinden wird der Konflikt auf beiden Geräten angezeigt, und beide Fassungen sind einsehbar.
- [ ] Im Flugmodus angezeigte ausstehende Änderungen werden nach dem Wiederverbinden übertragen. Die Anzeige geht danach auf 0.

**Dein Aufwand:** ca. 2–3 h

---

## Phase 10 – Dateisynchronisation

**Ziel:** Pläne, Fotos und Berichte zuverlässig zwischen Geräten übertragen.

**Umfang:**
- Fortsetzbares Hoch- und Herunterladen großer Dateien in Abschnitten.
- Eine Datei gilt erst nach erfolgreicher **Prüfwertkontrolle** als vollständig übertragen.
- Dateien sind über ihren Prüfwert identifiziert. Dieselbe Datei wird nicht doppelt übertragen.
- Projekte werden gezielt für die Offline-Nutzung heruntergeladen. Lokale Projektkopien lassen sich entfernen, ohne zentrale Daten zu löschen.
- Vor großen Downloads wird der Speicherplatz geprüft und bei Knappheit gewarnt.
- Fortschrittsanzeige je Projekt.

**Abnahmekriterien:**

*Automatisiert:*
- [ ] Eine Übertragung, die an zufälligen Stellen unterbrochen wird, wird fortgesetzt und endet mit identischem Prüfwert, ohne von vorn zu beginnen.
- [ ] Eine während der Übertragung beschädigte Datei wird erkannt und nicht als vollständig gekennzeichnet.
- [ ] „Lokale Kopie entfernen" löscht keine Daten auf dem Server.

*Auf deinen Geräten:*
- [ ] Du lädst dein Testprojekt mit realem Plan und mindestens 60 Fotos auf den Windows-PC herunter. Plan, Fotos und Berichte sind vollständig.
- [ ] Du unterbrichst einen laufenden Download, z. B. mit dem Flugmodus. Nach dem Wiederverbinden wird er fortgesetzt und erfolgreich abgeschlossen.
- [ ] Nach „Lokale Kopie entfernen" und erneutem Herunterladen ist das Projekt wieder vollständig.

**Dein Aufwand:** ca. 2 h

---

## Phase 11 – MVP-Integration

**Ziel:** Den vollständigen MVP-Ablauf (Masterkonzept, Abschnitt 22) über Android und Windows hinweg zusammenführen und absichern.

**Umfang:**
- Einfache Konfliktauflösung: bewusste Auswahl einer Fassung. Die andere bleibt im Verlauf erhalten.
- Durchgängiger Ablauf: Projekt am PC anlegen, Plan importieren, synchronisieren, auf der Baustelle mit Android markieren und fotografieren, synchronisieren, Bericht am PC erzeugen.
- Überarbeitung von Fehlermeldungen und Statusanzeigen anhand der bisherigen Rückmeldungen.
- MVP-Abnahmecheckliste für Windows, Android, Offlinebetrieb, Synchronisation, Backups und PDF-Export.

**Abnahmekriterien:**

*Automatisiert:*
- [ ] Ein automatisierter Durchlauf des gesamten Ablaufs mit zwei simulierten Geräten ist erfolgreich.
- [ ] Nach einer Konfliktauflösung ist die nicht gewählte Fassung im Verlauf vollständig abrufbar.
- [ ] Alle automatisierten Tests aus Phase 1–10 sind weiterhin erfolgreich.

*Auf deinen Geräten:*
- [ ] Der durchgängige Ablauf gelingt mit realem Plan und Fotos ohne Hilfe.
- [ ] Eine Baustellen-Simulation gelingt: Android 1 Stunde offline, 10 Tickets mit Fotos, danach Synchronisation. Am PC ist alles vollständig vorhanden.
- [ ] Ein Konflikt lässt sich verständlich auflösen.
- [ ] Die MVP-Abnahmecheckliste ist vollständig und ohne kritische Befunde abgearbeitet.

**Dein Aufwand:** ca. 3–4 h

---

## Meilenstein B – MVP-Abnahme und interner Praxistest

**Voraussetzungen:**
- [ ] Phase 11 ist abgenommen.
- [ ] Datenschutz- und Aufbewahrungsregeln für den Einsatz mit Echtdaten sind geklärt (Masterkonzept, Abschnitt 23).
- [ ] Serversicherung und Wiederherstellung sind mindestens einmal erfolgreich getestet.

**Ergebnis:** Freigabe für einen begrenzten internen Praxistest mit ausgewählten Mitarbeitern. Danach folgt die Planung der Phasen nach dem MVP auf Grundlage der Praxiserfahrungen: Katalog, Prüfabläufe, Mängel, Aufgaben, Rollen und Rechte, externe Firmen, vollständige Konfliktauflösung und iOS.

---

## 4. Wichtigste Risiken

| Risiko | Auswirkung | Gegenmaßnahme |
|---|---|---|
| SQLCipher lässt sich unter Windows nicht zuverlässig einbinden | Kein verschlüsselter Datenbestand auf dem PC | Prüfung in Phase 0.2; Alternativen bewerten |
| Große Pläne laufen auf Mittelklasse-Android-Geräten nicht flüssig | Schlechte Baustellentauglichkeit | Messung in Phase 0.4; ggf. Kachel-Zwischenspeicher oder Mindestanforderungen an Geräte |
| Umfangreiche Berichte überschreiten den Arbeitsspeicher | Absturz bei großen Projekten | Messung in Phase 0.5; Aufteilung in Teildokumente |
| Schlüsselverlust macht lokale Daten unlesbar | Datenverlust vor Einführung des Servers | Kennwortgeschützte Backups (Phase 0.6 / 7) als Pflicht vor Echtdaten |
| Serverbetrieb übersteigt die verfügbare Zeit | Ausfälle, fehlende Updates | Entscheidung über Betreuung vor Phase 8 |
| Begrenzte Testzeit verzögert Abnahmen | Längere Gesamtdauer | Kleine Teilschritte, Messwerte automatisch von der App ermittelt |
| Unsignierte Testversionen lösen Sicherheitswarnungen aus | Verunsicherung beim Testen | Erklärung in den Checklisten; Signierung vor dem Praxistest prüfen |

## 5. Freigabe

| | |
|---|---|
| Phasenplan freigegeben am | _______________ |
| Durch | _______________ |
| Anmerkungen | _______________ |

Phase 0 beginnt erst nach dieser Freigabe.

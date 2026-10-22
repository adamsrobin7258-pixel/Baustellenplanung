# Phasenplan – Brandschutz-Dokumentationssoftware

| | |
|---|---|
| **Status** | Entwurf, 1. Überarbeitung – wartet auf Freigabe |
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
5. Du installierst die Testversion, arbeitest die Checkliste ab und meldest Ergebnisse, Messwerte und Fehler zurück – **ohne vertrauliche Projektinhalte** (siehe 2.5).
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
- [ ] Datenbankänderungen sind als getestete Migration umgesetzt (ab Phase 2). Sie nutzen den Migrationsrahmen aus Phase 1, also eine geprüfte Sicherung vor der Migration (Masterkonzept 15.4). Automatisierte Tests belegen für jede neue Migration:
  - Die Daten des vorherigen Stands bleiben erhalten.
  - Bei fehlgeschlagener Sicherung findet keine Migration statt.
  - Eine unterbrochene Migration wird wiederhergestellt.
- [ ] Repository, Testprotokolle, Logs, Screenshots und GitHub-Actions-Artefakte enthalten keine vertraulichen Projektinhalte (2.5). Nachweis:
  - Eine automatische Prüfung in GitHub Actions weist PDF-, Bild- und Office-Dateien außerhalb der Ordner für künstliche Testdaten zurück.
  - Dazu kommt eine Sichtprüfung der eingereichten Protokolle.

### 2.4 Schnitt der Phasen

Weil dir weniger als 5 Stunden pro Woche zur Verfügung stehen, ist jede Phase so geschnitten, dass Test und Abnahme **in der Regel 1–3 Stunden** dauern. Größere Phasen sind in Teilschritte zerlegt, die einzeln abgenommen werden.

### 2.5 Vertrauliche Daten (verbindlich, Masterkonzept 17.1)

- Echte Pläne, Fotos und Dokumentationsvorlagen werden **niemals** ins Repository übernommen – **auch nicht anonymisiert**. Es gibt keine Ausnahme.
- Automatisierte Tests verwenden **ausschließlich künstlich erzeugte Daten**. Dazu gehören ein künstlicher A0-Plan mit ca. 50 MB, künstliche 12-Megapixel-Fotos und eine künstliche Nachbildung der Vorlage mit Fantasiedaten.
- Echte Testunterlagen bleiben **lokal auf den freigegebenen Testgeräten** (Referenzgeräte, siehe Phase V).
- **Testprotokolle, Logs, Messprotokolle, Screenshots und GitHub-Actions-Artefakte** enthalten keine vertraulichen Inhalte. Dazu zählen Projekt-, Datei- und Kundennamen, Adressen, Personendaten sowie Plan- oder Fotoausschnitte.
  - Messprotokolle enthalten nur technische Kennwerte wie Dateigröße, Seitenzahl, Seitenformat und Zeiten.
  - Screenshots für Fehlermeldungen werden nur mit künstlichen Testdaten angefertigt.
- Deine Rückmeldungen an Claude Code enthalten ebenfalls keine vertraulichen Inhalte.

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
| **7** | Backup und Wiederherstellung | Datensicherung ohne Datenverlust; Pflichtvoraussetzungen für Pilotbetrieb | 2–3 h |
| **A** | **Meilenstein A: Einzelgerät-Funktionstest** | Echtes Kleinprojekt auf einem Gerät | 2–4 h verteilt |
| **8** | Server-Grundlage (erst nach geklärter Betriebsverantwortung) | Betriebsbereiter Server, Konten, Geräteregistrierung | 2–4 h |
| **9** | Datensynchronisation | Datenaustausch mit sichtbarer Konflikterkennung | 2–3 h |
| **10** | Dateisynchronisation | Fotos und Pläne fortsetzbar übertragen | 2 h |
| **11** | MVP-Integration | Durchgängiger Ablauf Android ↔ Windows | 3–4 h |
| **B** | **Meilenstein B: MVP-Abnahme und Praxistest** | Freigabe für den internen Praxistest | nach Bedarf |

Die Schätzungen sind Richtwerte, keine Zusagen.

---

## Phase V – Vorbereitung

**Ziel:** Alles bereitstellen, was Phase 0 für aussagekräftige Messungen braucht.

**Referenzgeräte (festgelegt, Masterkonzept 4.1):**

| Plattform | Gerät |
|---|---|
| Android | Xiaomi 15 Ultra, 16 GB RAM, Android 16 |
| Windows | Windows 11, Intel Core i5-12400, 8 GB RAM |

*Hinweis:* Das Android-Referenzgerät ist ein Oberklassegerät. Alle Android-Messwerte gelten nur für dieses Gerät und sind nicht auf schwächere Geräte übertragbar (siehe Risiken).

**Deine Aufgaben:**

1. **Beispielpläne** lokal auf beiden Referenzgeräten bereitlegen:
   - mindestens ein großformatiger Plan (möglichst A0, möglichst groß in MB),
   - mindestens ein mehrseitiger Plan.
2. **Aktuelle Dokumentationsvorlage** lokal auf beiden Referenzgeräten bereitlegen.
3. Für die künstliche Nachbildung der Vorlage eine **Strukturbeschreibung in eigenen Worten** liefern, ohne vertrauliche Inhalte:
   - Gliederung,
   - Feldbezeichnungen,
   - Reihenfolge,
   - ungefähre Anordnung.

   Daraus erstellt Claude Code eine Nachbildung mit Fantasiedaten. Du vergleichst sie später auf deinem Gerät mit dem Original.
4. Android: Installation von Apps aus unbekannten Quellen für den Testzeitraum erlauben. Die Checkliste in Phase 0.1 erklärt, wie das geht.

**Wichtig:** Echte Pläne, Fotos und Vorlagen werden **niemals** ins Repository übernommen, auch nicht anonymisiert, und auch nicht als Bildschirmfoto (2.5).

**Abnahmekriterien:**

- [x] Die Referenzgeräte sind mit Modell und Kenndaten in diesem Phasenplan und im Masterkonzept (4.1) dokumentiert.
- [ ] Mindestens ein realer großer Plan und ein mehrseitiger Plan liegen lokal auf beiden Referenzgeräten bereit.
- [ ] Die reale Vorlage liegt lokal auf den Referenzgeräten bereit. Die Strukturbeschreibung ohne vertrauliche Inhalte liegt Claude Code vor.

---

## Phase 0 – Technischer Machbarkeitstest

**Ziel:** Vor der eigentlichen Entwicklung belastbar klären, ob die vorgesehenen Bibliotheken auf **Windows und Android** die Anforderungen erfüllen. Wo nicht, wird eine Alternative ermittelt.

**Grundsätze:**

- Der Prototyp liegt im Ordner `prototype/` und ist ein **Wegwerf-Prototyp**. Sein Code wird **nicht** in die eigentliche App übernommen, nur die Erkenntnisse.
  - Mit Daten des Prototyps wird nie echte Dokumentation erstellt. Sie werden nie in die eigentliche App übernommen.
  - Nach Abnahme von Phase 0.7 wird der Ordner `prototype/` aus dem aktuellen Entwicklungsstand entfernt. Er bleibt nur in der Git-Historie erhalten.
- Reale Pläne werden in Phase 0 nur lokal auf den Referenzgeräten angezeigt und vermessen. Das ist **kein** Pilotbetrieb (Masterkonzept 15.5).
- Das Messprotokoll enthält ausschließlich technische Kennwerte, keine Datei- oder Projektnamen und keine Inhalte (2.5).
- Leistungswerte unterscheiden zwei Arten:
  - **Pflichtkriterien** müssen erfüllt sein.
  - **Testziele** sind ausdrücklich so gekennzeichnet. Sie sind keine bestätigten Leistungsversprechen. Wird ein Testziel verfehlt, ist die Phase nicht automatisch gescheitert. Das Ergebnis wird bewertet und eine Gegenmaßnahme oder Alternative vorgeschlagen.
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
- [ ] Die GitHub-Actions-Artefakte enthalten ausschließlich die Testversionen. Die automatische Prüfung auf unzulässige Dateien (2.3) ist eingerichtet und schlägt bei einer absichtlich eingeschleusten Test-PDF außerhalb des Testdatenordners an.

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
- Erzeugung eines umfangreichen Berichts mit `pdf` nach der künstlichen Nachbildung deiner Vorlage (Phase V).
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
- Erstellen einer Sicherungsdatei mit Datenbank, Plänen und Fotos in einem zueinander passenden Stand.
- Erprobung der Schlüsselhinterlegung gemäß Masterkonzept 15.2. Kandidat: Der Sicherungsschlüssel wird doppelt hinterlegt, mit dem Geräteschlüssel und mit einem vom Gerät unabhängigen Wiederherstellungsschlüssel.
- Wiederherstellung auf einer **anderen** Installation **ohne den ursprünglichen Geräteschlüssel**, auch plattformübergreifend von Android nach Windows.
- Erprobung der Ticketnummern-Regeln aus Masterkonzept 9.1:
  - neues Gerätekürzel nach einer Wiederherstellung,
  - Sperre bei unklarer Zählerhistorie.

**Abnahmekriterien:**

*Automatisiert:*
- [ ] Nach der Wiederherstellung stimmen Anzahl der Datensätze und **alle** SHA-256-Prüfwerte der Dateien mit dem Ausgangsbestand überein.
- [ ] **Pflichtkriterium:** Die Wiederherstellung gelingt auf einer frischen Installation, die den ursprünglichen Geräteschlüssel nicht kennt, nur mit dem Wiederherstellungsschlüssel.
- [ ] Ohne Wiederherstellungsschlüssel bzw. mit falschem Schlüssel sind die Inhalte der Sicherungsdatei nicht lesbar. Es gibt eine verständliche Fehlermeldung, und vorhandene Daten bleiben unverändert.
- [ ] Eine beschädigte oder abgeschnittene Sicherungsdatei wird erkannt und nicht teilweise eingespielt.
- [ ] Nach einer Wiederherstellung werden neue Ticketnummern erst nach Zuweisung eines neuen Gerätekürzels vergeben. Das Anlegen von 1.000 neuen Tickets führt zu keiner Ticketnummer, die im Ausgangsbestand schon vergeben war. Die Ticketnummern des Ausgangsbestands sind unverändert.
- [ ] Ein absichtlich beschädigter oder zurückgesetzter Zählerstand führt dazu, dass die Vergabe gesperrt wird und keine Nummer vergeben wird.

*Auf deinen Geräten:*
- [ ] **Pflichtkriterium:** Eine auf dem Android-Referenzgerät erstellte Sicherung lässt sich auf dem Windows-Referenz-PC mit dem Wiederherstellungsschlüssel vollständig wiederherstellen. Plan und Fotos werden dort korrekt angezeigt.
- [ ] Testziel: Die Sicherung eines Projekts mit 1 großem Plan und 200 Fotos dauert ≤ 3 min auf dem Android-Referenzgerät.

**Dein Aufwand:** ca. 1–2 h

### Phase 0.7 – Ergebnisbericht und Technikentscheidung

**Umfang:**
- `docs/phase0-ergebnis.md` mit allen Messwerten je Plattform und einer Bewertung je Kandidat (geeignet / eingeschränkt geeignet / ungeeignet).
- Bei Bedarf Empfehlung von Alternativen und Gegenmaßnahmen.
- Verbindliche Festlegung folgender Punkte:
  - Dateiverschlüsselungsverfahren,
  - Schlüsselablage und Hinterlegung des Wiederherstellungsschlüssels,
  - Wiederherstellungsverfahren,
  - Verfahren der Migrationssicherung (Masterkonzept 15.4),
  - Umgang mit „Nummer ausstehend" bei gesperrter Nummernvergabe (Masterkonzept 9.1).
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
- **Migrationsrahmen** gemäß Masterkonzept 15.4:
  - geprüfte Sicherung von Datenbank und zugehörigen Dateien vor jeder Migration,
  - keine Migration ohne gültige Sicherung,
  - Erkennung und Wiederherstellung bei unterbrochener oder fehlgeschlagener Migration,
  - dokumentiertes Wiederherstellungsverfahren in `docs/`.
- **Ersteinrichtung:** Benutzername und Gerätekürzel aus dem Register des Firmenadministrators festlegen. Das Kürzel ist danach nicht frei änderbar. Ein Wechsel ist nur über die geregelten Verfahren möglich (Masterkonzept 9.1).
- UUID als technische Identität aller Objekte.
- Einrichtung des Wiederherstellungsschlüssels gemäß dem in Phase 0.7 festgelegten Verfahren, mit verständlicher Anleitung zur sicheren Verwahrung.
- Grundlegendes Erscheinungsbild: Farben, Schriftgrößen, Textskalierung, Offline-Anzeige als Platzhalter.
- Build-Pipeline mit Tests, Code-Analyse und Testversionen für Android und Windows.

**Nicht enthalten:** Fachfunktionen.

**Abnahmekriterien:**

*Automatisiert:*
- [ ] Jede Datenänderung erzeugt einen Eintrag im Änderungsprotokoll mit UUID, Versionszähler, Zeitpunkt und Gerätekürzel.
- [ ] Ein „Löschen" setzt nur einen Löschvermerk, der Datensatz bleibt erhalten.
- [ ] Jedes neu angelegte Objekt erhält eine UUID. Die UUID ist nach Bearbeiten, Speichern und erneutem Laden unverändert.
- [ ] **Erfolgreiche Migration:** Eine Testmigration von Schemaversion 1 auf 2 läuft in dieser Reihenfolge ab:
  1. Vorher wird eine Sicherung erstellt und geprüft (Prüfwerte, Testöffnung, Zählprüfung).
  2. Die Migration läuft.
  3. Danach sind alle Datensätze und die Prüfwerte aller Dateien identisch mit dem Ausgangsstand.
- [ ] **Fehlgeschlagene Sicherung:** Simuliert werden fehlender Speicherplatz, ein Schreibfehler und eine fehlschlagende Prüfung der Sicherung. In jedem Fall beginnt die Migration nicht, die Datenbank ist bitgenau unverändert, und es erscheint eine verständliche Meldung.
- [ ] **Unterbrochene Migration:** Ein Abbruch wird nach jedem einzelnen Migrationsschritt simuliert. Beim nächsten Start wird der unvollständige Zustand erkannt und der Stand vor der Migration aus der Sicherung wiederhergestellt. Datensätze und Prüfwerte sind identisch mit dem Ausgangsstand, und teilmigrierte Daten werden nicht weiterverwendet.
- [ ] **Wiederherstellung:** Die Migrationssicherung lässt sich auf einer frischen Installation ohne den ursprünglichen Geräteschlüssel mit dem Wiederherstellungsschlüssel vollständig wiederherstellen.
- [ ] Ein Gerätekürzel, das in vorhandenen Ticketnummern bereits vorkommt, wird bei der Ersteinrichtung abgelehnt.
- [ ] Die Testabdeckung der Kernbausteine (Datenhaltung, Verschlüsselung, Migration, Nummernvergabe) beträgt mindestens 80 %.

*Auf deinen Geräten:*
- [ ] Die Ersteinrichtung lässt sich auf Android und Windows abschließen. Das Gerätekürzel wird danach angezeigt.
- [ ] **Update-Probe:** Du installierst eine Testversion mit Schemaversion 1 und legst Testdaten an. Danach installierst du eine Testversion mit Schemaversion 2 darüber. Die App meldet die erfolgreiche Sicherung und Migration, und alle Testdaten sind vorhanden.
- [ ] Das Wiederherstellungsverfahren bei fehlgeschlagener Migration ist dokumentiert. Du hast es gelesen und verstanden.
- [ ] Nach einem Neustart erscheint die Ersteinrichtung nicht erneut, und die Angaben bleiben erhalten.
- [ ] Mit größter Systemschriftgröße bleiben alle Texte lesbar und nicht abgeschnitten.

**Dein Aufwand:** ca. 1 h

---

## Phase 2 – Projekte

**Ziel:** Projekte anlegen und verwalten.

**Umfang:**
- Projekt anlegen und bearbeiten mit Projektnummer, Name, Auftraggeber, Adresse, verantwortlicher Person, Status und Terminen.
- Automatische Projektnummer im Format `P<Jahr>-<lfd. Nr.>`, z. B. `P2026-014`. Sie ist bearbeitbar, eine doppelte Vergabe wird lokal verhindert. Dass eine Änderung keine bestehenden Ticketnummern verändert, wird in Phase 4 geprüft, sobald es Tickets gibt.
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
- Ticketnummer gemäß Masterkonzept 9.1, z. B. `P2026-014 / K3-0042`:
  - bei Vergabe als fester Text gespeichert,
  - Eindeutigkeitsprüfung der vollständigen Nummer in der Datenbank,
  - absturzsicherer Zähler mit Prüfung der Zählerhistorie,
  - Sperre der Vergabe bei unklarer oder beschädigter Historie.
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
- [ ] **Projektnummer-Änderung:** Es werden 100 Tickets angelegt und danach die Projektnummer geändert. Alle 100 Ticketnummern sind zeichengenau unverändert. Neu angelegte Tickets tragen die neue Projektnummer. Es entsteht keine Doppelung.
- [ ] Die Datenbank lehnt eine zweite, identische vollständige Ticketnummer technisch ab, auch bei direktem Einfügen unter Umgehung der Bedienoberfläche.
- [ ] **Zählerhistorie:** In drei Szenarien sperrt die App die Vergabe, vergibt keine Nummer, zeigt eine verständliche Meldung und lässt die vorhandenen Daten unverändert:
  - Zählerstand fehlt,
  - Zählerstand ist unlesbar,
  - Zählerstand ist kleiner als die höchste vergebene Nummer.
- [ ] Nach Zuweisung eines neuen Gerätekürzels wird die Vergabe fortgesetzt. Alle bisherigen Ticketnummern bleiben unverändert.
- [ ] Ein Ticket mit fehlenden Pflichtfeldern wird immer als „unvollständig" gekennzeichnet. Kein Ablauf setzt es stillschweigend auf vollständig.
- [ ] Die Markierungsposition bleibt nach Speichern und Laden exakt erhalten.

*Auf deinen Geräten:*
- [ ] Auf deinem realen Plan legst du per Schnellerfassung 20 Tickets an. Jede Markierung sitzt nach dem Neustart an derselben Planstelle.
- [ ] Du vervollständigst 5 Tickets. Danach verschwindet die Kennzeichnung „unvollständig" nur bei diesen.
- [ ] Du notierst die Ticketnummern von 5 Tickets, änderst die Projektnummer und vergleichst. Alle 5 Nummern sind unverändert, und ein neues Ticket trägt die neue Projektnummer.
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

**Umfang** (im Repository nur als künstliche Nachbildung mit Fantasiedaten; Firmenlogo und Firmendaten werden auf dem Gerät eingerichtet, siehe 2.5):
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
- Datenbank und zugehörige Dateien werden gemeinsam und in einem zueinander passenden Stand gesichert.
- Schutz vor unbefugtem Zugriff durch Verschlüsselung gemäß dem in Phase 0.7 festgelegten Verfahren. Die Wiederherstellung ist auch ohne den ursprünglichen Geräteschlüssel mit dem Wiederherstellungsschlüssel möglich (Masterkonzept 15.2).
- Wiederherstellung, auch auf einem anderen Gerät und plattformübergreifend.
- Integritätsprüfung einer Sicherung ohne Wiederherstellung („Sicherung prüfen").
- Verständliche Rückmeldung über Erfolg oder Fehler **jeder** Sicherung.
- Neues Gerätekürzel nach einer Wiederherstellung. Bestehende Ticketnummern bleiben unverändert.
- Anleitung **„Verlorenes Gerät / verlorener Schlüssel"** in einfacher Sprache unter `docs/` (Masterkonzept 15.2).
- Warnung bei knappem Speicherplatz. Es werden keine Daten automatisch gelöscht.

**Abnahmekriterien:**

*Automatisiert:*
- [ ] Sicherung und Wiederherstellung erhalten alle Datensätze, den Änderungsverlauf und alle Dateien mit identischen Prüfwerten.
- [ ] Ohne gültigen Schlüssel bzw. gültiges Kennwort ist der Inhalt einer Sicherung nicht lesbar. Es gibt keine im Klartext auffindbaren Testinhalte.
- [ ] Die Wiederherstellung gelingt auf einer frischen Installation ohne den ursprünglichen Geräteschlüssel mit dem Wiederherstellungsschlüssel.
- [ ] Beschädigte Sicherungen werden erkannt und nicht teilweise eingespielt.
- [ ] **Keine doppelten Ticketnummern nach Wiederherstellung:** Ein Bestand mit 10.000 Tickets, einschließlich gelöschter, wird gesichert und wiederhergestellt. Anschließend werden 10.000 weitere Tickets angelegt. Ergebnis:
  - Es gibt keine doppelte Ticketnummer.
  - Alle ursprünglichen Ticketnummern sind zeichengenau unverändert.
  - Neue Nummern tragen ausschließlich das neue Gerätekürzel.
- [ ] Vor Zuweisung eines neuen Gerätekürzels vergibt die wiederhergestellte Installation keine Ticketnummern.
- [ ] Eine Sicherung, die durch Beenden der App, fehlenden Speicherplatz oder ein entferntes Speichermedium abbricht, wird nie als gültig gekennzeichnet. Der Nutzer erhält eine Fehlermeldung.

*Auf deinen Geräten:*
- [ ] **Ernstfallprobe auf dem vorgesehenen Gerät** (Xiaomi 15 Ultra):
  1. Du sicherst dein Testprojekt.
  2. Du deinstallierst die App und installierst sie neu.
  3. Du stellst die Sicherung mit dem Wiederherstellungsschlüssel wieder her.

  Danach sind alle Tickets, Markierungen, Fotos und Berichte vorhanden. Die App meldet „alle Prüfwerte identisch", mit Anzahl der geprüften Dateien.
- [ ] Nach der Wiederherstellung sind die Ticketnummern von 5 vorher notierten Tickets unverändert. Ein neues Ticket trägt das neue Gerätekürzel.
- [ ] Du stellst dieselbe Sicherung auf dem Windows-PC wieder her. Der Inhalt ist identisch.
- [ ] **Fehlerprobe** auf dem Windows-PC:
  1. Du startest eine Sicherung auf einen USB-Stick.
  2. Du ziehst den Stick während der Sicherung ab.

  Die App meldet einen verständlichen Fehler und kennzeichnet die Sicherung nicht als gültig.
- [ ] „Sicherung prüfen" meldet bei einer intakten Sicherung Erfolg und bei einer absichtlich beschädigten Sicherung einen Fehler.
- [ ] Du hast die Anleitung „Verlorenes Gerät / verlorener Schlüssel" gelesen und verstanden. Der Wiederherstellungsschlüssel ist getrennt von den Geräten verwahrt.

*Hinweis:* Eine lediglich erfolgreich erstellte Sicherungsdatei gilt **nicht** als Nachweis. Nachweis ist nur die erfolgreiche Ernstfallprobe.

**Dein Aufwand:** ca. 2–3 h

---

## Meilenstein A – Einzelgerät-Funktionstest

**Ziel:** Der MVP-Kernablauf (Masterkonzept, Abschnitt 22, Schritte 1–7) wird an einem echten, kleinen Projekt auf **einem** Gerät erprobt. Das ist der Beginn des Pilotbetriebs mit Echtdaten.

**Pflichtvoraussetzungen vor Beginn (Masterkonzept 15.5)** – ohne diese Punkte beginnt Meilenstein A nicht:
- [ ] Die lokale Sicherung ist implementiert, manuell und automatisch (Phase 7 abgenommen).
- [ ] Sicherungen sind vor unbefugtem Zugriff geschützt (Phase 7, automatisierte Prüfung).
- [ ] Die Wiederherstellung wurde auf dem vorgesehenen Gerät praktisch getestet, mit Abgleich aller Prüfwerte (Ernstfallprobe Phase 7).
- [ ] Der Umgang mit verlorenen Geräten und Schlüsseln ist dokumentiert, und der Wiederherstellungsschlüssel ist verwahrt.
- [ ] Erfolg und Fehler einer Sicherung werden verständlich zurückgemeldet (Phase 7, Fehlerprobe).

Eine lediglich erstellte Sicherungsdatei reicht als Nachweis nicht aus.

**Ablauf:**
- Zeitraum 1–2 Wochen.
- Echtes oder realitätsnahes Kleinprojekt mit mindestens 1 realem Plan, 30 Tickets und 60 Fotos.
- Mindestens eine wöchentliche Sicherung.
- Am Ende ein Bericht nach Unternehmensvorlage.
- Rückmeldungen sammelst du formlos, ohne vertrauliche Projektinhalte (2.5). Stichpunkte genügen. Claude Code wertet sie aus und ordnet sie ein: Fehler, Verbesserung oder später.
- Am Ende des Zeitraums wird eine Wiederherstellung der letzten Sicherung erneut praktisch geprüft.

**Abnahmekriterien:**
- [ ] Im Testzeitraum ist kein Datenverlust aufgetreten.
- [ ] Die Wiederherstellung der letzten Sicherung am Ende des Zeitraums war erfolgreich, mit Abgleich aller Prüfwerte.
- [ ] Der erzeugte Bericht ist inhaltlich korrekt. Das prüfst du stichprobenartig an 10 Tickets.
- [ ] Alle als „kritisch" eingestuften Rückmeldungen sind behoben.
- [ ] Du entscheidest ausdrücklich, ob die Serverphase beginnen kann oder zuerst Verbesserungen umgesetzt werden.

---

## Phase 8 – Server-Grundlage

**Ziel:** Ein selbst betriebener, abgesicherter Server als Grundlage der Synchronisation.

**Verbindliche Freigabebedingung (Masterkonzept 16.3):** Die Phase beginnt **erst**, wenn alle folgenden Punkte erfüllt und von dir ausdrücklich bestätigt sind. **Ohne geklärte Betriebsverantwortung beginnt die Serverphase nicht.**

- [ ] Es ist schriftlich geklärt, wer für folgende Aufgaben verantwortlich ist:
  - Serverbetrieb,
  - Sicherheitsupdates,
  - Überwachung,
  - Backups,
  - Störungsbehebung.
- [ ] Die Verantwortung liegt bei einer **fachkundigen Person** oder einem **beauftragten Dienstleister** (Name, Kontakt, Vertretung).
- [ ] Folgende Punkte sind dokumentiert:
  - Zugriffsrechte (wer hat welchen Zugang),
  - Erreichbarkeit im Störungsfall (Zeiten, Kontaktweg, Vertretung),
  - Wiederherstellungsverfahren.
- [ ] Eine Aufwandsschätzung für den laufenden Betrieb liegt vor. Der Anteil, der bei dir verbleibt, passt zusammen mit Test- und Abnahmeaufwand realistisch in **weniger als 5 Stunden pro Woche**.

**Zusätzlich vorab zu klären:**
- Hosting: eigener Server oder angemieteter Server bei einem deutschen Anbieter.
- Domain, TLS-Zertifikat, Erreichbarkeit von Baustellen (direkt über das Internet oder per VPN).
- Server-Technologie: Claude Code legt dazu zu Beginn der Phase eine begründete Empfehlung vor.
- Backupziel für Serversicherungen.

Claude Code liefert eine vollständige Schritt-für-Schritt-Betriebsdokumentation und eine weitgehend automatisierte Einrichtung. Das ersetzt aber nicht die geklärte Betriebsverantwortung.

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
- [ ] Ein Gerätekürzel wird nie doppelt vergeben, auch nicht bei gleichzeitigen Registrierungen. Bereits verwendete und stillgelegte Kürzel aus der Einzelgerät-Phase werden ins Register übernommen und nie neu vergeben.
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
- [ ] Ticketnummern bleiben über alle Geräte hinweg eindeutig. Der Server lehnt eine doppelte vollständige Ticketnummer ab. Eine trotzdem auftretende Doppelung, etwa aus einer Einzelgerät-Phase, wird als Konflikt angezeigt und nie still umnummeriert.

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
| Große Pläne laufen auf dem Android-Referenzgerät nicht flüssig | Schlechte Baustellentauglichkeit | Messung in Phase 0.4; ggf. Kachel-Zwischenspeicher |
| Referenzgerät Xiaomi 15 Ultra ist ein Oberklassegerät; Messwerte sind auf schwächere Geräte nicht übertragbar | Ruckeln oder Abstürze auf anderen Baustellengeräten im Praxistest | Vor dem Praxistest ergänzender Test auf einem schwächeren Gerät, falls solche eingesetzt werden; ggf. Mindestanforderungen an Geräte |
| Umfangreiche Berichte überschreiten den Arbeitsspeicher, vor allem auf dem Windows-PC mit 8 GB RAM | Absturz bei großen Projekten | Messung in Phase 0.5; Aufteilung in Teildokumente |
| Schlüsselverlust macht lokale Daten unlesbar | Datenverlust vor Einführung des Servers | Wiederherstellungsschlüssel unabhängig vom Gerät (Phase 0.6 / 1 / 7); Pflichtvoraussetzungen vor Meilenstein A |
| Vor Einführung des Servers hängt die Eindeutigkeit der Gerätekürzel an einem manuell geführten Register | Doppelte Kürzel und damit doppelte Ticketnummern bei Fehlbedienung | Register durch den Administrator; App lehnt bekannte Kürzel ab; Eindeutigkeitsprüfung; Übernahme ins Server-Register in Phase 8 |
| Migrationssicherung benötigt zusätzlichen Speicherplatz | Update kann bei vollem Speicher nicht migrieren | Speicherprüfung vor Migration; Migration beginnt nicht; verständliche Meldung (Phase 1) |
| Serverbetrieb übersteigt die verfügbare Zeit | Ausfälle, fehlende Updates | Verbindliche Freigabebedingung „Betriebsverantwortung" vor Phase 8 |
| Vertrauliche Inhalte gelangen versehentlich in Repository, Protokolle oder Artefakte | Datenschutzverletzung | Regeln 2.5; automatische Dateiprüfung in GitHub Actions; Sichtprüfung |
| Begrenzte Testzeit verzögert Abnahmen | Längere Gesamtdauer | Kleine Teilschritte, Messwerte automatisch von der App ermittelt |
| Unsignierte Testversionen lösen Sicherheitswarnungen aus | Verunsicherung beim Testen | Erklärung in den Checklisten; Signierung vor dem Praxistest prüfen |

## 5. Nachweismatrix der Pflichtanforderungen

Diese Tabelle zeigt, in welcher Phase jede Pflichtanforderung des MVP durch ein messbares Abnahmekriterium nachgewiesen wird.

| Pflichtanforderung (Masterkonzept) | Nachweis in Phase |
|---|---|
| UUID als technische Identität (9.1) | 1 |
| Ticketnummer getrennt von UUID, als fester Text gespeichert (9.1) | 4 |
| Ticketnummer bleibt bei Änderung der Projektnummer unverändert (9.1) | 4 |
| Ticketnummern werden nie erneut vergeben (9.1) | 4, 7, 9 |
| Globale Eindeutigkeit nicht allein über das Gerätekürzel (Register, Eindeutigkeitsprüfung) (9.1) | 1, 4, 8, 9 |
| Absturzsicherer, dauerhaft gespeicherter Zähler (9.1) | 4 |
| Sperre bei unklarer oder beschädigter Zählerhistorie (9.1) | 0.6, 4 |
| Neues Gerätekürzel nach Wiederherstellung; bestehende Nummern unverändert (9.1) | 0.6, 7 |
| Stabile Markierungskoordinaten (8) | 0.4, 4 |
| Keine erfundenen Werte; unvollständige Tickets gekennzeichnet (9) | 4, 6 |
| Verschlüsselte Datenbank (15.1) | 0.2, 1 |
| Verschlüsselte Dateien; SHA-256 über das unverschlüsselte Original (13, 15.1) | 0.3, 3, 5 |
| Kein Schlüssel ausschließlich auf einem Gerät (15.2) | 0.6, 1, 7 |
| Geprüfte Sicherung vor jeder Migration; keine Migration ohne Sicherung; Wiederherstellung bei Abbruch (15.4) | 1; danach jede Phase (2.3) |
| Pflichtvoraussetzungen vor Pilotbetrieb (15.5) | 7, Meilenstein A |
| Freigegebene Berichte unveränderlich, mit Verweis auf Datenstand und Planrevision (14) | 6 |
| Kein stilles Überschreiben; Konflikte sichtbar; beide Zustände erhalten (16.1) | 9, 11 |
| Fortsetzbare Übertragung mit Integritätsprüfung (15.3) | 10 |
| Keine automatische Löschung bei Speicherknappheit (15.3) | 7, 10 |
| Offline-Arbeit im Kernablauf (15) | 11 |
| Keine vertraulichen Inhalte in Repository, Protokollen und Artefakten (17.1) | 0.1; danach jede Phase (2.3) |
| Geklärte Betriebsverantwortung vor der Serverphase (16.3) | Freigabebedingung Phase 8 |

Anforderungen außerhalb des MVP (Katalog, Prüfabläufe, Mängel, Aufgaben, Rollen, externe Firmen, iOS) werden nach Meilenstein B geplant.

## 6. Freigabe

**Vor der ausdrücklichen Freigabe dieses Phasenplans erfolgt keine Implementierung.** Das umfasst App-Code, Prototyp und Build-Pipeline. Der Beginn von Phase 0 erfordert darüber hinaus eine **gesonderte, ausdrückliche Zustimmung** des Projektverantwortlichen.

| | |
|---|---|
| Phasenplan freigegeben am | _______________ |
| Durch | _______________ |
| Anmerkungen | _______________ |
| Zustimmung zum Beginn von Phase 0 am | _______________ |

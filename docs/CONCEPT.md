## Konzept Semesterprojekt

Vorhersage von Studienabbruch Risiken bis Ende des 3. Semesters

### 1. Business Understanding
1.1 Projektziel und Forschungsfrage
Ziel dieses Semesterprojekts ist es zu untersuchen, ob sich auf Basis anonymisierter oder stark pseudonymisierter Hochschuldaten ein interpretierbares Modell zur Früherkennung von Studienabbruch Risiken entwickeln lässt. Im Mittelpunkt steht die Frage, ob nach dem zweiten Semester ein erhöhtes Risiko für einen Studienabbruch bis Ende des dritten Semesters erkannt werden kann.
Das Projekt versteht sich ausdrücklich als methodische Machbarkeitsstudie. Der Schwerpunkt liegt auf Datenverständnis, Feature Engineering, Modellvergleich, Validierung und fachlicher Interpretation. Ein produktives Entscheidungssystem ist nicht Teil des Semesterumfangs.

1.2 Motivation und praktischer Nutzen
Frühe Hinweise auf mögliche Studienabbrüche können Hochschulen dabei unterstützen, Beratungs- und Unterstützungsangebote gezielter einzusetzen. Studierende mit erhöhtem Risiko könnten frühzeitig auf freiwillige Unterstützungsangebote hingewiesen werden. Gleichzeitig soll vermieden werden, dass das Modell automatisiert über Personen entscheidet oder sie stigmatisiert.

1.3 Erfolgskriterien
Die Erfolgskriterien werden nach Sichtung der Daten und Prüfung der Klassenverteilung final festgelegt. Als fachliche Leitplanken gelten:

- Das Modell soll Abbrecher möglichst zuverlässig erkennen.
- Interpretierbarkeit hat Vorrang vor maximaler Komplexität.
- Datenschutz und rechtliche Freigabe sind zwingende Voraussetzungen.
- Das Ergebnis muss im Rahmen eines Semesterprojekts reproduzierbar und nachvollziehbar sein.


### 2. Data Understanding
2.1 Datenquellen und Datenzugang
Die geplanten Daten stammen aus dem internen Hochschul-Informationssystem bzw. dem Campus-Management-System. Die Bereitstellung erfolgt nur, wenn Prüfungsamt und Studierendensekretariat die Daten zeitnah, anonymisiert bzw. stark pseudonymisiert und rechtlich freigegeben zur Verfügung stellen.
Der Datenzugang ist das zentrale Projektrisiko. Sollte die Freigabe nicht rechtzeitig erfolgen, wird auf einen vorbereiteten Fallback-Datensatz ausgewichen, damit die methodische Bearbeitung trotzdem möglich bleibt.

2.2 Geplante Grundgesamtheit
Untersucht werden Studierende, die mindestens das erste und zweite Semester abgeschlossen haben. Für die Modellierung wird geprüft, ob ein Abbruch bis Ende des dritten Semesters vorliegt.

2.3 Geplante Merkmale
Für die Semester 1 und 2 werden folgende Merkmalsgruppen vorgesehen:
● Prüfungsleistungen: Anzahl bestandener und nicht bestandener Prüfungen, Durchschnittsnote, Rücktritte, Fehlversuche.
● Studienorganisation: Anzahl angemeldeter und tatsächlich abgelegter Prüfungen, Anzahl belegter Lehrveranstaltungen.
● Zeitliche Faktoren: früher oder später Prüfungsanmeldezeitpunkt, Rücktrittsmuster kurz vor Prüfungen.
● Soziodemographische Merkmale: Studiengang, HZB-Note, Alter bei Studienbeginn, Geschlecht in pseudonymisierter Form.

2.4 Zielvariable Die Zielvariable lautet:
● Studienabbruch_S3 = 1: Studium wurde bis Ende des dritten Semesters abgebrochen.
● Studienabbruch_S3 = 0: Studium wurde fortgeführt.
Wichtig ist eine saubere fachliche Abgrenzung. Ein Studiengangswechsel, ein Urlaubssemester oder ein Hochschulwechsel dürfen nicht automatisch als Abbruch gewertet werden.

2.5 Datenqualität und Risiken
Vor der eigentlichen Modellierung werden typische Datenqualitätsrisiken geprüft:
● mögliche Klassenungleichverteilung,
● fehlende Werte,
● historische Lücken durch Systemwechsel,
● unklare oder uneinheitliche Definitionen in den Quelldaten.

### 3. Data Preparation
3.1 Vorgehen und Werkzeuge
Die Datenverarbeitung erfolgt prototypisch in einem Python-Notebook mit pandas, scikit-learn und ergänzenden Auswertungsbibliotheken. Rohdaten werden nur in freigegebenen, geschützten Umgebungen verarbeitet.
Die wesentlichen Schritte sind:
1. Import der bereitgestellten CSV- oder Excel-Dateien.
2. Prüfung auf Duplikate, Ausreißer und fehlende Werte.
3. Feature Engineering auf Semesterbasis.
4. Label-Zuweisung über die Abbruchdefinition.
5. AufbereitungfürTraining,ValidierungundTest.

3.2 Feature Engineering
Aus den Rohdaten werden aggregierte Merkmale gebildet, zum Beispiel:
● Bestehensquote_S1 und Bestehensquote_S2,
● Anmeldungsquote_S1 und Anmeldungsquote_S2,
● Notendurchschnitt_S1 und Notendurchschnitt_S2,
● Rücktrittsrate_S1 und Rücktrittsrate_S2,
● Veränderung der Bestehensquote zwischen S1 und S2.
Diese Merkmale sollen eine kompakte und interpretierbare Beschreibung der bisherigen Studienentwicklung ermöglichen.

3.3 Datenschutz und organisatorische Vorgaben Für die Datenverarbeitung gelten folgende Vorgaben:
● keine Rohdaten auf privaten Geräten,
● Zugriff nur für autorisierte Projektmitglieder,
● keine Weitergabe an Dritte,
● dokumentierter Speicherort,
● Löschung der Rohdaten nach Projektabschluss,
● Nutzung ausschließlich für wissenschaftliche Zwecke im Rahmen
des Semesters. 

### 4. Modeling
4.1 Lernproblem
Da eine binäre Zielvariable vorliegt, handelt es sich um ein überwachtes Lernproblem der binären Klassifikation.

4.2 Modellwahl
Im Fokus stehen interpretierbare und praxisnahe Verfahren:
● Logistische Regression als Baseline,
● Decision Tree für einfache Nachvollziehbarkeit,
● Random Forest als robuster Vergleich,
● XGBoost nur optional als zusätzliches Vergleichsmodell.
Interpretierbarkeit soll Vorrang vor maximaler Komplexität haben.

4.3 Validierung
Zur Modellbewertung werden ein stratifizierter Train-Test-Split und eine 5-fache Kreuzvalidierung genutzt. Zusätzlich wird auf mögliche Klassenungleichgewichte geachtet. Falls notwendig, werden geeignete Verfahren wie Class Weights oder Sampling-Strategien eingesetzt.

4.4 Metriken
Die Hauptmetrik ist Recall, da möglichst wenige Abbrecher übersehen werden sollen. Ergänzend werden Precision, Confusion Matrix und gegebenenfalls F1-Score betrachtet. Konkrete Zielwerte werden erst nach Analyse der Datenverteilung festgelegt.

4.5 Einsatzszenario als Konzept
Ein möglicher späterer Einsatz wäre eine semestrische Risikoeinschätzung für Studienberater. Dieser Einsatz ist jedoch nicht Teil des aktuellen Semesterumfangs und wird nur als Ausblick beschrieben.

### 5. Evaluation
5.1 Technische Evaluation
Die Modelle werden hinsichtlich Recall, Precision und allgemeiner Vorhersageleistung auf dem Testdatensatz verglichen. Anschließend wird geprüft, ob die Ergebnisse stabil und nachvollziehbar sind.

5.2 Fachliche Evaluation
Die Resultate sollen zusätzlich fachlich mit Studienberatung bzw. zuständigen Ansprechpartnern besprochen werden. Ziel ist zu prüfen, ob die Ergebnisse sinnvoll interpretierbar sind und ob die wichtigsten Merkmale fachlich plausibel erscheinen.

5.3 Interpretation
Besondere Aufmerksamkeit gilt den Einflussfaktoren auf die Vorhersage. Beispielsweise können geringe Bestehensquoten, hohe Rücktrittsquoten oder wiederholt nicht bestandene Prüfungen auf ein erhöhtes Risiko hinweisen. Die Interpretation soll verständlich und nicht stigmatisierend erfolgen.

### 6. Deployment
Der produktive Einsatz ist nicht Bestandteil des Semesterprojekts. Im Rahmen des Projekts wird ein lauffähiges Python-Notebook mit vollständiger Pipeline erstellt. Als Zukunftsausblick können eine Batch-Verarbeitung oder ein einfaches Dashboard genannt werden, jedoch nur als optionale Perspektive.

### 7. Risikomanagement
7.1 Zentrale Risiken
Risiko 1: Datenzugang wird verzögert oder verweigert
Dieses Risiko ist hoch und kann das Projekt grundsätzlich gefährden. Deshalb werden frühzeitige Abstimmung und ein Fallback-Datensatz vorbereitet.
Risiko 2: Starkes Klassenungleichgewicht
Wenn nur wenige Abbrüche vorliegen, kann das Modell Abbrüche schlecht erkennen. Deshalb liegt der Fokus auf Recall und auf geeigneten Ausgleichsverfahren.
Risiko 3: Datenschutzverletzungen
Unzureichende Pseudonymisierung oder unsichere Speicherung würden das Projekt sofort gefährden. Daher werden klare organisatorische Regeln, Zugriffsbeschränkungen und Löschfristen definiert.

7.2 Fallback-Strategie
Falls die Hochschuldaten nicht rechtzeitig verfügbar sind, wird ein öffentlicher Alternativdatensatz verwendet, um das methodische Vorgehen dennoch umzusetzen. Der Fallback ist nicht nur eine Erwähnung, sondern als realistische Projektalternative einzuplanen.

7.3 Iterationspunkte
Gemäß CRISP-DM sind Rücksprünge zwischen den Phasen ausdrücklich eingeplant:
● von Data Understanding zurück zu Business Understanding, falls die Daten die Fragestellung nicht ausreichend abbilden,
● von Modeling zurück zu Data Preparation, falls Feature Engineering verbessert werden muss,
● von Evaluation zurück zu Modeling, falls die Zielwerte nicht erreicht werden.

### 8. Schlussbemerkung
Das Projekt ist fachlich sinnvoll und für ein Semesterprojekt geeignet, wenn Datenzugang, Datenschutz und Umfang realistisch begrenzt werden. Die stärkste Version des Konzepts ist eine interpretierbare Machbarkeitsstudie mit klarer Fragestellung, sauberer Datenschutzstruktur und einem Fallback-Datensatz als Absicherung.

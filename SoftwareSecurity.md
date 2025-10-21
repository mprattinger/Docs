## Sicherheitsanforderungen

### Identifizieren und analysieren von potenziellen Bedrohungen und Schwachstellen

### Nutzung von verlässlichen Methoden und Standards für sicheres Programmieren und Vermeidung von häufigen Sicherheitslücken

### Fehlerbehandlungsmechanismen implementieren

Fehlerbehandlung macht Programme robust und wartbar: 
* Erwartungen prüfen, 
* Ausnahmen klar behandeln und 
* sensible Informationen nicht preisgeben. 
Gute Fehlerbehandlung trennt Benutzermeldungen von Entwickler-Logs, sorgt für Aufräumarbeiten (z. B. `finally` / `using`) und setzt gezielte Wiederholungslogik bei transienten Fehlern ein.

Best Practices:
- Validierung am Eingang (fail fast).
- Spezifische Ausnahmen fangen, nicht alle pauschal verschlucken.
- Kontextreiche Logs für Debugging, aber keine sensiblen Daten ins Log schreiben.
- Zentrale Fehlerbehandlung (Middleware/global handler) für konsistente Reaktionen und HTTP-Fehlercodes.
- Nutzerfreundliche Fehlermeldungen ohne interne Details.
- Retries mit Exponential Backoff bei Netzwerk-/IO-Transientfehlern.
- Unit- und Integrationstests für Fehlerpfade schreiben.

Gotcha: Vermeide stilles Ignorieren von Ausnahmen — das versteckt Fehler und führt zu nicht-deterministischem Verhalten.

<u>In C#/Java/JavaScript:</u>
- try-catch

<u>RPG:</u>
- monitor ... pn-error
verwenden

### Sicherstellen, dass nur berechtigte Nutzer Zugang zu sensiblen Daten und Funktionen haben

Programme sollten immer mit Zuganssperren programmiert werden. Zugriffe auf weitere Systeme (API, Datenbanken, ...) sollten immer im UserContext geschehen. Dadurch können Berechtigungen sicher geprüft werden.

### Einsatz von Verschlüsselungstechniken zum Schutz von Daten

In erster Linie soll hier die Kommunikation zwischen den einzelnen Systemen gesichert werden (https). 

### Regelmäßige überprüfungen des Quellcodes

Quellcode sollte von Kollegen gegengeprüft werden. Dadurch können Bad-Practices erkannt werden. Dies sollte aber immer in kollegialer Form und nie belehrend erfolgen. 

### Regelmäßige Schulung der Entwickler für ein Sicherheitsbewusstsein

Alle Benutzer, inkl. der Entwickler, sollten regelmäßig Security Awareness Schulungen erhalten. Für Entwickler sollten auch Beispiel für Schwachtstellen im Code und deren Auswirkungen gezeigt werden (SQL-Injection, ...)

### Regelmäßiges Aktualisieren der Software und alle verwendeten Bibliotheken zur Behebung von Sicherheitslücken 

Verwendete Packete und Bibliotheken sowie Frameworks sollten regelmäßig (1. Monat oder 1. Jahr) aktualisert werden. Dazu muss allerdings auch immer ein gewisser Zeitrahmen mitgedacht werden, da ein Upgrade möglicherweise auch zu Anpassungen führn kann.

### Gründliches Dokumentieren der Software und aller Sicherheitsmaßnahmen

Software sollte dokumentiert sein (Nein Code ist keine Dokumentation). In dieser sollte auch auf die Verwendeten 3. System eingegangen werden. Auch eine List der Bibliotheken und Frameworks sollte enthalten sein.
Wichtig ist auch, dass das Erstellen und Verteilen der Anwendung beschrieben wird.

### SBOM, um alle Softwarekomponenten im Blick zu behalten. 

Eine SBOM ist eine Stückliste der verwendeten Softwarekomponenten. Darin sollten alle Bibliotheken und in den jeweiligen Bibliotheken referenzierten Komponenten aufgelistet werden.
Dies ist wichtig um bei bekannten Sicherheitslücken in Packeten oder Bibliotheken (log4j, leftPad,...) geprüft werden kann, ob diese in Anwendungen verwendet werden.

## Secure- Coding- Rules

### Alle Benutzereingaben validieren, um sicherzustellen, dass sie den erwarteten Formaten- und Inhaltforderungen entsprechen. 

SQL Injection ist immer noch häufiger Angriffsvektor. Der Entwickler sollte immer davon ausgehen, dass den Eingaben der Nutzer nicht zu trauen ist. Daher ist jede Eingabe zu prüfen bevor damit weiter gearbeitet wird.

### Gut getestet (weite Verbreitung) Bibliotheken verwenden, anstatt Funktionen selbst zu entwickeln.

In den diversen Frameworks gibt es meist auch Package-Repositories von denene Biblitheken geladen werden können. Im besten Fall lösen diese ein Problem, dass sonst selbst gelöst werden muss. Aber Achtung, der Enwtickler ist verantwortlich die Sicherheit und die Aktualität dieses Packets zu prüfen. Sei es durch prüfen des Quellcodes bei einer Open-Source Bibliothek oder durch prüfen des Herstellers

### Fehler sollten sicher behandelt werden. Ein Fehler soll nicht zum Absturz des Programms führen, sondern dokumentiert (Logging) und dem User angezeigt werden. 

Ein Fehler soll nicht zum Absturz des Programms führen, sondern dokumentiert (Logging) und dem User angezeigt werden. (Siehe Fehlerbehandlungsmechanismen implementieren)

### Nutzung von Tools um Schwachstellen im Code frühzeitig zu erkennen ode zu beheben

Wird der Sourcecode auf Github gehostet, kann mittels GitHub Dependabot Softwareabhängigkeiten (Dependencies) automatisch aktuell und sicher gehalten werden.

### Regelmäßiges schulen der Entwickler in sicheren Programmiertechniken und aktuellen Bedrohungen

Erweiterte Security Awareness Schulung.

Sicherheitsanforderungen definieren


Alle Sicherheitsmaßnahmen gründlich dokumentieren

Entwicklung eines Notfallplans

## Testkonzept

Wie weiter oben bereits beschrieben muss die auszurollende Software vor dem Einsatz getestet werden. Dies beinhaltet zum Einen Test durch den Entwickler bzw. Kollegen in der Softwareentwicklung und Tests durch den Benutzer bzw. einer Benutzergruppe. Dabei werden die Tests sowohl auf erstellten Testdaten, als auch auf annähernd Echtdaten auf einer dezidierten Testumgebung durchgeführt.

Aus dem Pflichtenheft das Testziel ermitteln.

Testabdeckung

Übersicht Testfälle

Beurteilung Testziele und Testabdeckung

Testvoraussetzungen definieren

Was müssen die Tester mitbringen

Welche Voraussetzung muss die Testumgebung mitbringen

Testsystem

Testdaten

Testhilfsmittel (Software für das Testmanagement)

Definition wie die Test zu dokumentieren sind

Testplan erstellen
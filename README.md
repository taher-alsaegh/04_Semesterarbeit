* [ ] Titelblatt
* [ ] Management Summary / Abstract

# Initialisierungsphase

## Einleitung

Im Rahmen meiner 4. Semesterarbeit an der Technischen Berufsschule Zürich soll ein GitOps Workflow auf Kubnernetes realisiert werden. Die Arbeit legt dabei besonderen Wert auf den Sicherheitsaspekt verfolgt dem Prinzip von DevSecOps. Als Proof of Concept, später auch PoC gennant, soll die zentrale Frage: _Wie kann mithilfe von GitOps (ArgoCD) und integrierten Sicherheitsprüfungen, wie Trivy ein sicherer, reproduzierbarer und automatisierter Deployment-Prozess für containerisierte Webapplikationen in Kubernetes realisiert werden? beantwortet werden._ beantwortet werden.

### Ausgangslage & Motivation

In der modernen Softwareentwicklung steigen die Anforderungen an Automatisierung, Sicherheit und Nachvollziehbarkeit entlang des gesamten Softwarebereitstellungsprozesses. Traditionelle CI/CD-Prozesse bieten zwar bereits eine gewisse Automatisierung, jedoch fehlt häufig eine integrierte Sicherheitsüberprüfung und eine vollständige Rückverfolgbarkeit von Änderungen bis in die Produktionsumgebung.
Insbesondere bei containerisierten Anwendungen in Kubernetes-Clustern besteht das Risiko, dass unsichere oder veraltete Container-Images im Betrieb genutzt.
Herkömmliche Deployments erfordern oftmals manuelle Eingriffe durch Entwickler oder Administratoren, was Fehleranfälligkeit begünstigen.

Die fiktive Firma Kubinet AG betreibt mehrere containerisierte Webapplikationen in einem Kubernetes-Cluster.
Der aktuelle Deployment-Prozess erfolgt manuell über ein klassisches CI/CD-System (Github Actions) ohne zentrale Sicherheitsprüfung oder automatische Validierung der Container-Images.
Dadurch besteht die Gefahr, dass fehlerhafte oder unsichere Images deployed werden, was sowohl Compliance-Vorgaben als auch Betriebssicherheit gefährdet. Da das Unternehmen nun an weitere Kunden gewinnt, steigen gleichzeitig die Sicherheitsmassnahmen an und Anforderungen. Ziel ist es einen Shift Left zu erzielen um den automatisierten Security Ansatz so früh wie möglichst einzubringen.

Das Unternehmen möchte den Bereitstellungsprozess modernisieren, indem ein GitOps-basierter Workflow eingeführt wird, welcher Sicherheitsüberprüfungen, wie Trivy integriert, Deployments automatisiert (ArgoCD) und sämtliche Änderungen nachvollziehbar im Git-Repo dokumentiert.

### Product Vision
Die Product Vision beschreibt kurz und klar, wofür ein Produkt existiert und welchen Nutzen es liefern soll. Im unteren Bild wurde ein Product Vision Board nach Roman Pichler erstellt, um das Produkt ganzheitlich zu verstehen und zu planen. Es ist deutlich detaillierter, konkreter und umfangreicher als die Vision selbst.

![Product Vision Board](image/product_vision.png)
[Quelle](https://www.romanpichler.com/blog/the-product-vision-board/)

### Nicht Teil der Arbeit (Out of Scope)

Das Erarbeiten der webbasierten Flask Applikation ist nicht Teil dieser Arbeit und wird daher nicht im Detail erläutert. Bestandteile wie, ERM, Sequenzdiagramm oder UML fallen hier weg, da diese Bereiche, den Rahmen der Arbeit sprengen würden und nicht im Vordergrund stehen.

Als Webapplikation wird stattdessen auf eine vulnerable Webapplikation zurückgeriffen. Damit können die Security Askpekte in der Arbeit realisitisch geprüft und nachverfolgt werden. Damn Vulnerable Web Application kurz _DVWA_ ist ein Penetration Testing Projekt, das bewusst Schwachstellen in der Anwendung aufweisst und für Cyber Security Studenten eine Spielwiese fürs Hacken bietet. In meiner Arbeit soll die Security-Chain auf folgendes DVWA durchlaufen und dadurch aufzeigen, welche Gefahren zu erkennen sind.

## Projektmanagement
In der folgenden Semesterarbeit wird das Konzept der Agilen Projektmanagementmethode Scrum angewendet. Vorteil dieser Methode ist die flexible Anpassungsfähigkeit des Projekts, ohne dabei ein Risiko auf die Projektfortführung darzustellen. Durch kontinuierlichen Sprintzyklen kann die Arbeit fortgehend verbessert und weiterentwickelt werden. In den Reviews bzw. Closers Termine werden die erledigten und angehenden Aufgaben besprochen und ein konstruktives Feedback wird dabei von den jeweiligen Parteien gegeben.

## Projektorganisation
Das Scrum-Konzept verfolgt einen immer wiederkehrenden und inkrementellen Ansatz in der Projektentwicklung. In dieser Arbeit übernimmt der Projektabnehmer alle Scrum-Rollen selbst, was in der Regel nicht im eigentlichen Sinne des Konzepts vorgedacht ist. Nichtsdestotrotz kann es bei einer Einzelarbeit, wie dieser vorkommen, dass alle Rollen selbst vom Autor getragen werden. Die Organisation sieht wie folgt aus:

### SCRUM Master/Product Owner/Developer
```
Taher Al Saegh
Bertastrasse 2
8003 Zürich
Gitlab: taher.alsaegh
```

### Endbenutzer
```
Kubinet AG
Musterstrasse 10
3001 Bern
```

### Dozenten
```
Vor-/Nachname: Patrick Morgenegg
Funktion: Fachexperte DevOps
E-Mail: patrick.morgenegg@tbz.ch
Github: patrickmorgeneggtbz
```
```
Vor-/Nachname: Florian Huber
Funktion: Fachexperte Projektmanagement
E-Mail: florian.huber@tbz.ch
```

## Projektziele
Im folgenden Abschnitt werden die Ziele dieser Semesterarbeit definiert. Ausgangslange bildet die Analyse des aktuellen Zustands (IST-Zustand), aus dem anschliessend der gewünschte Soll-Zustand sowie die konkreten Projektziele abgeleitet werden.

### IST-Analyse
Aktuell werden containerisierte Applikationen häufig über klassische CI/CD-Pipelines bereitgestellt, die nur teilweise automatisiert sind und meist keine integrierten Sicherheitsmechanismen enthalten. Dadurch können fehlerhafte oder verwundbare Container-Images in produktionsnahe Umgebungen gelangen.
In vielen Umgebungen fehlt eine klare Trennung zwischen Build-, Security- und Deployment-Schritten, und Deployments erfolgen teilweise manuell oder ohne konsequente Nachvollziehbarkeit.

Die fiktive Firma Kubinet AG verwendet GitHub Actions als CI-Pipeline und führt Deployments in ein Kubernetes-Cluster aktuell ohne automatisierte Security-Gates und ohne GitOps-Prinzipien durch. Dadurch bestehen folgende Risiken:

- Unsichere oder veraltete Images können unbemerkt deployed werden.
- Manuelle Eingriffe führen zu Inkonsistenzen und Fehlern.
- Fehlende Transparenz erschwert Audits und Compliance.
- Keine vollständige Rückverfolgbarkeit von Änderungen.

### SOLL-Analyse (Systemziele)

Der Soll-Zustand beschreibt die gewünschte Zielarchitektur der Deployment-Pipeline und die Anforderungen an den zukünftigen Workflow:
 - Deployments sollen vollständig automatisiert, reproduzierbar und versioniert sein.
 - Sicherheitsprüfungen sollen fest in den Pipeline-Ablauf integriert sein.
 - Der Deployment-Prozess soll nach GitOps-Prinzipien erfolgen d.h Änderungen werden ausschliesslich über Git gesteuert.
 - Das System soll leicht erweiterbar und testbar sein, insbesondere für zukünftige Security-Integrationen.
 - Der PoC soll demonstrieren, dass sichere, reproduzierbare und nachvollziehbare Deployments mittels GitOps und DevSecOps erfolgreich umsetzbar sind.

### SAMAT-Ziele

- **Spezifisch**: Aufbau eines GitOps-basierten Deployment-Workflows inkl. Sicherheitsprüfungen.

- **Messbar**: Deployment erfolgt über Kubernetes und die Sicherheitsanalyse ist durch das DVWA zu klar zu erkennen.

- **Akzeptiert**: Ziele entsprechen den Vorgaben der Semesterarbeit und sind realistisch umsetzbar.

- **Anspruchsvoll**: Integration mehrerer Tools (GitHub Actions, ArgoCD, Trivy, Kubernetes).

- **Terminiert**: Umsetzung der Arbeit erfolgt in 3 Sprints und ist am 27.01.2026 abzugeben.

## Abwicklungsziele

Die Abwicklungsziele beschreiben die wesentlichen Merkmale des Projektweges, die zur Erreichung
der Systemziele nötig sind. (B.Jenny, 2019, S. 132)

Das Projekt wird nach der agilen Projektmanagementmethode Scrum umgesetzt. Es ist in drei Sprints unterteilt, die jeweils konkrete User-Stories beinhalten. Nach jedem Sprint liegt ein Zwischenstand des Projektes vor. Der Fortschritt wird durch Sprint-Reviews überprüft und mit Sprint Retrospektiven reflektiert und verbessert. Anforderungen und Aufgaben können während der Entwicklung angepasst oder verfeinert werden. Die Umsetzung erfolgt in Zyklen, wodurch Risiken frühzeitig erkannt und der Projekterfolg schrittweise gesichert wird.

### Definition of Done (DoD)

Die Definition of Done (DoD) beschreibt eine klare Vereinbarung innerhalb des Teams, welche
Kriterien erfüllt sein müssen, damit das Product Backlog Item oder ein Sprint als fertig gilt. (Gärtner, 2020)

In den unten beschriebenen Punkten werden die nötigen Schritte definiert, welche dafür sorgen, dass
dieses Projekt als erledigt gilt. Neben den Akzeptanzkriterien, die jeweils in den User-Stories definiert
sind, gilt die DoD generell zur Erledigung des Projekts.

- **Inhaltliche Vollständigkeit**: Alle beschriebenen Anforderungen der Story oder Aufgabe wurden umgesetzt.
- **Dokumentation erstellt oder aktualisiert:**: Relevante Inhalte sind in der Semesterarbeit, im Architekturdiagramm oder in technischen Dokumenten nachvollziehbar dokumentiert.
- **Zeremonien eingehalten**: Alle in SCRUM beinhalteten Zeremonien sind eingeplant und werden durgefürht.
- **Qualitätsanforderungen eingehalten**: Verständliche Formulierung, korrekte Struktur und keine Rechtschreib- oder Grammatikfehler.
- **Testing durchgeführt**: Die Implemtierung ist erfolgreich getestet und läuft durch alle CI/CD Steps durch.

### Meilensteine
1. Meilenstein: Initialisierungsphase
   Ziel: Projektstart, Definition von Zielen, Rahmenbedingungen und Rollen
   Erledigt: XX

2. Meilenstein: Konzeptionsphase
   Ziel: Ausarbeitung der Systemarchitektur, Schnittstellen, Ressourcen- und Risikoplanung
   Erledigt: XX

3. Meilenstein: Realisierungsphase
   Ziel: Technsiche Umsetzung des GitOps-Workflows, Deployment auf K8s, Security Tests und Validation sicherstellen
   Erledigt: XX

4. Meilenstein: Einführungsphase
   Ziel: Fazit, Reflextion, Lessons Learned,
   Erledigt: XX

## Roadmap / Releases-Planning

### 1. Sprint vom xx.xx - xx.xx.2025

Als Table mit den Stories/Tasks und Akzepttanzkriterien und Sprint Goals

### 2. Sprint vom xx.xx - xx.xx.2025

Als Table mit den Stories/Tasks und Akzepttanzkriterien

### 3. Sprint vom xx.xx - xx.xx.2025

Als Table mit den Stories/Tasks und Akzepttanzkriterien

## Anforderungsdefinition

### Funktionale Anforderung

### Nicht-funktionale Anforderungen

# Konzeptionsphase

## Theoretische Grundlagen

- CI/CD
- Kubnernetes & ArgoCD
- Security Aspekte (Trivy & DevSecOps)
- GitHub Actions
- Flask

## Systemgrenzen

### SEUSAG

#### Interne-Schnittstellen

#### Externe-Schnittstellen

## Ressourcen

### Ressourcenplanung

### Nicht-verzehrbare Mittel

### Verzehrbare Mittel

## Risikomanagement

### Risikoregister

### Risikoportfolio

## GitOps Konzept

## Security Konzept

### Evaluation von Trivy etc.

## Test Konzept

# Realisierungsphase

## GitHub-Repository & Branching

## FlaskApp & Tests

## App in Docker

## CI/CD Pipeline

## Kubernetes minikube & ArgoCD implementation

## Security implementation

- Trivy implementieren
- Secret Management
- RBAC / Least Privilege

## Post Deploy Smoke Tests

# Einführungsphase

## Fazit

### Evaluation / Zielerreichung

## Reflexion

### Lesson Learned

## Aussicht

# Literaturverzeichnis

# Anhang

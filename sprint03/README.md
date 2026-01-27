# 3. Sprint vom 06.12 - 23.01

![Sprint Board](../image/03sprint_board.png)

| Story                                   | Akzeptanzkriterium                       | Points |
| :-------------------------------------- | :--------------------------------------- | :----- |
| DAST implementation                     | [SEM04-46](https://tinyurl.com/546453wc) | 5      |
| GitOps verification pipeline erstellen  | [SEM04-47](https://tinyurl.com/2s35nxkw) | 5      |
| Lösung für den Build in MAIN erarbeiten | [SEM04-48](https://tinyurl.com/9ucwy3jz) | 4      |
| Testing                                 | [SEM04-49](https://tinyurl.com/yzjhwayj) | 4      |


**Sprint Goal**: Am Ende des Sprints ist die Anwendung vollständig GitOps-basiert in Kubernetes deployt und zur Laufzeit testbar.

# Sprint Review

1. **Zielerreichung** <br>
   a. Wurde das Sprint-Ziel erreicht? <br>
   Am Ende des Sprints wurde das Ziel erreicht. Die Image Version wird automatisch nach einem Merge von dev in main überprüft und durch ein Pull Request zum updaten des K8s Clusters ergäntzt.  

   b. Welche User Stories wurden vollständig umgesetzt? <br>
   Alle Stories wurden erfolgreich umgesetzt.

2. **Produktinkrement** <br>
   a. Was wurde im Sprint konkret geliefert? <br>
   In diesem Sprint wurde die DAST-Integration hinzugefügt und eine weitere Pipeline, welche das aktuelle Image überprüft und durch ein PR den K8s Cluster aktuell hält.

   b. Welche Funktionalitäten sind produktiv nutzbar? <br>
   Von nun an können die Entwicker an ihrem Code arbeiten und gleichzeitig werden sie über Sicherheitsschwachstellen informiert. Das Deployment auf eine produktive Umgebung ist ganz einfach automatisiert, sodass es nur noch über einen PR apporved werden muss.


3. **Abweichungen & offene Punkte** <br>
   a. Welche geplanten Inhalte konnten nicht umgesetzt werden? <br>
   Keine

   b. Warum wurden diese Inhalte nicht abgeschlossen? <br>
   Keine
   
   c. Müssen Stories in den nächsten Sprint übernommen werden? <br>
   Es werden keine Stories übernommen.<br>

# Sprint Retrospektive

![Retro](../image/03sprint_retro.png)

## Liked

- Die vollständige GitOps-Automatisierung konnte erfolgreich umgesetzt werden, inklusive Pull-Request-basierter Aktualisierung des Kubernetes-Deployments.
- Die DAST-Integration lieferte aussagekräftige Ergebnisse und ergänzte die bestehenden statischen Sicherheitsprüfungen sinnvoll.

## Leared

- Automatisierte PRs sind ein effektiver Weg, um Kontrolle und Nachvollziehbarkeit trotz hoher Automatisierung sicherzustellen.

## Lacked

- Dokumentation der DAST-Ergebnisse direkt im GitHub-Security-Kontext (Issues/Annotations).

## Longed for

- Erweiterte DAST-Profile mit Authentifizierung und tieferem Crawl-Verhalten.
- Zentrale Auswertung aller Security-Scans in einem Dashboard.
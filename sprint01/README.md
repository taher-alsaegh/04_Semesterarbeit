# 1. Sprint vom 09.12 - 22.12

![Sprint Board](../image/01sprint_board.png)

| Story                             | Akzeptanzkriterium                       | Points |
| :-------------------------------- | :--------------------------------------- | :----- |
| Security Konzept erstellen        | [SEM04-32](https://shorturl.at/EOXJX)    | 5      |
| Git-Repository Struktur ausfetzen | [SEM04-34](https://shorturl.at/7ThLE)    | 1      |
| Ci-Pipeline Grundgerüst erstellen | [SEM04-35](https://shorturl.at/kyv76)    | 2      |
| DVPWA Docker Image vorbereiten    | [SEM04-36](https://shorturl.at/voJ7B)    | 2      |
| GitOps-Repo initialisieren        | [SEM04-37](https://shorturl.at/85Fhm)    | 2      |
| Minikube & ArgoCD aufsetzen       | [SEM04-38](https://tinyurl.com/ymcarjx8) | 2      |

**Sprint Goal**: Am Ende des Sprints steht die Grund-Infrastruktur der Projektarbeit und das Grundgerüst der Security Pipeline.

# Sprint Review

1. **Zielerreichung** <br>
   a. Wurde das Sprint-Ziel erreicht? <br>
   Das Sprint Ziel wurde erreicht. Alle Stories konnten, wie geplant erledigt werden.

   b. Welche User Stories wurden vollständig umgesetzt? <br>
   Alle User-Stories wurden erledigt. Es sind keine neuen Aufgaben hinzugekommen.

2. **Produktinkrement** <br>
   a. Was wurde im Sprint konkret geliefert? <br>
   In diesem Sprint wurde das Grundgerüst für die Projektarbeit aufgebaut. Das beinhaltet die Initialisierung der Repositories und das VM Setup für den Kubernetes Cluster. Ausserdem konnte bereits mit der CI Pipeline gestartet werden.

   b. Welche Funktionalitäten sind produktiv nutzbar? <br>
   Momentan steht der K8s Cluster mit dem ArgoCD Service. Das Main Repo ist im ArgoCD hinterlegt und wird aktiv gesynct.

3. **Abweichungen & offene Punkte** <br>
   a. Welche geplanten Inhalte konnten nicht umgesetzt werden? <br>
   Keine

   b. Warum wurden diese Inhalte nicht abgeschlossen? <br>
   Keine
   
   c. Müssen Stories in den nächsten Sprint übernommen werden? <br>
   Es werden keine Stories übernommen.<br>

# Sprint Retrospektive

![Retro](../image/01sprint_retro.png)

## Liked

- In diesem Sprint bin ich sehr gut vorwärts gekommen, obwohl ich aus Projektmanagement Sicht einiges anpassen musste. Die komplette Projektinitialisierungsphase wurde als Vorarbeit abgehandelt, anstatt wie vorgesehen im Sprint 1.
- Ich konnte zum Thema K8s sehr viel neues dazulernen. Da hat mir insbesondere KodeKloud und die offizielle Dokumentation von Kubernetes gut weitergeholfen.
- Zum Thema DevSecOps wusste ich bis anhin auch nicht viel, doch das TBZ Repo von Patrick Morgenegg war für mich eine solide Stütze, um mich mit dem Thema familier zu machen.

## Leared

- Ich habe gelert, wie ich eine CI-Pipeline aufbaue und welche Kernfunktionen ich nutzen soll.
- Das Aufsezten von ArgoCD habe ich zuvor auch noch nie gemacht. Ich habe es bisher nur aus der Theorie gekannt.
- Auch habe ich nie gross mit Multi-Branches gearbeitet. Es ist beeindruckend zu sehen, wie sich die effizienz steigert, wenn man mit mehreren Branches arbeitet.
- Nach der Sprint Umstellung habe ich auch ein besseres Gefühl zum Thema Srum bekommen und weiss nun, wie ich meine Arbeitsmethodik in Zusammenhang mit Scrum zukünftig einsezten werde.

## Lacked

- Ich hatte zum Teil das Gefühl das Projektmanagement aussen vor zu lassen, während ich an der Realisierung dran war. Trotzdem habe ich mir stets Zeit eingeplant, um meine Stories zu überprüfen.

## Longed for

- Was ich mir wünschen würde, wäre eine saubere Dokumentation zum Thema Kubernetes, sowie es bei DevSecOps der Fall war.

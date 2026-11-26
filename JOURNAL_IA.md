# Journal IA — Kilasy

Outil utilisé : Claude (chat), terminal

## Changement : pénalité de retard (C1)

### Échange 1 — 22:37
Demande : coller la consigne C1 et demander quoi faire.
Proposition : lire le code (contrôleurs, GradeReport, CsvExport) avant de modifier.
Décision : gardé.
Pourquoi : je ne connaissais pas le code.
Vérification : j'ai collé les fichiers demandés.

### Échange 2 — 22:42
Demande : « Propose le changement minimal. »
Proposition : même calcul de pénalité (-10 %/jour, plafond 50 %) copié dans
SubmissionController (2 endroits), GradeReport et CsvExport. Elle a aussi
repéré que le CSV tronquait alors que les autres arrondissaient.
Décision : gardé.
Pourquoi : pas de réorganisation autorisée ; l'écart d'arrondi était réel
(Emma : 13.8 vs 13,7 avant le changement).
Vérification : transcript, CSV et /submissions/{id} comparés sur les cas
1, 2, 3 et 8 jours de retard : mêmes notes.

### Échange 3 — 22:50
Demande : tester la correction elle-même.
Proposition : noter la soumission 7 (8/10, 1 jour de retard).
Décision : gardé.
Pourquoi : c'était le seul critère non testé.
Vérification : 14.4 dans la réponse, le relevé et le CSV.

## Bilan
- Fichiers modifiés : SubmissionController.java, GradeReport.java, CsvExport.java
- Point d'attention : le calcul est dupliqué à 4 endroits, ce qui est fragile.

## Changement : notification par SMS (C2)

### Échange 4 — 23:12
Demande : coller la consigne C2 et demander quoi faire.
Proposition : une interface SmsSender et une implémentation LogSmsSender (SMS simulé
dans les logs), appelée depuis SubmissionController dans un try/catch, après
l'enregistrement de la note et l'envoi de l'email.
Décision : gardé.
Pourquoi : le critère 3 (changer de fournisseur sans toucher à la notation) impose une
interface ; cela oblige à créer 2 petits fichiers, sans réorganiser le code existant.
Vérification : note de la soumission 7 : ligne [SMS] dans les logs, email dans Mailpit.

### Échange 5 — 23:27
Demande : simuler une panne du SMS.
Proposition : faire lever une exception à LogSmsSender, noter la soumission 12, puis
restaurer le fichier.
Décision : gardé.
Pourquoi : c'est le test demandé par la consigne pour le critère 2.
Vérification : réponse HTTP 200 avec grade 15.0 ; /submissions/12 et le relevé
affichent 15.0 : la note reste publiée. Fichier restauré (grep "panne" vide).

## Bilan C2
- Fichiers modifiés : SubmissionController.java
- Fichiers ajoutés : SmsSender.java, LogSmsSender.java

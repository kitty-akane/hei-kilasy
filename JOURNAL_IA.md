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

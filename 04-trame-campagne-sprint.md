## Trame de campagne de sprint priorisée par risque

- Phase du cycle : planification
- Pattern : R.C.T.F.C
- Cas d'usage : en début de sprint, il faut bâtir rapidement une trame de campagne à partir des user stories livrées, avec un premier tri par risque, avant validation humaine du périmètre.

### Gabarit

```
Rôle : Tu es testeur logiciel senior certifié ISTQB, en charge de la
planification d'une campagne de tests.
Contexte : Application FitRes. User stories du sprint : <liste des
user stories du sprint, une ligne par story>.

Tâche : Propose une trame de campagne : regroupe les stories par
fonctionnalité, identifie pour chacune un niveau de risque
(impact x probabilité) et une justification courte, et propose un
ordre de priorité de test.

Format : Tableau Fonctionnalité | Stories concernées | Risque
(faible/moyen/élevé) | Justification | Ordre de priorité.

Contraintes : En français ; pas plus d'une ligne par fonctionnalité ;
ne pas inventer de story non fournie.
```

### Exemple de sortie (teste sur FitRes le 20/08/2026)

Stories testées : US-05 (liste d'attente), US-12 (paiement créneau premium), US-18 (modification de profil).

| Fonctionnalité | Stories | Risque | Justification | Priorité |
|---|---|---|---|---|
| Liste d'attente | US-05 | Élevé | Logique métier nouvelle avec délai de confirmation, parcours vital de réservation | 1 |
| Paiement créneau premium | US-12 | Élevé | Impact financier direct, règle de calcul RG-TARIF impliquée | 2 |
| Modification de profil | US-18 | Faible | Fonction périphérique, pas de règle métier critique | 3 |

### Vigilance

La trame proposée par l'IA est une base de discussion, pas un arbitrage final : le niveau de risque et l'ordre de priorité doivent être validés en équipe — c'est la stratégie qui engage, pas la génération.

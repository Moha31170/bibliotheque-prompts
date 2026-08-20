## Clarifier une exigence ambiguë avant conception

- Phase du cycle : analyse
- Pattern : questions d'abord
- Cas d'usage : une exigence métier arrive formulée en une phrase vague, sans règle chiffrée ni cas limite explicite. À sortir systématiquement avant d'écrire le premier cas de test.

### Gabarit

```
Rôle : Tu es testeur logiciel senior certifié ISTQB.
Contexte : Application FitRes, réservation de créneaux sportifs.
Voici l'extrait d'exigence à analyser : « <exigence brute collée telle quelle> ».

Tâche : Avant toute production, liste les ambiguïtés, informations
manquantes et contradictions que tu identifies dans cette exigence,
sous forme de questions numérotées classées par criticité
(bloquant / important / secondaire).

Contraintes : Ne génère aucun cas de test à ce stade. En français.
```

### Exemple de sortie (teste sur FitRes le 20/08/2026)

Exigence testée : « le système limite le nombre de réservations par utilisateur ».

```
Criticité bloquante :
- Quel est le nombre maximal de réservations autorisées par utilisateur ? La valeur (ex. 3, 5, 10) n'est pas définie.
- La limite porte-t-elle sur les réservations futures, les réservations actives, ou toutes les réservations de l'utilisateur ?
- La limite est-elle globale à l'ensemble de l'application ou définie par activité, équipement, séance, salle ou type de créneau ?
- Sur quelle période la limite s'applique-t-elle ? Est-elle permanente, quotidienne, hebdomadaire, mensuelle, ou calculée sur une période glissante ?
- À quel moment une réservation est-elle comptabilisée dans la limite ? Lors de sa création, après confirmation, après paiement, ou à un autre moment ?
- Que se passe-t-il lorsqu'un utilisateur atteint la limite ? La nouvelle réservation doit-elle être refusée, bloquée temporairement ou soumise à une validation particulière ?
- Une réservation annulée libère-t-elle une place dans la limite ? Si oui, immédiatement ou après un certain délai ?
- Une réservation passée continue-t-elle à compter dans la limite ? Si oui, jusqu'à quand ?
- Comment la limite est-elle appliquée en cas de réservation simultanée ? Le système doit-il garantir qu'un utilisateur ne puisse jamais dépasser la limite malgré plusieurs demandes concurrentes ?

Criticité importante :
- La limite est-elle identique pour tous les utilisateurs ou dépend-elle de leur profil, abonnement, rôle ou niveau d'accès ?
- Existe-t-il des utilisateurs exemptés de cette limitation, par exemple les administrateurs, coachs ou comptes professionnels ?
- La limite concerne-t-elle uniquement les réservations confirmées ou également les réservations en attente, provisoires ou en cours de paiement ?
- Que se passe-t-il lorsqu'une réservation est modifiée ? Une modification vers un autre créneau doit-elle être considérée comme une nouvelle réservation pour le calcul de la limite ?
- Que se passe-t-il lorsqu'un utilisateur réserve plusieurs places pour une même séance ? La limite porte-t-elle sur le nombre de réservations ou sur le nombre de places réservées ?
- Une réservation effectuée par un utilisateur pour une autre personne est-elle comptabilisée dans sa propre limite ?
- La limite est-elle calculée à partir de l'identifiant du compte utilisateur ou d'un autre critère permettant d'identifier l'utilisateur ?
- Le système doit-il informer l'utilisateur de la limite maximale et du nombre de réservations qu'il lui reste ?
- Le comportement attendu est-il défini lorsqu'une limite est modifiée alors que des utilisateurs ont déjà des réservations dépassant la nouvelle limite ?

Criticité secondaire :
- Le nombre de réservations restantes doit-il être affiché sur la page de réservation, sur la page « Mes réservations », ou ailleurs ?
- Un message spécifique doit-il être affiché lorsque la limite est atteinte ? Si oui, quel contenu et quel niveau d'information sont attendus ?
- La limite doit-elle être la même sur tous les canaux d'accès à l'application (web, mobile, API, etc.) ?
- Existe-t-il des règles particulières concernant les réservations récurrentes ou groupées dans le calcul de la limite ?
- La limite doit-elle être configurable par un administrateur ? Si oui, selon quels paramètres et avec quelles valeurs autorisées ?
- Que doit-il se passer lorsqu'une réservation expire automatiquement ou est annulée par le système ? Doit-elle continuer à être prise en compte dans la limite ?
- La règle de limitation doit-elle être appliquée immédiatement après chaque changement de réservation ou selon une mise à jour différée ?
```

### Vigilance

1.Aucune question ne doit avoir sa réponse déjà disponible dans le référentiel (règles métier, sélecteurs, documentation existante). Si c'est le cas, c'est un signe que le contexte fourni dans le prompt était incomplet, il faut alors reformuler la question en confirmation, ou la retirer.

2.Éliminer les questions redondantes : sur une liste longue, plusieurs formulations différentes interrogent souvent le même point. Les fusionner avant diffusion, sinon le métier répond deux fois à la même chose.

3.Ne pas prendre la classification de criticité (bloquant / important / secondaire) proposée par l'IA comme un arbitrage final, c'est un tri de départ à challenger. Une question rangée en « secondaire » peut s'avérer bloquante si elle touche un critère d'acceptation attendu, et inversement.

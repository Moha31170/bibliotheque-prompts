## Cas de test depuis une règle métier (format Squash)

- Phase du cycle : conception
- Pattern : generation structuree
- Cas d'usage : une règle métier est stabilisée et non ambiguë ; il faut produire des cas de test exploitables directement dans l'outil de gestion de campagne (Squash).

### Gabarit

```
Rôle : Tu es testeur logiciel senior certifié ISTQB.
Contexte : Application FitRes. Règle métier : <règle métier complète>.

Tâche : Génère les cas de test de cette règle, y compris les valeurs
limites.

Format : Tableau ID | Titre | Préconditions | Étapes | Résultat
attendu | Priorité — format directement importable dans Squash.

Contraintes : Couvre chaque zone de la règle et ses bornes ; un cas
par ligne ; en français ; pas de cas redondant.
```

### Exemple de sortie (teste sur FitRes le 20/08/2026)

Règle testée : annulation gratuite à plus de 24h, avoir de 50 % entre 24h et 2h, rien à moins de 2h.

| ID     | Titre                       | Préconditions                                                   | Étapes                                                                                           | Résultat attendu                                                                      | Priorité |
| ------ | --------------------------- | --------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------- | -------- |
| CT-001 | Annulation à plus de 24h    | Une réservation est créée pour un créneau dans plus de 24h      | 1. Accéder à « Mes réservations »<br>2. Sélectionner la réservation<br>3. Annuler la réservation | L’annulation est acceptée et l’utilisateur obtient un remboursement de **100 %**      | Haute    |
| CT-002 | Annulation exactement à 24h | Une réservation est créée pour un créneau dans exactement 24h   | 1. Accéder à « Mes réservations »<br>2. Sélectionner la réservation<br>3. Annuler la réservation | L’annulation est acceptée et l’utilisateur obtient un avoir de **50 %**               | Critique |
| CT-003 | Annulation entre 24h et 2h  | Une réservation est créée pour un créneau situé entre 24h et 2h | 1. Accéder à « Mes réservations »<br>2. Sélectionner la réservation<br>3. Annuler la réservation | L’annulation est acceptée et l’utilisateur obtient un avoir de **50 %**               | Haute    |
| CT-004 | Annulation exactement à 2h  | Une réservation est créée pour un créneau dans exactement 2h    | 1. Accéder à « Mes réservations »<br>2. Sélectionner la réservation<br>3. Annuler la réservation | L’annulation est acceptée et l’utilisateur obtient un avoir de **50 %**               | Critique |
| CT-005 | Annulation à moins de 2h    | Une réservation est créée pour un créneau situé à moins de 2h   | 1. Accéder à « Mes réservations »<br>2. Sélectionner la réservation<br>3. Annuler la réservation | L’annulation est acceptée et l’utilisateur ne reçoit **aucun remboursement ni avoir** | Haute    |

### Vigilance

Vérifier que tous les intervalles et les bornes 24 h et 2 h sont couverts, sans chevauchement ni omision, et que chaque résultat respecte strictement la règle métier, sans ajout d'informations non précisées.

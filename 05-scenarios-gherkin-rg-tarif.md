## Scénarios Gherkin depuis une règle de calcul

- Phase du cycle : conception
- Pattern : generation structuree
- Cas d'usage : la règle métier est stabilisée et doit être formalisée en scénarios Gherkin pour alimenter un outil BDD ou documenter le comportement attendu de façon lisible par le métier.

### Gabarit

```
Rôle : Tu es testeur logiciel senior certifié ISTQB.
Contexte : Application FitRes. Règle métier : <règle métier complète>.

Tâche : Génère un scénario Gherkin par cas significatif de la règle
(nominal, limites, cumul si applicable).

Format : Scénario / Étant donné / Quand / Alors, un scénario par cas,
en Gherkin standard.

Contraintes : En français ; noms de scénario explicites ; pas de
scénario redondant.
```

### Exemple de sortie (teste sur FitRes le 20/08/2026)

Règle testée : RG-TARIF (base 10 EUR, premium -20 %, heures creuses -30 %, cumul plafonné à -40 %).

```gherkin
Scénario : Membre premium réservant en heures creuses, cumul plafonné
  Étant donné un membre avec un statut premium
  Et un créneau en heures creuses
  Quand il réserve le créneau
  Alors le prix affiché est de 6,00 EUR
  Et le message indique que la remise est plafonnée à -40 %

Scénario : Membre standard réservant en heures creuses
  Étant donné un membre sans statut premium
  Et un créneau en heures creuses
  Quand il réserve le créneau
  Alors le prix affiché est de 7,00 EUR
```

### Vigilance

Recompter chaque montant du scénario contre la grille RG-TARIF (10,00 / 8,00 / 7,00 / 6,00 EUR) et vérifier que le plafond à -40 % est bien appliqué dans le scénario cumulé

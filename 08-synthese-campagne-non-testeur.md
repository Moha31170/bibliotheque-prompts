## Synthèse de campagne pour un lecteur non testeur

- Phase du cycle : cloture
- Pattern : analyse de campagne
- Cas d'usage : à la fin d'une campagne, produire un rapport court et lisible pour le chef de projet, à partir des résultats bruts issus des outils.

### Gabarit

```
Rôle : Tu es testeur logiciel senior certifié ISTQB.
Contexte : Application FitRes. Voici les résultats de la campagne
<nom de la campagne> et le périmètre prévu : <coller résultats bruts
ou tableau de synthèse>.

Tâche : Produis un rapport court : taux de réussite par
fonctionnalité, échecs regroupés par cause probable, tendance par
rapport à la campagne précédente si fournie, et 3 actions
prioritaires.

Format : Rapport court pour un chef de projet non testeur, sans
jargon technique inutile.

Contraintes : N'invente aucun chiffre non présent dans les données
fournies ; en français.
```

### Exemple de sortie (teste sur FitRes le 20/08/2026)

Données testées : 39 tests exécutés, 36 réussis, 3 échecs (2 sur le module réservation, 1 sur le module annulation).

> **Résultat global : 36/39 tests réussis (92 %).**
>
> - Réservation de créneaux : 2 échecs sur 15 tests, tous liés à un sélecteur de bouton modifié récemment (fragilité de test, pas de bug applicatif confirmé).
> - Annulation : 1 échec sur 10 tests, lié à un calcul d'avoir incorrect sur le cas limite à 24h — à investiguer en priorité.
> - Autres modules : 100 % de réussite.
>
> **Actions prioritaires :**
>
> 1. Corriger le sélecteur fragile du module réservation.
> 2. Ouvrir une anomalie sur le calcul d'avoir à la limite de 24h.
> 3. Reconduire la campagne complète après correction avant la mise en production.

### Vigilance

Chaque chiffre du rapport doit être vérifié à la source (39, 36, 92 %) avant envoi : ne jamais publier un taux calculé ou reformulé par l'IA sans le recalculer soi-même.

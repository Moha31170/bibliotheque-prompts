## Contre-vérification croisée d'un script Playwright

- Phase du cycle : implementation
- Pattern : contre-verification
- Cas d'usage : un script d'automatisation généré par une première IA doit être audité par une seconde IA indépendante avant revue humaine, pour un parcours critique (réservation, paiement, connexion).

### Gabarit

```
Rôle : Tu es testeur logiciel senior spécialisé en automatisation
Playwright, agissant comme second auditeur indépendant.
Contexte : Application FitRes, parcours <nom du parcours>. Voici le
script généré par un autre assistant, sans son raisonnement :
<coller le script>.

Tâche : Évalue de façon indépendante ce script selon 3 axes :
robustesse des sélecteurs (locators orientés utilisateur ou
data-testid, pas de sélecteurs CSS/XPath fragiles), présence
d'assertions fortes et spécifiques (expect() avec auto-retry, pas de
simple absence d'exception), bon usage de l'auto-attente native de
Playwright (pas de page.wait_for_timeout ni de sleep arbitraire en
remplacement des assertions).
Rends un verdict : conforme / à compléter / à refaire, avec
justification par axe.

Contraintes : En français ; pas de réécriture du script à ce stade,
uniquement l'évaluation.
```

### Exemple de sortie (teste sur FitRes le 20/08/2026)

Script audité : parcours de réservation d'un créneau (`page.get_by_test_id("btn-reserver")`).

> **Sélecteurs : conforme** — utilisation de `get_by_test_id`, cohérent avec les attributs `data-testid` du référentiel FitRes ; pas de sélecteur CSS positionnel.
> **Assertions : à compléter** — le script clique puis vérifie seulement `page.url` sans contrôler le message de confirmation. Ajouter `expect(page.locator(".confirmation")).to_have_text("Réservation confirmée")`.
> **Auto-attente : à refaire** — un `page.wait_for_timeout(5000)` est inséré avant la vérification, ce qui contourne l'auto-attente native de Playwright ; à remplacer par une assertion `expect(...).to_be_visible()`, qui réessaie automatiquement jusqu'au timeout par défaut.
>
> **Verdict global : à compléter.**

### Vigilance

Les deux IA (celle qui a généré, celle qui audite) peuvent partager le même angle mort — par exemple ne pas relever qu'un `get_by_test_id` est correct en apparence mais pointe vers le mauvais bouton. Vérifier en particulier qu'aucun `wait_for_timeout` ne remplace une assertion `expect()` : c'est le réflexe Selenium (attente aveugle) le plus susceptible de survivre dans du code généré « façon Playwright » sans exploiter son auto-attente. Le croisement réduit le risque, il ne le supprime pas : la revue humaine reste obligatoire avant merge, conformément à la definition of done.

## Diagnostic d'échec CI

- Phase du cycle : execution
- Pattern : diagnostic d'echec
- Cas d'usage : un test automatisé passait la veille et échoue aujourd'hui en pipeline ; il faut qualifier rapidement la cause avant d'ouvrir une anomalie.

### Gabarit

```
Rôle : Tu es testeur logiciel senior spécialisé en automatisation.
Contexte : Pipeline GitLab CI, projet fitres-tests. Le test <nom du
test> passait hier, il échoue aujourd'hui.

Tâche : Voici le code du test, le message d'erreur complet et la
stack trace : <coller code + erreur + stack trace>.
Propose les 3 causes les plus probables, classées, en distinguant :
défaut de l'application / fragilité du test / problème
d'environnement. Pour chacune, indique comment la confirmer ou
l'écarter.

Contraintes : En français ; réponse actionnable, pas de généralités.
```

### Exemple de sortie (teste sur FitRes le 20/08/2026)

Erreur testée : `NoSuchElementException` sur `#btn-login`.

> 1. **Fragilité du test (la plus probable)** — Le sélecteur `#btn-login` a peut-être été remplacé par `[data-testid="btn-login"]` lors d'une refonte récente du HTML. _Confirmer :_ inspecter le DOM actuel de la page de connexion ; comparer avec le dernier commit front-end.
> 2. **Problème d'environnement** — Le temps de chargement de la page a pu augmenter (environnement de test surchargé), et le test n'attend pas assez avant de chercher l'élément. _Confirmer :_ vérifier si un `WebDriverWait` explicite est présent ; rejouer localement avec un réseau lent simulé.
> 3. **Défaut de l'application** — La page de connexion pourrait ne plus se charger correctement (erreur JS bloquante). _Confirmer :_ ouvrir l'URL manuellement et vérifier la console navigateur.

### Vigilance

L'IA n'a pas vu l'exécution réelle : chaque hypothèse doit être confrontée aux logs CI et à l'application avant de trancher.

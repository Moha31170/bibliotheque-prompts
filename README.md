# Bibliothèque de prompts

**Auteur :** Mohamed
**Date de création :** 20/08/2026

## Format de fiche

Chaque gabarit est documenté dans un fichier dédié selon le format suivant :

```markdown
## <Nom du gabarit>

- Phase du cycle : <planification | analyse | conception | implementation | execution | cloture>
- Pattern : <R.C.T.F.C | questions d'abord | generation structuree | critique | contre-verification | diagnostic d'echec | analyse de campagne>
- Cas d'usage : <quand sortir ce gabarit>

### Gabarit

(le prompt complet, variables en <chevrons>)

### Exemple de sortie (teste sur FitRes le <date>)

(extrait de la sortie reellement obtenue)

### Vigilance

(ce qu'il faut systematiquement verifier dans la sortie)
```

## Les 8 situations de la bibliothèque

| #   | Situation                                                                   | Phase ISTQB    | Fichier                                        |
| --- | --------------------------------------------------------------------------- | -------------- | ---------------------------------------------- |
| 1   | Clarifier une exigence ambiguë sur la limite de réservations                | Analyse        | `01-clarifier-exigence-limite-reservations.md` |
| 2   | Concevoir les cas de test de la règle d'annulation pour Squash              | Conception     | `02-cas-test-regle-annulation.md`              |
| 3   | Diagnostiquer un échec CI sur le test de connexion                          | Exécution      | `03-diagnostic-echec-btn-login.md`             |
| 4   | Bâtir la trame d'une campagne de sprint avec priorisation par risque        | Planification  | `04-trame-campagne-sprint.md`                  |
| 5   | Convertir la grille RG-TARIF en scénarios Gherkin                           | Conception     | `05-scenarios-gherkin-rg-tarif.md`             |
| 6   | Générer un jeu de données CSV d'emails valides/invalides pour l'inscription | Implémentation | `06-jeu-donnees-emails-csv.md`                 |
| 7   | Faire auditer un script Playwright de réservation par une IA indépendante   | Implémentation | `07-contre-verification-script-playwright.md`  |
| 8   | Rédiger la synthèse de fin de campagne pour le chef de projet               | Clôture        | `08-synthese-campagne-non-testeur.md`          |

Situations personnelles: **#4** et **#7**

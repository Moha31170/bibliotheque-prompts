## Jeu de données fictives (CSV) pour un champ de saisie

- Phase du cycle : implementation
- Pattern : generation structuree
- Cas d'usage : préparer les données d'entrée d'un script automatisé (nominal, limites, invalides) sans jamais utiliser de données réelles.

### Gabarit

```
Rôle : Tu es testeur logiciel senior spécialisé en automatisation.
Contexte : Application FitRes, champ <nom du champ> sur le formulaire
<nom du formulaire>. Règles de validation attendues : <règles de
validation connues>.

Tâche : Génère un jeu de données fictives pour tester ce champ :
valeurs nominales valides, valeurs limites, valeurs invalides.

Format : CSV avec en-têtes value,categorie,resultat_attendu.

Contraintes : Uniquement des données fictives (aucune donnée réelle
ou plausible d'un vrai utilisateur) ; en français pour les libellés ;
au moins 3 lignes par catégorie.
```

### Exemple de sortie (teste sur FitRes le 20/08/2026)

Champ testé : email d'inscription.

```csv
value,categorie,resultat_attendu
test.fictif@exemple.fr,valide,inscription acceptée
a@b.io,valide,inscription acceptée
prenom.nom+tag@exemple.fr,valide,inscription acceptée
sans-arobase-exemple.fr,invalide,message d'erreur format
test@,invalide,message d'erreur format
@exemple.fr,invalide,message d'erreur format
```

### Vigilance

Vérifier qu'aucune valeur ne ressemble à une donnée réelle collectée par erreur (nom, domaine d'entreprise identifiable) et que chaque valeur invalide correspond bien à une règle de validation existante côté application, pas à une règle inventée par l'IA.

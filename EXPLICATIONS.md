# EXPLICATIONS – CC Portail d'entraide

PETIT Manon

## Commit de départ
- Commit initial de main (test initial) : `4a266e1`
- Départ de main pour mes branches : `76184a8`
- Test initial observé (sur `4a266e1`, refait en détachant HEAD sur ce commit) : 2 clics sur « Ajouter un créneau » → 2 créneaux / 40 min ; « Recommencer » → 0 / 0 min.
- Sur `76184a8` (départ de mes branches) : 1 créneau = 200 min → durée erronée introduite par `b88cc98`.
## Branches
| Branche | Rôle                 | Point de départ |
|---|----------------------|---|
| feature/accueil | annoncer l'accueil libre sans inscription le jeudi à 16 h | `76184a8` |
| feature/contact | rendre entraide@example.org cliquable (mailto)| `76184a8` |
| feature/tutorat | contribution fournie : tutorat individuel sur inscription à 16 h 30 | `76184a8` |
| hotfix/duree | annuler la durée erronée de 200 min | `39c40a7` (main après intégration) |

## Mes changements
- `5c9489d` (feature/accueil) : modification du paragraphe `#permanence` dans index.html.
- `f31ef48` (feature/contact) : ajout d'un lien `mailto:` autour de l'adresse.
- Intégration dans main : feature/accueil en fast-forward, puis feature/contact via le commit de fusion `3fce183`.

## Conflit
- Pourquoi les branches ont divergé : feature/accueil et feature/tutorat partent toutes les deux de `76184a8` et modifient chacune la même ligne, le paragraphe `#permanence` d'index.html. Git ne peut pas choisir seul quelle version garder.
- Conflit constaté lors de `git merge feature/tutorat` depuis main (`3fce183`) : marqueurs `<<<<<<<` / `=======` / `>>>>>>>` dans index.html.
- Décision : j'ai gardé les deux informations dans le paragraphe : accueil libre sans inscription le jeudi à 16 h + tutorat individuel sur inscription le jeudi à 16 h 30. Le lien mailto est conservé.
- Vérification : aucun marqueur restant (recherche Ctrl+F), `git status` propre, page vérifiée dans le navigateur.
- Commit de fusion : `39c40a7` (parents `3fce183` et `a43f314`).

## Annulation
- Commit annulé : `b88cc98bf3fae11998895be8365305f22b2cc49c` (« Mettre à jour la durée de référence des créneaux »), qui avait passé la durée d'un créneau de 20 à 200 minutes dans app.js.
- Branche : hotfix/duree, créée depuis main intégré (`39c40a7`).
- Commit d'annulation : `496c876` (créé avec `git revert`).
- Pourquoi un revert et pas un reset : l'historique est considéré comme déjà partagé. Le revert crée un nouveau commit qui annule seulement ce changement, sans réécrire l'historique.
- Le commit suivant `76184a8` (conseil du README) est conservé : vérifié dans README.md et sur GitHub.
- Intégration : main avancé en fast-forward sur `496c876`.

## Tests avant / après
| Test | Commit | Attendu | Observé |
|---|---|---|---------|
| 1 créneau | `4a266e1` (initial) | 20 min | 20 min  |
| 1 créneau | `39c40a7` (avant hotfix) | 200 min (bug) | 200 min |
| 1 créneau | `496c876` (après hotfix) | 20 min | 20 min  |
| Recommencer | `496c876` | 0 créneau / 0 min | 0 créneau / 0 min     |
| Accueil 16 h + tutorat 16 h 30 visibles | `496c876` | les deux affichés | les deux affichés     |
| Clic sur entraide@example.org | `496c876` | ouvre l'appli mail | ouvre l'appli mail     |

## Difficultés
1. Mauvais dossier
  - État constaté : je modifiais un index.html qui n'était pas dans cc-portail-entraide (`git status` montrait un autre dépôt).
  - Tentative : retour dans cc-portail-entraide (`cd`), vérification avec `git status`.
  - Résultat : modif refaite au bon endroit, commit `5c9489d`.
  - Vérification : `git log --oneline --graph --all`.
2. Push refusé
  - État constaté : `error: src refspec feature/acceuil does not match any`.
  - Tentative : correction de la faute de frappe (feature/accueil).
  - Résultat : push réussi des 5 branches.
  - Vérification : branches visibles sur GitHub, main = `496c876` en local et sur GitHub.

## Publication
- Dépôt public : https://github.com/PimPim135/cc-portail-entraide
- Branches publiées : main, feature/accueil, feature/contact, feature/tutorat, hotfix/duree
- Dernier ID de main : indiqué dans le message de remise (commit d'EXPLICATIONS.md)

## Aides et vérifications personnelles
- Aide : Claude (IA), utilisé pour me guider dans l'ordre des commandes Git et la structure de ce fichier.
- J'ai fait moi-même toutes les modifications, les commandes et les tests du navigateur, et j'ai vérifié le graphe et GitHub à chaque étape.
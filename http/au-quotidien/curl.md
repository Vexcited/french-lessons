---
description: Comment voir les messages HTTP en utilisant cURL ?
---

# cURL

## Présentation de l'outil

cURL est une commande qui permet de faire des requêtes HTTP depuis son terminal.

Il est installé par défaut sur les dernières versions de Windows 10 et est inclus dans Windows 11 et macOS au préalable.

## Exemple sans paramètre

```
curl http://example.com/
```

Cette simple commande vous donnera directement le contenu de la réponse HTTP renvoyé après une requête GET à `http://example.com`

## Voir la requête et les en-têtes

Pour voir tout ce qu'il se passe dans les _coulisses_, on peut activer le mode "verbose" qui permet d'afficher plus d'informations lors de l'exécution de la commande.

```
curl -v http://example.com/
```

On peut ainsi voir toute la communication, avec premièrement la requête HTTP envoyé (préfixé par `>`), puis le contenu de la requête envoyé, ensuite la réponse HTTP du serveur (préfixé par `<`) et le contenu de la réponse HTTP.

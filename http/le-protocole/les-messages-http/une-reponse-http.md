---
description: >-
  Comment est structuré le message HTTP venant de la machine "serveur" pour
  répondre à notre machine "client" ?
---

# Une réponse HTTP

La structure est à peu près la même que celle pour la requête HTTP avec quelques modifications.

## Les headers (en-têtes)

### La première ligne

```
HTTP/1.1 200 OK
```

Premièrement nous avons la version du protocole, ici `1.1`.

Ensuite nous avons le code de status de la réponse, ici `200` suivi dans sa description, ici OK.

Vous pourrez trouver tout les autres code de status dans la documentation MDN : [https://developer.mozilla.org/fr/docs/Web/HTTP/Status](https://developer.mozilla.org/fr/docs/Web/HTTP/Status)

* 2xx veut généralement dire que tout s'est bien déroulé et 200 et le cas normal de réponse.
* 3xx veut dire qu'il y a une redirection ;
* 4xx qu'il y a une erreur dans la requête du client ;
  * `404 NOT FOUND` était la plus connue quand un chemin n'existe pas
* 5xx qu'il y a une erreur coté serveur.

### Les champs

La structure est la même que pour la requête HTTP.

Pour recevoir une page HTML, la réponse HTTP peut ressembler à ceci :

```
Content-Type: text/html; charset=UTF-8
Server: Apache
Content-Length: 500
```

* `Content-Type` correspond à text/html qui est le MIME des documents HTML.\
  On explicite aussi que son encodage est en UTF-8.
* `Server` (optionnel) correspond au nom du serveur qui a traité la requête et répondu
* `Content-Length` est la longueur du contenu en bits

## Le contenu

Sans surprise, on obtient ici le contenu de la réponse dont le type correspond au MIME du Content-Type dans les en-têtes.

## Recevoir les données

{% code title="index.mjs" %}
```javascript
let response = ""; // On initialise les données de la réponse.

// Lorsque la machine "serveur" nous envoie des données en retour...
socket.on("data", (data) => {
  // On ajoute les données reçues dans notre variable.
  // Ici, on part du principe que les données sont du *texte*, pas du binaire,
  // c'est pour ça qu'on s'autorise à faire "toString()" sur les données reçues.
  response += data.toString();
});

// Lorsque la connexion est terminée (elle le sera à la fin de la réponse
// grâce à l'en-tête "Connection: close")...
socket.once("close", () => {
  console.log("---- RESPONSE ----");
  // On affiche la réponse que l'on a récupéré avec le socket.
  console.log(response);
});
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption><p>On peut voir un bout de la réponse que l'on reçoit dans notre console.</p></figcaption></figure>

On reçoit bien la page HTML de `http://example.com/`

On peut lire que le contenu est du HTML grâce au `Content-Type: text/html`

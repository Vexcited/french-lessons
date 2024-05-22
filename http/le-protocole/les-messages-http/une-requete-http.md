---
description: >-
  Comment est structuré un message HTTP pour effectuer une requête vers la
  machine "serveur" ?
---

# Une requête HTTP

Nous avons maintenant une connexion TCP sur la machine "serveur" à l'adresse `example.com` sur le port `80`.&#x20;

Il est temps de faire une requête HTTP au serveur HTTP !

## Les headers (en-têtes)

Avant de mettre le contenu de la requête, on vient placer ce qu'on appelle les "headers" (ou en-têtes en français).

### La première ligne

```
GET / HTTP/1.1
```

Nous avons premièrement `GET` qui correspond au nom de la méthode HTTP que l'on veut utiliser.\
Il en existe plusieurs ([https://www.rfc-editor.org/rfc/rfc9110.html#name-methods](https://www.rfc-editor.org/rfc/rfc9110.html#name-methods)), `GET` est la plus courante car c'est celle qui permet de récupérer du contenu. C'est celle que votre navigateur utilise par défaut lors des navigations.

`/` correspond tout simplement au chemin que vous voulez accéder.\
Ici, l'on veut faire une requête à `http://example.com/` mais si l'on voulait faire une requête à `http://example.com/some/path`, on aurait du écrire `/some/path`.

Finalement, `HTTP/1.1` est une constante : c'est la version utilisée du protocole HTTP, ici `1.1`.

### Les champs

Après cette première ligne, nous avons plusieurs champs qui sont formatés ainsi, `Key: value`.

```
Host: example.com
User-Agent: http-1o1/1.0.0
Accept-Language: fr, en
Autre-Parametre: valeur-possible
```

Le champ `Host` est **obligatoire** car il permet au serveur de savoir à quelle adresse (et port si utilisé explicitement : `example.com:8080`) la requête a été faite. Cela est utile dans des cas de configurations assez complexes.

Tout les autres champs sont optionnels, on peut même ajouter nos propre champs, cependant quelques champs peuvent avoir un impact sur le contenu.

Par exemple, le champ `User-Agent` contient des informations sur la version de l'application faisant la requête HTTP. Ici, nous avons décidé d'utiliser le `User-Agent` suivant : `http-1o1` et on a précisé qu'on était à la version `1.0.0`. Cependant, un vrai `User-Agent` tel que celui de Chrome, par exemple, est bien plus long : `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Safari/537.36`.\
Ce champ permet au serveur de pouvoir potentiellement adapter le contenu en fonction du navigateur.

Un autre exemple : le champ `Accept-Language` permet de dire au serveur quel langue notre navigateur préfère (par ordre de préférence). Ainsi le serveur peut potentiellement adapter le contenu en fonction des langues données.

## Le contenu

Dans cet exemple, le contenu **DOIT** être vide.\
Nous faisons une requête `GET` et lorsque l'on utilise cette méthode, le contenu **DOIT** être vide : on ne peut pas envoyer de données avec un `GET` car **cette méthode est faite pour la lecture seulement**.

Si l'on veut envoyer des données au serveur lors de notre requête HTTP, on peut utiliser les autres méthodes tel que `POST`, par exemple :

```
POST /api/send/data HTTP/1.1
Host: example.com
User-Agent: http-1o1/1.0.0
Content-Type: application/json

{"data":"hello world!"}
```

Vous pourrez remarquer que j'ai ajouté le champ `Content-Type` pour spécifier le MIME du contenu que j'ai envoyé au serveur. Ici, j'ai envoyé un JSON qui correspond donc au MIME : `application/json`

Vous pourrez retrouver d'autres MIME dans la documentation de la MDN, [https://developer.mozilla.org/fr/docs/Web/HTTP/Basics\_of\_HTTP/MIME\_types](https://developer.mozilla.org/fr/docs/Web/HTTP/Basics\_of\_HTTP/MIME\_types).

## Envoyer la requête

Nous allons revenir sur notre requête `GET` (vers [http://example.com](http://example.com)) et allons l'envoyer à la machine "serveur" via notre socket. Nous utiliserons une version plus simplifiée de la requête.

{% code title="index.mjs" fullWidth="false" %}
```javascript
// Lorsqu'on est connecté à la machine "serveur"
socket.once("connect", () => {
  // On initialise l'en-tête avec la méthode "GET" sur le chemin "/"
  // On oublie pas que chaque saut de ligne doit utiliser "\r\n" et non "\n".
  let request = "GET / HTTP/1.1\r\n"
    // On ajoute le champ "Host"
    + "Host: example.com\r\n"
    // On ajoute le champ "User-Agent"
    + "User-Agent: http-1o1/1.0.0\r\n"
    // On dit que l'on veut fermer la connexion
    // (une fois la réponse arrivée)
    + "Connection: close\r\n"
    // On ajoute la séparation entre l'en-tête et le contenu.
    + "\r\n";

  // On affiche la requête que l'on envoie.
  console.log("---- REQUEST ----");
  console.log(request);

  // On écrit la requête dans le socket.
  // La machine "serveur" va recevoir notre requête.
  socket.write(request);
});

```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption><p>On peut voir la requête que l'on a envoyé.</p></figcaption></figure>

On a envoyé notre requête, maintenant il faut avoir la réponse !

# Une réponse HTTP

## Reçu de la requête

```javascript
// Lorsque la machine "serveur" nous envoie des données en retour...
socket.on("data", (data) => {
  console.log("---- RESPONSE ----");

  // On récupère la réponse.
  const response = data.toString();
  // On affiche la réponse
  console.log(response);
});
```

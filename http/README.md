---
description: Le début d'une aventure...
---

# Introduction

Vous êtes vous déjà demandé comment fonctionne une requête HTTP ?\
Comment votre navigateur peut naviguer sur l'Internet, demander et récupérer des données ?

Alors vous êtes bien tombés car c'est exactement de quoi on va parler dans ce cours sur HTTP !

On va principalement regarder comment se déroule une requête HTTP en les écrivant à partir de 0.&#x20;

{% hint style="warning" %}
Nous parlerons uniquement de la version 1.1 de HTTP, car c'est actuellement celle qui est la plus utilisé malgré la version 2 qui est sensé la remplacer dans un futur proche.
{% endhint %}

## Prérequis

Avant toute chose, pour comprendre ce cours, il faut savoir un peu ce qu'est TCP puisque le protocole HTTP se base sur le protocole TCP.

Si vous avez besoin d'un petit rafraîchissement, je vous conseille d'aller consulter la page Wikipédia à son sujet : [https://fr.wikipedia.org/wiki/Transmission\_Control\_Protocol](https://fr.wikipedia.org/wiki/Transmission\_Control\_Protocol).

Vous aurez aussi besoin de quelques connaissances en JavaScript et Node.js pour comprendre les exemples présentés, bien qu'ils ne sont pas si compliqués.

## Crédits

Petit aparté pour donner les sources que j'ai utilisé pour rédiger ce cours.

* [https://www.rfc-editor.org/rfc/rfc9110.html](https://www.rfc-editor.org/rfc/rfc9110.html)
* [https://nodejs.org/api/net.html#netcreateconnection](https://nodejs.org/api/net.html#netcreateconnection)
* [https://stackoverflow.com/questions/3252851/how-to-display-request-headers-with-command-line-curl](https://stackoverflow.com/questions/3252851/how-to-display-request-headers-with-command-line-curl)
* [https://developer.chrome.com/docs/devtools/network](https://developer.chrome.com/docs/devtools/network)

Passons maintenant au cours !

---
name: grilling
description: Cuisiner l'utilisateur sans relâche sur un plan, une décision ou une idée. À utiliser quand l'utilisateur veut éprouver sa réflexion, ou emploie une formule du type « cuisine-moi », « grill me ».
---

Toute la session se déroule **en français** : questions, recommandations et synthèses.

Interroge l'utilisateur sans relâche jusqu'à atteindre une compréhension partagée. Représente cela sous forme d'**arbre de décisions** : chaque décision se ramifie en décisions qui en dépendent.

Parcours l'arbre par **tours**. La **frontière** est l'ensemble des décisions dont les prérequis sont déjà tranchés : les questions que l'on peut poser _maintenant_ sans présumer de réponses pas encore entendues. Pose toute la frontière en un seul tour : numérote chaque question et donne ta réponse recommandée. Attends ensuite les réponses de l'utilisateur avant le tour suivant.

Présente un tour ainsi :

```
❓ **Q1** - **<titre de la question>** : <corps de la question, éventuellement sur plusieurs paragraphes, avec plusieurs choix>

➡️ <ta réponse recommandée>

---

❓ **Q2** - **<titre de la question>** : <corps de la question, éventuellement sur plusieurs paragraphes, avec plusieurs choix>

➡️ <ta réponse recommandée>
```

Formule chaque question de sorte qu'un « oui » valide ta réponse recommandée.

Chaque tour de réponses remodèle l'arbre : les décisions tranchées repoussent la frontière et débloquent les questions qui en dépendaient. Recalcule la frontière et pose le tour suivant. Une question dont la réponse dépend d'une autre question encore ouverte dans ce tour appartient à un tour _ultérieur_, pas à celui-ci.

Trouver les _faits_ est ton travail, jamais celui de l'utilisateur. Quand une question de la frontière nécessite un fait de l'environnement (fichiers, outils, etc.), lance un sous-agent avec un contexte vierge pour le trouver ; ne demande jamais à l'utilisateur ce que tu peux vérifier toi-même. Ne bloque pas dessus : une exploration en cours est un prérequis non tranché, donc seules les questions qui en dépendent attendent le retour du sous-agent ; pose le reste de la frontière tout de suite. Les _décisions_ appartiennent à l'utilisateur : soumets-les-lui une à une et attends.

La session est terminée quand la frontière est vide : chaque branche de l'arbre a été visitée, rien n'a été supposé en silence. N'agis pas avant que l'utilisateur confirme que vous avez atteint une compréhension partagée.

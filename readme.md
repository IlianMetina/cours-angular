# Angular 20+

Angular est un framework offrant de nombreux outils pour développer un front-end réactif, proposant même une fonctionnalité SSR (Server Side Rendering / Rendu Côté Serveur)

## Server Side Rendering / Single Page Application

Dans le cadre d'une SPA, lors du chargement d'une page, cette dernière ne contient que très peu de contenu / code HTML.

Tout le contenu est "hydraté" après que le Javascript ait été téléchargé par le navigateur, qui va généré le HTML et rendre la page réactive.

Quant au SSR, ce n'est pas le navigateur mais le serveur qui va exécuter le Javascript, et donc lors de l'envoi de la page au client (navigateur), la page sera donc déjà largement hydratée, avec moins de code à exécuter pour le navigateur, ce qui offre de meilleures performances.

Le gros atout du SSR reste également le référencement : lorsqu'un serveur renvoie une page HTML à un client, c'est là que les robots de moteurs de recherche comme Google vont l'intercepter et donner une note en fonction du contenu présent.

Sauf qu'en SPA, le contenu est maigre : il est donc difficile d'obtenir de bons scores de la part des bots, mais en SSR on renvoie une page riche en contenu, donc un meilleur score. Le SSR permet donc d'avoir à la fois de meilleures performances, mais également un meilleur référencement.



## Commandes à connaître

#### - ng new 
Créer un nouveau projet Angular
#### - ng g c / ng generate component 
 Générer un dossier composant avec les fichiers de base (HTML/CSS/TypeScript)
#### - ng g s / ng generate service 
 Générer un dossier service avec les fichiers de base
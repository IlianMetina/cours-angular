# Angular 20+

Angular est un framework offrant de nombreux outils pour développer un front-end réactif, proposant même une fonctionnalité SSR (Server Side Rendering / Rendu Côté Serveur).

Angular fonctionne sous forme de composants, ce qui permet de découper une application en morceaux de code réutilisables, et de mieux séparer chaque blocs d'éléments, ce qui permet d'être plus organisé et de s'y retrouver plus facilement.

## L'arborescence d'un projet Angular

#### Exemple simple d'arborescence :

- front-end/
  - src/
    - app/
      - account-component/
        - account-component.ts
        - account-component.html
        - account-component.css
      - services/
      - assets/
  - main.ts
  - index.html
  - styles.css
- public/
- angular.json
- package.json
- tsconfig.json

#### Exemple recommandé :

- front-end
  - src/
    - main.ts
    - index.html
    - styles.css
    - app/
      - core/
      - services/
        - guards/
        - interceptors/
      - models/
      - features/
        - account/
          - account.component.ts
          - account.component.html
          - account.component.css
        - products/
        - cart/
        - orders/
      - shared/
        - components/
        - pipes/
        - directives/
      - layout/
        - header/
        - footer/
        - navbar/
- app.routes.ts
- app.component.ts
- app.config.ts
- assets/
- environments/
- public/
- angular.json
- package.json
- tsconfig.json
- README.md


#### - Core/ : Tout ce qui est global à l'application 

Exemple : Services globaux comme l'authentification ou les Guards.

#### - Features/ : Contient les fonctionnalités métiers séparés par domaine 

Exemple : Account pour le compte utilisateur, products pour les produits, orders pour les commandes.

#### - Shared/ : Contient ce qui peut être réutilisé partout

Exemple : Une carte produit qui servira comme d'un moule où l'on viendra remplacé dynamiquement les valeurs souhaitées, un bouton personnalisé.

#### - Layout/ : Contient tout les composants qui apparaitront sur toutes les pages

Exemple : Le header, le footer, la barre de navigation.

En clair : le dossier core pour le global, features pour tout ce qui est logique métier, shared pour les composants réutilisables, et layout pour la structure visuelle globale.

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
#### - ng serve 
Lancer l'application Angular

## Getting Started

Lorsque vous exécuterez la commande ng new, on vous proposera de faire des choix, comme choisir Angular en SSR ou classique, le nom de votre projet, des options particulières etc.

Une fois cela fait, Angular va générer les dossiers & fichiers pendant quelques instants, et vous vous retrouverez avec une architecture presque identique à celle schématisée plus haut, avec seulement quelques dossiers à créer (services, shared, core, features, layout).


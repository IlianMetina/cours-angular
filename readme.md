# Angular 20+

Angular est un framework offrant de nombreux outils pour développer un front-end réactif, proposant même une fonctionnalité SSR (Server Side Rendering / Rendu Côté Serveur).

Angular fonctionne sous forme de composants, ce qui permet de découper une application en morceaux de code réutilisables, et de mieux séparer chaque blocs d'éléments, ce qui permet d'être plus organisé et de s'y retrouver plus facilement.

## Le système de composants

Comme dis plus haut, les composants correspondent aux briques d'une application Angular. 

Un composant contrôle une partie de l'interface, et est constituée de 3 fichiers : HTML, CSS, TypeScript.

Donc chaque composant à son fichier HTML, avec son CSS propre à lui, et lié à un fichier TypeScript, qui peut par exemple servir à afficher dynamiquement des données :

    // app.component.ts
    import { Component } from '@angular/core';

    @Component({
    selector: 'app-root',        // Balise HTML utilisée dans les templates
    templateUrl: './app.component.html',  // Fichier HTML associé
    styleUrls: ['./app.component.css']    // Fichier(s) CSS associé(s) (On peut en mettre plusieurs)
    })
    export class AppComponent {
    titre = 'Mon Application';   // Attribut de ma classe

    saluer() {                   // Méthode 
        return `Bonjour depuis ${this.titre}`;
    }
    }

On voit qu'on pourrait utiliser mon attribut "titre" pour afficher le nom de l'application par exemple, ou utiliser la méthode saluer. Mais comment ça fonctionne ? C'est très simple.

Dans votre HTML, il vous suffit d'utiliser les doubles accolades `{{}}`, et d'y placer le nom de l'attribut si vous voulez l'afficher, et la même chose pour une méthode, sans oublier les parenthèses pour celles-ci :

    <!-- app.component.html -->
    <h1>{{ titre }}</h1> 
    Affichera la valeur de "titre" : Mon Application

    <p>{{ saluer() }}</p>
    Affichera la valeur de retour de saluer() : Mon Application

Cette façon d'afficher des données, ou plutôt de les liées (Data Binding) s'appelle l'interpolation. Il en existe d'autres qui seront utilisées pour d'autres choses que l'affichage.

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

Exemple : Une carte produit qui servira comme d'un moule où l'on viendra remplacé dynamiquement les valeurs souhaitées, ou plus simplement un bouton personnalisé.

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

Une fois le projet généré, vous pouvez regarder dans le fichier src/index.html.

Il contient une balise spéciale :

#### `<app-root>`

C'est le composant principal de toute l'application, Angular démarre toujours pas lui. Tout le reste passe à l'intérieur de ce composant.

Il y a également une balise spéciale dans le fichier src/app/app.html :

#### `<router-outlet>`

Cette balise est centrale : c'est celle-ci qui va permettre et choisir quel composant afficher en fonction de la route.

Dans le fichier `app.html`, c'est là que vous mettrez les composants globaux contenus dans le dossier `layout/`. Si dans votre application vous aimeriez que le header & le footer soient toujours présents, il suffira de les ajouter dans le bon ordre :

    <app-header-component></app-header-component>
    <router-outlet></router-outlet>
    <app-footer-component></app-footer-component>

Comme vous pouvez le voir, le header tout en haut car il sera affiché en haut, le footer en bas, et le router-outlet au milieu qui insèrera dynamiquement le composant correspondant à la route.

Le fichier permettant à la balise `<router-outlet>` de fonctionner est le fichier `app/app.routes.ts`

#### Extrait :

    export const routes: Routes = [];

Ce fichier va permettre de lier une route à un composant, de manière très simple :

    export const routes: Routes = [

        {path: "login", component: Login},

        {path: "register", component: Register},

    ]},
    ];

Le "path" signifie la route après le nom de domaine, par exemple en local pour la route login, on met login (localhost:4200/login), et on lie ensuite le composant (créer auparavant avec la commande ng g c) dans le paramètre component. 

Et maintenant, le router-outlet se chargera à chaque changement de routes de venir voir ce fichier, et ensuite de suivre les directives qu'on lui aura donné pour charger dynamiquement les composants en fonction des routes empruntées par l'utilisateur.

Vous pouvez essayer : faites la commande `ng g c NomDuComposant` dans le dossier app/, et associez le à une route de votre choix dans `app.routes.ts`, par exemple l'accueil `(http://localhost:4200/)`:

    export const routes: Routes = [

        {path: "", component: NomDeVotreComposant},
    ]},
    ];  

Exécutez ensuite la commande `ng serve` pour lancer l'application, et rendez vous sur `http://localhost:4200/` (4200 étant le port par défaut d'une application Angular)

Si vous n'avez pas modifier le HTML, en imaginant que vous avez appeler votre composant Home, vous devriez voir afficher : `home works!`

## Les directives Angular

Les directives ce sont des marqueurs placés sur des éléments HTML, et qui indiquent à Angular de leur appliquer un comportement particulier.

Par exemple, on peut appliquer directement une condition dans le HTML, ce qui va permettre d'afficher ou non quelque chose. Repartons de l'exemple précédent :

    app.component.ts

        import { Component } from '@angular/core';

        @Component({
        selector: 'app-root',        
        templateUrl: './app.component.html',  
        styleUrls: ['./app.component.css']    
        })
        export class AppComponent {
        titre = 'Mon Application';   
        isUserConnected = true;
        username = "Jean";

        saluer() {                   
            return `Bonjour depuis ${this.titre}`;
        }
        }

Vous pouvez voir que j'ai ajouté un nouvel attribut de type booléen, `isUserConnected` que j'ai initialisé à true pour l'exemple, ainsi qu'un autre pour stocker un prénom.

Imaginons que vous ayez une logique permettant de déterminer si un utilisateur est connecté, et que c'est la variable `isUserConnected` qui la stockera (dans notre cas, l'utilisateur est connecté).

En général, lorsqu'un utilisateur est connecté, on affiche son prénom ou pseudo, et lorsqu'il ne l'est pas, on peut afficher "Visiteur" ou "Invité" par exemple. Et bien avec Angular ça s'articule comme ça : 

    Si l'utilisateur est connecté, on affiche le prénom stocké dans username :
    @if (isUserConnected == true) {
    <p>Bienvenue, {{ username }} !</p>

    Sinon, on affiche "Mode Invité" :
    } @else if (isUserConnected == false) {
    <p>Mode invité</p>
    }

On peut également utiliser la directive @for dans le HTML d'un composant, par exemple sur un site e-commerce, pour afficher dynamiquement tous les produits :

    @for (produit of produits; track produit.id) {
    <div class="carte">
        <h3>{{ produit.nom }}</h3>
        <p>{{ produit.prix }} €</p>
    </div>
    } @empty {
    <p>Aucun produit disponible.</p>
    }

Ici dans cet exemple, on imagine que dans notre fichier TypeScript on ait rajouté un attribut produits qui serait un tableau :

        @Component({
        selector: 'app-root',        
        templateUrl: './app.component.html',  
        styleUrls: ['./app.component.css']    
        })
        export class AppComponent {
        titre = 'Mon Application';   
        isUserConnected = true;
        username = "Jean";
        produits = [];

        async ngOnInit(){

            const response = await fetch("http://localhost:PORT/getAllProducts")

            this.produits = await response.json();
        }

        saluer() {                   
            return `Bonjour depuis ${this.titre}`;
        }
        }

Vous pouvez voir ici que grâce à la méthode fetch, je peux réaliser un appel API vers l'URL correspondant à la route me permettant de récupérer tous mes produits.
Sauf que du code exécutable en TypeScript doit être contenu dans une méthode, ici `ngOnInit()`. Cette méthode est un "hook" de cycle de vie, c'est à dire une méthode qui sera appelée automatiquement à un moment précis de la vie d'un composant. Pour `ngOnInit`, c'est à l'initialisation du composant, donc quand la personne sera sur la page associée à ce fichier TypeScript, une seule fois et dans ce cas précis.

Je le stocke ensuite dans mon attribut produits, qui est un tableau.

Je reprends donc l'exemple mis plus haut :

    @for (produit of produits; track produit.id) {
    <div class="carte">
        <h3>{{ produit.nom }}</h3>
        <p>{{ produit.prix }} €</p>
    </div>
    } @empty {
    <p>Aucun produit disponible.</p>
    }

C'est donc une boucle foreach plutôt classique, mis à part le mot clé `track` dans les paramètres de la boucle for qui est obligatoire, ainsi que le `@empty`, qui permet de gérer le cas où le tableau de produits serait vide, et ainsi afficher quelque chose par défaut.

Ces deux directives sont les deux que vous utiliserez et croiserez le plus souvent, même s'il en existe d'autres.

## Les Guards avec Angular

Un Guard avec Angular est une fonctionnalité permettant de contrôler et réguler l'accès à des routes spécifiques.
Ils peuvent être utilisés pour exécuter certaines vérifications et actions avant l'accès à une route. 

L'exemple le plus commun est de créer un Guard d'authentification afin de s'assurer que l'utilisateur est authentifié pour pouvoir accéder aux routes nécessitant une connexion de la part de l'utilisateur.

Ces Guards peuvent être utilisés simplement en les ajoutant à nos routes définies dans `app.routes.ts` plus tôt, avec le paramètre `canActivate`, comme tel :

    import { AuthGuard } from './auth.guard';
    import { AdminComponent } from './admin.component';

    const routes: Routes = [
    {
        path: 'admin',
        component: AdminComponent,
        canActivate: [AuthGuard], // Utilisation du guard
    }
    ];


Imaginons que vous ayez un service appelé `AuthService`, s'occupant de toute la logique relative à l'authentification :

    import { Injectable } from '@angular/core';

    @Injectable({
    providedIn: 'root'
    })
    export class AuthService {
    private isAuthenticated = false;

    login() {
        this.isAuthenticated = true;
    }

    logout() {
        this.isAuthenticated = false;
    }

    isAuthenticated(): boolean {
        return this.isAuthenticated;
    }
    }

Ici, on imagine que lorsque les identifiants envoyés par l'utilisateur lors du login, la méthode login() soit exécutée en cas de connexion réussie.

Et inversement en cas de déconnexion, lorsque l'utilisateur clique sur le bouton de déconnexion, que ce soit la méthode logout() qui soit exécutée.

Il est donc possible ensuite d'utiliser notre attribut de classe `isAuthenticated` pour vérifier si un utilisateur est connecté ou non.

Et on peut ensuite utiliser cet attribut dans notre Guard, qui sera dédié à vérifier qu'un utilisateur est authentifié lorsqu'il accède à une route que l'on souhaite protéger :

    import { inject } from "@angular/core";
    import { Router } from "@angular/router";
    import { AuthService } from "./auth.service";

    export const AuthGuard = () => {
        const auth = inject(AuthService);
        const router = inject(Router);

        if(!auth.isAuthenticated()) {
            router.navigateByUrl('/login')
            return false
        }
        return true
    }

En Angular, l'injection de dépendance se fait via la méthode inject. Donc au lieu de créer un constructeur, il suffit d'écrire `const auth = inject(AuthService);`.

On aura donc injecté notre service AuthService dans notre AuthGuard, et on fait une deuxième injection de dépendances pour Router, qui est un service Angular qui permet de naviguer entre les routes, et de forcer une redirection par exemple.

Et avec une simple condition qui vérifie si l'utilisateur est connecté (`if(!auth.isAuthenticated())`), on exécute la méthode de notre AuthService `isAuthenticated()`, pour ensuite définir des actions :

Dans notre exemple, si l'utilisateur n'est pas connecté, alors on utilise le service Router d'Angular pour rediriger l'utilisateur vers la page `login`, et on retourne false.

Au contraire, si `isAuthenticated()` retourne la valeur true, alors le AuthGuard aussi, et donc l'accès à cette route sera autorisée pour l'utilisateur.

## La navigation dans Angular

En HTML lorsque l'on veut qu'un élément redirige vers une route lors du clic, on utilise la balise `<a>`, avec l'attribut `href` :

`<a href="/login">`

Cette méthode fonctionne mais on perd les nombreux avantages que nous offre Angular, car lors du clic sur une balise `<a href="/ma-page">`, cela force le rechargement de la page.

Mais en Angular, il y a un nouveau paramètre disponible à utiliser à chaque fois que vous voudrez rediriger sur l'une de vos pages : `RouterLink`.

C'est à dire qu'à la place d'utiliser `href`, vous utiliserez `routerLink`.

#### Sans Angular :

`<a href="/produits">Voir les produits</a>`

#### Avec Angular :

`<a routerLink="/produits">Voir les produits</a>`

RouterLink nous permet de mettre à jour l'URL dans le navigateur et d'afficher le bon composant, sans même avoir à recharger la page. La navigation est donc beaucoup plus rapide car on ne recharge pas tous les éléments, on remplace seulement ceux qui ont besoin d'être remplacés (composants).

Évidemment, si vous voulez que votre balise `<a>` redirige vers un site externe, il faudra utiliser l'attribut `href`.
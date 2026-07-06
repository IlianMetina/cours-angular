# Angular 20+

Angular est un framework offrant de nombreux outils pour développer un front-end réactif, proposant même une fonctionnalité SSR (Server Side Rendering / Rendu Côté Serveur).

Angular fonctionne sous forme de composants, ce qui permet de découper une application en morceaux de code réutilisables, et de mieux séparer chaque blocs d'éléments, ce qui permet d'être plus organisé et de s'y retrouver plus facilement.
À noter qu'Angular est basé uniquement sur TypeScript.

## Le système de composants

Comme dis plus haut, les composants correspondent aux briques d'une application Angular. 

Un composant contrôle une partie de l'interface, et est constituée de 3 fichiers : HTML, CSS, TypeScript.

Donc chaque composant à son fichier HTML, avec son CSS propre à lui, et lié à un fichier TypeScript, qui peut par exemple servir à afficher dynamiquement des données :
```typescript
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
```
On voit qu'on pourrait utiliser mon attribut "titre" pour afficher le nom de l'application par exemple, ou utiliser la méthode saluer. Mais comment ça fonctionne ? C'est très simple.

Dans votre HTML, il vous suffit d'utiliser les doubles accolades `{{}}`, et d'y placer le nom de l'attribut si vous voulez l'afficher, et la même chose pour une méthode, sans oublier les parenthèses pour celles-ci :
```html
<!-- app.component.html -->
<h1>{{ titre }}</h1> 
Affichera la valeur de "titre" : Mon Application

<p>{{ saluer() }}</p>
Affichera la valeur de retour de saluer() : Mon Application
```
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
#### - ng build
Compile l'application Angular pour la production, et transforme les fichiers TypeScript, HTML & CSS en fichiers JS/HTML/CSS optimisés et prêts à être déployés.

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
```html
<app-header-component></app-header-component>
<router-outlet></router-outlet>
<app-footer-component></app-footer-component>
```
Comme vous pouvez le voir, le header tout en haut car il sera affiché en haut, le footer en bas, et le router-outlet au milieu qui insèrera dynamiquement le composant correspondant à la route.

Le fichier permettant à la balise `<router-outlet>` de fonctionner est le fichier `app/app.routes.ts`

#### Extrait :
```typescript
export const routes: Routes = [];
```
Ce fichier va permettre de lier une route à un composant, de manière très simple :
```typescript
export const routes: Routes = [

    {path: "login", component: Login},
    {path: "register", component: Register},
];
```
Le "path" signifie la route après le nom de domaine, par exemple en local pour la route login, on met login (localhost:4200/login), et on lie ensuite le composant (créer auparavant avec la commande ng g c) dans le paramètre component. 

Et maintenant, le router-outlet se chargera à chaque changement de routes de venir voir ce fichier, et ensuite de suivre les directives qu'on lui aura donné pour charger dynamiquement les composants en fonction des routes empruntées par l'utilisateur.

Vous pouvez essayer : faites la commande `ng g c NomDuComposant` dans le dossier app/, et associez le à une route de votre choix dans `app.routes.ts`, par exemple l'accueil `(http://localhost:4200/)`:
```typescript
export const routes: Routes = [

    {path: "", component: NomDeVotreComposant},
];  
```
Exécutez ensuite la commande `ng serve` pour lancer l'application, et rendez vous sur `http://localhost:4200/` (4200 étant le port par défaut d'une application Angular)

Si vous n'avez pas modifier le HTML, en imaginant que vous avez appeler votre composant Home, vous devriez voir afficher : `home works!`

## Les directives Angular

Les directives ce sont des marqueurs placés sur des éléments HTML, et qui indiquent à Angular de leur appliquer un comportement particulier.

Par exemple, on peut appliquer directement une condition dans le HTML, ce qui va permettre d'afficher ou non quelque chose. Repartons de l'exemple précédent :
```typescript
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
```
Vous pouvez voir que j'ai ajouté un nouvel attribut de type booléen, `isUserConnected` que j'ai initialisé à true pour l'exemple, ainsi qu'un autre pour stocker un prénom.

Imaginons que vous ayez une logique permettant de déterminer si un utilisateur est connecté, et que c'est la variable `isUserConnected` qui la stockera (dans notre cas, l'utilisateur est connecté).

En général, lorsqu'un utilisateur est connecté, on affiche son prénom ou pseudo, et lorsqu'il ne l'est pas, on peut afficher "Visiteur" ou "Invité" par exemple. Et bien avec Angular ça s'articule comme ça : 
```html
    Si l'utilisateur est connecté, on affiche le prénom stocké dans username :
    @if (isUserConnected == true) {
        <p>Bienvenue, {{ username }} !</p>

    Sinon, on affiche "Mode Invité" :
    } @else if (isUserConnected == false) {
        <p>Mode invité</p>
    }
```
On peut également utiliser la directive @for dans le HTML d'un composant, par exemple sur un site e-commerce, pour afficher dynamiquement tous les produits :
```html
    @for (produit of produits; track produit.id) {
    <div class="carte">
        <h3>{{ produit.nom }}</h3>
        <p>{{ produit.prix }} €</p>
    </div>
    } @empty {
    <p>Aucun produit disponible.</p>
    }
```
Ici dans cet exemple, on imagine que dans notre fichier TypeScript on ait rajouté un attribut produits qui serait un tableau :
```typescript
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

        const response = await fetch("http://localhost:PORT/getAllProducts");

        this.produits = await response.json();
    }

    saluer() {                   
        return `Bonjour depuis ${this.titre}`;
    }
}
```
Vous pouvez voir ici que grâce à la méthode fetch, je peux réaliser un appel API vers l'URL correspondant à la route me permettant de récupérer tous mes produits.
Sauf que du code exécutable en TypeScript doit être contenu dans une méthode, ici `ngOnInit()`. Cette méthode est un "hook" de cycle de vie, c'est à dire une méthode qui sera appelée automatiquement à un moment précis de la vie d'un composant. Pour `ngOnInit`, c'est à l'initialisation du composant, donc quand la personne sera sur la page associée à ce fichier TypeScript, une seule fois et dans ce cas précis.

Je le stocke ensuite dans mon attribut produits, qui est un tableau.

Je reprends donc l'exemple mis plus haut :
```html
    @for (produit of produits; track produit.id) {
    <div class="carte">
        <h3>{{ produit.nom }}</h3>
        <p>{{ produit.prix }} €</p>
    </div>
    } @empty {
    <p>Aucun produit disponible.</p>
    }
```
C'est donc une boucle foreach plutôt classique, mis à part le mot clé `track` dans les paramètres de la boucle for qui est obligatoire, ainsi que le `@empty`, qui permet de gérer le cas où le tableau de produits serait vide, et ainsi afficher quelque chose par défaut.

Ces deux directives sont les deux que vous utiliserez et croiserez le plus souvent, même s'il en existe d'autres.

## Les Guards avec Angular

Un Guard avec Angular est une fonctionnalité permettant de contrôler et réguler l'accès à des routes spécifiques.
Ils peuvent être utilisés pour exécuter certaines vérifications et actions avant l'accès à une route. 

L'exemple le plus commun est de créer un Guard d'authentification afin de s'assurer que l'utilisateur est authentifié pour pouvoir accéder aux routes nécessitant une connexion de la part de l'utilisateur.

Ces Guards peuvent être utilisés simplement en les ajoutant à nos routes définies dans `app.routes.ts` plus tôt, avec le paramètre `canActivate`, comme tel :
```typescript
import { AuthGuard } from './auth.guard';
import { AdminComponent } from './admin.component';

const routes: Routes = [
{
    path: 'admin',
    component: AdminComponent,
    canActivate: [AuthGuard], // Utilisation du guard
}
];
```

Imaginons que vous ayez un service appelé `AuthService`, s'occupant de toute la logique relative à l'authentification :
```typescript
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
```
Ici, on imagine que lorsque les identifiants envoyés par l'utilisateur lors du login, la méthode login() soit exécutée en cas de connexion réussie.

Et inversement en cas de déconnexion, lorsque l'utilisateur clique sur le bouton de déconnexion, que ce soit la méthode logout() qui soit exécutée.

Il est donc possible ensuite d'utiliser notre attribut de classe `isAuthenticated` pour vérifier si un utilisateur est connecté ou non.

Et on peut ensuite utiliser cet attribut dans notre Guard, qui sera dédié à vérifier qu'un utilisateur est authentifié lorsqu'il accède à une route que l'on souhaite protéger :
```typescript
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
```
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

## Les formulaires Angular (Reactive Forms)

Il existe deux façons de gérer des formulaires avec Angular : 

- Template-driven forms
- Reactive forms

J'aborderais seulement les formulaires avec Reactive Forms puisque c'est l'approche la plus puissante, même si ça reste un peu plus verbeux.

La différence entre les deux c'est que la logique du formulaire pour `reactive forms` est définie dans le HTML, avec des attributs spécifiques, alors que pour `template-driven forms`, la logique est définie dans le fichier TypeScript, en utilisant des classes comme `FormControl`, `FormBuilder` et `FormGroup`.

- `FormControl` : représente un seul champ du formulaire
- `FormGroup` : représente un groupe de `FormControl`, donc en général un formulaire entier
- `FormBuilder` : un service qui permet simplement de raccourcir la syntaxe à écrire, comme un builder en Java qui permettrait de faire les setters plus rapidement par exemple. C'est facultatif, ce n'est pas obligatoire pour que ça fonctionne, dans les prochains exemples on n'utilisera pas `FormBuilder`.

Tout d'abord pour utiliser les `reactive forms` d'Angular, il faut que vous importiez `ReactiveFormsModule` dans le module du composant où vous voulez l'utiliser, par exemple pour un composant Login pour récupérer les données du formulaire de connexion :
```typescript
import { ReactiveFormsModule } from '@angular/forms';

@Component({
selector: 'app-login',
standalone: true,
imports: [ReactiveFormsModule],
templateUrl: './login.component.html',
})
export class LoginComponent { }
```
Dans le tableau `imports`, c'est ici que vous devrez l'importer.
Pour `FormControl` & `FormGroup`, il faudra les importer en haut du fichier.

Ensuite, vous devrez également réaliser un autre import, qui ne sert pas au fonctionnement mais à la validation des formulaires. Il faudra l'importer en haut du fichier et non pas dans le tableau d'imports où on a ajouté `ReactiveFormsModule`. Il s'agit de  la classe `Validators`. Exemple mis à jour :
```typescript
import { ReactiveFormsModule, FormGroup, FormControl, Validators } from '@angular/forms';

@Component({
selector: 'app-login',
standalone: true,
imports: [ReactiveFormsModule],
templateUrl: './login.component.html',
})
export class LoginComponent { }
```

Il faut donc d'abord créer le formulaire dans notre fichier TypeScript, puis ensuite le raccorder dans notre HTML. Mais comment ça se présente ?
Voici un exemple:
```typescript
export class Login{

    formulaire = new FormGroup({
        email:      new FormControl('', [Validators.required, Validators.email]),
        motDePasse: new FormControl('', [Validators.required, Validators.minLength(6)]),
    });

    onSubmit() {
        if (this.formulaire.valid) {
            console.log(this.formulaire.value);
        }
    }
}
```
Vous pouvez voir que `FormControl` & `FormGroup` sont bien des classes : on doit les instancier avec le mot clé `new`.

Donc on crée un groupe de `FormControl` (FormGroup), que l'on appelle "formulaire" ici dans cet exemple. `FormGroup` c'est simplement un groupe de `FormControl`, qui eux mêmes représentent seulement un champ d'un formulaire.

`FormGroup` attends donc forcément des champs à récolter. Pour cela, il demande des objets, c'est à dire des instances de la classe `FormControl`.
```typescript
formulaire = new FormGroup({
    email:      new FormControl('', [Validators.required, Validators.email]),
    motDePasse: new FormControl('', [Validators.required, Validators.minLength(6)]),
});
```
On voit que `formulaire` possède deux objets de type `FormControl` : `email` & `motDePasse`.

`FormControl` attends 1 paramètre obligatoire, et un second facultatif :
```typescript
new FormControl(valeurInitiale, validators)
```
On donne donc en premier la valeur de départ du champ (on souhaite qu'il soit vide donc `''`), puis on peut rajouter en deuxième argument des validators (de la classe `Validators` rajoutée plus tôt) qui nous permettrons de valider les champs de notre formulaire.
On utilise les `Validators` sur nos 2 objets `email` et `motDePasse` :
```css
[Validators.required, Validators.email]
[Validators.required, Validators.minLength(6)]
```
#### - Validators.required : 
S'assure que le champ n'est pas vide

#### - Validators.email :
S'assure que la valeur respecte un format email (grâce à une regex)

#### - Validators.minLength(number)
S'assure que la valeur respecte un nombre minimum de caractères, via le paramètre donné dans les parenthèses.

Il existe d'autres, consultables ici : https://angular.dev/api/forms/Validators

#### Et donc une fois cela fait, comment le lier au HTML ?
```html
    <form [formGroup]="formulaire" (ngSubmit)="onSubmit()">
        <input formControlName="email" placeholder="Email" />
        <input type="password" formControlName="motDePasse" placeholder="Mot de passe" />
        <button type="submit" [disabled]="formulaire.invalid">Connexion</button>
    </form>
```
Regardez : on doit d'abord insérer une balise `<form>`, avec un paramètre `[formGroup]` pour dire que ce formulaire est de type `FormGroup`, et on lui associe le nom de la variable donnée à notre `FormGroup` dans notre fichier TypeScript : `formulaire`.

Il y a également un autre paramètre, `(ngSubmit)` qui écoute l'évènement de soumission du formulaire, et on lui associe une méthode qui sera exécutée lorsque l'utilisateur enverra le formulaire.
```typescript
onSubmit() {
    if (this.formulaire.valid) {
    console.log(this.formulaire.value);
    }
}
```

Notre méthode `onSubmit()` de l'exemple plus haut ne remplace pas le paramètre `type="submit"` mis sur le bouton de validation du formulaire.

`onSubmit()` de la balise `<form>` s'exécutera seulement après avoir cliqué sur le bouton, c'est à dire après le déclenchement de l'évènement `submit`.

Vous pouvez également voir ici : 
```html
<input type="password" formControlName="motDePasse" placeholder="Mot de passe" />
```
Que pour chaque input, qui représente un `FormControl`, doit avoir le paramètre `formControlName`, avec comme valeur le même nom que préciser dans votre `FormGroup` dans votre fichier TypeScript.
```typescript
motDePasse: new FormControl('', [Validators.required, Validators.minLength(6)])
```
Le nom donné à mon champ pour le mot de passe est `motDePasse`, je dois donc donner cette même valeur en paramètre de `formControlName`, et ce pour chacun des inputs correspondant aux `FormControls`, pour qu'ils puissent être <ins>**liées**</ins>.

Petite précision, dans l'extrait d'HTML donné plus haut, on voit un paramètre un peu spécial dans la balise `<button>` : `[disabled]="formulaire.invalid"`

`[disabled]` est tout simplement un paramètre, qui nous donne la possibilité d'utiliser 2 méthodes associées à notre `FormGroup` (qu'on a appelé `formulaire` dans notre exemple) :

- **leNomDeNotreFormGroup.invalid** : Vérifie que les champs respectent bien tous les validateurs qu'on a mis. Par exemple, pour le champ e-mail de notre `FormControl` email on a mis `Validators.email`, alors si l'utilisateur essaye d'envoyer le formulaire en appuyant sur le bouton, grâce à `[disabled]="formulaire.invalid"`, si un seul des champs ne respectent pas les validations mises, alors le `submit` ne s'effectue pas. 
  
L'avantage, c'est qu'on évite une requête vers notre serveur, et le traitement des données.

Pour terminer avec les Reactive Forms, vous avez pu voir que la méthode qu'on associe à notre balise `<form>` ne sert à rien, c'est seulement une méthode qui va exécuter un `console.log`.

Donc voyons un exemple concret, où un utilisateur est enregistré, et se connecte avec les bons identifiants. Il appuie sur le bouton, et le formulaire active la méthode associée définie plus tôt (`onSubmit()`).
```typescript
 async onSubmit() {
    if (!this.formulaire.valid) return;  // sécurité : on s'arrête si invalide

    try {
      const response = await fetch('http://localhost:3000/login', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(this.formulaire.value)  // envoie { email, motDePasse }
      });

      const data = await response.json();

      if (response.ok) {
        this.router.navigate(['/dashboard']);  // redirige si connexion réussie
      } else {
        console.log('Erreur :', data.message);
      }

    } catch (error) {
      console.log('Erreur réseau', error);
    }
  }
  ```

Vous voyez qu'avant toute chose, on vérifie que le formulaire est valide, avec une condition.
Ensuite, un `try/catch` où on va tout simplement utiliser `fetch` pour envoyer les données du formulaire à notre serveur/micro-service. 

Si le serveur nous répond que la connexion est réussie, on le redirige avec le service `Router` (comme plus tôt pour les `Guards`) vers la page d'accueil. Sinon, on affiche le message d'erreur. Si la moindre erreur arrive pendant le `try`, on récupère l'erreur dans notre variable error et on le `console.log`.

Maintenant, essayez avec une page login très simple, sans faire de vérification d'identifiants.

Tout d'abord, il vous faut donc un composant Login.
Placez vous dans le dossier de votre choix, soit vous créez un dossier `components` dans `app/` si vous voulez juste essayer, soit adopter une arborescence plus organisée comme montrée plus haut dans le cours, puis exécutez la commande `ng g c NomDuComposant`.

Vous pouvez partir de cette base HTML si vous le souhaitez :
```html
 <form [formGroup]="?" (ngSubmit)="?">

    <div class="champ">
      <label for="email">Email</label>
      <input id="email" placeholder="ton@email.com" />
    </div>

    <div class="champ">
      <label for="motDePasse">Mot de passe</label>
      <input id="motDePasse" type="password" placeholder="••••••••" />
    </div>

    <button type="submit" [disabled]="formulaire.invalid">
      Se connecter
    </button>

  </form>
```

Maintenant, il vous reste qu'à fabriquer vos `FormControls`, votre `FormGroup`, et lier les noms de vos `FormControls` à vos balises `<input>`.

L'objectif final : réussir à bien récupérer les valeurs de votre formulaire (mettez un voire plusieurs `console.log` au besoin pour vérifier la conformité des données envoyées), et les envoyer au controller de votre serveur.

# TODO


## Les signals



## @Input / @Output
#### Pour la partage de données entre composant parent/enfant


## Les observables ?
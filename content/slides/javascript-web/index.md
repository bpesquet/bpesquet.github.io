---
title: "Javascript pour le web"
date: 2022-02-02T11:09:39+01:00
draft: false
---

## Sommaire

- Le DOM
- Navigation dans le DOM
- Modification de la structure
- Gestion des évènements
- Manipulation des formulaires

---

## Le DOM

---

### Exemple de page web

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>My web page</title>
  </head>

  <body>
    <h1>My web page</h1>
    <p>Hello! My name's Baptiste.</p>
    <p>
      I live in the great city of
      <a href="https://en.wikipedia.org/wiki/Bordeaux">Bordeaux</a>.
    </p>
  </body>
</html>
```

---

### Le Document Object Model (DOM)

Description de la structure d'une page sous forme d'une arborescence de **noeuds**.

![DOM example](images/chapter13-02.png)

---

### Types de noeuds

- **Eléments** : noeuds structurants pouvant contenir des fils. Correspondent aux balises HTML comme `<body>`, `<p>`, etc.
- **Texte** : noeuds contenant uniquement du texte.

---

### Accès au DOM avec JavaScript

Quand le code JavaScript s'exécute dans le contexte d'une page web, la variable `document` permet d'accéder à la racine du DOM.

```js
const h = document.head; // Accès à l'en-tête de la page
const b = document.body; // Accès au corps de la page
```

La propriété `nodeType` permet de récupérer le type d'un noeud.

```js
if (document.body.nodeType === document.ELEMENT_NODE)
    // ...
```

---

## Navigation dans le DOM

---

### Enfants et parent d'un noeud

La propriété `childNodes` permet d'accéder aux enfants d'un noeud du DOM sous la forme d'une collection ordonnée.

```js
// Affiche les noeuds fils du corps de la page
document.body.childNodes.forEach((node) => {
  console.log(node);
});
```

A l'inverse, la propriété `parentNode` permet de remonter au noeud parent.

```js
document.body.childNodes[1].parentNode; // Accès au noeud <body>
```

---

### Sélection par type de balise

La méthode `getElementsByTagName()` renvoie la liste des noeuds correspond à une balise HTML.

```js
// Liste des noeuds h2
const titleElements = document.getElementsByTagName("h2");
```

---

### Sélection par classe

La méthode `getElementsByClassName()` renvoie la liste des noeuds possédant une certaine classe CSS.

Comme toutes les méthodes de sélection, elle renvoie une liste de noeuds qui doit être convertie en tableau (par exemple avec `Array.from()`) avant de pouvoir être parcourue.

```js
const existingElements = Array.from(document.getElementsByClassName("exists"));
existingElements.forEach((element) => {
  console.log(element);
});
```

---

### Sélection par identifiant

La méthode `getElementById()` renvoie le noeud possédant l'identifiant CSS spécifié, ou `null` si aucun noeud n'est trouvé.

```js
// Affiche le noeud identifié par "new"
console.log(document.getElementById("new"));
```

---

### Sélection par sélecteur CSS

Les méthodes `querySelectorAll()` et `querySelector()` permettent de rechercher des éléments en utilisant un [sélecteur CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors). La première renvoie une liste, la seconde le premier noeud résultat.

```js
// Tous les noeuds paragraphes
document.querySelectorAll("p");

// Tous les noeuds paragraphes descendants du noeud identifié par "content"
document.querySelectorAll("#content p");

// Tous les noeuds de classe "exists" fils du noeud identifié par "ancient"
document.querySelectorAll("#ancient > .exists");

// Le premier noeud paragraphe
document.querySelector("p");
```

---

### Méthodes de sélection

| Noeuds cibles              | Méthode                    |
| -------------------------- | -------------------------- |
| Plusieurs, par balise HTML | `getElementsByTagName()`   |
| Plusieurs, par classe      | `getElementsByClassName()` |
| Plusieurs                  | `querySelectorAll()`       |
| Un seul, par identifiant   | `getElementById()`         |
| Le premier                 | `querySelector()`          |

---

### Contenu d'un noeud

La propriété `innerHTML` renvoie le contenu HTML d'un noeud du DOM sous forme d'une chaîne de caractères.

```js
document.getElementById("content").innerHTML;
```

La propriété `textContent` renvoie le contenu textuel d'un noeud du DOM (sans les balises HTML) sous forme d'une chaîne de caractères.

```js
document.getElementById("content").textContent;
```

---

### Attributs d'un noeud

Les méthodes `getAttribute()` et `hasAttribute()` permettent de consulter les attributs d'un noeud du DOM.

Certains attributs comme `id`, `href` ou `value` peuvent être accédés directement.

```js
document.querySelector("a").getAttribute("href"); // Cible du premier noeud <a>
document.querySelector("a").href; // Idem
document.querySelector("ul").id; // Identifiant du premier noeud <a>

if (document.querySelector("a").hasAttribute("target"))
  //...
```

---

### Classes d'un noeud

La propriété `classList` permet d'accéder à la liste des classes CSS d'un noeud.

```js
// Liste des classes du noeud identifié par "ancient"
const classes = document.getElementById("ancient").classList
console.log(classes.length); // Nombre de classes

if (document.getElementById("ancient").classList.contains("wonders"))
  // ...
```

---

## Modification de la structure

---

### Modification d'un noeud

Les propriétés `innerHTML`, `textContent` et `classList` ainsi que la méthode `setAttribute()` peuvent permettre de mettre à jour un noeud existant.

```js
/// Suppression du contenu (y compris les éventuels fils)
document.getElementById("languages").innerHTML = "";

// Ajout d'une chaîne au texte
document.querySelector("h3").textContent += " and sons";

const titleElement = document.querySelector("h3");
titleElement.classList.remove("beginning"); // Suppression d'une classe
titleElement.classList.add("title"); // Ajout d'une classe

// Mise à jour de l'identifiant (deux solutions possibles)
document.querySelector("h3").setAttribute("id", "title");
document.querySelector("h3").id = "title";
```

---

{{% section %}}

### Ajout d'un nouveau noeud

Il s'effectue en 3 étapes :

1. Création du nouveau noeud
2. Définition de ses attributs
3. Insertion du noeud dans le DOM

```js
const pythonElement = document.createElement("li");
pythonElement.id = "python";
pythonElement.textContent = "Python";
document.getElementById("languages").appendChild(pythonElement);
```

---

### Création du noeud

La méthode `createElement()` prend en paramètre un type de balise HTML et renvoie un noeud.

```js
// Création d'un noeud élément de liste
const pythonElement = document.createElement("li");
```

---

### Définition des attributs du noeud

Les propriétés permettant de modifier un noeud (`textContent`, `classList`, etc) permettent de définir les valeurs des attributs du noeud créé.

```js
pythonElement.id = "python";
pythonElement.textContent = "Python";
```

---

### Insertion du noeud dans le DOM

La solution la plus courante est d'utiliser la méthode `appendChild()` sur un noeud existant. Elle ajoute le nouveau noeud à la fin de la liste de ses fils.

```js
document.getElementById("languages").appendChild(pythonElement);
```

On peut également utiliser `insertBefore()` pour ajouter le nouveau noeud avant un noeud fils spécifié.

```js
document
  .getElementById("languages")
  .insertBefore(pythonElement, document.getElementById("php"));
```

{{% /section %}}

---

### Remplacement ou suppression d'un noeud

La méthode `replaceChild()` permet de remplacer un noeud par un autre.

```js
document
  .getElementById("languages")
  .replaceChild(pythonElement, document.getElementById("perl"));
```

La méthode `removeChild()` permet de supprimer un noeud existant.

```js
document
  .getElementById("languages")
  .removeChild(document.getElementById("lisp"));
```

---

### Gestion du style

La propriété `style` permet d'accéder à l'attribut `style` du noeud, composé de propriétés CSS (`color`, `fontFamily`, etc) qu'il est possible d'exploiter.

```js
const paragraphElement = document.querySelector("p");
paragraphElement.style.color = "red";
paragraphElement.style.fontFamily = "Arial";
paragraphElement.style.backgroundColor = "black";
```

En cas d'utilisation d'une feuile de style CSS, il faut utiliser la fonction `getComputedStyle()` pour accéder à l'intégralité des styles d'un noeud.

```js
const paragraphStyle = getComputedStyle(document.getElementById("para"));
console.log(paragraphStyle.fontStyle);
console.log(paragraphStyle.color);
```

---

## Gestion des évènements

---

### Principe de fonctionnement

Un **gestionnaire d'évènement** est une fonction JavaScript qui va d'exécuter lorsqu'un évènement apparaît : clic sur un bouton, soumission d'un formulaire, survol d'une zone avec la souris, etc.

L'ajout de gestionnaires d'évènement va améliorer l'interactivité de la page web.

Cette manière d'écrire du code est appelée **programmation évènementielle** : l'ordre d'exécution des instructions n'est plus prédéfini, mais dépend des actions de l'utilisateur.

---

### Exemple de gestionnaire d'évènement

L'évènement intercepté est passé en paramètre de la fonction gestionnaire sous la forme d'un objet souvent nommé `e`.

```html
<button id="myButton">Cliquez-moi !</button>
```

```js
const showMessage = (e) => {
  console.log(`Type d'évènement : ${e.type}, cible: ${e.target}`);
  // Affiche une pop-up
  alert("Hello!");
};

// Accès au bouton
const buttonElement = document.getElementById("myButton");
// Gestion du clic via la fonction showMessage()
buttonElement.addEventListener("click", showMessage);
```

---

### Evènements utilisables

JavaScript permet d'exploiter de nombreux évènements sur la page : `click`, `keypress`, `mousedown`, `load`, etc.

```js
document.addEventListener("keypress", (e) => {
  console.log(
    `Vous avez appuyé sur la touche ${String.fromCharCode(e.charCode)}`
  );
});

// "window" représente la fenêtre du navigateur affichant la page
window.addEventListener("load", (e) => {
  console.log("Page web chargée !");
});

// Affiche un message de confirmation de fermeture
window.addEventListener("beforeunload", (e) => {
  const message = "Voulez-vous vraiment quitter ?";
  e.returnValue = message;
  return message;
});
```

---

### Propagation des évènements

Un évènement qui apparaît au niveau d'un noeud se propage vers ses noeuds parents, jusqu'à arriver à la racine du DOM.

Appelée sur un objet évènement, la méthode `stopPropagation()` permet d'interrompre sa propagation.

```js
document.getElementById("propa").addEventListener("click", (e) => {
  // ...
  // Interrompt la propagation de cet évènement
  e.stopPropagation();
});
```

---

### Comportement par défaut

De nombreux évènements déclenchent des comportements par défaut : clic sur un lien web, clic droit sur la page, etc. Appelée sur un objet évènement, la méthode `preventDefault()` annule ce comportement.

```html
<p>
  Du temps à perdre ? <a id="forbidden" href="https://9gag.com/">cliquez ici</a>
</p>
```

```js
document.getElementById("forbidden").addEventListener("click", (e) => {
  alert("Pas une bonne idée");
  // Annule l'ouverture du lien
  e.preventDefault();
});
```

---

## Manipulation des formulaires

---

### Exemple de formulaire

```html
<form>
  <h1>Formulaire d'inscription</h1>
  <p>
    <label for="username">Nom d'utilisateur</label>:
    <input type="text" name="username" id="username" required />
    <span id="usernameHelp"></span>
  </p>
  <p>
    <label for="password">Mot de passe</label>:
    <input type="password" name="password" id="password" required />
    <span id="passwordHelp"></span>
  </p>
  <p>
    <label for="nationality">Nationalité</label>:
    <select name="nationality" id="nationality">
      <option value="US" selected>Américaine</option>
      <option value="FR">Française</option>
      <option value="ES">Espagnole</option>
      <option value="XX">Autre</option>
    </select>
  </p>

  <input type="submit" value="Envoyer" />
  <input type="reset" value="Annuler" />
</form>
```

---

### Gestion du focus

Les évènements `focus` et `blur` permettent d'ajouter du comportement lorsqu'un champ du formulaire reçoit ou perd le focus.

```js
const usernameElement = document.getElementById("username");

// Ajoute le texte d'aide quand le champ reçoit le focus
usernameElement.addEventListener("focus", (e) => {
  document.getElementById("usernameHelp").textContent =
    "Ajoutez votre nom d'utilisateur";
});
// Vide la zone d'aide quand le champ perd le focus
usernameElement.addEventListener("blur", (e) => {
  document.getElementById("usernameHelp").textContent = "";
});
```

---

### Choix dans une liste déroulante

L'évènement `change` sur une liste déroulante permet de gérer le changement de sélection par l'utilisateur.

```js
document.getElementById("nationality").addEventListener("change", (e) => {
  console.log("Code de nationalité : " + e.target.value);
});
```

Les boutions radio et les cases à cocher fonctionnent sur le même principe.

---

### Validation pendant la saisie

L'évènement `input` permet de déclencher l'exécution de code à chaque modification du texte saisi dans un champ.

```js
// Affiche un texte d'aide qui dépend de la longueur du mot de passe saisi
document.getElementById("password").addEventListener("input", (e) => {
  const password = e.target.value; // Texte saisi dans le champ
  let helpText = "Trop court";
  let messageColor = "red";
  if (password.length >= 8) {
    helpText = "OK";
    messageColor = "green";
  }
  const passwordHelpElement = document.getElementById("passwordHelp");
  passwordHelpElement.textContent = helpText;
  passwordHelpElement.style.color = messageColor;
});
```

---

### Validation après soumission

Le noeud correspond à un formulaire dispose d'une propriété `elements` qui permet d'accéder aux champs par leur nom.

La gestion de l'évènement `submit` permet de réagir à la soumission du formulaire par l'utilisateur.

```js
document.querySelector("form").addEventListener("submit", (e) => {
  e.preventDefault(); // Annule l'envoi du formulaire au serveur web

  // Récupération des informations saisies par l'utilisateur
  const username = e.target.elements.username.value;
  const password = e.target.elements.password.value;
  const nationalityCode = e.target.elements.nationality.value;
  // ... (Vérification éventuelles)
});
```

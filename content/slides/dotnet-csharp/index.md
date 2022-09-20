---
title: ".NET et C#"
date: 2022-09-20T10:27:11+02:00
draft: true
---

## Sommaire

- Introduction à .NET
- Introduction à C#
- Guide de codage C\#
- Variables, types et expressions
- Conditions et alternatives
- Structures répétitives

---

## Introduction à .NET

---

### Aux origines de .NET

- Plate-forme de développement d'applications créée par Microsoft en 2002.
- Réponse à la domination du langage Java (multi-plateformes).
- Inclut plusieurs langages de programmation : C#, VB.NET, F#, PowerShell...
- Uniquement disponible sous Windows.
- Licence propriétaire.

---

[![Pile .NET](images/dotnet_stack.png)](https://en.wikipedia.org/wiki/.NET_Framework)

---

{{% section %}}

### Architecture technique de .NET

- Une application .NET s'exécute dans un environnement contrôlé appelé [CLR](https://github.com/dotnet/runtime/blob/main/docs/design/coreclr/botr/intro-to-clr.md) (_Common Language Runtime_).
- La compilation du code source produit un résultat indépendant du système d'exploitation, conformément à un standard nommé **CIL** (_Common Intermediate Language_).

---

[![CLI et CLR](images/dotnet_cli_clr.png)](https://en.wikipedia.org/wiki/Common_Language_Infrastructure)

{{% /section %}}

---

### .NET Framework et .NET Core

- [2004](https://www.mono-project.com/docs/about-mono/history/) : le projet **Mono**, indépendant de Microsoft, débute le portage de .NET vers Linux.
- [2014](https://devblogs.microsoft.com/dotnet/net-core-is-open-source/) : Microsoft publie **.NET Core**, la première version open source et multi-plateformes de .NET. La version WIndows-only de .NET est renommée **.NET Framework**.
- [2019](https://devblogs.microsoft.com/dotnet/net-core-is-the-future-of-net/) : la nouvelle version de .NET Core est renommée **.NET**, et .NET Framework passe en mode maintenance.

---

### .NET 5+ : multiplateforme par défaut

[![.NET 5](images/dotnet-unified-platform.png)](https://devblogs.microsoft.com/dotnet/announcing-net-6/)

---

### La ligne de commande .NET

- **.NET CLI** (_Command Line Interface_) permet d'interagir avec .NET depuis un terminal.
- Nécessite que .NET soit installé sur la machine.
- Syntaxe : `dotnet <commande> <options>`

---

### Création d'une application

`> dotnet new <template> -o <output directory>`

| Type d'application      | Template   |
| ----------------------- | ---------- |
| Console                 | `console`  |
| Bibliothèque de classes | `classlib` |
| ASP.NET (vide)          | `web`      |
| ASP.NET (API)           | `webapi`   |
| ASP.NET (MVC)           | `mvc`      |

---

### Création d'un fichier .gitignore

`> dotnet new gitignore`

- Le fichier `.gitignore` permet d'exclure certains fichiers/dossiers de la gestion des versions avec [Git](https://git-scm.com/). Il le plus souvent s'agit de fichiers locaux (exemple : configuration de l'environnement de développement) ou de fichiers recréés systématiquement par le processus de génération de l'application.
- Cette commande crée un fichier `.gitignore` adapté aux projets .NET.

---

### Gestion des packages

`> dotnet add package <name>`

- Utilise [NuGet](https://www.nuget.org/) pour télécharger un package et l'ajouter au projet.
- Vérifie la compatibilité du package à installer avec le projet.

`> dotnet list package`

- Liste les packages installés pour un projet.

---

### Lancement d'une application

`> dotnet run`

Si nécessaire, effectue la restauration des dépendances du projet (équivalent de `dotnet restore`).

---

### Surveillance des changements

`> dotnet watch run`

Pour une application web, jnjecte un script qui met à jour le contenu affiché par le navigateur lorsque des fichiers surveillés sont modifiés.

---

### Autres possibilités

- Nettoyage, test, publication, gestion des packages installés, etc.
- [Plus d'informations](https://docs.microsoft.com/en-us/dotnet/core/tools/).

---

## Introduction à C\#

---

### C\# en quelques mots

- Langage de programmation apparu avec la première version de .NET (Framework).
- Syntaxe très inspirée de Java et de C++.
- Typage fort, orienté objet.
- Permet de créer une grande variété d'applications (bureau, web, mobile, cloud, etc).

---

### Coder en C\#

- Environnements de développement intégré (IDE) :
  - [Visual Studio](https://visualstudio.microsoft.com/fr/)
  - [Rider](https://www.jetbrains.com/rider/)
- Editeurs de code :
  - [Visual Studio Code](https://code.visualstudio.com/)
  - [Atom](https://atom.io/)
  - [Sublime Text](https://www.sublimetext.com/)
  - ~~Notepad++~~

---

### Création d'une application console avec .NET

- Type d'application basique qui s'exécute dans un terminal.
- UI pauvre, interactions limitées au clavier.
- Création d'un projet console .NET nommé **HelloCSharp** :

```bash
# Le projet est créé dans le sous-répertoire HelloCSharp
dotnet new console -o HelloCSharp
```

---

### Résultat obtenu

![VS Code - HelloCSharp](images/vscode-hellocsharp.png)

---

### Le fichier .csproj

Décrit la configuration du projet.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net6.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
  </PropertyGroup>

</Project>
```

---

### Le fichier Program.cs

Fichier source principal contenant le code C#.

```csharp
// See https://aka.ms/new-console-template for more information
Console.WriteLine("Hello, World!");
```

---

### Exécution du programme

```bash
# Cette commande doit être lancée dans le répertoire HelloCSharp
dotnet run
```

![VS Code - HelloCSharp run](images/vscode-hellocsharp-run.png)

---

### Littéraux

- Un littéral est une valeur donnée explicitement dans le code source.
- Exemples : `2`, `3.14`, `"Hello World!"`.
- Séparateur décimal : le point `.`
- Chaînes de caractères (texte) : guillemets doubles `"..."`.

---

### Instructions

- Une instruction est un ordre écrit dans le code.
- Un programme est une suite d'instructions.
- Elles se terminent par `;` en C#.
- Elles peuvent être regroupées dans des **blocs** délimités par des accolades `{ ... }`.
- Durant l'exécution, chaque instruction est "lue" séquentiellement et produit un résultat.

---

### Commentaires

- Rôle : expliquer _aux humains_ certaines parties du code.
- Syntaxe :  `//...` (monoligne) ou `/* ... */` (multilignes).
- Peuvent être ajoutés/supprimés automatiquement par les éditeurs de code et les IDE.

---

## Guide de codage C\#

---

### Nommage des identifiants

- Un **identifiant** est le nom donné à un élément du code créé par le développeur.
- Ils doivent commencer par une lettre ou un _underscore_ `_`.
- Ils sont sensibles à la casse (distinction majuscules/minuscules).
- Pas d'accents ! (même si ça fonctionne)
- Au sein d'un bloc, le même identifiant ne peut pas être attribué à des éléments distincts.

---

### Mots réservés du C\#

abstract as base bool break byte case catch
char checked class const continue decimal
default delegate do double else enum event
explicit extern false finally fixed float for
foreach goto if implicit in int interface
internal is lock long namespace new null
object operator out override params private
protected public readonly ref return sbyte
sealed short sizeof stackalloc static string
struct switch this throw true try typeof uint
ulong unchecked unsafe ushort using virtual
void while

---

### Conventions de nommage

- Notation [camelCase](https://fr.wikipedia.org/wiki/Camel_case) : `totalFacturesClient`.
  - Pas d'underscores entre les mots comme en Python !
- Notation PascalCase (première lettre en majuscule) pour certains éléments (fonctions, méthodes, structures, classes) : `CompteBancaire`.

---

### Formatage du code

- Pas plus d'une instruction par ligne.
- Longueur maximum d'une ligne : 80-ish caractères.
- Accolades ouvrantes et fermantes sur des lignes distinctes.
- Indentation = 4 espaces.
- ... Utiliser le formateur automatique de son éditeur/IDE !
  - Activer le formatage à la sauvegarde pour plus de confort.

---

### Formatage des commentaires

- Placer les commentaires sur des lignes distinctes.
- Débuter par une majuscule et terminer par un point.
- Laisser un espace entre le symbole de début et le texte.

```csharp
// Ceci est un commentaire tellement long qu'il est réparti
// sur plusieurs lignes
```

---

### Ressources

- [C# Coding Conventions](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions)
- [C# Coding Style](https://github.com/dotnet/runtime/blob/main/docs/coding-guidelines/coding-style.md)
- [Visual Studio Code - Formatting](https://code.visualstudio.com/docs/editor/codebasics#_formatting)

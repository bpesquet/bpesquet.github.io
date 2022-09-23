---
title: ".NET et C#"
date: 2022-09-20T10:27:11+02:00
draft: true
---

## Sommaire

- Introduction à .NET
- La notion de programme
- Premiers pas avec C#
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

Version de référence : .NET 6 (2021).

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

## La notion de programme

---

### Qu'est-ce qu'un programme ?

- **Programme** (application, logiciel) : implémentation (réalisation) d'un algorithme sous la forme d'un ensemble de commandes textuelles appelées **instructions**.
- Ces instructions sont spécifiques à un langage de programmation.
- Elles sont ensuite traduites dans un langage compris par (le processeur de) la machine qui exécute le programme.
- L'ensemble des instructions d'un programme est appelé son **code source**.

---

### Au plus près de la machine : l'assembleur

Jeu d'instructions élémentaires comprises par une famille de processeurs.

```asm
str:
 .ascii "Bonjour\n"
 .global _start

_start:
movl $4, %eax
movl $1, %ebx
movl $str, %ecx
movl $8, %edx
int $0x80
movl $1, %eax
movl $0, %ebx
int $0x80
```

---

### Langages compilés

- **Compilation** = phase de traduction du code source en langage machine, puis exécution du résultat de la compilation.
  - Performances optimales.
  - Permet de détecter les erreurs syntaxiques avant l'exécution.
  - Recompilation nécessaire sur un nouvel environnement.
  - Exemples : C, C++.

---

### Langages interprétés

- **Interprétation** = exécution du code source d'un programme ligne après ligne.
  - Pas de phase de compilation (gain de temps).
  - Code directement portable d'un environnement à l'autre.
  - Performances inférieures aux langages compilés.
  - Détection tardive des erreurs syntaxiques (durant l'exécution).
  - Exemples : Python, JavaScript, PHP.

---

### Langages pseudo-compilés

- Code source "compilé" vers un format intermédiaire multi-plaformes ("_Write once, run anywhere_").
  - Erreurs syntaxiques détectées à la "compilation".
  - Evite les recompilations.
  - Nécessite que l'environnement soit supporté par la plate-forme d'exécution du code intermédiaire.
  - Exemples : Java, C#.

---

### Le rôle du programmeur

- Créer des programmes qui réalisent de manière fiable les tâches attendues.
- Maîtriser la complexité qui apparaît inévitablement lorsque les fonctionnalités du programme évoluent.

> "Le programmeur est un créateur d'univers dont il est seul responsable." (Joseph Weizenbaum).

---

## Premiers pas avec C\#

---

### C\# en quelques mots

- Langage de programmation apparu en 2002 avec la première version de .NET (Framework).
- Syntaxe très inspirée de Java et de C++.
- Typage statique, orienté objet.
- Permet de créer une grande variété d'applications (bureau, web, mobile, cloud, etc).
- Version associée à .NET 6 : C# 10.

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

abstract
as
base
bool
break
byte
case
catch
char
checked
class
const
continue
decimal
default
delegate
do
double
else
enum
event
explicit
extern
false
file finally
fixed
float
for
foreach
goto
if
implicit
in
int
interface
internal
is
lock
long
namespace
new
null
object
operator
out
override
params
private
protected
public
readonly
ref
return
sbyte
sealed
short
sizeof
stackalloc
static
string
struct
switch
this
throw
true
try
typeof
uint
ulong
unchecked
unsafe
ushort
using
virtual
void
volatile
while

---

### Conventions de nommage

- Plus l'élément est utilisé dans le code, plus il faut le nommer avec soin.
- Notation [camelCase](https://fr.wikipedia.org/wiki/Camel_case) : `totalFacturesClient`.
  - Pas d'underscores entre les mots (!= Python).
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

---

## Variables, types et expressions

---

### Valeur Vs type

- **Valeur** = morceau d'information utilisée dans un programme.
- Chaque valeur possède un **type** qui détermine :
  - son encodage en mémoire ;
  - la plage des valeurs possibles ;
  - les opérations permises.
- C# est un langage à **typage statique** : les types doivent être explicitement précisés (!= Python).

---

### Variables

- **Variable** = zone de stockage d'information dans la mémoire allouée au programme.
  - Sorte de "boîte" dans laquelle on range des choses.
- Caractérisée par :
  - son nom (identifiant) ;
  - sa valeur ;
  - son type.

---

### Déclaration d'une variable

- Type défini explicitement à la déclaration.
- Valeur modifiée par l'opérateur d'affectation `=`.
  - Ne pas confondre avec l'égalité mathématique !
- Possibilité de définir la valeur initiale au moment de la déclaration.

```csharp
int x; // Déclaration : aucune valeur dans la variable x
x = 3; // Affectation de la valeur 3 à x

int y = 5; // Déclaration et initialisation de la variable y
y = "Coucou"; // NOK : valeur incompatible avec le type de y
```

---

### Portée d'une variable

- **Portée** (_scope_) = portion du code source dans laquelle une variable est visible et donc utilisable.
- L'unité de portée est le bloc de code `{ ... }` ainsi que ses sous-blocs éventuels.
- En l'absence d'accolades, un bloc par défaut est implicitement défini.

```csharp
int a = 1;
{
    a = 2; // OK : a est déclarée dans le bloc parent
    int b = 4; // La portée de b se limite au bloc actuel
}
Console.WriteLine(a); // OK : a est déclarée dans le bloc courant
Console.WriteLine(b); // NOK : b n'est pas visible ici
```

---

### Types prédéfinis

Extrait du vaste éventail de [types prédéfinis du C#](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/built-in-types) :

|Mot-clé|Nom complet|Description|
|---------|----|-|-|
|[int](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/integral-numeric-types)|`System.Int32`|Entier (signé)|
|[double](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/floating-point-numeric-types)|`System.Double`|Réel|
|[bool](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/bool)|`System.Boolean`|Booléen|
|[char](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/char)|`System.Char`|Caractère|
|[string](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/reference-types#the-string-type)|`System.String`|Chaîne de caractères|

---

### Valeurs prédéfinies

Plusieurs valeurs constantes sont associées à certains types.

```csharp
int i = int.MaxValue; // Plus grande valeur gérée par int
int j = int.MinValue; // Plus petite valeur gérée par int

double a = double.MaxValue; // Plus grande valeur gérée par double
double b = double.MinValue; // Plus petite valeur gérée par double
double c = double.Epsilon; // Plus petite valeur réelle positive
double d = double.NaN; // Pas un nombre (Not a Number)
double e = double.PositiveInfinity; // +∞
double f = double.NegativeInfinity; // −∞
```

---

### Notation suffixée

- Les litéraux réels sont considérés par défaut comme ayant le type `double`.
- Dans certaines situations, il est utile de préciser explicitement le type souhaité en utilisant la **notation suffixée**.

```csharp
float f = 1.2f; // Réel sur 32 bits
double d = 1.2d; // Réel sur 64 bits
decimal m = 1.2m; // Réel sur 128 bits
```

---

### Types valeur Vs types référence

Les types C# se divisent en deux catégories.

- [Types valeur](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/value-types) : la variable contient directement la valeur qu'elle stocke.

- [Types référence](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/reference-types) : la variable contient une référence vers la valeur (≈ son adresse dans la mémoire). Cette _indirection_ permet d'optimiser certaines opérations (comparaison, copie, etc).

Tous les exemples précédents sont des types valeur, sauf `string` (mais qui s'utilise comme un type valeur).

---

### Types valeur nullables

- Le mot-clé [null](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/null) indique l'absence de référence.
- C'est la "valeur" par défaut des variables de type référence.
- Un type valeur est _non-nullable_ par défaut. Il peut devenir [nullable]((https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/nullable-value-types)) en le suffixant par `?`.

```csharp
int a = null; // NOK : type valeur non nullable
int? b = null; // OK, type nullable
```

---

### Types référence nullables

- Depuis C# 8, on peut paramétrer un projet C# afin que les types référence deviennent _non-nullables_, cad [qu'on ne puisse pas leur affecter](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/nullable-reference-types) `null` ou une valeur potentiellement égale à `null`.
  - C'est le cas par défaut avec .NET 6.
  - Objectif : améliorer la sûreté du code.
- Le préfixage par `?` autorise `null`.

```csharp
string s; // OK, valeur de s = null (variable inutilisable en l'état)
s = null; // NOK, type référence non nullable (C# 8+)
string? t = null; // OK, type nullable
```

---

### Conversions de types implicites

- En C#, le type d'une variable ne peut plus être modifié après sa déclaration (typage statique).

- Une [conversion implicite](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/types/casting-and-type-conversions#implicit-conversions) a lieu quand la nouvelle valeur est directement compatible avec le type actuel (exemples : entier vers entier de plus grande précision, entier vers réel).

```csharp
int i = "Bonjour"; // NOK, valeur incompatible avec le type int

int n = 2147483647;
double d = n; // OK, conversion implicite
// Le type entier long peut stocker n'importe quel int
long l = n; // OK, conversion implicite
```

---

### Conversions de types explicites

- [Transtypage](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/types/casting-and-type-conversions#explicit-conversions) (_cast_) : on force le type de la nouvelle valeur en la préfixant par le nouveau type entre parenthèses.
  - Perte possible d'information.
  - Potentiellement dangereux !
- Fonctions de conversion C# : `{type}.Parse` ou `Convert.To{type}`.

```csharp
int x = (int)12.3; // OK : transtypage possible, x vaut 12

int y = int.Parse("123"); // OK, y vaut 123
int z = int.Parse("12.3"); // NOK : nouvelle valeur non entière
 ```

---

### Booléens

- Le type `bool` représente une valeur booléenne `true` ou `false`.
- Booléen nullable : `bool?`
- Un conversion explicite est requise vers/depuis les types entier : toutes les valeurs non-zéro sont converties à `true`.

```csharp
bool b = true;

bool? n = null; // OK : type nullable

bool p = Convert.ToBoolean(1); // p vaut true
bool q = Convert.ToBoolean(0); // r vaut false
```

---

### Caractères

- Le type `char` représente un caractère alphanumérique [Unicode](https://en.wikipedia.org/wiki/Unicode).
- On peut lui affecter un caractère litéral délimité par des guillemets simples `''` ou sa [valeur Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters#Basic_Latin) transtypée.
- Le caractère d'échappement est `\`.
- La conversion est implicite vers les principaux types entiers et réels.

```csharp
char c = 'a';
int cVal = c; // cVal vaut 97, la valeur Unicode de 'a'
char cBis = (char)97; // Initialisation à partir de la valeur Unicode
```

---

### Séquences d'échappement

Extrait de la [liste complète](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/strings/#string-escape-sequences).

|Séquence|Valeur|
|---------|----|
|`\'`|Guillemet simple|
|`\"`|Guillemet double|
|`\\`|Antislash|
|`\n`|Saut de ligne|
|`\t`|Tabulation|

---

### Chaînes de caractères

- Le type `string` représente une séquence de caractères Unicode.
- L'instruction `{chaîne}.Length` renvoie le nombre de caractères d'une chaîne.
- La syntaxe entre crochets `[]` permet d'accéder à un caractère de la chaîne à partir de son rang.

```csharp
string s = "abc";
char premier = s[0]; // 'a'
char dernier = s[s.Length - 1]; // 'c'
```

---

### Chaînes verbatim

Placé devant son début, le caractère `@` permet de créer une [chaîne verbatime](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/verbatim) dans laquelle on peut ajouter des caractères spéciaux sans les échapper.

```csharp
// Ces deux chaînes contiennent "c:\Windows\Temp"
string c1 = "c:\\Windows\\Temp";
string c2 = @"c:\Windows\Temp";
```

---

### Expressions

- Une **expression** est une combinaison de variables, de valeurs et d'opérateurs.
- Toute expression qui renvoie une valeur possède un type.
- Le résultat d'une expression peut être inclus dans une autre expression.

---

### Opérateurs arithmétiques

|Opérateur|Rôle|
|---------|----|
|`+`|Addition|
|`-`|Soustraction|
|`*`|Multiplication|
|`/`|Division|
|`%`|Modulo|

---

### Opérateurs de comparaison

Ne pas confondre `==` et `=` (affectation) !

|Opérateur|Rôle|
|---------|----|
|`==`|Egal à|
|`!=`|Différent de|
|`<`|Inférieur|
|`<=`|Inférieur ou égal|
|`>`|Supérieur|
|`>=`|Supérieur ou égal|

---

### Opérateurs logiques

|Opérateur|Rôle|
|---------|----|
|`&&`|ET logique|
|`\|\|`|OU logique|
|`!`|NON logique|

L'évaluation de l'expression est abrégée si possible.

---

### Tables de vérité des opérateurs

```csharp
// ET logique
Console.WriteLine(true && true); // true
Console.WriteLine(true && false); // false
Console.WriteLine(false && true); // false
Console.WriteLine(false && false); // false

// OU logique
Console.WriteLine(true || true); // true
Console.WriteLine(true || false); // true
Console.WriteLine(false || true); // true
Console.WriteLine(false || false); // false

// NON logique
Console.WriteLine(!true); // false
Console.WriteLine(!false); // true
```

---

### Priorité des opérateurs

Elle est gérée comme en mathématiques à l'aide de parenthèses `()`.

```csharp
let e = 3 + 2 * 4; // e contient la valeur 11
int f = (3 + 2) * 4; // f contient la valeur 20
```

---

### Division entière

- Une division entre deux entiers donne un résultat de type entier.
- Pour obtenir un résultat réel, il faut que l'un des deux opérandes soit de type réel ou que le résultat soit explicitement converti.

```csharp
int q = 5 / 2; // q vaut 2
int r = 5 % 2; // r vaut 1

double d = 5 / 2.0; // d vaut 2,5
double e = 5 / 2d; // e vaut 2,5
double f = (double)5 / 2; // f vaut 2,5

int z = 0;
int g = 5 / z; // NOK, division par zéro à l'exécution
```

---

### Incrémentation et décrémentation

- Les opérateurs `++` et `--` permettent resp. d'augmenter et de diminuer de 1 la valeur d'une variable.
- Ils équivalent à `variable = variable ± 1`.
- Attention, le résultat renvoyé par l'expression est différent selon la position de l'opérateur (pré- ou post-incrémentation/décrémentation).

```csharp
int a = 3;
a++; // a vaut 4
int b = a++; // a vaut 5, b vaut 4 !
int c = ++a; // a et c valent 6
```

---

### Opérateurs combinés d'affectation

- De la forme `variable {opérateur}= valeur`, ils équivalent à `variable = variable {operateur} valeur`
- Ils permettent de raccourcir certaines expressions.

```csharp
int i = 10;
i += 5; // Equivaut à i = i + 5, donc i vaut 15
i /= 3; // i vaut 5
```

---

### Dépassement de capacité

- Les types numériques ont une taille finie en mémoire, et donc une capacité limitée.
- Dans certaines circonstances, les limites des plages de valeur peuvent être dépassées

```csharp
int x = int.MaxValue; // Plus grand int possible
x++;
Console.WriteLine(x == int.MinValue); // true !
```

---

### Erreurs d'arrondi

L'arithmétique sur les types à virgule flottante peut entrainer des imprécisions et des erreurs d'arrondi.

```csharp
Console.WriteLine(5.32 + 2.23); // 7,550000000000001
Console.WriteLine(5.32m + 2.23m); // 7,55
```

---

### Concaténation de chaînes

Elle s'effectue à l'aide de l'opérateur `+` lorsqu'au moins l'une des deux opérandes est une chaîne.

```csharp
string s = "I " + "feel " + "good!";
Console.WriteLine(s);

int nbFamilles = 5;
string ecole = "ENSC";
string t = "Il y a " + nbFamilles + " familles à l'" + ecole;
Console.WriteLine(t); // "Il y a 5 familles à l'ENSC"
```

---

### Interpolation de chaînes

- Placé devant son début, le caractère `$` permet de créer une [chaîne interpolée](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/interpolated) dans laquelle on peut ajouter des expressions entre accolades `{}`.
- Ces expressions seront évaluées au moment du calcul de la valeur de la chaîne interpolée.

```csharp
int nbFamilles = 5;
string ecole = "ENSC";
string u = $"Il y a {nbFamilles} familles à l'{ecole}";
Console.WriteLine(u); "Il y a 5 familles à l'ENSC"
```

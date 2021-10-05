---
title: "ASP.NET Core"
date: 2021-09-21T09:40:11+02:00
draft: false
---

## Sommaire

- Qu'est-ce qu'ASP.NET Core ?
- Le framework ASP.NET Core MVC
- Mécanismes fondamentaux

---

## Qu'est-ce qu'ASP.NET Core ?

---

### Histoire d'ASP.NET Core

- A l'origine, .NET (Framework) incluait une technologie de création de pages web dynamiques nommée **ASP.NET** (_Active Server Pages_).
- **ASP.NET Core** est une réécriture d'ASP.NET basée sur .NET (Core).
- Standard actuel pour le développement web sous .NET.

---

### Points-clés d'ASP.NET Core

- Permet de créer des applications web et des services web (API) utilisés comme _backends_ par des clients riches ou des applications mobiles.
- Léger, moderne et modulaire.
- Inclut des technologies facilitant la gestion des pages dynamiques, des appels temps réel, des tests, etc.
- Déployable sur plusieurs serveurs web : Kestrel, Apache, nginx, etc.
- Multi-plateformes et [open source](https://github.com/dotnet/aspnetcore).

---

### UI générée côté serveur

Code HTML et CSS généré côté serveur, puis renvoyée au client.

- Peu d'exigences techniques côté client (navigateur simple, trafic réseau limité).
- Accès BD et contrôles centralisés.
- Exemples d'usages : sites dynamiques, blogs, CMS.

---

### UI générée côté client

Structure HTML (DOM) mise à jour dynamiquement côté client grâce à des appels asynchrones au serveur.

- Interactions riches avec l'utilisateur.
- Capacités matérielles et logicielles du client utilisables.
- Exemples d'usages : tableau de bord interactif, applications collaboratives.

---

## L'offre technique ASP.NET Core

- UI générée côté serveur : **Razor Pages**, **MVC**.
- UI générée côté client : **Blazor**, **SPA** avec Angular ou React.
- Une approche hybride est possible (exemple : MVC + Blazor).

---

## Le framework ASP.NET Core MVC

---

{{% section %}}

### Rappel : le fonctionnement du web

Le web est basé sur un modèle **client/serveur** :

- Le client (navigateur, application mobile, robot d'indexation, etc) envoie une demande (**requête**) au serveur.
- Le serveur prépare sa **réponse** à la requête du client, puis la lui renvoie.

---

![Modèle requête/réponse](images/web_request_response.png)

{{% /section %}}

---

### Le protocole HTTP

- _HyperText Transfer Protocol_.
- Socle technique du web.
- Equivalent sécurisé : **HTTPS**.
- Basé sur des **commandes** textuelles exprimant les différentes actions possibles : _GET_, _PUT_, _POST_, etc).

---

### L'architecture MVC

- _Model-View-Controller_ (_Modèle-Vue-Contrôleur_).
- Décomposition d’une application en trois grandes parties :
  - **Modèle** : accès aux données et logique métier (_business logic_).
  - **Vue** : affichage et interactions avec l’utilisateur.
  - **Contrôleur** : dynamique de l’application, lien entre Modèle et Vue.
- Application du principe de séparation des responsabilités.

---

### MVC : un peu d'histoire

- Apparu à la fin des années 1970 pour le langage OO **Smalltalk**. Objectif : séparer le code de l’IHM de la logique applicative.
- Appliqué depuis dans de très nombreux contextes et langages :
  - web côté serveur : frameworks Symfony (PHP), Django (Python), Rails (Ruby), etc.
  - web côté client : frameworks Angular, Ember (JavaScript), etc.
  - desktop : bibliothèque Swing (Java), etc.

---

[![Dynamique d'un serveur web MVC](images/symfony_mvc.png)](https://symfony.com/doc/current/index.html)

---

### Avantages et inconvénients

- Avantages :

  - Clarification de l’architecture.
  - Séparation nette des responsabilités => couplage faible, cohésion forte, maintenance et évolutions facilitées.

- Inconvénients :
  - Complexification de l’architecture.
  - Rigidité.

---

### ASP.NET Core MVC

- Framework de création d'applications web basées sur l'architecture MVC.
- Implémente de nombreux services et bonnes pratiques, parmi lesquels :
  - Routage des requêtes entrantes.
  - Gestion des pages dynamiques.
  - Authentification.
  - Injection de dépendance.
  - Tests.
  - ...

---

### Structure d'une application ASP.NET Core MVC

![Structure d'une application ASP.NET Core MVC](images/aspnetcoremvc_structure.png)

---

### Les contrôleurs

- Créés dans le répertoire `Controllers/`.
- Héritent de la classe abstraite `Controller`.
- Définissent les points d'entrée dans l'application sous la forme de méthodes d'action annotables.

```csharp
// GET: Movies/Details/5
public async Task<IActionResult> Details(int? id)
{
    //...
}

// POST: Movies/Delete/5
[HttpPost, ActionName("Delete")]
[ValidateAntiForgeryToken]
public async Task<IActionResult> DeleteConfirmed(int id)
{
  // ...
}
```

---

### Les modèles

- Créés dans le répertoire `Models/`.
- Implémentent la logique métier de l'application sous la forme de classes **POCO** (_Plain Old C# Objects_) souvent associées à des tables BD.

```csharp
public class Movie
{
    public int Id { get; set; }

    [StringLength(60, MinimumLength = 3)]
    public string Title { get; set; }

    [Display(Name = "Release Date"), DataType(DataType.Date)]
    public DateTime ReleaseDate { get; set; }
    // ...
```

---

### Les vues

- Créés dans le répertoire `Views/` sous la forme de fichiers Razor (`.cshtml`).
- Représentent l'interface utilisateur (UI) de l'application.

```csharp
@{
    ViewData["Title"] = "Welcome";
}

<h2>Welcome</h2>

<ul>
    @for (int i = 0; i < (int)ViewData["NumTimes"]; i++)
    {
        <li>@ViewData["Message"]</li>
    }
</ul>
```

---

### Code et librairies client

- Regroupés dans le répertoire `wwwroot/`.
- Rassemblent les fichiers CSS et JavaScript utilisés côté client.
- Incluent par défaut Bootstrap et jQuery.

---

### Le fichier appsettings.json

Centralise les paramètres de configuration de l'application.

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information",
      "Microsoft.EntityFrameworkCore.Database.Command": "Information"
    }
  },
  "AllowedHosts": "*",
  "ConnectionStrings": {
    "MvcMovieContext": "Data Source=MvcMovieContext-8719dcdb-c317-48bf-9cd8-a4c4167ce370.db"
  }
}
```

---

### Le fichier Startup.cs

Contient la classe `Startup` qui permet :

- la configuration des services utilisés par l'application ;
- la définition du _pipeline_ de gestion des requêtes HTTP entrantes.

---

### Exemple de classe Startup

```csharp
public class Startup
{
    // Use this method to add services to the container.
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddControllersWithViews();
    }

    // Use this method to configure the HTTP request pipeline.
    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        app.UseHttpsRedirection();
        app.UseStaticFiles();

        app.UseRouting();

        app.UseAuthorization();

        app.UseEndpoints(endpoints =>
        {
            endpoints.MapDefaultControllerRoute();
        });
    }
}
```

---

## Mécanismes fondamentaux

---

{{% section %}}

### Routage des requêtes

- Associe les requêtes HTTP entrantes au code à éxécuter (méthodes des contrôleurs).
- Permet à l'application web d'utiliser des URL propres et _SEO-friendly_, plutôt que des noms de fichiers.
- [Plus d'informations](https://docs.microsoft.com/en-us/aspnet/core/mvc/controllers/routing?view=aspnetcore-5.0).

---

### Routage par convention

- Permet de définir globalement la correspondance entre le format de l'URL et la méthode d'action d'un contrôleur à exécuter.
- Format par défaut : `/[Controller]/[ActionName]/[Parameters]`.
- Exemple : `https://myapp/Student/Details/Code=137` appelle la méthode `Details` du contrôleur `StudentController`, en lui passant un paramètre nommé `Code` ayant la valeur 137.

---

### Configuration du routage par convention dans Startup

```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    // ...
    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllerRoute(
            name: "default",
            pattern: "{controller=Home}/{action=Index}/{id?}");
    });
}
```

`Home`, `Index` et `id` sont resp. les noms par défaut du contrôleur, de l'action et du paramètre (optionnel).

{{% /section %}}

---

### Scaffolding

`> dotnet-aspnet-codegenerator [arguments]`

- Permet de générer le code source pour les opérations élémentaires **CRUD** (_Create, Read, Update, Delete_) liées à une classe du Modèle.
- [Plus d'informations](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/tools/dotnet-aspnet-codegenerator?view=aspnetcore-5.0).
- [Exemple de résultat](https://github.com/ensc-glog/MvcMovie/commit/f5c4ec45033f5509ec736bc1bebf010f200921f0).

---

### Database context

- Hérite de la classe abstraite `DbContext`.
- Spécifit les classes du Modèle à sauvegarder dans la base de données.

```csharp
public class MvcMovieContext : DbContext
{
    public MvcMovieContext(DbContextOptions<MvcMovieContext> options)
        : base(options)
    {}

    public DbSet<MvcMovie.Models.Movie> Movie { get; set; }
}
```

---

### Migrations

`> dotnet ef migrations add InitialCreate`

`> dotnet ef database update`

- Permettent à la base de données d'être synchronisée avec les évolutions du Modèle, sans perte de données.
- Migration = évolution incrémentale depuis la migration précédente.

---

### Envoi de données aux vues

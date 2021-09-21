---
title: "ASP.NET Core"
date: 2021-09-21T09:40:11+02:00
draft: true
---

## Sommaire

- Qu'est-ce qu'ASP.NET Core ?
- Le framework ASP.NET Core MVC
- Création d'API web

---

## Qu'est-ce qu'ASP.NET Core ?

---

### Histoire d'ASP.NET Core

- A l'origine, .NET (Framework) incluait une technologie de création de pages web dynamiques nommée **ASP.NET** (_Active Server Pages_).
- **ASP.NET Core** est une réécriture d'ASP.NET basée sur .NET (Core).
- Standard actuel pour le développement web sous .NET.

---

### Points-clé d'ASP.NET Core

- Permet de créer des applications web et des services web (API) utilisés comme _backends_ par des clients riches ou des applications mobiles.
- Léger, moderne et modulaire.
- Inclut des technologies facilitant la gestion des pages dynamiques, des appels temps réel, des tests, etc.
- Déployable sur plusieurs serveurs web : IIS, Apache, nginx, etc.
- Multi-plateformes et [open source](https://github.com/dotnet/aspnetcore).

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

### Routage des requêtes

- Associe le code à exécuter aux requêtes HTTP entrantes.
- Permet à l'application web d'utiliser des URL propres et _SEO-friendly_, plutôt que des noms de fichiers.
- [Plus d'informations](https://docs.microsoft.com/en-us/aspnet/core/mvc/controllers/routing?view=aspnetcore-5.0).

---

{{% section %}}

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

### Auto-certification de l'application

`> dotnet dev-certs https --trust`

Nécessaire pour lancer l'application localement avec HTTPS.

---

### Recompilation dynamique

`> dotnet add package Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation`

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddControllersWithViews().AddRazorRuntimeCompilation();
    // ...
}
```

Permet de modifier le code à la volée sans devoir relancer l'exécution.

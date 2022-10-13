## Tests

---

### Typologie des tests

- **Test unitaire** (TU) : vérifie un composant individuel de l'application.
- **Test d'intégration** : vérifie les interactions entre différents composants de l'application, y compris des composants externes comme une base de données ou un service web.
- **Test fonctionnel (ou test de validation)** : vérifie que l'application fonctionne comme prévu du point de vue de l'utilisateur.

---

### Tests unitaires Vs tests d'intégration

- Ils sont tous deux automatisés.
- Les TU isolent le composant à tester du reste de l'application à l'aide de _test doubles_ (parfois appelés _dummies_, _stubs_ ou encore _mocks_) qui simulent le comportement des autres composants. Leur exécution est rapide.
- Les tests d'intégration se basent sur les véritables composants de l'application. Leur mise en place est souvent plus complexe et leur exécution plus lente.

---

### Quelle stratégie adopter ?

- Vouloir tester tous les scénarios et configurations possibles est coûteux et pas forcément efficace.
- Il est préférable de se concentrer sur les éléments-clés offrant le meilleur rapport coût/bénéfices : composants essentiels, opérations élémentaires (CRUD), principaux services de l'application...
- Des _smoke tests_ vérifiant uniquement le renvoi d'un code HTTP de succès pour chaque route peuvent constituer un premier filet de sécurité.

---

### Etapes d'un test : le patron AAA

- _Arrange_ : préparation du test.
  - Lancement de l'application ;
  - Préparation de la base de données ;
  - ...
- _Act_ : réalisation des opérations à tester.
- _Assert_ : vérification des résultats des actions précédentes au moyen d'[assertions](<https://en.wikipedia.org/wiki/Assertion_(software_development)>).

---

### Création d'un projet de test .NET

`> dotnet new xunit -o <TestProjectName>`

[xUnit](https://xunit.net/) est un framework de tests unitaires _open source_ pour la plate-forme .NET.

`> dotnet add ./<TestProjectName>/<TestProjectName>.csproj reference ./<ProjectName>/<ProjectName>.csproj`

Ajoute au projet de test une référence vers le projet à tester (les deux étant situés dans le même répertoire parent).

---

### Exemple de classe de test

`[Fact]` indique une méthode de test.

```csharp
using Xunit;

namespace Prime.UnitTests.Services
{
    public class PrimeService_IsPrimeShould
    {
        [Fact]
        public void IsPrime_InputIs1_ReturnFalse()
        {
            // Arrange
            var primeService = new PrimeService();
            // Act
            bool result = primeService.IsPrime(1);
            // Assert
            Assert.False(result, "1 should not be prime");
        }
    }
}
```

---

### Initialisation du test

Permet d'éviter la duplication de code.

```csharp
ppublic class PrimeService_IsPrimeShould
{
    private readonly PrimeService _primeService;

    public PrimeService_IsPrimeShould()
    {
        // Create instance of tested class
        _primeService = new PrimeService();
    }
    // ...
```

---

### Paramétrage des méthodes de test

```csharp
    // ...
    [Theory]
    [InlineData(2)]
    [InlineData(3)]
    [InlineData(5)]
    [InlineData(7)]
    public void IsPrime_PrimesLessThan10_ReturnTrue(int value)
    {
        var result = _primeService.IsPrime(value);

        Assert.True(result, $"{value} should be prime");
    }
}
```

---

### Exécution des tests

`> dotnet test`

![dotnet test result](images/dotnet_test_result.png)

---

### Configuration d'un projet de test pour ASP.NET Core

`> dotnet add package Microsoft.AspNetCore.Mvc.Testing -v 5.0.12`

Ajoute un package dédié aux tests dans cet environnement, ici dans une version adaptée à .NET 5.

---

### Exemple de classe de test

```csharp
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc.Testing;
using Xunit;

namespace MvcMovie.Tests
{
    public class HomeControllerTests
    : IClassFixture<WebApplicationFactory<MvcMovie.Startup>>
    {
        private readonly WebApplicationFactory<MvcMovie.Startup> _factory;

        public HomeControllerTests(WebApplicationFactory<MvcMovie.Startup> factory)
        {
            _factory = factory;
        }
        // ...
```

---

### Smoke testing d'un contrôleur

```csharp
    // ...
    [Theory]
    [InlineData("/")]
    [InlineData("/Home/Index")]
    [InlineData("/Home/Privacy")]
    public async Task Get_EndpointsReturnSuccessAndCorrectContentType(string url)
    {
        // Arrange
        var client = _factory.CreateClient();
        // Act
        var response = await client.GetAsync(url);
        // Assert
        response.EnsureSuccessStatusCode(); // Status Code 200-299
        Assert.Equal("text/html; charset=utf-8",
            response.Content.Headers.ContentType.ToString());
    }
}
```

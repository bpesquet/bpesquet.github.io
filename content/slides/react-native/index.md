---
title: "React Native"
date: 2021-10-27T13:48:28+02:00
draft: false
---

## Sommaire

- Introduction
- Gestion de l'UI
- Gestion de l'état
- Utilisation d'API web

---

## Introduction

---

### L'écosystème mobile

- Absence de monopole.
- Deux poids lourds : Android et iOS.
- Parts de marché stables depuis plusieurs années.

---

![Smartphone platform market share](images/smartphone_market_share_2016.jpg)

---

![Market share evolution 2015-2019](images/market-share-2015_2019.png)

---

![Mobile OS Fragmentation](images/os-fragmentation_2018.jpg)

---

{{% section %}}

### Développement mobile natif

Création d'applications en utilisant la technologie prévue par le concepteur de l'OS.

- Android : Java
- IOS : Objective-C ou Swift

{{% fragment %}}Ces technologies sont **incompatibles**.{{% /fragment %}}

---

### Avantages

- Accès à l'intégralité des fonctionnalités matérielles et logicielles du terminal mobile.
- Performances optimales.

---

### Inconvénient (majeur !)

Nécessité de créer puis de faire évoluer une application pour chaque environnement.

{{% /section %}}

---

{{% section %}}

### Solutions hybrides

Création d'applications mobiles compatibles avec plusieurs OS mobiles grâce à un framework dédié.

Une application hybride est une application web qui s'exécute à l'intérieur d'un navigateur.

Exemples : [Apache Cordova](https://cordova.apache.org), [Ionic](https://ionicframework.com)

---

### Avantages

- Fonctionnalités et performances proches de celles d'une application native.
- Economies de ressources pour créer l'application.
- Une seule base de code : maintenance et évolution facilitées.

---

### Inconvénients

- Impossible d'accéder à certaines fonctionnalités matérielles ou logicielles spécifiques.
- _Look'n'feel_ non natif.
- Mauvaises performances dans certains scenarii.

{{% /section %}}

---

{{% section %}}

### Développement natif multi-plateformes

Création d'applications mobiles compatibles avec plusieurs OS mobiles grâce à un framework dédié.

Le framework encapsule les véritables composants natifs de l'OS.

Exemples : [React Native](https://facebook.github.io/react-native/), [Weex](https://weex.apache.org/), [Xamarin](https://www.visualstudio.com/fr/xamarin/)

---

### Le meilleur des deux mondes ?

Combine les avantages du natif (_look'n'feel_, performances) et de l'hybride (une seule base de code).

Limite potentielle : le support de l'OS dépend entièrement du framework.

{{% /section %}}

---

### React Native

Framework créé par Facebook, open source depuis 2015.

Déclinaison mobile du framework JavaScript [React](https://reactjs.org/).

![React logo](images/reactjs.png)

---

### Expo

Framework pour faciliter la création et le déploiement d'applications React Native.

![Expo logo](images/expo_logo.png)

- [Expo CLI](https://github.com/expo/expo-cli) : outil en ligne de commande pour le développement local.
- [Expo client](https://expo.io) : application mobile à installer sur le terminal cible pour le déploiement.

---

### Création d'une application

```bash
# Install expo-cli globally
# (Node.js and Git are prerequisites)
npm install -g expo-cli

# Create a new app in the my-new-project subfolder
# Use managed TypeScript template
expo init my-new-project -t expo-template-blank-typescript
```

- Workflow _managé_ : projet entièrement géré par Expo (plus simple).

- Workflow _bare_ : plus proche d'un projet React Native pur.

---

### Contenu du répertoire créé

![Arborescence React Native](images/rn-app-structure.png)

---

### Déploiement de l'application

```bash
cd my-new-project # move into project directory
npm start # Or 'expo start'
```

Ensuite, scan du QR Code depuis l'application Expo (Android) ou l'appareil photo du smartphone (iOS).

![Expo QR Code](images/expo_qrcode.png)

---

### Détails sur le déploiement

- L'application est hébergée sur un serveur web local.
- Expo s'y connecte pour la récupérer puis la lancer.
- Une interface web de gestion s'affiche.

![Expo Management](images/expo_management.png)

---

### Rechargement dynamique

[![Live Reload](images/expo_reload.jpeg)](https://openclassrooms.com/fr/courses/4902061-developpez-une-application-mobile-react-native/)

---

### Connexion au serveur Expo

L'application mobile Expo client doit accéder au serveur web de la machine de développement pour pouvoir lancer l'application RN.

Il existe plusieurs modes de connexion :

- **LAN** : utilisation du réseau Wifi local. Peut poser problème dans certains environnements Wifi sécurisés.
- **Tunnel** : création d'un tunnel avec [ngrok](https://ngrok.com/) pour accéder au serveur local via le web. Nécessite que le terminal mobile dispose d'un accès internet.

---

### Utilisation d'un émulateur

- Alternative à l'emploi d'un terminal mobile pour tester l'application RN.
- Nécessite l'installation de [XCode (iOS)](https://developer.apple.com/xcode/) ou [Android Studio](https://developer.android.com/studio) sur le machine de développement.
- Documentation : [iOS](https://docs.expo.io/workflow/ios-simulator/) | [Android](https://docs.expo.io/workflow/android-studio-emulator/).

![Expo emulator](images/expo-emulator.png)

---

### Le fichier de configuration app.json

```json
{
  "expo": {
    "name": "My New Project",
    "slug": "my-new-project",
    "version": "1.0.0",
    "orientation": "portrait",
    "icon": "./assets/icon.png",
    "splash": {
      "image": "./assets/splash.png",
      "resizeMode": "contain",
      "backgroundColor": "#ffffff"
    },
    "updates": {
      "fallbackToCacheTimeout": 0
    },
    "assetBundlePatterns": ["**/*"],
    "ios": {
      "supportsTablet": true
    },
    "android": {
      "adaptiveIcon": {
        "foregroundImage": "./assets/adaptive-icon.png",
        "backgroundColor": "#FFFFFF"
      }
    },
    "web": {
      "favicon": "./assets/favicon.png"
    }
  }
}
```

---

### Le fichier package.json

```json
{
  "main": "node_modules/expo/AppEntry.js",
  "scripts": {
    "start": "expo start",
    "android": "expo start --android",
    "ios": "expo start --ios",
    "web": "expo start --web",
    "eject": "expo eject"
  },
  "dependencies": {
    "expo": "~40.0.0",
    "expo-status-bar": "~1.0.3",
    "react": "16.13.1",
    "react-dom": "16.13.1",
    "react-native": "https://github.com/expo/react-native/archive/sdk-40.0.1.tar.gz",
    "react-native-web": "~0.13.12"
  },
  "devDependencies": {
    "@babel/core": "~7.9.0",
    "@types/react": "~16.9.35",
    "@types/react-dom": "~16.9.8",
    "@types/react-native": "~0.63.2",
    "typescript": "~4.0.0"
  },
  "private": true
}
```

---

### Le fichier principal App.tsx

```tsx
import { StatusBar } from "expo-status-bar";
import React from "react";
import { StyleSheet, Text, View } from "react-native";

export default function App() {
  return (
    <View style={styles.container}>
      <Text>Open up App.tsx to start working on your app!</Text>
      <StatusBar style="auto" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
  },
});
```

---

### Les formats JSX et TSX

- Syntaxe introduite pour le framework web [React](https://reactjs.org/).
- Permet de décrire une UI en intégrant balisage et logique applicative.
- TSX : équivalent de JSX avec support de TypeScript.

```jsx
// JSX for React (web)
const name = "Clarisse Agbegnenou";
const element = <h1>Hello, {name}</h1>;
```

```jsx
// JSX for React Native (mobile)
const a = <View />;
const b = (
  <View foo="hello" bar={baz}>
    <Text>42</Text>
  </View>
);
```

---

### La notion de composant

- Les **composants** sont les blocs de base d'une application React (Native).

- Ils permettent de créer une UI sous forme **déclarative** par assemblage de composants.

- Ils doivent comporter une fonction qui définit leur rendu visuel.

---

### Composants fonctions

- La valeur de retour de la fonction définit le rendu.
- Syntaxe la plus concise, pratique pour les composants simples.

```tsx
import React from "react";
import { Text } from "react-native";

const Cat = () => {
  const name = "Maru";
  return <Text>Hello, I am {name}!</Text>;
};

export default Cat;
```

---

### Composants classes

- La méthode `render()` définit le rendu.
- Syntaxe à privilégier pour les composants complexes.

```tsx
import React from "react";
import { Text } from "react-native";

class Cat extends React.Component {
  render() {
    const name = "Maru";
    return <Text>Hello, I am {name}!</Text>;
  }
}

export default Cat;
```

---

### Propriétés (_props_) d'un composant

Caractéristiques définies au moment de la création, modifiables uniquement par le composant parent ([démo](https://snack.expo.io/@bpesquet/greeting)).

```tsx
import React, { Component } from "react";
import { Text, View } from "react-native";

class Greeting extends Component {
  // Component has a name property which is of type string
  constructor(public props: { name: string }) {
    super(props);
  }
  render() {
    return <Text>Hello {this.props.name}!</Text>;
  }
}

export default class LotsOfGreetings extends Component {
  render() {
    return (
      <View style={{ alignItems: "center" }}>
        <Greeting name="John" />
        <Greeting name="Paul" />
        <Greeting name="Jones" />
      </View>
    );
  }
}
```

---

### Etat (_state_) d'un composant

Etat interne (données) d'un composant, susceptible de changer au cours du temps (mutable). Modifié uniquement via `setState()` ([démo](https://snack.expo.io/@bpesquet/counter)).

```tsx
import React, { Component } from "react";
import { StyleSheet, Text, View } from "react-native";

interface CoounterState {
  count: number;
}

class Counter extends Component<{}, CoounterState> {
  constructor(public props: { color: string; size: number }) {
    super(props);
    this.state = { count: 0 };
    setInterval(() => {
      this.setState({ count: this.state.count + 1 });
    }, 1000);
  }

  render() {
    const { count } = this.state;
    const { color, size } = this.props;

    return <Text style={{ color, fontSize: size }}>{count}</Text>;
  }
}

export default class CounterApp extends Component {
  render() {
    return (
      <View style={styles.container}>
        <Counter color="red" size={50} />
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
  },
});
```

---

### Composants de base

![React Native core components](images/basic_components.png)

---

### Composants d'interface utilisateur

![React native UI components](images/ui_components.png)

---

## Gestion de l'UI

---

### Cycle de vie d'un composant

Les composants RN suivent un cycle de vie bien défini composé d'étapes : **montage**, **rendu**, **mise à jour**, **démontage** et **suppression**.

[![React lifecycle](images/react-lifecycle.png)](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

---

### Méthodes liées au cycle de vie

Les redéfinir permet d'exécuter du code spécifique.

1. `constructor(props)` : initialisation des propriétés et de l'état.
1. `render()` : renvoi d'un élément React Native.
1. `componentDidMount()` : appels asynchrones.
1. `shouldComponentUpdate()` : renvoi d'un booléen pour annuler la mise à jour.
1. `componentDidUpdate()` : actions après la mise à jour du rendu.

---

### Gestion du style

Propriété `style` pour les composants de base.

Semblable à CSS avec nommage _camelCase_.

```jsx
import React, { Component } from "react";
import { StyleSheet, Text, View } from "react-native";

const styles = StyleSheet.create({
  bigblue: {
    color: "blue",
    fontWeight: "bold",
    fontSize: 30,
  },
  red: {
    color: "red",
  },
});

export default class LotsOfStyles extends Component {
  render() {
    return (
      <View>
        <Text style={styles.red}>just red</Text>
        <Text style={styles.bigblue}>just bigblue</Text>
        <Text style={[styles.bigblue, styles.red]}>bigblue, then red</Text>
        <Text style={[styles.red, styles.bigblue]}>red, then bigblue</Text>
      </View>
    );
  }
}
```

---

### Gestion des dimensions

Deux possibilités :

- Dimensions fixes
- Dimensions flexibles

---

### Dimensions fixes

Utile pour les composants qui doivent toujours être affichés à la même taille.

```jsx
import React, { Component } from "react";
import { View } from "react-native";

export default class FixedDimensionsBasics extends Component {
  render() {
    return (
      <View>
        <View
          style={{ width: 50, height: 50, backgroundColor: "powderblue" }}
        />
        <View style={{ width: 100, height: 100, backgroundColor: "skyblue" }} />
        <View
          style={{ width: 150, height: 150, backgroundColor: "steelblue" }}
        />
      </View>
    );
  }
}
```

---

### Dimensions flexibles

Les dimensions s'adaptent à l'espace disponible.

`flex:1` => espace partagé équitablement entre tous les composants d'un même parent ([démo](https://snack.expo.io/@bpesquet/dimensions)).

```jsx
import React, { Component } from "react";
import { View } from "react-native";

export default class FlexDimensionsBasics extends Component {
  render() {
    return (
      // Try removing the `flex: 1` on the parent View.
      // The parent will not have dimensions, so the children can't expand.
      // What if you add `height: 300` instead of `flex: 1`?
      <View style={{ flex: 1 }}>
        <View style={{ flex: 1, backgroundColor: "powderblue" }} />
        <View style={{ flex: 2, backgroundColor: "skyblue" }} />
        <View style={{ flex: 3, backgroundColor: "steelblue" }} />
      </View>
    );
  }
}
```

---

### Flexbox

- Mode de mise en page pour les éléments situés à l'intérieur d'un conteneur.
- Objectif : répartir au mieux l'espace disponible.

![Flexbox terminology](images/flexbox_terminology.png)

---

### `flexDirection` : flux des éléments

`column` (par défaut), `row`, `column-reverse`, `row-reverse`.

[![Flex direction](images/flexbox_flex_direction.png)](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

---

### `justifyContent` : axe principal

[![Flexbox: justify content](images/flexbox_justify_content.png)](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

---

### `alignItems` : axe secondaire

[![Flexbox: align Items](images/flexbox_align_items.png)](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

---

### Gestion de la navigation avec React Navigation

- Composant issu de la communauté des développeurs React Native.
- Devenu le standard pour les applications multi-vues.

[![React Navigation logo](images/react_navigation_logo.png)](https://reactnavigation.org)

---

### Installation de react-navigation

Utiliser `expo install` au lieu de `npm install` assure l'installation de versions compatibles avec celle d'Expo.

```bash
# Core components and dependencies
expo install @react-navigation/native react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view

# StackNavigator dependencies
expo install @react-navigation/stack

# BottomTabNavigator dependencies
expo install @react-navigation/bottom-tabs

# DrawerNavigator dependencies
expo install @react-navigation/drawer
```

---

### StackNavigator

Principe similaire au web : gestion d'une pile de vues.

```tsx
const Stack = createStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen name="Home" component={HomeScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

---

### Navigation entre vues

- Un objet `navigation` est automatiquement ajouté aux _props_ des vues gérées par React Navigation.
- Son API permet de naviguer entre les vues.

```ts
// Navigue vers une vue
this.props.navigation.navigate("RouteName");

// Permet d'aller plusieurs fois vers la même vue
this.props.navigation.push("RouteName");

// Revient à la vue précédente
this.props.navigation.goBack();
```

---

### Passage de paramètres entre vues

```ts
// Côté vue appelante
this.props.navigation.navigate("RouteName", {
  /* Objet dont les propriétés constituent les arguments */
  param1: "value1",
  // ...
});

// Côté vue appelée
// La propriété route.params permet de récupérer les paramètres passés à la vue
const { param1 } = this.props.route.params;
```

---

### En-tête des vues

```tsx
<MainStack.Navigator
  screenOptions={{
    headerStyle: {
      backgroundColor: "#f4511e",
    },
    headerTintColor: "#fff",
    headerTitleStyle: {
      fontWeight: "bold",
    },
  }}
>
// ...
```

---

### Vue modale

```tsx
<RootStack.Navigator mode="modal" headerMode="none">
  <RootStack.Screen
    name="Main"
    component={MainStackScreen}
    options={{ headerShown: false }}
  />
  <RootStack.Screen name="MyModal" component={ModalScreen} />
</RootStack.Navigator>
```

---

### Exemple récapitulatif

<https://github.com/ensc-mobi/StackNavigatorDemo>

![StackNavigator demo](images/stack-navigator-demo.png)

---

### TabNavigator

Affichage d'onglets en bas de l'écran.

```tsx
const Tab = createBottomTabNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Tab.Navigator>
        <Tab.Screen name="Home" component={HomeScreen} />
        <Tab.Screen name="Settings" component={SettingsScreen} />
      </Tab.Navigator>
    </NavigationContainer>
  );
}
```

---

### Navigation entre onglets

Fonctionnement identique à celui de la navigation entre les vues d'un `StackNavigator`.

```tsx
<Button
  title="Go to Settings"
  onPress={() => navigation.navigate("Settings")}
/>
```

---

### Affichage de piles (_stacks_) dans les onglets

```tsx
const HomeStack = createStackNavigator();
function HomeStackScreen() {
  // Define home stack
}

const SettingsStack = createStackNavigator();
function SettingsStackScreen() {
  // Define settings stack
}

const Tab = createBottomTabNavigator();
function TabScreen() {
  return (
    <Tab.Navigator>
      <Tab.Screen name="Home" component={HomeStackScreen} />
      <Tab.Screen name="Settings" component={SettingsStackScreen} />
    </Tab.Navigator>
  );
}
```

---

### Exemple récapitulatif

<https://github.com/ensc-mobi/TabNavigatorDemo>

![BottomTabNavigator demo](images/tab-navigator-demo.png)

---

### Autres possibilités de react-navigation

- [Navigation par menu accordéon](https://reactnavigation.org/docs/drawer-based-navigation)
- [Gestion de l'authentification](https://reactnavigation.org/docs/auth-flow)
- ...

---

## Gestion de l'état

---

### Rappels sur les propriétés

**Propriétés (_props_)** = caractéristiques définies au moment de la création du composant.

Les propriétés sont modifiables uniquement par le composant parent.

---

### Rappels sur l'état

**Etat (_state_)** = ensemble des données susceptibles d'être modifiées pendant l'exécution de l'application.

Chaque composant React Native possède un état interne, géré avec `this.state` et `this.setState()`.

Toute modification de l'état déclenche un nouveau rendu du composant.

---

### Problématique

La gestion locale de l'état devient insuffisante lorsqu'un composant doit **accéder à** ou **modifier** l'état d'un autre composant.

Nécessité de partager un état commun entre certains composants.

---

### Solution : _"lifting state up"_

- Remonter l'état au niveau du plus proche composant parent commun.
- Définir les actions de modification dans ce composant parent.
- Dans les composants enfants :
  - Remplacer l'état local par des propriétés définies par le parent.
  - Remplacer les actions locales par des appels aux actions définies dans le parent.

[Lifting State Up (React)](https://reactjs.org/docs/lifting-state-up.html)

---

### Application

<https://github.com/ensc-mobi/TempConverter>

![TempConverter demo](images/temp-converter.png)

---

### Utilisation de props dans les composants enfants

```jsx
class TemperatureInput extends React.Component {
  _onChangeText = (text) => {
    // Callback passed as component prop is called
    this.props.onTemperatureChange(text);
  };

  render() {
    const temperature = this.props.temperature;
    const scale = this.props.scale;
    const placeholder = `Enter temperature in ${scaleNames[scale]}`;
    return (
      <TextInput
        style={styles.text}
        placeholder={placeholder}
        value={temperature}
        onChangeText={this._onChangeText}
      />
    );
  }
}
```

---

### Remontée de l'état dans le composant parent

```jsx
class Calculator extends React.Component {
  constructor(props) {
    super(props);
    // Common state is lifted in closest parent of TemperatureInput components
    // Temperature can be set either in Celsius or in Fahrenheit
    this.state = { temperature: "", scale: "c" };
  }

  _onCelsiusChange = temperature => {
    this.setState({ scale: "c", temperature });
  };

  _onFahrenheitChange = temperature => {
    this.setState({ scale: "f", temperature });
  };
  // ...
```

---

### Appel aux actions définies dans le parent

```jsx
  // ...
  render() {
    const scale = this.state.scale;
    const temperature = this.state.temperature;
    const tempCelsius =
      scale === "f" ? tryConvert(temperature, toCelsius) : temperature;
    const tempFahrenheit =
      scale === "c" ? tryConvert(temperature, toFahrenheit) : temperature;

    return (
      <View>
        <TemperatureInput
          scale="c"
          temperature={tempCelsius}
          onTemperatureChange={this._onCelsiusChange}
        />
        <TemperatureInput
          scale="f"
          temperature={tempFahrenheit}
          onTemperatureChange={this._onFahrenheitChange}
        />
        <BoilingResult tempCelsius={parseFloat(tempCelsius)} />
      </View>
    );
  }
```

---

### Centralisation de l'état

Les composants parents peuvent finir par rassembler trop de choses :

- Etat commun
- Actions de modification
- Hiérarchie des composants enfants

Non-respect du principe de **séparation des responsabilités**.

---

### Solution

- Centraliser l'état et les actions de modifications dans des objets dédiés, souvent appelés **stores**.
- Donner accès à ces objets aux composants via des propriétés.
- Prévoir un mécanisme d'**abonnement** des composants aux mutations de l'état effectués uniquement dans les stores.

---

### Application

<https://github.com/ensc-mobi/TodoNative>

![TodoNative demo](images/todonative.png)

---

### Définition d'un store

```js
export default class TodoStore extends Store {
  constructor() {
    // Call to parent constructor is needed to init observation
    super();

    // The TODO task is used as key (unique identifier)
    // Therefore, each TODO must have a different task
    this.todos = [];
  }

  addTodo = (task) => {
    // Add new TODO at beginning of array
    this.todos = [{ task, completed: false }, ...this.todos];

    this.notifyObservers();
  };

  // ...

  // Used in parent class when notifying observers
  getState() {
    const todos = this.todos;
    return { todos };
  }
}
```

---

### Notification des changements d'état

Basée sur le Design Pattern [Observateur](https://fr.wikipedia.org/wiki/Observateur_%28patron_de_conception%29).

```js
export default class Store {
  constructor() {
    // Define an empty observer list
    this.observers = [];
  }

  // Add new observer to list
  addObserver(observer) {
    this.observers.push(observer);
  }

  // Notify all observers of a state change in the store
  notifyObservers() {
    this.observers.forEach((observer) => observer.setState(this.getState()));
  }
}
```

---

### Lien entre store et composant principal

```jsx
const App = () => {
  const todoStore = new TodoStore();

  return <MainView todoStore={todoStore} />;
};

export default App;
```

---

### Abonnement d'un composant

```jsx
export default class MainView extends React.Component {
  constructor(props) {
    super(props);
    this.state = this.props.todoStore.getState();
    this.props.todoStore.addObserver(this);
  }

  render() {
    return (
      <View style={styles.container}>
        <Header title="TodoNative" />
        <Input
          placeholder="Saisissez une nouvelle tâche"
          onSubmitEditing={this.props.todoStore.addTodo}
        />
        // ...
```

---

### Gestion de l'état avec MobX

- Quand l'application devient complexe, le nombre croissant de composants complique les évolutions de l'état.
- Les mutations de l'état peuvent déclencher un (trop) grand nombre de rendus des composants.

---

### Solution

- Utiliser une librairie dédiée à la gestion de l'état.
- [Bon choix](https://www.robinwieruch.de/redux-mobx-confusion/) pour la plupart des projets de taille intermédiaire : [MobX](https://mobx.js.org).

![MobX logo](images/mobx-logo.png)

```bash
# Add MobX to a React Native project
expo install mobx mobx-react
expo install --save-dev babel-preset-mobx
```

---

![MobX overview](images/mobx-overview.png)

---

### Application

<https://github.com/ensc-mobi/TodoNative-MobX>

![TodoNative-MobX demo](images/todonative.png)

---

### Définition d'une classe métier

```js
import { observable } from "mobx";

export default class Todo {
  @observable task;
  @observable completed;

  constructor(task = "", completed = false) {
    this.task = task;
    this.completed = completed;
  }

  toggle() {
    this.completed = !this.completed;
  }
}
```

---

### Définition d'un store

```js
import { observable } from "mobx";
import Todo from "../domain/Todo";

export default class TodoStore {
  @observable todos;
  @observable isLoading = true;

  constructor() {
    // The TODO task is used as key (unique identifier)
    // Therefore, each TODO must have a different task
    this.todos = [];
  }

  addTodo(task) {
    const todo = new Todo(task);
    // Add new TODO at beginning of array
    this.todos = [todo, ...this.todos];
  }

  // ...
}
```

---

### Lien entre store et composant principal

```jsx
const App = () => {
  const todoStore = new TodoStore();

  return <MainView todoStore={todoStore} />;
};

export default App;
```

---

### Abonnement d'un composant

```js
import { observer } from "mobx-react";
// ...

@observer
export default class MainView extends React.Component {
  onAddTodo = task => {
    this.props.todoStore.addTodo(task);
  };
  // ...

  render() {
    return (
      <View style={styles.container}>
        <Header title="TodoNative" />
        <Input
          placeholder="Saisissez une nouvelle tâche"
          onSubmitEditing={this.onAddTodo}
        />
        <FlatList
          style={styles.todoContainer}
          data={this.props.todoStore.todos}
          // ...
}
```

---

## Pourquoi pas Redux ?

![Redux all!](images/redux-all.jpeg)

- Librairie créée pour adresser des problématiques à l'échelle de Facebook
- Complexe et _overkill_ pour les projets "normaux"
- ["You might not need Redux"](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367) (écrit par son créateur)

---

## Utilisation d'API web

---

### La notion d'API

Une **API** (_Application Programming Interface_) est un point d'entrée programmatique dans un système.

Elle fournit un moyen d'interagir avec ce système.

Les API permettent aux développeurs d'intégrer des services externes dans leurs applications.

---

### Spécificités des API web

Une **API web** (appelée parfois service web) est une API accessible via les technologies du web : HTTP ou HTTPS.

Les API web utilisent le plus souvent le format de donnée **JSON**.

Certaines sont librement utilisables, d'autres nécessitent une authentification du client.

---

### Exemples d'API web

- [PokéAPI](https://pokeapi.co/)
- [Star Wars API](https://swapi.dev/)
- [Wikipedia](https://en.wikipedia.org/w/api.php?)
- [Spotify](https://developer.spotify.com/documentation/web-api/)
- [OMDb API](https://www.omdbapi.com/)

([Source](https://shkspr.mobi/blog/2016/05/easy-apis-without-authentication/))

---

### Outils pour la gestion des API web

- [Postman](https://www.getpostman.com/)
- Extension [RESTClient](https://addons.mozilla.org/fr/firefox/addon/restclient/) pour Firefox

---

### Appels réseau asynchrones avec JavaScript

Une [promesse](https://web.dev/promises/) (_promise_) est un objet qui encapsule une opération dont le résultat n'est pas encore connu.

La fonction JavaScript [fetch()](https://developers.google.com/web/updates/2015/03/introduction-to-fetch) exploite les possibilités des promesses.

```js
// Envoie une requête HTTP asynchrone vers l'URL spécifiée
fetch(url)
  .then(() => {
    // Code appelé ultérieurement si la requête réussit
  })
  .catch(() => {
    // Code appelé ultérieurement si la requête échoue
  });
```

---

### Accès à une ressource distante

```js
// Envoi d'une requête HTTP asynchrone vers l'URL spécifiée
// La réponse reçue ici contient des données JSON
fetch("http://my-api-url")
  // Accès au contenu JSON de la réponse
  .then((response) => response.json())
  .then((content) => {
    // Utilisation du contenu de la réponse
    // `content` est un objet ou un tableau JavaScript
  })
  .catch((error) => {
    console.error(error);
  });
```

---

### Mise à jour d'une ressource distante

```js
fetch("https://mywebsite.com/endpoint/", {
  method: "POST",
  headers: {
    Accept: "application/json",
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    firstParam: "yourValue",
    secondParam: "yourOtherValue",
  }),
});
```

---

### Application

<https://github.com/ensc-mobi/RandomBeer>

![Random Beer app](images/random_beer.png)

---

### Consommation d'une API web

```js
const headers = {
  "Content-Type": "application/json",
  Accept: "application/json",
};

// Retourne une recette de bière au hasard
export const getRandomBrewdog = () =>
  fetch(`${rootEndpoint}/beers/random`, { headers })
    .then((response) => response.json())
    // Access first element of returned array
    .then((beers) => beers[0])
    .catch((error) => {
      console.error(error);
    });
```

---

### Mise à jour de l'application

```jsx
  // ...
  _getRandomBrewdogWithFeedback = () => {
    this.setState({ isLoading: true });
    getRandomBrewdog().then(beer =>
      this.setState({
        name: beer.name,
        description: beer.description,
        isLoading: false // la requête est terminée
      })
    );
  };

  componentDidMount() {
    this._getRandomBrewdogWithFeedback();
  }

  // ...
```

---

### Interactions avec un SGBDR via une API web

<https://github.com/mevdschee/php-crud-api>

Fichier `api.php` à publier sur un serveur web PHP. Fournit une API web pour accéder aux données d'un SGBDR.

```php
// Update to reflect your local settings
$config = new Config([
  'username' => 'xxx',
  'password' => 'xxx',
  'database' => 'xxx',
]);
```

---

### Utilisation de PHP-CRUD-API

`http://my-server-url/api.php/records/...`

- `GET my-table` : renvoie la liste des enregistrements de la table `my-table`.
- `GET my-table/id` : renvoie l'enregistrement identifié par `id`.
- `POST my-table` : création d'un nouvel enregistrement avec les données contenues dans le corps de la requête.

---

### Application

<https://github.com/ensc-mobi/MyMoviesNative>

![MyMoviesNative demo](images/mymoviesnative.png)

---

### Classe métier film

```js
export default class Movie {
  @observable id;
  @observable title;
  // ...
  @observable image;

  constructor(
    id,
    title,
    // ...
    image
  ) {
    this.id = id;
    this.title = title;
    // ...
    this.image = image;
  }
}
```

---

### Accès au SGBDR

```js
const rootEndpoint = "http://localhost/mymovies/api.php/records";

const headers = {
  "Content-Type": "application/json",
  Accept: "application/json",
};

export const getAllMovies = () =>
  fetch(`${rootEndpoint}/movie/`, { headers })
    .then((response) => response.json())
    .then((jsonResponse) => jsonResponse.records)
    .catch((error) => {
      console.log(error);
    });
```

---

### Récupération de la liste des films

```js
export default class MovieStore {
  @observable movies;
  // ...

  fetchAll() {
    this.movies = [];
    getAllMovies().then((movies) => {
      //console.log(movies);
      movies.forEach((movieData) => {
        const movie = new Movie(
          movieData.mov_id,
          movieData.mov_title,
          // ...
          movieData.mov_image
        );
        this.movies = [movie, ...this.movies];
      });
    });
  }
}
```

---

### Vue principale

```jsx
export default class HomeScreen extends React.Component {
  render() {
    const movieStore = new MovieStore();
    // All React Navigation screens receive this object as prop
    const { navigation } = this.props;

    // Navigation object is passed down to children components
    return <MainView movieStore={movieStore} navigation={navigation} />;
  }
}
```

---

### Affichage d'un film dans la liste

```js
@observer
export default class MovieItem extends React.Component {
  render() {
    const { movie } = this.props;
    const { navigation } = this.props;

    return (
      <View style={styles.container}>
        <TouchableOpacity
          onPress={() => {
            navigation.navigate("Details", {
              movie: movie,
            });
          }}
        >
          <Text style={styles.text}>
            {movie.title} ({movie.year})
          </Text>
        </TouchableOpacity>
      </View>
    );
  }
}
```

---

### Détails sur un film

```js
export default class DetailsScreen extends React.Component {
  render() {
    const { navigation } = this.props;
    const movie = navigation.getParam("movie");
    const imageUrl = imagesEndpoint + movie.image;

    return (
      <View style={styles.container}>
        <Text style={styles.title}>
          {movie.title} ({movie.year})
        </Text>
        <Text style={styles.director}>Réalisateur(s) : {movie.director}</Text>
        <Text style={styles.description}>{movie.shortDescription}</Text>
        <Image style={styles.image} source={{ uri: imageUrl }}></Image>
      </View>
    );
  }
}
```

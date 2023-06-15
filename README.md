![logo_ironhack_blue 7](https://user-images.githubusercontent.com/23629340/40541063-a07a0a8a-601a-11e8-91b5-2f13e4e6b441.png)

# LAB | IronChronomètre JS

![giphy (1)](https://user-images.githubusercontent.com/76580/167427065-a674fb55-44ea-448a-a7ef-940b45eeb9df.gif)

<details>
  <summary>
   <h2>Objectifs d'apprentissage</h2>
  </summary>

Cet exercice vous permet de pratiquer et d'appliquer les concepts et les techniques enseignés en classe.

À la fin de cet exercice, vous serez capable de :

- Définir une `class` et l'utiliser pour créer des objets (instances).
- Définir et implémenter des méthodes de classe qui utilisent `this` pour accéder et manipuler les propriétés des objets.
- Utiliser des fonctions fléchées pour maintenir le contexte de `this`.
- Passer des fonctions en tant qu'arguments à d'autres fonctions (rappels).
- Utiliser `setInterval()` pour exécuter du code à intervalles spécifiés.
- Utiliser la méthode `clearInterval()` pour arrêter un minuteur d'intervalle.
- Utiliser l'objet `Math` et ses méthodes `Math.random()` pour générer des nombres aléatoires et `Math.floor()`, `Math.ceil()` ou `Math.round()` pour arrondir les nombres.

  <br>
  <hr>

</details>

## Introduction

Dans ce lab, nous allons créer un [chronomètre](https://www.dictionary.com/browse/chronometer). Les chronomètres sont très couramment utilisés dans le sport - course automobile, athlétisme, etc. Nous utiliserons des classes pour organiser et abstraire notre code et les timers JavaScript pour implémenter la fonctionnalité du chronomètre. C'est une occasion parfaite pour perfectionner nos compétences en programmation orientée objet (POO) et pratiquer le travail avec JavaScript asynchrone.

Commençons !

## Exigences

- Forker ce repo.
- Cloner ce repo.

## Soumission

- Une fois terminé, exécutez les commandes suivantes :

```shell
git add .
git commit -m "Solved lab"
git push origin master
```

- Créez une Pull Request pour que vos TAs puissent vérifier votre travail.

## Testez votre code

Ce LAB est équipé de tests unitaires pour fournir des retours automatisés sur votre progression. Si vous souhaitez vérifier les tests, ils se trouvent dans le fichier `tests/chronometer.spec.js`.

Pour exécuter les tests et votre code JavaScript, ouvrez le fichier `SpecRunner.html` à l'aide de l'extension VSCode [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer).

Pour voir les sorties des `console.log` de votre code JavaScript, ouvrez la [Console dans les outils de développement](https://developer.chrome.com/docs/devtools/open/#console).

<br>

## Instructions

Pour voir comment la version finale du chronomètre devrait fonctionner, consultez cette **[démonstration](https://sandrabosk.github.io/demo-chrono/index.html)**.

<br>

### Itération 0 : Commencer

#### L'interface utilisateur du chronomètre

Pour vous permettre de vous concentrer sur la partie JavaScript de l'exercice et sur le développement de la fonctionnalité du chronomètre, nous avons créé l'interface _utilisateur (UI)_ du chronomètre pour vous.

Pour commencer, **ouvrez la page `index.html` dans le navigateur**. Ensuite, vous devriez voir le chronomètre comme indiqué dans l'exemple ci-dessous. De cette façon, vous pouvez vérifier visuellement la fonctionnalité de votre chronomètre au fur et à mesure de votre progression dans l'exercice.

<details>
  <summary> Cliquez ici pour voir l'image</summary>

<br>

![](https://education-team-2020.s3-eu-west-1.amazonaws.com/web-dev/labs/chronometer.png)

</details>

<br>

La structure HTML, les styles CSS et la fonctionnalité du DOM du chronomètre se trouvent dans les fichiers `styles/style.css`, index.html et src/index.js. Ces fichiers contiennent déjà tout le code nécessaire, et **vous ne devez pas les modifier**.

<br>

#### Le chronomètre

**Vous effectuerez tout votre travail dans le fichier `src/chronometer.js`.**

L'objectif de l'exercice est de terminer l'implémentation de la classe `Chronometer` et de ses méthodes. La classe et les méthodes sont déjà définies dans le fichier `chronometer.js`, mais elles n'ont aucune fonctionnalité.

Le fichier `src/index.js` dépend des méthodes de la classe `Chronometer` pour afficher l'heure sur le chronomètre et inclut une instance de `Chronometer` de la manière suivante :

> ```js
> // src/index.js
> const chronometer = new Chronometer(); // instance of the Chronometer
>
> // ...
> ```

Les méthodes de `Chronometer` ne sont pas encore fonctionnelles. Votre tâche consistera à les implémenter dans les itérations suivantes.

<br>

### Itération 1 : La classe `Chronometer`

Implémentons la classe `Chronometer` en suivant les exigences suivantes :

- La classe (`constructor`) ne doit prendre aucun argument.
- La classe (`constructor`) doit initialiser deux propriétés pour chaque nouvel objet chronomètre :
  - `currentTime`, avec la valeur initiale définie à `0`.
  - `intervalId`, avec la valeur initiale définie à `null`.

Une fois terminé, vérifiez les résultats des tests et vérifiez que votre code passe les vérifications.

<br>

### Itération 2 : La méthode `start`

##### Méthode `start()`

- doit être déclarée dans la classe `Chronometer`
- doit recevoir un argument (`printTimeCallback`)
- doit incrémenter la propriété `currentTime` de `1` chaque seconde
- doit appeler la fonction `printTimeCallback` transmise toutes les secondes

Lorsqu'elle est appelée, la méthode `start` commencera à mesurer le temps en exécutant une fonction à intervalles de 1 seconde et en incrémentant le nombre de secondes stockées dans la propriété `currentTime` de `1`.

Vous devriez utiliser la méthode `setInterval` pour y parvenir. L'identifiant d'intervalle retourné par l'appel à `setInterval` devrait être attribué à la propriété `intervalId`, de cette manière, nous pourrons l'effacer ultérieurement lorsque nous devrons arrêter le minuteur.

De plus, la méthode `start` devrait accepter une fonction de rappel en tant qu'argument. Appelons-la `printTimeCallback`. Une fois que start est invoqué, la fonction `printTimeCallback` en question devrait être exécutée à des intervalles de 1 seconde, c'est-à-dire à l'intérieur de `setInterval`.
Si `printTimeCallback` n'est pas passé, il devrait être ignoré (indice : vous devriez vérifier si le rappel a été passé avant de tenter de l'exécuter).

:bulb: _Indice 1_ : Gardez à l'esprit que si vous passez une déclaration de fonction à la méthode `setInterval()` (en écrivant `setInterval(function () {/* */})`), le mot clé `this` ne fera pas référence à l'objet _chronomètre_, mais à la portée globale. Pour pouvoir faire référence au chronomètre en accédant à `this`, passez une expression de fonction (appelée fonction fléchée) à la méthode `setInterval()` (en écrivant `setInterval(() => {/* */})` à la place).

<br>

### Itération 3 : La méthode `getMinutes`

##### Méthode `getMinutes()`

- devrait être déclarée dans la classe `Chronometer`
- ne devrait recevoir aucun argument
- devrait renvoyer le nombre de _minutes_ entières écoulées

Nous stockons le nombre de secondes écoulées dans la propriété `currentTime`. Toutefois, nous devrons d'abord calculer combien de minutes se sont écoulées.

La méthode `getMinutes` ne devrait pas prendre d'arguments et renvoyer le nombre de minutes entières écoulées en tant que nombre entier, c'est-à-dire un nombre entier.
Pour calculer les minutes, divisez le temps actuel par 60 et utilisez la méthode `Math.floor()` pour obtenir un nombre arrondi.

<br>

### Itération 4 : La méthode `getSeconds`

##### Méthode `getSeconds()`

- devrait être déclarée dans la classe `Chronometer`
- ne devrait recevoir aucun argument
- devrait renvoyer le nombre de _secondes_ entières écoulées

Nous avons précédemment implémenté la méthode qui renvoie le nombre de minutes écoulées. Et si nous voulons obtenir le nombre de secondes écoulées depuis le début de la minute en cours ?

La méthode `getSeconds` devrait renvoyer le nombre de secondes écoulées depuis le début de la minute en cours.

Par exemple, si la propriété `currentTime` contient `75`, `getSeconds` devrait renvoyer `15`. Si `currentTime` contient `210`, `getSeconds` devrait renvoyer `30`, et ainsi de suite.

Vous pouvez utiliser [l'opérateur modulo](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Remainder) (temps actuel % 60) pour obtenir le nombre de secondes restantes.
<br>

### Itération 5 : La méthode `computeTwoDigitNumber`

##### Méthode `computeTwoDigitNumber()`

- doit être déclarée dans la classe `Chronometer`
- doit recevoir _un_ argument (`value` (valeur))
- doit renvoyer une chaîne de caractères
- doit toujours renvoyer une chaîne de caractères de longueur 2

Notre _chronomètre_ possède un écran qui affiche le nombre de minutes et de secondes écoulées. Cependant, parfois les méthodes `getMinutes` et `getSeconds` renvoient un nombre à un seul chiffre. Créons une fonction d'aide qui convertira n'importe quel nombre en une représentation sous forme de chaîne de caractères de deux chiffres.

La méthode `computeTwoDigitNumber` doit prendre un argument `value` (valeur), un nombre, et renvoyer une chaîne de caractères. Le nombre reçu doit être _rempli_ de zéros lorsque la valeur est un nombre à un seul chiffre.

Par exemple, si `computeTwoDigitNumber` est appelée avec le nombre `7`, elle doit renvoyer une chaîne de caractères `"07"`. Si elle est appelée avec le nombre `36`, elle doit renvoyer une chaîne de caractères avec la valeur `"36"`.

:bulb: _Astuce_ : Vous pouvez réaliser cela de manière dynamique en utilisant la méthode `.slice()`.

Nous utiliserons la méthode `computeTwoDigitNumber` dans les itérations suivantes pour formater les valeurs avant de les afficher sur le _chronomètre_.

<br>

### Itération 6 : La méthode `stop`

##### Méthode `stop()`

- doit être déclarée dans la classe `Chronometer`
- ne doit recevoir aucun argument
- doit appeler `clearInterval`
- doit effacer l'intervalle de temps existant

Nous pouvons démarrer notre chronomètre, mais nous devons encore implémenter une méthode pour l'arrêter.

Lorsqu'elle est appelée, la méthode `stop` doit effacer l'intervalle avec l'identifiant que nous avions stocké dans la propriété `intervalId`. C'est aussi simple que ça.

:bulb: _Astuce_ : Utilisez `clearInterval`.

<br>

### Itération 7 : La méthode `reset`

##### Méthode `reset()`

- doit être déclarée dans la classe `Chronometer`
- ne doit recevoir aucun argument
- doit réinitialiser la valeur de la propriété `currentTime` à `0`

La méthode `reset()` va réinitialiser notre chronomètre. Pour cela, nous devons définir la valeur de la propriété `currentTime` à `0`, et c'est tout !

<br>

### BONUS - Itération 8 : La méthode `split`

##### Méthode `split()`

- doit être déclarée dans la classe `Chronometer`
- ne doit recevoir aucun argument
- doit renvoyer une chaîne de caractères
- doit renvoyer une chaîne de caractères indiquant les minutes et les secondes au format _"mm:ss"_

Nous pourrions vouloir extraire un horodatage formaté représentant le temps écoulé depuis le démarrage du chronomètre. Nous appelons cela "obtenir le temps intermédiaire".

La méthode `split` ne devrait prendre aucun argument et devrait renvoyer une chaîne de caractères où le temps depuis le démarrage est formaté comme _"mm:ss"_. En interne, la méthode `split` peut utiliser les méthodes précédemment déclarées `getMinutes`, `getSeconds` et `computeTwoDigitNumber`.

<details>
  <summary> Cliquez ici pour voir l'image </summary>
<br>

![](https://s3-eu-west-1.amazonaws.com/ih-materials/uploads/upload_a5c9687f25bd710b2e7658ee6d997174.png)

</details>

<br>

### BONUS - Itération 9 : Centièmes de seconde

Notre chronomètre est désormais entièrement fonctionnel et nous pouvons l'utiliser pour mesurer le temps que nous passons sur chaque exercice. Maintenant, que se passe-t-il si nous voulons calculer notre temps dans une course ? Nous aurions besoin d'être plus précis avec notre chronomètre. Comment pouvons-nous être plus précis ? En ajoutant les centièmes de seconde ([centiseconds](https://en.wiktionary.org/wiki/centisecond)) !

Enfin, en JavaScript, nous devrons ajouter toute la logique pour afficher les centièmes de seconde sur le chronomètre. Vous devrez également afficher ces centièmes de seconde dans chaque instantané des _Splits_.

![](https://s3-eu-west-1.amazonaws.com/ih-materials/uploads/upload_82e9d1fd5976a3f98bb1382f2385f6a1.png)

Votre objectif est de créer la logique JavaScript pour :

- Pouvoir compter les centièmes de seconde.
- Capturer les centièmes de seconde lorsque vous capturez un temps intermédiaire.
- Réinitialiser le temps actuel à 0.

**Remarque** : Cette itération légèrement plus compliquée nécessitera de modifier l'intervalle du timer et de mettre à jour la logique de calcul des _minutes_, _secondes_ et _centièmes de seconde_. Utilisez les lignes directrices de conversion suivantes comme référence :

> 1 centième de seconde = 10 millisecondes
>
> 1 seconde = 100 centièmes de seconde = 1000 millisecondes

<br>

#### Tests et configuration des fichiers (Bonus - Itération 9 : Centièmes de seconde)

Vous utiliserez différents tests et un fichier de travail différent pour cette itération. Pour ce faire, modifiez vos fichiers HTML :

1. Dans `SpecRunner.html`, _commentez_ les deux balises de script utilisées et décommentez les deux pour l'itération bonus, comme ceci :

   ```html
   <!--  Iterations 1 - 8 -->
   <!-- <script src="src/chronometer.js"></script> -->
   <!-- <script src="tests/chronometer.spec.js"></script> -->

   <!-- Bonus Iteration 9: Centiseconds -->
   <script src="src/chronometer-centiseconds.js"></script>
   <script src="tests/chronometer-centiseconds.spec.js"></script>
   ```

2. Dans `index.html`, _commentez_ la balise de script qui charge le fichier `chronometer.js` et décommentez celle qui charge `chronometer-centiseconds.js`, comme ceci :

   ```html
   <!--  Iterations 1 - 8 -->
   <!-- <script src="src/chronometer.js"></script> -->

   <!-- Bonus Iteration 9: Centiseconds -->
   <script src="src/chronometer-centiseconds.js"></script>
   ```

<br>

**Bon codage !** :heart:

## FAQs

<br>

<details>
  <summary>Je suis bloqué dans l'exercice et je ne sais pas comment résoudre le problème ni par où commencer.</summary>
  <br>

Si vous êtes bloqué dans votre code et que vous ne savez pas comment résoudre le problème ou par où commencer, vous devriez prendre du recul et essayer de formuler une question claire sur le problème spécifique auquel vous êtes confronté. Cela vous aidera à cibler le problème et à développer des solutions potentielles.

Par exemple, s'agit-il d'un concept que vous ne comprenez pas, ou recevez-vous un message d'erreur que vous ne savez pas comment résoudre ? Il est généralement utile de tenter de formuler le problème le plus clairement possible, en incluant les messages d'erreur que vous recevez. Cela peut vous aider à communiquer le problème à d'autres personnes et éventuellement obtenir de l'aide de vos camarades de classe ou de ressources en ligne.

Une fois que vous avez une compréhension claire du problème, vous pourrez commencer à travailler vers la solution.

[Retour en haut](#faqs)

</details>

<details>
  <summary>Tous les tests Jasmine échouent et sont en rouge. Pourquoi cela s'est-il produit ?</summary>
  
  <br>
  
  Une raison possible pour laquelle tous les tests Jasmine échouent est qu'il y a une erreur de syntaxe dans le code testé. Si le code contient une erreur de syntaxe, il ne sera pas chargé correctement et aucun des tests ne pourra s'exécuter. Cela entraînera l'échec de tous les tests.

Pour résoudre ce problème, vous devrez examiner le code testé à la recherche d'erreurs de syntaxe. Recherchez des crochets manquants, des points-virgules ou d'autres problèmes de syntaxe qui pourraient causer le problème. Si vous trouvez une erreur de syntaxe, corrigez-la et réessayez d'exécuter les tests.

Une autre possibilité est qu'il y ait un problème avec les tests eux-mêmes. Il est possible que vous ayez modifié le fichier de test et causé un problème. Si vous avez apporté des modifications au fichier de test, essayez de copier et coller le fichier de test d'origine, puis exécutez à nouveau les tests pour voir si cela résout le problème.

[Retour en haut](#faqs)

</details>

<details>
  <summary>Comment utiliser <code>setTimeout()</code> et <code>clearTimeout()</code> ?</summary>
  <br>

`setTimeout()` est une fonction globale qui peut être utilisée pour exécuter une fonction de rappel après un délai spécifié.

  <br>

#### Syntaxe

```js
setTimeout(callback, delay);
```

- `callback` est la fonction qui sera exécutée après le délai spécifié.
- `delay` est le temps en millisecondes pendant lequel la fonction de rappel doit être retardée avant d'être exécutée.

  <br>

#### Utilisation de `setTimeout()`

Voici un exemple d'utilisation de `setTimeout()` pour afficher un message dans la console après un délai de 2000 millisecondes (2 secondes) :

```js
setTimeout(() => {
  console.log("Hi!");
}, 2000);
```

#### Annulation d'un délai avec `clearTimeout()`

Lorsqu'il est invoqué, `setTimeout()` renvoie un ID de minuterie qui peut être utilisé pour annuler l'exécution de la fonction de rappel à l'aide de la fonction `clearTimeout()` :

```js
const timerId = setTimeout(() => {
  console.log("Hi!");
}, 2000);

// Cancel the execution of the callback function
clearTimeout(timerId);
```

  <br>

[Retour en haut](#faqs)

</details>

<details>
  <summary>Comment utiliser <code>setInterval()</code> et <code>clearInterval()</code> ?</summary>
  <br>

`setInterval()` est une fonction globale qui peut être utilisée pour exécuter une fonction de rappel de manière répétée à un intervalle spécifié.

  <br>

#### Syntaxe

```js
setTimeout(callback, delay);
```

- `callback` est la fonction qui sera exécutée après le délai spécifié.
- `delay` est le temps en millisecondes pendant lequel la fonction de rappel doit être retardée avant d'être exécutée.

  <br>

#### Utilisation de `setInterval()`

Voici un exemple d'utilisation de `setInterval()` pour afficher un message dans la console après un délai de 2000 millisecondes (2 secondes) :

```js
setInterval(() => {
  console.log("Hello, world!");
}, 2000);
```

#### Annulation d'un intervalle avec `clearInterval()`

Lorsqu'il est invoqué, `setInterval()` renvoie un identifiant de minuterie qui peut être utilisé pour annuler l'exécution de la fonction de rappel à l'aide de la fonction `clearInterval()` :

```js
const timerId = setInterval(() => {
  console.log("Hello, world!");
}, 2000);

// Cancel the execution of the interval function after 10 seconds
setTimeout(() => {
  clearInterval(timerId);
}, 10000);
```

  <br>

[Retour en haut](#faqs)

</details>

<details>
   <summary>Quelle est la manière appropriée de passer une fonction de callback (rappel) en tant qu'argument et l'exécuter ?</summary>
  <br>

En JavaScript, vous pouvez passer une fonction de rappel en tant qu'argument à une autre fonction et l'exécuter en l'appelant à l'intérieur de la fonction externe.

  <br>

Voici un exemple de **passage d'une fonction de rappel en tant qu'argument d'une fonction** :

```js
function sayHello() {
  console.log("Hello!!!");
}

function outerFunction(callback) {
  console.log("Inside outerFunction");

  callback();
}

outerFunction(sayHello);
```

Dans cet exemple, la fonction `sayHello` est passée en tant que fonction de rappel à la fonction `outerFunction`. La fonction `outerFunction` appelle la fonction passée en utilisant son nom de paramètre `callback` en l'invoquant avec `callback()`. Lorsque vous exécutez le code, vous verrez les messages journaux des deux fonctions affichés dans la console.

  <br>

Voici un exemple de **passage d'une fonction de rappel en tant qu'argument d'une méthode** :

```js
class ExampleClass {
  constructor() {
    this.name = "ExampleClass";
  }

  myMethod(callback) {
    console.log("Inside myMethod");

    callback();
  }
}
```

  <br>

Voici un exemple de **passage d'une callback en tant qu'argument d'une méthode** :

```js
class ExampleClass {
  constructor() {
    this.name = "ExampleClass";
  }

  myMethod(callback) {
    console.log("Inside myMethod");

    if (callback) {
      // Check if the callback is passed before invoking it to prevent errors
      callback();
    }
  }
}
```

Dans cet exemple, la méthode `myMethod` prend une fonction de rappel en tant qu'argument. À l'intérieur de la méthode, elle vérifie d'abord si une fonction de rappel a réellement été passée en utilisant une instruction if. Si une fonction de rappel a été passée, la méthode l'invoque en appelant `callback()`.

Cette approche évite les erreurs si la fonction de rappel n'a pas été passée (si elle est `undefined`).

  <br>

[Retour en haut](#faqs)

</details>

<details>
  <summary>Je ne peux pas pousser les modifications vers le dépôt. Que dois-je faire ?</summary>
  <br>

There are a couple of possible reasons why you may be unable to _push_ changes to a Git repository:

1. **Vous n'avez pas validé vos modifications** : Avant de pouvoir pousser vos modifications vers le dépôt, vous devez les valider en utilisant la commande `git commit`. Assurez-vous d'avoir validé vos modifications et essayez de pousser à nouveau. Pour ce faire, exécutez les commandes terminal suivantes à partir du dossier du projet :

```bash
git add .
git commit -m "Your commit message"
git push
```

2. **Vous n'avez pas la permission de pousser vers le dépôt** : Si vous avez cloné le dépôt directement à partir du dépôt principal d'Ironhack sans faire d'abord une Fork, vous n'avez pas d'accès en écriture au dépôt.
   Pour vérifier à quel dépôt distant vous avez cloné, exécutez la commande terminal suivante à partir du dossier du projet :

```bash
git remote -v
```

Si le lien affiché est le même que le dépôt principal d'Ironhack, vous devrez d'abord effectuer un fork du dépôt vers votre compte GitHub, puis cloner votre fork sur votre machine locale pour pouvoir pousser les modifications.

**Note**: Vous devriez faire une copie de votre code local pour éviter de le perdre dans le processus.

[Retour en haut](#faqs)

</details>

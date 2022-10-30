# Le jargon de la programmation fonctionnelle

> Ce document est une traduction française de [hemanth/functional-programming-jargon](https://github.com/hemanth/functional-programming-jargon).

La programmation fonctionnelle (PF) offre de nombreux avantages et sa popularité n'a cessé d'augmenter en conséquence. Cependant, chaque paradigme de programmation défini son propre jargon et la PF ne fait pas exception. En fournissant un glossaire, nous espérons faciliter l'apprentissage de la PF.

Les exemples sont écrits en JavaScript (ES2015). [Pourquoi JavaScript ?](https://github.com/hemanth/functional-programming-jargon/wiki/Why-JavaScript%3F)

Lorsque cela est possible, ce document utilise les termes définis dans la [spécification Fantasy Land](https://github.com/fantasyland/fantasy-land).

__Traductions__
* [Portugaise](https://github.com/alexmoreno/jargoes-programacao-funcional)
* [Espagnole](https://github.com/idcmardelplata/functional-programming-jargon/tree/master)
* [Chinoise](https://github.com/shfshanyue/fp-jargon-zh)
* [Indonésienne](https://github.com/wisn/jargon-pemrograman-fungsional)
* [Anglaise (exemples en Python)](https://github.com/jmesyou/functional-programming-jargon.py)
* [Anglaise (exemples en Scala)](https://github.com/ikhoon/functional-programming-jargon.scala)
* [Anglaise (exemples en Rust)](https://github.com/JasonShin/functional-programming-jargon.rs)
* [Coréenne](https://github.com/sphilee/functional-programming-jargon)
* [Polonaise](https://github.com/Deloryn/functional-programming-jargon)
* [Turque (exemples en Haskell)](https://github.com/mrtkp9993/functional-programming-jargon)
* [Russe (exemples en Haskell)](https://github.com/epogrebnyak/functional-programming-jargon)
* [Anglaise (exemples en Julia)](https://github.com/Moelf/functional-programming-jargon.jl)

__Table des matières__
<!-- RM(noparent,notop) -->

* [Arité](#arité)
* [Fonction d'ordre supérieur](#fonction-dordre-supérieur)
* [Fermeture](#fermeture)
* [Application partielle](#application-partielle)
* [Curryfication](#curryfication)
* [Auto-curryfication](#auto-curryfication)
* [Composition de fonctions](#composition-de-fonctions)
* [Continuation](#continuation)
* [Fonction pure](#fonction-pure)
* [Effets de bord](#effets-de-bord)
* [Idempotence](#idempotence)
* [Programmation tacite (point-free style)](#programmation-tacite-point-free-style)
* [Prédicat](#prédicat)
* [Contrats](#contrats)
* [Catégorie](#catégorie)
* [Valeur](#valeur)
* [Constante](#constante)
  * [Fonction constante](#fonction-constante)
  * [Foncteur constant](#foncteur-constant)
  * [Monade constante](#monade-constante)
* [Foncteur](#foncteur)
* [Foncteur pointé](#foncteur-pointé)
* [Relèvement](#relèvement)
* [Transparence référentielle](#transparence-référentielle)
* [Raisonnement équationnel](#raisonnement-équationnel)
* [Lambda](#lambda)
* [Lambda-calcul](#lambda-calcul)
* [Combinateur fonctionnel](#combinateur-fonctionnel)
* [Évaluation paresseuse](#évaluation-paresseuse)
* [Monoïde](#monoïde)
* [Monade](#monade)
* [Comonade](#comonade)
* [Composition de Kleisi](#composition-de-kleisi)
* [Foncteur applicatif](#foncteur-applicatif)
* [Morphisme](#morphisme)
  * [Homomorphisme](#homomorphisme)
  * [Endomorphisme](#endomorphisme)
  * [Isomorphisme](#isomorphisme)
  * [Catamorphisme](#catamorphisme)
  * [Anamorphisme](#anamorphisme)
  * [Hylomorphisme](#hylomorphisme)
  * [Paramorphisme](#paramorphisme)
  * [Apomorphisme](#apomorphisme)
* [Setoïde](#setoïde)
* [Demi-groupe](#demi-groupe)
* [Foldable](#foldable)
* [Lentille](#lentille)
* [Signatures de type](#signatures-de-type)
* [Type algébrique de données](#type-algébrique-de-données)
  * [Types somme](#types-somme)
  * [Types produit](#types-produit)
* [Option](#option)
* [Fonction](#fonction)
* [Fonction partielle](#fonction-partielle)
  * [Manipuler des fonctions partielles](#manipuler-des-fonctions-partielles)
* [Fonction totale](#fonction-totale)
* [Functional Programming Libraries in JavaScript](#functional-programming-libraries-in-javascript)


<!-- /RM -->

## Arité

Le nombre d'arguments qu'une fonction requiert. On utilise aussi des mots comme unaire, binaire, ternaire, etc.

```js
const somme = (a, b) => a + b
// L'arité de somme est 2 (binaire)
const inc = a => a + 1
// L'arité de inc est 1 (unaire)
const zero = () => 0
// L'arité de zero est 0 (nullaires)
```

__Pour aller plus loin__

* [Arité](https://fr.wikipedia.org/wiki/Arit%C3%A9) sur Wikipédia

## Fonction d'ordre supérieur

Une fonction qui prend une fonction en argument et/ou qui renvoie une fonction.

```js
const filtre = (predicat, xs) => xs.filter(predicat)
```

```js
const est = (type) => (x) => Object(x) instanceof type
```

```js
filtre(est(Number), [0, '1', 2, null]) // [0, 2]
```

## Fermeture

Une fermeture (closure en anglais) est une fonction accompagnée de l'ensemble des variables locales qu'elle a capturées au moment où elle a été définie.
Ces variables restent alors accessibles même après que le programme soit sorti du bloc où elles ont été définies.

```js
const ajouterA = x => y => x + y
const ajouterACinq = ajouterA(5)
ajouterACinq(3) // => 8
```

Dans ce cas, `x` a été capturée par la fermeture `ajouterACinq` avec la valeur `5`. `ajouterACinq` peut alors être
appelée avec `y` pour retourner la somme.

__Pour aller plus loin / Sources__
* [Closures (Fermetures)](https://developer.mozilla.org/fr/docs/Web/JavaScript/Closures)
* [Lambda Vs Closure (en)](http://stackoverflow.com/questions/220658/what-is-the-difference-between-a-closure-and-a-lambda)
* [JavaScript Closures highly voted discussion (en)](http://stackoverflow.com/questions/111102/how-do-javascript-closures-work)

## Application partielle

Appliquer partiellement une fonction signifie créer une nouvelle fonction en préremplissant certains des arguments de la fonction originale.

```js
// Permet de créer des fonctions appliquées partiellement
// Prend en paramètre une fonction et des arguments
const appliquerPartiellement = (f, ...args) =>
  // retourne une function qui prend en paramètre le reste des arguments
  (...resteDesArgs) =>
    // et appelle la fonction originale avec tous les arguments
    f(...args, ...resteDesArgs)

// une fonction à appliquer partiellement
const ajouter3 = (a, b, c) => a + b + c

// Applique partiellement `2` et `3` à `ajouter3` produit une fonction à un argument
const cinqPlus = appliquerPartiellement(ajouter3, 2, 3) // (c) => 2 + 3 + c

cinqPlus(4) // 9
```

Vous pouvez aussi utiliser `Function.prototype.bind` pour appliquer partiellement une fonction en JavaScript :

```js
const cinqPlus = ajouter3.bind(null, 2, 3) // (c) => 2 + 3 + c
```

L'application partielle permet de créer des fonctions plus simples à partir de fonctions plus complexes en y intégrant les données au fur et à mesure où elles sont disponibles. Les fonctions [curryfiées](#curryfication) sont automatiquement partiellement appliquées.


## Curryfication

Processus de conversion d'une fonction qui prend plusieurs arguments en une fonction qui les prend un à la fois.

Chaque fois que la fonction est appelée, elle n'accepte qu'un seul argument et retourne une fonction qui prend un argument jusqu'à ce que tous les arguments soient passés.

```js
const somme = (a, b) => a + b

const sommeCurryfiee = (a) => (b) => a + b

sommeCurryfiee(40)(2) // 42.

const ajouter2 = sommeCurryfiee(2) // (b) => 2 + b

ajouter2(10) // 12
```

## Auto-curryfication

La transformation d'une fonction qui prend plusieurs arguments en une fonction qui, si on lui donne moins que son nombre correct d'arguments, renvoie une fonction qui prend le reste des arguments. Lorsque la fonction est appelée avec le nombre correct d'arguments, elle est ensuite évaluée. 

Lodash et Ramda ont une fonction `curry` qui marche comme suit.

```js
const somme = (x, y) => x + y

const sommeCurryfiee = _.curry(somme)
sommeCurryfiee(1, 2) // 3
sommeCurryfiee(1) // (y) => 1 + y
sommeCurryfiee(1)(2) // 3
```

__Pour aller plus loin__
* [Favoring Curry (en)](http://fr.umio.us/favoring-curry/)
* [Hey Underscore, You're Doing It Wrong! (en)](https://www.youtube.com/watch?v=m3svKOdZijA)

## Composition de fonctions

L'acte de mettre deux fonctions ensemble pour en former une troisième, où la sortie d'une fonction est l'entrée de l'autre. C'est l'une des idées les plus importantes de la programmation fonctionnelle.

```js
const composer = (f, g) => (a) => f(g(a)) // Définition
const floorEtToString = composer((val) => val.toString(), Math.floor) // Utilisation
floorEtToString(121.212121) // '121'
```

## Continuation

À tout moment d'un programme, la partie du code qui n'a pas encore été exécutée est appelée _continuation_.

```js
const afficher = (nombre) => console.log(`Nombre ${nombre}`)

const ajouterUnEtContinuer = (nombre, cc) => {
  const resultat = nombre + 1
  cc(resultat)
}

ajouterUnEtContinuer(2, afficher) // 'Nombre 3'
```

Les continuations sont souvent observées en programmation asynchrone lorsque le programme doit attendre de recevoir des données avant de pouvoir continuer à s'exécuter. La réponse est souvent transmise au reste du programme, qui est la continuation, une fois qu'elle a été reçue.

```js
const poursuivreLeProgrammeAvec = (donnees) => {
  // Poursuit le programme avec les données
}

lireFichierAsync('chemin/vers/fichier', (err, reponse) => {
  if (err) {
    // prend en charge l'erreur
    return
  }
  poursuivreLeProgrammeAvec(reponse)
})
```

## Fonction pure

Une fonction est pure si sa valeur de retour n'est déterminée que par ses valeurs d'entrée, et qu'elle ne produit pas d'effets secondaires. La fonction doit toujours renvoyer le même résultat lorsqu'elle reçoit les mêmes entrées.

```js
const saluer = (nom) => `Salut, ${nom}`

saluer('Brianne') // 'Salut, Brianne'
```

Contrairement à chacun des exemples suivants :

```js
window.name = 'Brianne'

const saluer = () => `Salut, ${window.name}`

saluer() // "Salut, Brianne"
```

La sortie de l'exemple ci-dessus dépend de données stockées en dehors de la fonction...

```js
let salutation

const saluer = (nom) => {
  salutation = `Salut, ${nom}`
}

saluer('Brianne')
salutation // "Salut, Brianne"
```

... et celui-ci modifie l'état en dehors de la fonction.

## Effets de bord

Une fonction ou une expression est dite à effet de bord si, en plus de renvoyer une valeur, elle interagit (lit ou écrit) avec son environnement externe et que ce dernier est mutable.

```js
const differentAChaqueFois = new Date()
```

```js
console.log('Les entrées-sorties sont un effet de bord !')
```

## Idempotence

Une fonction est idempotente si, quand on l'applique à nouveau à son résultat, elle ne produit pas un résultat différent.

```js
Math.abs(Math.abs(10))
```

```js
sort(sort(sort([2, 1])))
```

## Programmation tacite (point-free style)

La programmation tacite, aussi connu sous le nom de _point-free style_, est une manière d'écrire une fonction en n'identifiant pas explicitement les arguments utilisés. Ce style de programmation requiert généralement les notions de [curryfication](#curryfication) ou de [fonctions d'ordre supérieur](#fonction-dordre-supérieur).

```js
// Étant donné
const map = (fn) => (liste) => liste.map(fn)
const ajouter = (a) => (b) => a + b

// Alors

// Sans la programmation tacite - `nombres` est un argument explicite
const incrementerTout = (nombres) => map(ajouter(1))(nombres)

// Avec la programmation tacite - La liste est un argument implicite
const incrementerTout2 = map(ajouter(1))
```

Les définitions de fonctions _point-free_ ressemblent à des affectations normales sans `function` ou `=>`. Il convient de mentionner que les fonctions _point-free_ ne sont pas nécessairement meilleures que leurs homologues non-_point-free_, car elles peuvent être plus difficiles à comprendre lorsqu'elles sont complexes.

## Prédicat

Un prédicat est une fonction qui retourne vrai ou faux pour une valeur donnée. Une utilisation courante d'un prédicat est la fonction utilisée pour filtrer un tableau.

```js
const predicat = (a) => a > 2

[1, 2, 3, 4].filter(predicat) // [3, 4]
```

## Contrats

Un contrat spécifie les obligations et les garanties de comportement qu'une fonction ou une expression doit respecter lors de son exécution. C'est un ensemble de règles qui s'appliquent aux entrées et sorties d'une fonction ou d'une expression. Des erreurs sont levées quand le contrat n'est pas respecté.

```js
// Definie le contrat : int -> boolean
const contrat = (entree) => {
  if (typeof entree === 'number') return true
  throw new Error('Contrat non respecté : attendu int -> boolean')
}

const ajouterUn = (nombre) => contrat(nombre) && nombre + 1

ajouterUn(2) // 3
ajouterUn('une chaine') // Contrat non respecté : attendu int -> boolean
```

## Catégorie

Une catégorie, dans la théorie des catégories, est un ensemble composé d'objets et des morphismes entre eux.
En programmation, les types représentent généralement les objets et les fonctions représentent les morphismes.

Pour qu'une catégorie soit valide, trois règles doivent être respectées :

1. Un morphisme d'identité, qui mappe un objet à lui-même, doit exister.
    Si `a` est un objet d'une catégorie,
    alors il doit y avoir une fonction de `a -> a`.
2. Les morphismes doivent pouvoir être composés.
    Si `a`, `b`, and `c` sont des objets d'une catégorie,
    `f` est un morphisme de `a -> b` et `g` est un morphisme de `b -> c`,
    alors `g(f(x))` doit être équivalent à `(g • f)(x)`.
3. La composition doit être associative.
    `f • (g • h)` est équivalent à `(f • g) • h`

Puisque ces règles régissent la composition à un niveau très abstrait, la théorie des catégories est excellente pour découvrir de nouvelles façons de composer des choses.

À titre d'exemple, nous pouvons définir une catégorie Max en tant que classe
```js

class Max {
  constructor (a) {
    this.a = a
  }

  id () {
    return this
  }

  compose (b) {
    return this.a > b.a ? this : b
  }

  toString () {
    return `Max(${this.a})`
  }
}

new Max(2).compose(new Max(3)).compose(new Max(5)).id().id() // => Max(5)
```

__Pour aller plus loin__

* [Théorie des catégories](https://fr.wikipedia.org/wiki/Th%C3%A9orie_des_cat%C3%A9gories) sur Wikipédia
* [Category Theory for Programmers (en)](https://bartoszmilewski.com/2014/10/28/category-theory-for-programmers-the-preface/)

## Valeur

Tout ce qui peut être assigné à une variable.

```js
5
Object.freeze({ nom: 'John', age: 30 }) // La fonction `freeze` renforce l'immutabilité.
;(a) => a
;[1]
undefined
```

## Constante

Une variable qui ne peut pas être réaffectée une fois définie.

```js
const five = 5
const john = Object.freeze({ name: 'John', age: 30 })
```

Les constantes sont [référentiellement transparentes](#transparence-référentielle). Cela veut dire qu'une constante peut être remplacée par la valeur qu'elle représente sans que le résultat soit modifié.

Avec les deux constantes ci-dessus, l'expression suivante renverra toujours `true`.

```js
john.age + five === ({ name: 'John', age: 30 }).age + 5
```

### Fonction constante

Une fonction [curryfiée](#curryfication) qui ignore son deuxième argument :

```js
const constante = a => () => a

;[1, 2].map(constante(0)) // => [0, 0]
```

### Foncteur constant

Un object dont la fonction `map` ne transforme pas le contenu. Voir [Foncteur](#foncteur).

```js
Constante(1).map(n => n + 1) // => Constante(1)
```

### Monade constante

Un object dont la fonction `chain` ne transforme pas le contenu. Voir [Monade](#monade).

```js
Constante(1).chain(n => Constante(n + 1)) // => Constante(1)
```

## Foncteur

Un objet qui implémente une fonction `map` qui prend en paramètre une fonction qui sera exécutée sur son contenu. Un foncteur doit respecter deux règles :

__Préserver l'identité__

```js
objet.map(x => x)
``` 

équivaut à `objet`. 


__Être composable__

```js
objet.map(x => g(f(x)))
```

équivaut à

```js
objet.map(f).map(g)
```

(où `f`, `g` sont des fonctions composables arbitraires).

L'implémentation de référence d'[Option](#option) est un foncteur car il satisfait ces deux règles :

```js
some(1).map(x => x) // = some(1)
```

and

```js
const f = x => x + 1
const g = x => x * 2

some(1).map(x => g(f(x))) // = some(3)
some(1).map(f).map(g) // = some(3)
```

## Foncteur pointé

Un objet avec une fonction `of` qui stocke _n'importe_ quelle valeur.

ES2015 a ajouté `Array.of`, transformant ainsi les tableaux en foncteur pointé.

```js
Array.of(1) // [1]
```

## Relèvement

Le relèvement est l'action de prendre une valeur et de la mettre dans un objet tel qu'un [foncteur](#foncteur-pointé). Si vous relevez une fonction dans un [foncteur applicatif](#foncteur-applicatif), vous pouvez l'appliquer aux valeurs qui se trouvent également dans ce foncteur.

Certaines implémentations ont une fonction appelée `lift` ou `liftA2` pour faciliter l'exécution de fonctions sur des foncteurs.

```js
const liftA2 = (f) => (a, b) => a.map(f).ap(b) // note: c'est bien `ap` et non `map`.

const mult = a => b => a * b

const multRelevé = liftA2(mult) // cette nouvelle fonction s'appliquer à des foncteurs comme array

multRelevé([1, 2], [3]) // [3, 6]
liftA2(a => b => a + b)([1, 2], [3, 4]) // [4, 5, 5, 6]
```

Relever une fonction à un argument et l'appliquer fait la même chose que `map`.

```js
const incrementer = (x) => x + 1

lift(incrementer)([2]) // [3]
;[2].map(incrementer) // [3]
```

Relever de simples valeurs peut consister à créer uniquement l'objet.

```js
Array.of(1) // => [1]
```

## Transparence référentielle

Une expression qui peut être remplacée par sa valeur sans changer le
comportement du programme est dite référentiellement transparente.

Étant donné la fonction `saluer`:

```js
const saluer = () => 'Bonjour le monde !'
```

Toute invocation de `saluer()` peut être remplacée par `Bonjour le monde !`, donc `saluer` est
référentiellement transparente. Cela ne serait pas le cas si `saluer` dépendait d'un état externe
comme de la configuration ou un appel à une base de données. Voir aussi [Fonction pure](#fonction-pure) et
[Raisonnement équationnel](#raisonnement-équationnel).

## Raisonnement équationnel

Lorsqu'une application est composée d'expressions et dépourvue d'effets secondaires,
des affirmations peuvent être déduites de ses parties. Vous pouvez également être sûr
des détails de votre programme sans avoir à parcourir toutes les fonctions.

```js
const grainesDansChiens = compose(pouletsDansChiens, grainesDansPoulets)
const grainesDansChats = compose(chiensDansChats, grainesDansChiens)
```

Dans l'exemple ci-dessus, si vous savez que `pouletsDansChiens` et `grainesDansPoulets` sont [pures](#fonction-pure),
alors vous savez que la composition est également pure. Les choses peuvent être poussées un peu plus loin lorsque l'on
en sait plus sur les fonctions (associativité, commutativité, idempotence, etc...).

## Lambda

Une fonction anonyme qui peut être traitée comme une valeur.

```js
;(function (a) {
  return a + 1
})

;(a) => a + 1
```

Les lambdas sont souvent utilisées en tant qu'arguments de fonctions d'ordre supérieur.

```js
;[1, 2].map((a) => a + 1) // [2, 3]
```

Une lambda peut être affectée à une variable :

```js
const ajouter1 = (a) => a + 1
```

## Lambda-calcul

Une branche des mathématiques qui utilise les fonctions pour créer un [modèle universel de calcul](https://fr.wikipedia.org/wiki/Lambda-calcul).

## Combinateur fonctionnel

Une fonction d'ordre supérieur, généralement curryfiée, qui renvoie une nouvelle fonction modifiée d'une manière ou d'une autre. Les combinateurs fonctionnels sont souvent utilisés en [programmation tacite](#programmation-tacite-point-free-style) pour écrire des programmes particulièrement concis.

```js
// Le combinateur "C" prend une fonction curryfiée à deux arguments et en renvoie une nouvelle qui appelle la fonction d'origine avec les arguments inversés.
const C = (f) => (a) => (b) => f(b)(a)

const diviser = (a) => (b) => a / b

const diviserPar = C(diviser)

const diviserPar10 = diviserPar(10)

diviserPar10(30) // => 3
```

Voir aussi [List of Functional Combinators in JavaScript (en)](https://gist.github.com/Avaq/1f0636ec5c8d6aed2e45) qui donne aussi des liens vers plus de références.

## Évaluation paresseuse

L'évaluation paresseuse est un mécanisme qui retarde l'évaluation d'une expression jusqu'à ce que sa valeur soit nécessaire. Dans les langages fonctionnels, cela permet des structures telles que les listes infinies, qui ne seraient normalement pas disponibles dans un langage impératif où l'enchaînement des commandes est important.

```js
const rand = function * () {
  while (1 < 2) {
    yield Math.random()
  }
}
```

```js
const randIter = rand()
randIter.next() // Chaque exécution donne une valeur aléatoire, l'expression est évaluée au besoin.
```

## Monoïde

Un objet avec une fonction qui « combine » cet objet avec un autre du même type ([demi-groupe](#demi-groupe)) qui a de plus une valeur neutre.

Un exemple de monoïde simple est l'addition de nombres :

```js
1 + 1 // 2
```

Dans ce cas, le nombre est l'objet et `+` est la fonction.

Lorsqu'une valeur est combinée avec la valeur neutre, le résultat doit être la valeur d'origine. La fonction doit également être commutative dans ce cas.

La valeur neutre pour l'addition est `0` :

```js
1 + 0 // 1
0 + 1 // 1
1 + 0 === 0 + 1
```

Il est également nécessaire que le regroupement des opérations n'influe pas sur le résultat (associativité) :

```js
1 + (2 + 3) === (1 + 2) + 3 // true
```

La concaténation de tableaux forme également un monoïde :

```js
;[1, 2].concat([3, 4]) // [1, 2, 3, 4]
```

La valeur neutre est alors un tableau vide `[]` :

```js
;[1, 2].concat([]) // [1, 2]
```

À titre de contre-exemple, la soustraction ne forme pas de monoïde car il n'y a pas de valeur neutre commutative :

```js
0 - 4 === 4 - 0 // false
```

## Monade

Une monade est un objet avec les fonctions [`of`](#foncteur-pointé) et `chain`. `chain` est comme [`map`](#foncteur) sauf qu'il désimbrique les objets imbriqués résultants.

```js
// Implémentation
Array.prototype.chain = function (f) {
  return this.reduce((acc, it) => acc.concat(f(it)), [])
}

// Utilisation
Array.of('chat,chien', 'poisson,oiseau').chain((a) => a.split(',')) // ['chat', 'chien', 'poisson', 'oiseau']

// Contraste avec map
Array.of('chat,chien', 'poisson,oiseau').map((a) => a.split(',')) // [['chat', 'chien'], ['poisson', 'oiseau']]
```

`of` est également connu sous le nom de `return` dans d'autres langages fonctionnels.
`chain` est par ailleurs connu sous le nom de `flatmap` ou `bind` dans d'autres langages.

## Comonade

Un objet qui a les fonctions `extract` et `extend`.

```js
const CoIdentité = (v) => ({
  val: v,
  extract () {
    return this.val
  },
  extend (f) {
    return CoIdentité(f(this))
  }
})
```

`extract` extrait une valeur d'un foncteur :

```js
CoIdentité(1).extract() // 1
```

`extend` exécute une fonction sur la comonade. La fonction doit renvoyer le même type que la comonade :

```js
CoIdentité(1).extend((co) => co.extract() + 1) // CoIdentité(2)
```

## Composition de Kleisi

Une opération pour composer deux fonctions qui retournent des [monades](#monade) (flèches de Kleisli) quand elles ont des types compatibles. En Haskell, il s'agit de l'opérateur `>=>`.

En utilisant [Option](#option) :

```js
// safeParseNum :: String -> Option Number
const safeParseNum = (b) => {
  const n = parseNumber(b)
  return isNaN(n) ? none() : some(n)
}

// validatePositive :: Number -> Option Number
const validatePositive = (a) => a > 0 ? some(a) : none()

// kleisliCompose :: Monad M => ((b -> M c), (a -> M b)) -> a -> M c
const kleisliCompose = (g, f) => (x) => f(x).chain(g)

// parseAndValidate :: String -> Option Number
const parseAndValidate = kleisliCompose(validatePositive, safeParseNum)

parseAndValidate('1') // => Some(1)
parseAndValidate('asdf') // => None
parseAndValidate('999') // => None
```

Ceci fonctionne car :

 * [Option](#option) est une [monade](#monade)
 * `validatePositive` et `safeParseNum` renvoient le même type de monade (Option).
 * Le type d'argument de `validatePositive` correspond au retour non encapsulé de `safeParseNum`.

## Foncteur applicatif

Un foncteur applicatif est un objet avec une fonction `ap`. `ap` applique une fonction de l'objet à une valeur d'un autre objet du même type.

```js
// Implémentation
Array.prototype.ap = function (xs) {
  return this.reduce((acc, f) => acc.concat(xs.map(f)), [])
}

// Exemple d'utilisation
;[(a) => a + 1].ap([1]) // [2]
```

C'est utile quand vous avez deux objets et que vous souhaitez appliquer une fonction binaire à leurs contenus.

```js
// Tableaux que vous souhaitez fusionner
const arg1 = [1, 3]
const arg2 = [4, 5]

// fonction de fusion - doit être curryfiée pour que cela fonctionne
const ajouter = (x) => (y) => x + y

const ajoutsPartiels = [ajouter].ap(arg1) // [(y) => 1 + y, (y) => 3 + y]
```

Cela vous donne un tableau de fonctions sur lequel vous pouvez appeler `ap` pour obtenir le résultat final :

```js
ajoutsPartiels.ap(arg2) // [5, 6, 7, 8]
```

## Morphisme

Une relation entre des objets au sein d'une [catégorie](#catégorie). En programmation fonctionnelle, toutes les fonctions sont des morphismes.

### Homomorphisme

Une fonction où l'entrée et la sortie partagent une même propriété structurelle.

Par exemple, dans un homomorphisme [monoïde](#monoïde), l'entrée et la sortie sont des monoïdes même si leurs types sont différents.

```js
// convertir :: [number] -> string
const convertir = (a) => a.join(', ')
```

`convertir` est un homomorphisme car :
* array est un monoïde - il possède une opération `concat` et une valeur neutre (`[]`),
* string est un monoïde - il possède une opération `concat` et une valeur neutre (`''`).

Ainsi, un homomorphisme se rapporte à la propriété qui vous intéresse dans l'entrée et la sortie d'une fonction de transformation.

Les [endomorphismes](#endomorphisme) et les [isomorphismes](#isomorphisme) sont des exemples d'homomorphisme.

__Pour aller plus loin__ 
* [Homomorphism | Learning Functional Programming in Go (en)](https://subscription.packtpub.com/book/application-development/9781787281394/11/ch11lvl1sec90/homomorphism#:~:text=A%20homomorphism%20is%20a%20correspondence,pointing%20to%20it%20from%20A.)

### Endomorphisme

Une fonction où le type de l'entrée est identique à celui de sortie.

```js
// majuscule :: String -> String
const enMajuscule = (str) => str.toUpperCase()

// decrementer :: Number -> Number
const decrementer = (x) => x - 1
```

### Isomorphisme

Un morphisme pour lequel il existe un morphisme inverse. Ce type de morphismes préserve la structure des objets.

Par exemple, des coordonnées 2D peuvent être stockées sous forme de tableau (`[2,3]`) ou d'objet (`{x: 2, y: 3}`).

```js
// Fonctions de conversions
const paireVersCoords = (paire) => ({ x: paire[0], y: paire[1] })
const coordsVersPaire = (coords) => [coords.x, coords.y]

coordsVersPaire(paireVersCoords([1, 2])) // [1, 2]
paireVersCoords(coordsVersPaire({ x: 1, y: 2 })) // {x: 1, y: 2}
```

Les isomorphismes sont aussi des [homomorphismes](#homomorphisme) puisque les types d'entrée et de sortie sont réversibles.

### Catamorphisme

Une fonction qui déconstruit une structure en une seule valeur. `reduceRight` est un exemple de catamorphisme pour les structures de type tableau.

```js
// somme est un catamorphisme de [Number] -> Number
const somme = xs => xs.reduceRight((acc, x) => acc + x, 0)

somme([1, 2, 3, 4, 5]) // 15
```

### Anamorphisme

Une fonction qui construit une structure en appliquant de manière répétée une autre fonction à son argument. `unfold` est un exemple qui génère un tableau par à partir d'une fonction et d'une valeur initiale. C'est le contraire d'un [catamorphisme](#catamorphisme) : un anamorphisme construit une structure et le catamorphisme la décompose.

```js
const deplier = (f, valeurInitiale) => {
  function appliquer (f, valeurInitiale, acc) {
    const res = f(valeurInitiale)
    return res ? appliquer(f, res[1], acc.concat([res[0]])) : acc
  }
  return appliquer(f, valeurInitiale, [])
}
```

```js
const compteARebour = n => deplier((n) => {
  return n <= 0 ? undefined : [n, n - 1]
}, n)

compteARebour(5) // [5, 4, 3, 2, 1]
```

### Hylomorphisme

Une fonction récursive composée d'un [anamorphisme](#anamorphisme) suivi d'un [catamorphisme](#catamorphisme).

```js
const sommeJusquaX = (x) => somme(compteARebour(x))
sommeJusquaX(5) // 15
```

### Paramorphisme

Une fonction similaire `reduceRight`, bien qu'il y ait une différence :

Dans un paramorphisme, les arguments de votre réducteur sont la valeur actuelle, la réduction de toutes les valeurs précédentes et la liste des valeurs qui ont formé cette réduction.

```js
// Dangereux avec des listes contenant `undefined`,
// mais suffisant pour notre exemple.
const paramorphisme = (reducteur, accumulateur, elements) => {
  if (elements.length === 0) { return accumulateur }

  const premierElement = elements[0]
  const autresElements = elements.slice(1)

  return reducteur(premierElement, autresElements, paramorphisme(reducteur, accumulateur, autresElements))
}

const suffixes = liste => paramorphisme(
  (x, xs, suffxs) => [xs, ...suffxs],
  [],
  liste
)

suffixes([1, 2, 3, 4, 5]) // [[2, 3, 4, 5], [3, 4, 5], [4, 5], [5], []]
```

Le troisième paramètre du réducteur (dans l'exemple ci-dessus, `[x, ... xs]`) donne une sorte d'historique de ce qui à conduit à la valeur `accumulateur` actuelle.

### Apomorphisme

Le contraire du paramorphisme, tout comme l'anamorphisme est le contraire du catamorphisme. Avec le paramorphisme, l'accès à l'accumulateur et à ce qui a été accumulé sont conservés. L'apomorphisme permet de _déplier (`unfold`)_ et laisse la possibilité de retourner une valeur plus tôt.

## Setoïde

Un objet qui a une fonction `equals` qui peut être utilisée pour le comparer à d'autres objets du même type.

Pour faire de `array` un setoïde :

```js
Array.prototype.equals = function (arr) {
  const taille = this.length
  if (taille !== arr.length) {
    return false
  }
  for (let i = 0; i < taille; i++) {
    if (this[i] !== arr[i]) {
      return false
    }
  }
  return true
}

;[1, 2].equals([1, 2]) // true
;[1, 2].equals([0]) // false
```

## Demi-groupe

Un demi-groupe (aussi appelé semi-groupe), est un objet doté d'une fonction `concat` qui permet de le combiner avec un autre objet du même type.

```js
;[1].concat([2]) // [1, 2]
```

## Foldable

Un objet doté d'une fonction `reduce` qui applique une fonction à un accumulateur et à chaque élément du tableau (de gauche à droite) pour le réduire à une seule valeur.

```js
const somme = (liste) => liste.reduce((acc, val) => acc + val, 0)
somme([1, 2, 3]) // 6
```

## Lentille

Une lentille (lens en anglais) est une structure (souvent un objet ou une fonction) qui associe un _getter_ et un
_setter_ non mutable et est utilisé sur d'autres structures.

```js
// En utilisant les [lentilles de Ramda (en)](http://ramdajs.com/docs/#lens)
const lentilleSurLeNom = R.lens(
  // getter pour la propriété nom
  (obj) => obj.nom,
  // setter pour la propriété nom
  (val, obj) => Object.assign({}, obj, { nom: val })
)
```

Le fait d'avoir des accesseurs pour une structure donnée permet quelques fonctionnalités clés.

```js
const personne = { nom: 'Gertrude Blanch' }

// utilisation du getter
R.view(lentilleNom, personne) // 'Gertrude Blanch'

// utilisation du setter
R.set(lentilleNom, 'Shafi Goldwasser', personne) // {nom: 'Shafi Goldwasser'}

// applique la fonction `majuscule` sur la valeur de la structure
R.over(lentilleNom, majuscule, personne) // {nom: 'GERTRUDE BLANCH'}
```

Les lenses sont aussi composable. Cela permet d'effectuer facilement des mises à jour de données profondément imbriquées.

```js
// Cette lentille se concentre sur le premier élément d'un tableau non vide
const lentillePremierElement = R.lens(
  // getter sur le premier élément du tableau
  xs => xs[0],
  // setter non mutable du premier élément du tableau
  (val, [__, ...xs]) => [val, ...xs]
)

const personnes = [{ nom: 'Gertrude Blanch' }, { nom: 'Shafi Goldwasser' }]

// Malgré ce que vous pourriez supposer, les lens se composent de gauche à droite.
R.over(compose(lentillePremierElement, lentilleNom), majuscule, personnes) // [{'nom': 'GERTRUDE BLANCH'}, {'nom': 'Shafi Goldwasser'}]
```

Autres implémentations :
* [partial.lenses (en)](https://github.com/calmm-js/partial.lenses)
* [nanoscope (en)](http://www.kovach.me/nanoscope/)

## Signatures de type

Souvent, les fonctions en JavaScript incluent des commentaires qui indiquent les types de leurs arguments et les valeurs de retour.

Les pratiques varient beaucoup au sein de la communauté, mais ils suivent souvent les modèles suivants :

```js
// nomFonction :: premierType -> secondType -> typeDeRetour

// ajouter :: Number -> Number -> Number
const ajouter = (x) => (y) => x + y

// incrementer :: Number -> Number
const incrementer = (x) => x + 1
```

Si une fonction accepte une autre fonction comme argument, elle est placée entre parenthèses :

```js
// appeler :: (a -> b) -> a -> b
const appeler = (f) => (x) => f(x)
```

Les lettres `a`, `b`, `c`, `d` sont utilisée pour signifier que l'argument peut être de n'importe quel type. La version suivante de `map` prend une fonction qui transforme une valeur d'un type `a` en un autre type `b`, un tableau de valeurs de type `a`, et retourne un tableau de valeurs de type `b`.

```js
// map :: (a -> b) -> [a] -> [b]
const map = (f) => (liste) => liste.map(f)
```

__Pour aller plus loin__
* [Ramda's type signatures (en)](https://github.com/ramda/ramda/wiki/Type-Signatures)
* [Mostly Adequate Guide (en)](https://drboolean.gitbooks.io/mostly-adequate-guide/content/ch7.html#whats-your-type)
* [What is Hindley-Milner? (en)](http://stackoverflow.com/a/399392/22425) sur Stack Overflow

## Type algébrique de données

Un type composite fabriqué à partir de l'assemblage d'autres types. Deux classes communes de types algébriques sont les [sommes](#types-somme) et les [produits](#types-produit).

### Types somme

Un type somme est l'union de deux types l'un avec l'autre. On l'appelle ainsi car le nombre de valeurs possibles dans le type résultant est la somme des types d'entrée.

JavaScript n'a pas de types somme, mais on peut néanmoins utiliser les `Set`s le simuler :

```js
// Imaginez que plutôt que des ensembles ici, nous avons des types qui ne peuvent prendre que ces valeurs.
const bools = new Set([true, false])
const halfTrue = new Set(['half-true'])

// Le type LogiqueFaible contient la somme des valeurs de bools et halfTrue
const valeursDeLogiqueFaible = new Set([...bools, ...halfTrue])
```

Les types somme sont parfois appelés _types union_, _unions discriminées_ ou _unions étiquetées_.

Il existe [plusieurs](https://github.com/paldepind/union-type) [bibliothèques](https://github.com/puffnfresh/daggy) en JavaScript qui facilitent la définition et l'utilisation des types somme.

Flow défini [des types union](https://flow.org/en/docs/types/unions/) et TypeScript [des énumérations](https://www.typescriptlang.org/docs/handbook/enums.html) pour jouer ce rôle.

### Types produit

Un type produit combine des types d'une manière que vous connaissez probablement mieux :

```js
// point :: (Number, Number) -> {x: Number, y: Number}
const point = (x, y) => ({ x, y })
```

L'exemple précédent est ce qu'on appelle un produit car l'ensemble des valeurs possibles de la structure de données est le produit des différentes valeurs. De nombreux languages ont un type tuple qui est la formulation la plus simple d'un type produit.

__Pour aller plus loin__
* [Théorie des ensembles](https://fr.wikipedia.org/wiki/Th%C3%A9orie_des_ensembles) sur Wikipédia

## Option

L'option est un [type somme](#types-somme) qui encapsule deux cas souvent appelés `Some` et `None`.

Les options sont utiles avec des fonctions qui peuvent ne pas renvoyer de valeur.

```js
// Définition naïve

const Some = (v) => ({
  val: v,
  map (f) {
    return Some(f(this.val))
  },
  chain (f) {
    return f(this.val)
  }
})

const None = () => ({
  map (f) {
    return this
  },
  chain (f) {
    return this
  }
})

// optionnel :: (String, {a}) -> Option a
const optionnel = (key, obj) => typeof obj[key] === 'undefined' ? None() : Some(obj[key])
```

Utilisez `chain` pour enchaîner des fonctions qui retournent des `Option`s:

```js

// getArticle :: Panier -> Option Article
const getArticle = (panier) => optionnel('article', panier)

// getPrix :: Article -> Option Number
const getPrix = (article) => optionnel('prix', article)

// getPrixImbrique :: cart -> Option a
const getPrixImbrique = (panier) => getArticle(panier).chain(getPrix)

getPrixImbrique({}) // None()
getPrixImbrique({ item: { foo: 1 } }) // None()
getPrixImbrique({ item: { price: 9.99 } }) // Some(9.99)
```

`Option` est aussi connu sous le nom `Maybe`. `Some` est parfois appelé `Just`. `None` est parfois appelé `Nothing`.

## Fonction

En programmation fonctionnelle, une fonction (ou expression lambda) `f :: A => B` est une expression avec un seul argument immuable de type `A`et une seule valeur de retour de type `B`. La valeur de retour dépend entièrement de l'argument, ce qui rend la fonction [référentiellement transparente](#transparence-référentielle). Cela implique donc que la fonction ne produit aucun [effet de bord](#effets-de-bord) caché. Une fonction est donc [pure](#fonction-pure) par définition. Ces propriétés rendent les fonctions agréables à manipuler : elles sont complètement déterministes et ainsi prévisibles. Les fonctions permettent d'utiliser le code comme des données, en faisant abstraction du comportement :

```js
// fois2 :: Number -> Number
const fois2 = n => n * 2

;[1, 2, 3].map(fois2) // [2, 4, 6]
```

## Fonction partielle

Une fonction partielle est une [function](#fonction) qui n'est pas définie pour tous les arguments - elle peut renvoyer un résultat inattendu ou ne jamais se terminer. Les fonctions partielles ajoutent de la surcharge cognitive, elles sont plus difficiles à appréhender et peuvent entraîner des erreurs d'exécution.

```js
// exemple 1 : somme d'une liste
// somme :: [Number] -> Number
const somme = nombres => nombres.reduce((a, b) => a + b)
somme([1, 2, 3]) // 6
sum([]) // TypeError: Reduce of empty array with no initial value

// exemple 2 : récupération du premier élément d'une liste
// premier :: [A] -> A
const premier = a => a[0]
premier([42]) // 42
premier([]) // undefined
// ou pire
premier([[42]])[0] // 42
premier([])[0] // Uncaught TypeError: Cannot read property '0' of undefined

// exemple 3 : repéter une fonction N fois
// repeter :: Number -> (Number -> Number) -> Number
const repeter = n => fn => n && (fn(n), times(n - 1)(fn))
repeter(3)(console.log)
// 3
// 2
// 1
repeter(-1)(console.log) // RangeError: Maximum call stack size exceeded
```

### Manipuler des fonctions partielles

Les fonctions partielles sont dangereuses et doivent être utilisées avec prudence. Vous pouvez en effet obtenir un résultat inattendu (erroné), rencontrer des erreurs d'exécution, ou même s'exécuter indéfiniment lorsque vous les utilisez. Connaitre et traiter tous ces cas aux limites peut donc devenir très fastidieux.

Heureusement, il est possible de transformer une fonction partielle en fonction traditionnelle (ou fonction totale).
On peut en effet utiliser des valeurs par défaut ou des garde-fous pour traiter les entrées pour lesquelles la fonction partielle n'a pas de comportement défini.
En utilisant par exemple le type ['Option'](#Option), nous pouvons obtenir soit `Some(value)` ou `None` là où la fonction se serait comportée de manière inattendue. 

```js
// exemple 1: somme d'une liste
// on peut fournir une valeur par défaut afin que la fonction renvoie toujours un résultat
// somme :: [Number] -> Number
const somme = arr => arr.reduce((a, b) => a + b, 0)
somme([1, 2, 3]) // 6
somme([]) // 0

// exemple 2: récupération du premier élément d'une liste
// on peut utiliser le type Option
// premier :: [A] -> Option A
const premier = a => a.length ? Some(a[0]) : None()
premier([42]).map(a => console.log(a)) // 42
premier([]).map(a => console.log(a)) // console.log ne s'exécutera pas
// et avec le pire scénario
premier([[42]]).map(a => console.log(a[0])) // 42
premier([]).map(a => console.log(a[0])) // console.log ne s'exécutera pas, et il n'y aura pas d'erreur
// De plus, vous saurez grâce au type de retour (Option) que vous devez utiliser `.map`
// pour accèder à la valeur de retour et vous n'oublierez plus de vérifier l'argument
// car cela devient obligatoire.

// exemple 3: repéter une fonction N fois
// on fait en sorte que la fonction se termine toujours en changeant les conditions
// repeter :: Number -> (Number -> Number) -> Number
const repeter = n => fn => n > 0 && (fn(n), times(n - 1)(fn))
repeter(3)(console.log)
// 3
// 2
// 1
repeter(-1)(console.log) // ne fera rien
```

En rendant vos fonctions partielles totales, les erreurs d'exécution peuvent être évités. Toujours renvoyer une valeur permet de plus d'obtenir du code qui est à la fois plus facile à comprendre et à maintenir.

## Fonction totale

Une fonction qui renvoie un résultat valide pour toutes les valeurs d'entrées possibles. Les fonctions totales s'opposent aux [fonctions partielles](#fonction-partielle) qui peuvent générer des erreurs, renvoyer un résultat inattendu ou s'exécuter indéfiniment.

## Functional Programming Libraries in JavaScript

* [mori](https://github.com/swannodette/mori)
* [Immutable](https://github.com/facebook/immutable-js/)
* [Immer](https://github.com/mweststrate/immer)
* [Ramda](https://github.com/ramda/ramda)
* [ramda-adjunct](https://github.com/char0n/ramda-adjunct)
* [ramda-extension](https://github.com/tommmyy/ramda-extension)
* [Folktale](http://folktale.origamitower.com/)
* [monet.js](https://cwmyers.github.io/monet.js/)
* [lodash](https://github.com/lodash/lodash)
* [Underscore.js](https://github.com/jashkenas/underscore)
* [Lazy.js](https://github.com/dtao/lazy.js)
* [maryamyriameliamurphies.js](https://github.com/sjsyrek/maryamyriameliamurphies.js)
* [Haskell in ES6](https://github.com/casualjavascript/haskell-in-es6)
* [Sanctuary](https://github.com/sanctuary-js/sanctuary)
* [Crocks](https://github.com/evilsoft/crocks)
* [Fluture](https://github.com/fluture-js/Fluture)
* [fp-ts](https://github.com/gcanti/fp-ts)

---

__P.S:__ This repo is successful due to the wonderful [contributions](https://github.com/hemanth/functional-programming-jargon/graphs/contributors)!

# Fonctions

{{quote {author: "Donald Knuth", chapter: true}

Les gens pensent que l'informatique est l'art des génies mais la
réalité est tout le contraire, juste beaucoup de gens faisant des choses qui
qui se construisent les unes sur les autres, comme un mur de mini-pierres.

quote}}

{{index "Knuth, Donald"}}

{{figure {url: "img/chapter_picture_3.jpg", alt: "Picture of fern leaves with a fractal shape", chapter: framed}}}

{{index function, [code, "structure of"]}}

Les fonctions sont le pain et le beurre de la programmation JavaScript. Le
concept d'envelopper un morceau de programme dans une valeur a de nombreuses
utilisations. Il nous permet de structurer des programmes plus importants,
de réduire les répétitions, d'associer des noms aux sous-programmes et
d'isoler ces sous-programmes les uns des autres.

L'application la plus évidente des fonctions est la définition de nouveaux
((vocabulaire)). La création de nouveaux mots dans la prose est généralement
une mauvaise idée mais en programmation, c'est indispensable.

{{index abstraction, vocabulary}}

Un adulte anglophone typique possède environ 20 000 mots dans son
vocabulaire. Peu de langages de programmation intègrent 20 000 commandes.
Et le vocabulaire qui est disponible a tendance à être défini de manière
plus précise, et donc moins flexible, que dans le langage humain. Par
conséquent, nous _devons_ généralement introduire de nouveaux concepts
pour éviter de nous répéter trop souvent.


## Définir une fonction

{{index "square example", [function, definition], [binding, definition]}}

Une définition de fonction est une liaison normale dont la valeur est
une fonction. Par exemple, ce code définit `carre` pour faire référence
à une fonction qui produit le carré d'un nombre donné :

```
const carre = function(x) {
  return x * x;
};

console.log(carre(12));
// → 144
```

{{indexsee "curly braces", braces}}
{{index [braces, "function body"], block, [syntax, function], "function keyword", [function, body], [function, "as value"], [parentheses, arguments]}}

Une fonction est créée avec une expression qui commence par le mot-clé
`function`. Les fonctions ont un ensemble de _((paramètre))s_ (dans ce cas,
seulement `x`) et un _corps_, qui contient les instructions qui doivent être
exécutées lorsque la fonction est appelée. Le corps d'une fonction
créée de cette manière doit toujours être entourée d'accolades, même
lorsqu'elle est constitué d'une seule ((instruction)).

{{index "power example"}}

Une fonction peut avoir plusieurs paramètres ou ne pas avoir de paramètres
du tout. Dans l'exemple suivant, `faireDuBruit` ne liste aucun nom de
paramètre, alors que `puissance` en liste deux :

```
const faireDuBruit = function() {
  console.log("Bim Bam Boum!");
};

faireDuBruit();
// → Bim Bam Boum!

const puissance = function(base, exposant) {
  let resultat = 1;
  for (let compteur = 0; compteur < exposant; compteur++) {
    resultat *= base;
  }
  return result;
};

console.log(puissance(2, 10));
// → 1024
```

{{index "return value", "return keyword", undefined}}

Certaines fonctions produisent une valeur, comme `puissance` et `carre`, et
d'autres ne le font pas, comme `faireDuBruit`, dont le seul résultat est un
((effet de bord)). Une déclaration `return` détermine la valeur que la
fonction retourne. Lorsque le contrôle rencontre une telle instruction,
il sort immédiatement de la fonction en cours et donne la valeur retournée
au code qui a appelé la fonction. Un mot-clé `return` sans expression après
lui aura pour effet que la fonction retournera `undefined`. Les fonctions
qui n'ont pas d'instruction `return` du tout, comme `faireDuBruit`, retournent
également `undefined`.

{{index parameter, [function, application], [binding, "from parameter"]}}

Les paramètres d'une fonction se comportent comme des liaisons ordinaires,
mais leurs valeurs initiales sont données par l'_appelant_ de la fonction, et
non pas par le code de la fonction elle-même.

## Liaisons et portées

{{indexsee "top-level scope", "global scope"}}
{{index "var keyword", "global scope", [binding, global], [binding, "scope of"]}}

Chaque liaison a une _((portée))_ (scope), qui est la partie du programme dans
laquelle la liaison est visible. Pour les liaisons définies en dehors de toute
fonction ou d'un bloc, le champ d'application est l'ensemble du programme.
vous pouvez vous référer à de telles liaisons où vous voulez. Elles sont
appelées _globales_.

{{index "local scope", [binding, local]}}

Mais les liaisons créées pour les ((paramètres)) des fonctions ou déclarées à
l'intérieur d'une fonction ne peuvent être référencées que dans cette fonction,
elles sont donc connues sous le nom de liaisons _locales_. Chaque fois que
la fonction est appelée, de nouvelles instances de ces liaisons sont créées.
Cela fournit une certaine isolation entre fonctions - chaque appel de fonction
agit dans son propre petit monde (son environnement local) et peut souvent
être compris sans savoir ce qui se passe dans l'environnement global.

{{index "let keyword", "const keyword", "var keyword"}}

Les liaisons déclarées avec `let` et `const` sont en fait locales au
bloc _((bloc)_ dans lequel elles sont déclarées, donc si vous créez l'une
d'elles à l'intérieur d'une boucle, le code avant et après la boucle ne
peut pas la "voir". Dans le JavaScript d'avant 2015, seules les fonctions
créaient de nouveaux scopes, les liaisons à l'ancienne, créées avec le
mot clé `var`, sont visibles dans l'ensemble de la fonction dans laquelle
elles apparaissent ou dans la ou dans la portée globale, si elles ne sont
pas dans une fonction.

```
let x = 10;
if (true) {
  let y = 20;
  var z = 30;
  console.log(x + y + z);
  // → 60
}
// y est invisible ici
console.log(x + z);
// → 40
```

{{index [binding, visibility]}}

Chaque ((scope)) peut "regarder" dans le scope qui l'entoure, ainsi `x` est
visible à l'intérieur du bloc dans l'exemple. L'exception est lorsque
plusieurs liaisons portent le même nom, dans ce cas, le code ne peut voir
que celle qui est la plus proche. Par exemple, lorsque le code à l'intérieur
de la fonction `moitie` fait référence à `n`, il voit son _propre_ `n`,
et non le `n` global.

```
const moitie = function(n) {
  return n / 2;
};

let n = 10;
console.log(moitie(100));
// → 50
console.log(n);
// → 10
```

{{id scoping}}

### Portée imbriquée

{{index [nesting, "of functions"], [nesting, "of scope"], scope, "inner function", "lexical scoping"}}

JavaScript ne distingue pas seulement les liaisons _globales_ et _locales_.
Les blocs et fonctions peuvent être créés à l'intérieur d'autres blocs et
fonctions, ce qui produit de multiples degrés de localité.

{{index "landscape example"}}

Par exemple, cette fonction - qui fournit les ingrédients nécessaires pour
pour faire un lot de houmous - contient une autre fonction :

```
const houmous = function(facteur) {
  const ingredient = function(quantite, unite, nom) {
    let quantiteIngredient = quantite * facteur;
    if (quantiteIngredient > 1) {
      unite += "s";
    }
    console.log(`${quantiteIngredient} ${unite} ${nom}`);
  };
  ingredient(1, "boite", "pois chiche");
  ingredient(0.25, "tasse", "tahini");
  ingredient(0.25, "tasse", "jus de citron");
  ingredient(1, "gousse", "ail");
  ingredient(2, "cuillere a soupe", "huile d'olive");
  ingredient(0.5, "petite cuillere", "cumin");
};
```

{{index [function, scope], scope}}

Le code à l'intérieur de la fonction `ingredient` peut voir la liaison `facteur`.
de la fonction externe. Mais ses liaisons locales, telles que `unite` ou
`quantiteIngredient`, ne sont pas visibles dans la fonction externe.

L'ensemble des liaisons visibles à l'intérieur d'un bloc est déterminé par la
place de ce bloc dans le texte du programme. Chaque scope local peut également
voir tous les locaux qui la contiennent, et tous les scopes peuvent voir le
scope global. Cette approche de la visibilité des liaisons est appelée
_((portée lexcicale))_ (lexical scoping).

## Fonctions comme valeurs

{{index [function, "as value"], [binding, definition]}}

Une liaison de fonction sert généralement de nom à un élément spécifique du
programme. Une telle liaison est définie une fois et n'est jamais modifiée.
Il est donc facile de confondre la fonction et son nom.

{{index [binding, assignment]}}

Mais les deux sont différents. Une valeur de fonction peut faire toutes les
choses que d'autres valeurs peuvent faire - vous pouvez l'utiliser dans des
((expression))s arbitraires, et pas seulement l'appeler. Il est possible de
stocker une valeur de fonction dans une nouvelle liaison et de la transmettre
comme argument à une fonction, etc. De même, une liaison qui contient une
fonction n'est toujours qu'une liaison ordinaire et peut,si elle n'est pas
constante, se voir attribuer une nouvelle valeur, comme suit :

```{test: no}
let lancerMissiles = function() {
  systemeMissile.lance("maintenant");
};
if (safeMode) {
  lancerMissiles = function() {/* do nothing */};
}
```

{{index [function, "higher-order"]}}

Dans le [Chapitre ?](higher_order), nous discuterons des choses intéressantes
qui peuvent être réalisées en transmettant des valeurs de fonctions à d'autres
fonctions.

## Notation de déclaration

{{index [syntax, function], "function keyword", "square example", [function, definition], [function, declaration]}}

Il existe un moyen légèrement plus court de créer une liaison de fonction.
Lorsque le mot-clé `function` est utilisé au début d'une déclaration, cela
fonctionne différemment.

```{test: wrap}
function carre(x) {
  return x * x;
}
```

{{index future, "execution order"}}

Il s'agit d'une _déclaration_ de fonction. La déclaration définit la liaison
`carre` et la dirige vers la fonction donnée. Elle est légèrement plus facile
à écrire et ne nécessite pas de point-virgule après la fonction.

Il y a une subtilité avec cette forme de définition de fonction.

```
console.log("Le futur nous dit:", future());

function future() {
  return "Vous n'aurez pas de voitures volantes";
}
```

Le code précédent fonctionne, même si la fonction est définie _sous_ le code qui
l'utilise. Les déclarations de fonctions ne font pas partie du flux de contrôle
régulier de haut en bas. Elles sont conceptuellement déplacées vers le haut
de leur portée et peuvent être utilisées par tout le code dans cette portée.
Ceci est parfois utile, car dela offre la liberté d'ordonner le code d'une
manière qui semble significative, sans se soucier de devoir définir toutes les
fonctions avant qu'elles ne soient utilisées.

## Fonctions fléchées

{{index function, "arrow function"}}

Il y a une troisième notation pour les fonctions, qui semble très différente
des autres. Au lieu du mot-clé `function`, elle utilise une flèche
(`=>`) composée d'un signe égal et d'un caractère plus grand que (à ne pas
(à ne pas confondre avec l'opérateur supérieur ou égal, qui s'écrit `>=`).
`>=`).

```{test: wrap}
const puissance = (base, exposant) => {
  let resultat = 1;
  for (let compteur = 0; compteur < exposant; compteur++) {
    resultat *= base;
  }
  return resultat;
};
```

{{index [function, body]}}

La flèche vient _après_ la liste des paramètres et est suivie par le
corps de la fonction. Elle exprime quelque chose comme "cette entrée (les
((paramètre))s) produit ce résultat (le corps)".

{{index [braces, "function body"], "square example", [parentheses, arguments]}}

Lorsqu'il n'y a qu'un seul nom de paramètre, vous pouvez omettre les
parenthèses autour de la liste de paramètres. Si le corps est une seule
expression, plutôt qu'un ((bloc)) entre accolades, cette expression sera
retournée de la fonction. Ainsi, ces deux définitions de `carre` font la
même chose:

```
const carre1 = (x) => { return x * x; };
const carre2 = x => x * x;
```

{{index [parentheses, arguments]}}

Lorsqu'une fonction flèche ne possède aucun paramètre, sa liste de paramètres
est simplement un ensemble vide de parenthèses.

```
const klaxon = () => {
  console.log("Tuuut");
};
```

{{index verbosity}}

Il n'y a pas de raison profonde d'avoir à la fois des fonctions flèches
et des expressions `function` dans le langage. A part un détail mineur,
que nous aborderons dans le [Chapitre ?](objet), elles font la même chose.
Les fonctions fléchées ont été ajoutées en 2015, principalement pour rendre
possible d'écrire de petites expressions de fonctions de manière moins
verbeuse. Nous les utiliserons beaucoup dans le [Chapitre ?](higher_order).

{{id stack}}

## La pile d'appel

{{indexsee stack, "call stack"}}
{{index "call stack", [function, application]}}

La façon dont le contrôle circule dans les fonctions est quelque peu complexe.
Examinons-la de plus près. Voici un programme simple qui fait quelques
appels de fonctions :

```
function saluer(qui) {
  console.log("Bonjour " + qui);
}
saluer("Johnny");
console.log("Au revoir");
```

{{index ["control flow", functions], "execution order", "console.log"}}

Une exécution de ce programme se déroule à peu près comme suit : l'appel
à `saluer` fait sauter le contrôle au début de cette fonction (ligne 2).
La fonction fonction appelle `console.log`, qui prend le contrôle, fait son
travail, et retourne puis retourne le contrôle à la ligne 2. Là, il atteint
la fin de la fonction `saluer`, donc elle retourne à l'endroit qui l'a
appelée, c'est-à-dire à la la ligne 4. La ligne suivante appelle à nouveau `console.log`. Après ce retour, le programme se termine.

Nous pourrions montrer le flux de contrôle de manière schématique comme ceci :

```{lang: null}
pas dans une fonction
   dans saluer
        dans console.log
   dans saluer
pas dans une fonction
   dans console.log
pas dans une fonction
```

{{index "return keyword", [memory, call stack]}}

Parce qu'une fonction doit retourner à l'endroit qui l'a appelée
lorsqu'elle revient, l'ordinateur doit se souvenir du contexte dans lequel
l'appel a été effectué. Dans un cas, `console.log` doit retourner à la
fonction `saluer` lorsqu'il a terminé. Dans l'autre cas, il retourne à la
fin du programme.

L'endroit où l'ordinateur stocke ce contexte est la _((pile d'appel))_
(call stack). Chaque fois qu'une fonction est appelée, le contexte actuel
est stocké au sommet de cette pile. Lorsqu'une fonction revient, elle retire
le contexte supérieur de la pile et utilise ce contexte pour poursuivre
l'exécution.

{{index "infinite loop", "stack overflow", recursion}}

Le stockage de cette pile nécessite de l'espace dans la mémoire de l'ordinateur.
Lorsque la pile devient trop grande, l'ordinateur échoue avec un message tel
que "out of stack space" ou "too much recursion". Le code suivant
illustre ce phénomène en posant à l'ordinateur une question vraiment difficile
qui provoque un va-et-vient infini entre deux fonctions. En fait, il
serait infini, si l'ordinateur avait une pile infinie. En l'état actuel
des choses, nous allons manquer d'espace, ou "faire sauter la pile".

```{test: no}
function poule() {
  return oeuf();
}
function oeuf() {
  return poule();
}
console.log("La " + poule() + " vient d'abord !");
// → ??
```

## Arguments optionnels

{{index argument, [function, application]}}

Le code suivant est autorisé et s'exécute sans aucun problème :

```
function carre(x) { return x * x; }
console.log(carre(4, true, "hérisson"));
// → 16
```

Nous avons défini `square` avec un seul ((paramètre)). Pourtant, lorsque
nous l'appelons avec trois, le langage ne se plaint pas. Il ignore les
arguments supplémentaires et calcule le carré du premier.

{{index undefined}}

JavaScript est extrêmement large d'esprit quant au nombre d'arguments que vous
que vous passez à une fonction. Si vous en passez trop, les paramètres
supplémentaires sont ignorés. Si vous n'en passez pas assez, les paramètres
manquants se voient attribuer la valeur `undefined`.

L'inconvénient, c'est qu'il est possible - voire même probable - que vous
passiez accidentellement le mauvais nombre d'arguments aux fonctions. Et
personne ne vous le dira.

Le bon côté est que ce comportement peut être utilisé pour permettre à une
fonction d'être appelée avec différents nombres d'arguments. Par exemple,
cette fonction `soustrait` essaie d'imiter l'opérateur `-` en agissant soit
sur un ou deux arguments:

```
function soustrait(a, b) {
  if (b === undefined) return -a;
  else return a - b;
}

console.log(soustrait(10));
// → -10
console.log(soustrait(10, 5));
// → 5
```

{{id power}}
{{index "optional argument", "default value", parameter, ["= operator", "for default value"]}}

Si vous écrivez un opérateur `=` après un paramètre, suivi par une expression,
la valeur de cette expression remplacera l'argument lorsqu'il n'est pas donné.

{{index "power example"}}

Par exemple, cette version de `puissance` rend son deuxième argument
facultatif. Si vous ne le fournissez pas ou si vous passez la valeur
`undefined`, la valeur par défaut sera de deux, et la fonction se comportera
comme `carre`.


```{test: wrap}
function puissance(base, exposant = 2) {
  let resultat = 1;
  for (let compteur = 0; compteur < exposant; compteur++) {
    resultat *= base;
  }
  return resultat;
}

console.log(puissance(4));
// → 16
console.log(puissance(2, 6));
// → 64
```

{{index "console.log"}}

Dans le [prochain chapitre](data#rest_parameters), nous verrons une manière
dont un corps de fonction peut obtenir la liste complète des arguments qui lui
ont été passés. C'est utile car cela permet à une fonction d'accepter un nombre
quelconque d'arguments. Par exemple, `console.log` fait ceci: il affiche
toutes les valeurs qui lui sont données.

```
console.log("C", "O", 2);
// → C O 2
```

## Fermeture

{{index "call stack", "local binding", [function, "as value"], scope}}


La possibilité de traiter les fonctions comme des valeurs, associée au
fait que les liaisons locales sont recréées chaque fois qu'une fonction est
appelée, soulève une question intéressante. Qu'advient-il des liaisons
locales lorsque l'appel de fonction qui les a créées n'est plus active ?

Le code suivant montre un exemple de cette question. Il définit une fonction,
`emballeValeur`, qui crée une liaison locale. Il renvoie ensuite une fonction
qui accède à cette liaison locale et la renvoie.

```
function emballeValeur(n) {
  let local = n;
  return () => local;
}

let emballe1 = emballeValeur(1);
let emballe2 = emballeValeur(2);
console.log(emballe1());
// → 1
console.log(emballe2());
// → 2
```

C'est autorisé et cela fonctionne comme vous l'espérez - les deux instances
de la liaison sont toujours accessibles. Cette situation est une bonne
démonstration du fait que les liaisons locales sont créées à nouveau pour
chaque appel, et que les différents appels ne peuvent pas empiéter sur
les liaisons locales des autres.

Cette fonctionnalité - la possibilité de référencer une instance spécifique
d'une liaison locale dans une portée englobante, est appelée _((fermeture))_
(closure). Une fonction qui fait référence aux liaisons des scopes locaux qui
l'entourent est appelée _une_ fermeture. Ce comportement non seulement vous
évite d'avoir à vous préoccuper de la durée de vie des liaisons mais
permet également d'utiliser les valeurs de fonction de manière créative.

{{index "multiplier function"}}

Avec une légère modification, nous pouvons transformer l'exemple précédent
en un moyen de créer des fonctions qui multiplient par une quantité arbitraire.

```
function multiplicateur(facteur) {
  return nombre => nombre * facteur;
}

let doubleur = multiplicateur(2);
console.log(doubleur(5));
// → 10
```

{{index [binding, "from parameter"]}}

La liaison `locale` explicite de l'exemple `emballeValeur` n'est pas réellement
nécessaire puisqu'un paramètre est lui-même une liaison locale.

{{index [function, "model of"]}}

Réfléchir à de tels programmes demande un certain entraînement. Un bon modèle
mental consiste à considérer les valeurs des fonctions comme contenant à la
fois le code dans leur corps et l'environnement dans lequel elles sont créées. Lorsqu'elles sont appelées, le corps de la fonction voit l'environnement dans
lequel il a été créé, pas l'environnement dans lequel elle est appelée.

Dans l'exemple, la fonction `multiplicateur` est appelée et crée un
environnement dans lequel le parametre `facteur` vaut 2. La valeur de la
fonction qu'il retourne, qui est stockée dans `doubleur`, se souvient de cet environnement. Ainsi, lorsque cette fonction est appelée, elle multiplie
son argument par 2.

## Récursion

{{index "power example", "stack overflow", recursion, [function, application]}}

Une fonction peut parfaitement s'appeler elle-même, tant qu'elle ne le fait pas
si souvent qu'elle fasse déborder la pile. Une fonction qui s'appelle
elle-même est appelée _récursive_. La récursivité permet à certaines
fonctions d'être écrites dans un style différent. Prenez, par exemple,
cette alternative de `puissance` :

```{test: wrap}
function puissance(base, exposant) {
  if (exposant == 0) {
    return 1;
  } else {
    return base * puissance(base, exposant - 1);
  }
}

console.log(puissance(2, 3));
// → 8
```

{{index loop, readability, mathematics}}

Ceci est assez proche de la façon dont les mathématiciens définissent
l'exponentiation et décrit sans doute le concept plus clairement que la
variante en boucle. La fonction s'appelle plusieurs fois avec des
exposants toujours plus petits pour réaliser la multiplication répétée.

{{index [function, application], efficiency}}

Mais cette implémentation a un problème : dans les implémentations
JavaScript typiques elle est environ trois fois plus lente que la version
en boucle. L'exécution d'une boucle simple est généralement moins coûteuse
que l'appel d'une fonction plusieurs fois.

{{index optimization}}

Le dilemme entre vitesse et ((élégance)) est intéressant. Vous pouvez
le voir comme une sorte de continuum entre la convivialité pour l'homme et
la convivialité de la machine. Presque tout programme peut être rendu
plus rapide en le rendant plus gros et plus alambiqué. Le programmeur
doit décider d'un équilibre approprié.

Dans le cas de la fonction `puissance`, la version moins élégante (en boucle)
est encore assez simple et facile à lire. Cela n'a pas beaucoup de sens de
de la remplacer par la version récursive. Souvent, cependant, un programme
traite des concepts si complexes qu'il est préférable de renoncer à une certaine efficacité pour rendre le programme plus simple est préférable.

{{index profiling}}

Se préoccuper de l'efficacité peut être une distraction. C'est encore un autre
facteur qui complique la conception du programme, et lorsque vous faites
quelque chose qui est déjà difficile, cette chose supplémentaire dont il faut
s'inquiéter peut être paralysant.


{{index "premature optimization"}}

Par conséquent, commencez toujours par écrire quelque chose qui est correct
et facile à comprendre. Si vous craignez que cela soit trop lent, ce qui
n'est généralement pas le cas, car la plupart du code n'est pas exécuté
assez souvent pour prendre un temps significatif, vous pouvez mesurer après
coup et l'améliorer si nécessaire.

{{index "branching recursion"}}

La récursion n'est pas toujours une alternative inefficace au bouclage.
Certains problèmes sont vraiment plus faciles à résoudre avec la récursion
qu'avec des boucles. Le plus souvent, il s'agit de problèmes qui nécessitent l'exploration ou le traitement de plusieurs "branches", chacune d'entre elles
pouvant se ramifier à nouveau en encore plus de branches.

{{id recursive_puzzle}}
{{index recursion, "number puzzle example"}}

Considérez cette énigme : en partant du nombre 1 et en répétant plusieurs fois
l'ajout de 5 ou la multiplication par 3, on peut produire un ensemble
infini de nombres . Comment écririez-vous une fonction qui, étant
donné un nombre, essaie de trouver une séquence de telles additions et
multiplications qui produit ce nombre ?

Par exemple, le nombre 13 pourrait être atteint en multipliant d'abord par 3
puis en ajoutant 5 deux fois, alors que le nombre 15 ne peut pas être atteint
du tout.

Voici une solution récursive :

```
function trouveSolution(cible) {
  function trouve(actuel, histoire) {
    if (actuel == cible) {
      return histoire;
    } else if (actuel > cible) {
      return null;
    } else {
      return find(actuel + 5, `(${histoire} + 5)`) ||
             find(actuel * 3, `(${histoire} * 3)`);
    }
  }
  return trouve(1, "1");
}

console.log(trouveSolution(24));
// → (((1 * 3) + 5) * 3)
```

Notez que ce programme ne trouve pas nécessairement la séquence d'opérations
la plus courte. Il est satisfait lorsqu'il trouve une séquence quelconque.

Ce n'est pas grave si vous ne voyez pas tout de suite comment cela fonctionne.
Nous allons travailler dessus, car c'est un excellent exercice de pensée
récursive.

La fonction interne `trouve` produit la récursivité. Elle prend deux
((argument))s : le nombre actuel et une chaîne de caractères qui enregistre
comment nous atteignons ce nombre. Si elle trouve une solution, elle retourne
une chaîne de caractères qui qui montre comment atteindre la cible. Si aucune
solution ne peut être trouvée à partir à partir de ce nombre, il renvoie `null`.

{{index null, "|| operator", "short-circuit evaluation"}}

Pour ce faire, la fonction effectue l'une des trois actions suivantes. Si le
nombre actuel courant est le nombre cible, l'historique courant est un moyen d'atteindre cette cible, il est donc renvoyé. Si le nombre actuel est supérieur à
l'objectif, il n'y a pas de raison d'explorer plus avant cette branche car
l'addition et la multiplication ne feront qu'augmenter le nombre. Enfin, si
nous sommes toujours en dessous du nombre cible, la fonction essaye les deux
chemins possibles qui partent du nombre actuel courant en s'appelant deux
fois, une fois pour l'addition et une fois pour la multiplication. Si le
premier appel renvoie quelque chose qui n'est pas `null`, il est retourné.
Sinon, le deuxième appel est retourné, qu'il produise une chaîne ou `null`.

{{index "call stack"}}

Pour mieux comprendre comment cette fonction produit l'effet que nous
recherchons, regardons tous les appels à `trouve` qui sont faits lors de la
la recherche d'une solution pour le nombre 13.

```{lang: null}
trouve(1, "1")
  trouve(6, "(1 + 5)")
    trouve(11, "((1 + 5) + 5)")
      trouve(16, "(((1 + 5) + 5) + 5)")
        trop gros
      trouve(33, "(((1 + 5) + 5) * 3)")
        trop gros
    trouve(18, "((1 + 5) * 3)")
      trop gros
  trouve(3, "(1 * 3)")
    trouve(8, "((1 * 3) + 5)")
      trouve(13, "(((1 * 3) + 5) + 5)")
        trouvé!
```

L'indentation indique la profondeur de la pile d'appels. La première fois que
`trouve` est appelé, il commence par s'appeler lui-même pour explorer la solution
qui commence par `(1 + 5)`. Cet appel sera ensuite récursif pour explorer
_chaque_ solution qui donne un nombre inférieur ou égal au le nombre cible.
Puisqu'il n'en trouve aucune qui atteigne la cible, il renvoie `null` au
premier appel. Là, l'opérateur `||` provoque l'appel qui explore `(1 * 3)`.
Cette recherche a plus de chance - son premier appel récursif, à travers
encore _un autre_ appel récursif, tombe sur le nombre cible. L'appel le plus
intérieur renvoie une chaîne de caractères, et chacun des opérateurs `||` dans
les appels intermédiaires transmet cette chaîne de caractères pour finalement
retourner la solution.

## Créer des fonctions

{{index [function, definition]}}

Il existe deux façons plus ou moins naturelles d'introduire des fonctions
dans les programmes.

{{index repetition}}

La première est que vous vous retrouvez à écrire un code similaire plusieurs
fois. Vous préféreriez ne pas le faire. Avoir plus de code signifie plus
d'espace pour que les erreurs se cachent et plus de choses à lire pour les
personnes qui essaient de comprendre le programme. Vous prenez donc la
fonctionnalité répétée, vous lui trouvez un bon nom, et vous la mettez dans
une fonction.

La deuxième façon est que vous trouvez que vous avez besoin d'une
fonctionnalité que vous n'avez pas encore écrite et qui semble
mériter sa propre fonction. Vous commencerez par nommer la fonction, puis
vous écrirez son corps. Vous pouvez même commencer à écrire le code qui
utilise la fonction avant de avant de définir la fonction elle-même.

{{index [function, naming], [binding, naming]}}

La difficulté à trouver un bon nom pour une fonction est une bonne
indication de la clarté du concept que vous essayez d'envelopper.
Prenons un exemple.

{{index "farm example"}}

Nous voulons écrire un programme qui imprime deux nombres : les nombres de
vaches et de poulets d'une ferme, suivis des mots "vaches" et "poulets".
et des zéros placés devant les deux nombres de sorte qu'ils soient toujours
sur trois positions.

```{lang: null}
007 Vaches
011 Poulets
```

Cela demande une fonction de deux arguments - le nombre de vaches et le
nombre de poulets. Commençons à coder.

```
function afficheInventaireFerme(vaches, poulets) {
  let chaineVaches = String(vaches);
  while (chaineVaches.length < 3) {
    chaineVaches = "0" + chaineVaches;
  }
  console.log(`${chaineVaches} Vaches`);
  let chainePoulets = String(poulets);
  while (chainePoulets.length < 3) {
    chainePoulets = "0" + chainePoulets;
  }
  console.log(`${chainePoulets} Poulets`);
}
afficheInventaireFerme(7, 11);
```

{{index ["length property", "for string"], "while loop"}}

Écrire `.length` après une expression de chaîne de caractères nous donnera
la longueur de cette chaîne. Ainsi, les boucles `while` ajoutent des zéros
devant les chaînes de chiffres jusqu'à ce qu'elles aient au moins trois
caractères de long.

Mission accomplie ! Mais juste au moment où nous sommes sur le point
d'envoyer au fermier le code (ainsi qu'une facture salée), elle nous appelle
pour nous dire qu'elle a commencé à élever des porcs, et que nous ne
pourrions pas étendre le logiciel afin de d'imprimer aussi des cochons ?

{{index "copy-paste programming"}}


On peut le faire. Mais juste au moment où nous sommes sur le point de copier
et coller ces quatre lignes une fois de plus, nous nous arrêtons et nous
reconsidérons. Il doit y avoir un meilleur moyen. Voici une première tentative :

```
function afficheDesZerosEtUnLibelle(nombre, libelle) {
  let chaineDeNombre = String(nombre);
  while (chaineDeNombre.length < 3) {
    chaineDeNombre = "0" + chaineDeNombre;
  }
  console.log(`${chaineDeNombre} ${libelle}`);
}

function afficheInventaireFerme(vaches, poulets, cochons) {
  afficheDesZerosEtUnLibelle(vaches, "Vaches");
  afficheDesZerosEtUnLibelle(poulets, "Poulets");
  afficheDesZerosEtUnLibelle(cochons, "Cochons");
}

afficheInventaireFerme(7, 11, 3);
```

{{index [function, naming]}}

Ça marche ! Mais ce nom, `afficheDesZerosEtUnLibelle`, est un peu
maladroit. Il regroupe trois choses - l'impression, la mise à zéro et
l'ajout d'une étiquette - en une seule fonction.

{{index "zeroPad function"}}

Au lieu de retirer la partie répétée de notre programme en bloc,
essayons d'en extraire un seul _concept_.

```
function prefixeAvecDesZeros(nombre, taille) {
  let chaine = String(nombre);
  while (chaine.length < taille) {
    chaine = "0" + chaine;
  }
  return chaine;
}

function afficheInventaireFerme(vaches, poulets, cochons) {
  console.log(`${prefixeAvecDesZeros(vaches, 3)} Vaches`);
  console.log(`${prefixeAvecDesZeros(poulets, 3)} Poulets`);
  console.log(`${prefixeAvecDesZeros(cochons, 3)} Cochons`);
}

afficheInventaireFerme(7, 16, 3);
```

{{index readability, "pure function"}}

Une fonction avec un nom agréable et évident comme `prefixeAvecDesZeros` rend
plus facile pour quelqu'un qui lit le code de comprendre ce qu'elle fait. Et
une telle fonction est utile dans plus de situations que ce programme spécifique.
Par exemple, vous pouvez l'utiliser pour imprimer des tableaux de nombres
bien alignés.

{{index [interface, design]}}

À quel point notre fonction devrait-elle être intelligente et polyvalente ?
Nous pourrions écrire n'importe quoi, d'une fonction terriblement simple qui
ne peut que compléter un nombre de trois caractères à un système compliqué
de formatage de nombres qui gère les nombres fractionnaires, les nombres
négatifs, l'alignement des points décimaux, le remplissage avec différents
caractères, et ainsi de suite.

Un principe utile est de ne pas ajouter d'astuces à moins d'être absolument
sûr d'en avoir besoin. Il peut être tentant d'écrire des "((framework))s"
pour chaque fonctionnalité que vous rencontrez. Résistez à cette envie. Vous
ne ferez pas un vrai travail, vous ne ferez qu'écrire du code que vous
n'utiliserez jamais.

{{id pure}}
## Fonctions et effets de bord

{{index "side effect", "pure function", [function, purity]}}

Les fonctions peuvent être grossièrement divisées entre celles qui sont
appelées pour leurs effets de bord et celles qui sont appelées pour
leur valeur de retour. (Bien qu'il est tout à fait possible d'avoir des effets
de bord et de retourner une valeur).

{{index reuse}}

La première fonction d'aide dans l'exemple ((ferme)),
`afficheDesZerosEtUnLibelle`, est appelée pour son effet de bord :
elle imprime une ligne. La deuxième version, `prefixeAvecDesZeros`, est
appelée pour sa valeur de retour. Ce n'est pas une coïncidence si la
seconde est utile dans plus de situations que la première. Les fonctions
qui créent des valeurs sont plus faciles à combiner que les fonctions
qui produisent directement des effets secondaires.

{{index substitution}}

Une fonction _pure_ est un type spécifique de fonction productrice de valeur
qui non seulement n'a pas d'effets secondaires, mais ne dépend pas non plus
des effets secondaires d'un autre code - par exemple, elle ne lit pas des
liaisons globales dont la valeur pourrait changer. Une fonction pure possède
l'agréable propriété suivante, lorsqu'elle est appelée avec les mêmes
arguments, elle produit toujours la même valeur (et ne fait rien d'autre).
Un appel à une telle fonction peut être substituée par sa valeur de retour
sans changer le sens du code. Lorsque vous n'êtes pas sûr qu'une fonction pure fonctionne correctement, vous pouvez la tester en l'appelant tout simplement
et savoir que si elle fonctionne dans dans ce contexte, elle fonctionnera dans
n'importe quel contexte. Les fonctions non pures ont tendance à nécessitent
plus d'échafaudages pour être testées.

{{index optimization, "console.log"}}

Pourtant, il n'est pas nécessaire de se sentir mal quand on écrit des
fonctions qui ne sont pas pures ou de mener une guerre sainte pour les purger
de votre code. Les effets de bord sont souvent utiles. Il n'y aurait aucun
moyen d'écrire une version pure de `console.log`, par exemple, et `console.log`
est bon à avoir. Certaines opérations sont également plus faciles à exprimer
de manière efficace lorsqu'on utilise les effets de bord, donc la vitesse
de calcul peut être une raison d'éviter la pureté.

## Résumé

Ce chapitre vous a appris à écrire vos propres fonctions. Le mot-clé
mot-clé `function`, lorsqu'il est utilisé comme une expression, peut créer
une fonction valeur. Lorsqu'il est utilisé comme une déclaration, il peut
être utilisé pour déclarer une liaison et lui donner une fonction comme valeur.
Les fonctions flèches sont encore une autre manière de créer des fonctions.

```
// Definir f pour lier une valer de fonction
const f = function(a) {
  console.log(a + 2);
};

// Declarer g en tant que fonction
function g(a, b) {
  return a * b * 3.5;
}

// Une valeur de fonction moins verbeuse
let h = a => a % 3;
```

Un aspect essentiel de la compréhension des fonctions est la compréhension
des portées. Chaque bloc crée une nouvelle portée. Les paramètres et les liaisons
déclarés dans une étendue sont locaux et non visibles de l'extérieur. Les
liaisons déclarées avec `var` se comportent différemment - elles finissent
dans la fonction la plus proche ou dans la portée globale.

Il est utile de séparer les tâches effectuées par votre programme en
plusieurs fonctions utile. Vous n'aurez pas à vous répéter autant, et les
fonctions peuvent aider à organiser un programme en regroupant le code en
plusieurs parties spécifiques.

## Exercices

### Minimum

{{index "Math object", "minimum (exercise)", "Math.min function", minimum}}

Le [chapitre précédent](program_structure#return_values) a introduit la fonction standard `Math.min` qui retourne son plus petit argument. Nous pouvons maintenant
construire quelque chose comme ça. Ecrivez une fonction `min` qui prend
deux arguments et renvoie leur minimum.

{{if interactive

```{test: no}
// Votre code ici.

console.log(min(0, 10));
// → 0
console.log(min(0, -10));
// → -10
```
if}}

{{hint

{{index "minimum (exercise)"}}

Si vous avez du mal à placer les accolades et les parenthèses au bon endroit
pour obtenir une définition de fonction valide, commencez par copier l'un
des exemples de ce chapitre et modifiez-le.

{{index "return keyword"}}

Une fonction peut contenir plusieurs instructions `return`.

hint}}

### Récursion

{{index recursion, "isEven (exercise)", "even number"}}

Nous avons vu que `%` (l'opérateur de reste) peut être utilisé pour tester
pour tester si un nombre est pair ou impair, en utilisant `% 2` pour voir
si le nombre est divisible par deux. Voici une autre façon de déterminer
si un nombre entier positif est pair ou impair.

- Zéro est pair.

- Un est impair.

- Pour tout autre nombre _N_, son égalité est égale à _N_ - 2.

Définissez une fonction récursive `estPair` correspondant à cette
description. La fonction doit accepter un seul paramètre (un
nombre entier positif) et retourner un booléen.

{{index "stack overflow"}}

Testez-le sur 50 et 75. Voyez comment il se comporte à -1. Pourquoi ?
Pouvez-vous penser à un moyen de résoudre ce problème ?

{{if interactive

```{test: no}
// Votre code ici.

console.log(estPair(50));
// → true
console.log(estPair(75));
// → false
console.log(estPair(-1));
// → ??
```

if}}

{{hint

{{index "isEven (exercise)", ["if keyword", chaining], recursion}}

Votre fonction ressemblera probablement à la fonction interne `trouve`
de l'exemple récursif `trouveSolution` [récursive](functions#recursive_puzzle)
de ce chapitre, avec une chaîne `if`/`else if`/`else` qui teste lequel des
trois cas s'applique. Le dernier `else`, correspondant au troisième cas,
lance l'appel récursif. Chacune des branches doit contenir une instruction
`return` ou, d'une manière ou d'une autre, faire en sorte qu'une valeur
spécifique soit retournée.

{{index "stack overflow"}}

Lorsqu'on lui donne un nombre négatif, la fonction va récursiver encore et
encore, en se passant un nombre de plus en plus négatif, s'éloignant ainsi
de plus en plus loin de retourner un résultat. Elle finira par manquer de
place sur la pile et s'arrêtera.

hint}}

### Comptage des haricots

{{index "bean counting (exercise)", [string, indexing], "zero-based counting", ["length property", "for string"]}}

Vous pouvez obtenir le Nième caractère, ou lettre, d'une chaîne de caractères en écrivant `"string"[N]`. La valeur retournée sera une chaîne de caractères ne
contenant qu'un seul caractère (par exemple, `"b"`). Le premier caractère a la
position 0, ce qui fait que le dernier se trouve à la position
`string.length - 1`. En d'autres termes, une chaîne de deux caractères a une
longueur de 2 et ses caractères ont les positions 0 et 1.

Écrivez une fonction `compteBs` qui prend une chaîne de caractères comme seul
argument et renvoie un nombre qui indique le nombre de caractères "B" majuscules
dans la chaîne de caractères.

Ensuite, écrivez une fonction appelée `compteChar` qui se comporte comme
`compteBs`, sauf qu'elle prend un deuxième argument qui indique le caractère
qui est à compter (au lieu de ne compter que les caractères majuscules "B").
Réécrivez `compteBs` pour utiliser cette nouvelle fonction.

{{if interactive

```{test: no}
// Votre code ici.

console.log(compteBs("BBC"));
// → 2
console.log(compteChar("kakkerlak", "k"));
// → 4
```

if}}

{{hint

{{index "bean counting (exercise)", ["length property", "for string"], "counter variable"}}

Votre fonction aura besoin d'une ((boucle)) qui regarde chaque caractère de la
la chaîne. Elle peut exécuter un index de zéro à un en dessous de sa longueur (`<
string.length`). Si le caractère qui se trouve à la position actuelle est le même
que celui que la fonction recherche, elle ajoute 1 à une variable de compteur.
Une fois la boucle terminée, le compteur peut être retourné.

{{index "local binding"}}

Veillez à ce que toutes les liaisons utilisées dans la fonction soient
_locales_ à la fonction en les déclarant correctement avec le mot clé
`let` ou `const'.

hint}}

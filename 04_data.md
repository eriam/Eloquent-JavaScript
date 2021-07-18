{{meta {load_files: ["code/journal.js", "code/chapter/04_data.js"], zip: "node/html"}}}

# Structures de données : Objets et tableaux

{{quote {author: "Charles Babbage", title: "Passages from the Life of a Philosopher (1864)", chapter: true}

A deux reprises, on m'a demandé, "Priez, Mr. Babbage, si vous mettez
dans la machine des chiffres erronés, est-ce que les bonnes réponses en sortiront ?
[...] Je ne suis pas capable d'appréhender correctement le genre d'idées confuses
qui pourrait provoquer une telle question.

quote}}

{{index "Babbage, Charles"}}

{{figure {url: "img/chapter_picture_4.jpg", alt: "Picture of a weresquirrel", chapter: framed}}}

{{index object, "data structure"}}

Les nombres, les booléens et les chaînes de caractères sont les atomes à partir
desquels les structures de ((données)) sont construites. Cependant de nombreux
types d'informations nécessitent plus d'un atomes. Les _Objets_ permettent
de regrouper des valeurs - y compris d'autres objets - pour construire des
structures plus complexes.

Les programmes que nous avons construits jusqu'à présent étaient limités par
le fait qu'ils n'opéraient que sur des types de données simples. Ce chapitre va
introduire les structures de données de base. À la fin de ce chapitre, vous en
saurez suffisamment pour commencer à écrire des programmes utiles.

Le chapitre traitera d'un exemple de programmation plus ou moins réaliste, en
introduisant les concepts tels qu'ils s'appliquent au problème à résoudre.
Le code de l'exemple s'appuiera souvent sur les fonctions et les liaisons qui
ont été introduites plus tôt dans le texte.

{{if book

Le bac a sable ((sandbox)) pour le livre
([_https://eloquentjavascript.net/code_](https://eloquentjavascript.net/code))
permet d'exécuter du code dans le contexte d'un chapitre spécifique. Si
Si vous décidez de travailler avec les exemples dans un autre environnement
de télécharger d'abord le code complet de ce chapitre à partir de la page sandbox
de la page Sandbox.

if}}

## L'Écureuil-garou

{{index "weresquirrel example", lycanthropy}}

De temps en temps, généralement entre 20 et 22 heures, ((Jacques)) se
retrouve transformé en un petit rongeur à fourrure avec une queue touffue.

D'un côté, Jacques est assez content de ne pas avoir la classique lycanthropie.
Se transformer en écureuil cause moins de problèmes que que de se transformer
en loup. Au lieu d'avoir à s'inquiéter de manger accidentellement le voisin
(_ça_ serait gênant), il s'inquiète d'être mangé par le chat du voisin.
Après deux occasions où il s'est réveillé sur une branche très fine de la
couronne d'un chêne, nu et désorienté, il a pris l'habitude de fermer à clé
les portes et les fenêtres de sa chambre la nuit et à mettre quelques noix
sur le sol pour s'occuper.

Cela règle les problèmes du chat et de l'arbre. Mais Jacques préférerait
se débarrasser complètement de son état. Les occurrences irrégulières de la
transformation lui font penser qu'elles pourraient être déclenchées par
quelque chose. Pendant un temps, il a cru que cela se produisait uniquement
les jours où il avait été près de chênes. Mais éviter les chênes n'a pas
arrêté le problème.

{{index journal}}

Passant à une approche plus scientifique, Jacques a commencé à tenir un journal quotidien de tout ce qu'il fait dans une journée donnée et de savoir s'il a
changé de forme. Avec ces données, il espère affiner les conditions qui
déclenchent les transformations.

La première chose dont il a besoin est une structure de données pour stocker ces
informations.

## Jeu de données

{{index ["data structure", collection], [memory, organization]}}

Pour travailler avec un morceau de données numériques, nous devons d'abord
trouver un moyen de le représenter dans la mémoire de notre machine. Disons,
par exemple, que nous voulons représenter une ((collection)) des nombres
2, 3, 5, 7, et 11.

{{index string}}

Nous pourrions être créatifs avec les chaînes de caractères après tout, les
chaînes de caractères peuvent avoir n'importe quelle longueur, donc nous
pouvons y mettre beaucoup de données et utiliser `"2 3 5 7 11"` comme
représentation. Mais cela n'est pas très pratique. Il faudrait en quelque sorte
extraire les chiffres et les reconvertir en nombres pour y accéder.

{{index [array, creation], "[] (array)"}}

Heureusement, JavaScript fournit un type de données spécifique pour le
stockage de séquences de valeurs. Il s'agit d'un _tableau_ qui s'écrit comme
une liste de valeurs entre ((crochets), séparées par des virgules.

```
let listeDeNombres = [2, 3, 5, 7, 11];
console.log(listeDeNombres[2]);
// → 5
console.log(listeDeNombres[0]);
// → 2
console.log(listeDeNombres[2 - 1]);
// → 3
```

{{index "[] (subscript)", [array, indexing]}}

La notation pour accéder aux éléments d'un tableau utilise également des
((crochets)). Une paire de crochets immédiatement après une expression
avec une autre expression à l'intérieur, cherchera l'élément
dans l'expression de gauche qui correspond à l'((index))_ donné par
l'expression entre crochets.

{{id array_indexing}}
{{index "zero-based counting"}}

Le premier indice d'un tableau est zéro, pas un. Donc le premier élément est
récupéré avec `listeDeNombres[0]`. Le comptage basé sur zéro a une longue
longue tradition dans la technologie et, d'une certaine manière, est très
logique, mais il faut s'y habituer. Considérez l'index comme le nombre
d'éléments éléments à sauter, en comptant depuis le début du tableau.

{{id properties}}

## Propriétés

{{index "Math object", "Math.max function", ["length property", "for string"], [object, property], "period character", [property, access]}}

Nous avons déjà vu quelques expressions suspectes comme `maChaine.length`.
(pour obtenir la longueur d'une chaîne) et `Math.max` (la fonction maximum)
dans les chapitres précédents. Ces expressions accèdent à une _propriété_
d'une certaine valeur. Dans le premier cas, on accède à la propriété `length`
(longueur) de la valeur de `maChaine`. Dans le second, nous accédons à la
propriété nommée `max` dans l'objet `Math` (qui est une collection de
constantes et de fonctions mathématiques).

{{index [property, access], null, undefined}}

Presque toutes les valeurs JavaScript ont des propriétés. Les exceptions sont
`null` et `undefined`. Si vous essayez d'accéder à une propriété sur l'une
de ces non-valeurs, vous obtenez une erreur.

```{test: no}
null.length;
// → TypeError: null has no properties
```

{{indexsee "dot character", "period character"}}
{{index "[] (subscript)", "period character", "square brackets", "computed property", [property, access]}}

Les deux principales façons d'accéder aux propriétés en JavaScript sont le
point et les crochets. Les expressions `valeur.x` et `valeur[x]` permettent
d'accéder à une propriété de `valeur`, mais pas nécessairement à la même
propriété. La différence réside dans la façon dont `x` est interprété.
Lorsqu'on utilise un point, le mot après le point est le nom littéral de la
propriété. Si vous utilisez des crochets, l'expression entre les crochets
est évaluée pour obtenir le nom de la propriété. Alors que `valeur.x`
récupère la propriété de `valeur` nommée "x", `valeur[x]` essaie d'évaluer
l'expression `x` et utilise le résultat, converti en chaîne, comme nom de
propriété.

Ainsi, si vous savez que la propriété qui vous intéresse s'appelle
_color_, vous dites `valeur.color`. Si vous voulez extraire la propriété
nommée par la valeur contenue dans la liaison `i`, vous dites `valeur[i]`.
Les noms de propriétés sont des chaînes de caractères. Ils peuvent être
n'importe quelle chaîne, mais la notation par points ne fonctionne qu'avec
des noms qui ressemblent à des noms de liaisons valides. Ainsi, si vous
voulez accéder à une propriété nommée _2_ ou _Jean Dupont_, vous devez utiliser
des crochets : `valeur[2]` ou `valeur["Jean Dupont"]`.

Les éléments d'un ((tableau)) sont stockés comme les propriétés du tableau, en
utilisant des nombres comme noms de propriétés. Comme vous ne pouvez pas
utiliser la notation par points avec des nombres et que vous souhaitez généralement
utiliser une liaison qui contient l'index, vous devez de toute façon utiliser
la notation entre crochets pour les atteindre.

{{index ["length property", "for array"], [array, "length of"]}}

La propriété `length` d'un tableau nous indique combien d'éléments il possède.
Ce nom de propriété est un nom de liaison valide, et nous connaissons son nom à
l'avance. Ainsi, pour trouver la longueur d'un tableau, on écrit généralement
`tableau.length` car c'est plus facile à écrire que `tableau["length"]`.

{{id methods}}

## Méthodes

{{index [function, "as property"], method, string}}

Les valeurs des chaînes et des tableaux contiennent, en plus de la
propriété `length`. un certain nombre de propriétés qui contiennent des
valeurs de fonction.

```
let doh = "Doh";
console.log(typeof doh.toUpperCase);
// → function
console.log(doh.toUpperCase());
// → DOH
```

{{index "case conversion", "toUpperCase method", "toLowerCase method"}}

Chaque chaîne a une propriété `toUpperCase`. Lorsqu'elle est appelée, elle
renvoie une copie de la chaîne dans laquelle toutes les lettres ont été
converties en majuscules. Il existe aussi la propriété `toLowerCase`, qui
va dans le sens inverse.

{{index "this binding"}}

Il est intéressant de noter que, bien que l'appel à `toUpperCase` ne passe
aucun arguments, la fonction a en quelque sorte accès à la chaîne de
caractères "Doh", la valeur dont nous avons appelé la propriété. La façon
dont cela fonctionne est décrite dans le [Chapitre ?](object#obj_methods).

Les propriétés qui contiennent des fonctions sont généralement appelées
_méthodes_ de la valeur à laquelle elles appartiennent, comme dans
"`toUpperCase` est une méthode d'une chaîne de caractères".

{{id array_methods}}

Cet exemple illustre deux méthodes que vous pouvez utiliser pour manipuler
des tableaux :

```
let sequence = [1, 2, 3];
sequence.push(4);
sequence.push(5);
console.log(sequence);
// → [1, 2, 3, 4, 5]
console.log(sequence.pop());
// → 5
console.log(sequence);
// → [1, 2, 3, 4]
```

{{index collection, array, "push method", "pop method"}}

La méthode `push` ajoute des valeurs à la fin d'un tableau, et la méthode
`pop` fait le contraire, en retirant la dernière valeur du tableau et
la retourne.

{{index ["data structure", stack]}}

Ces noms un peu ridicules sont les termes traditionnels pour les opérations
sur une _((pile))_. Une pile, dans la programmation, est une structure de
données qui vous permet d'y insérer des valeurs et de les ressortir dans
l'ordre inverse, de sorte que ce qui a été ajouté en dernier est retiré en
premier. Elles sont courantes en programmation - vous vous souvenez peut-être
de la fonction ((pile d'appel)) du [chapitre précédent](functions#stack),
qui est un exemple de la même idée.

## Objets

{{index journal, "weresquirrel example", array, record}}

Retour à l'écureuilgarou. Un ensemble d'entrées de journal quotidien peut
être représenté comme un tableau. Mais les entrées ne consistent pas seulement
en un nombre ou une chaîne de caractères, chaque entrée doit contenir une
liste d'activités et une valeur booléenne indiquant si Jacques s'est
transformé en écureuil ou non. Dans l'idéal, nous aimerions regrouper ces
valeurs en une seule valeur unique, puis placer ces valeurs groupées dans
un tableau d'entrées de journal.

{{index [syntax, object], [property, definition], [braces, object], "{} (object)"}}

Les valeurs du type _((objet))_ sont des collections arbitraires de
propriétés. L'une des façons de créer un objet est d'utiliser les accolades
comme une expression.

```
let jour1 = {
  ecureuil: false,
  evenements: ["travail", "touché arbre", "pizza", "jogging"]
};
console.log(jour1.ecureuil);
// → false
console.log(jour1.loup);
// → undefined
jour1.loup = false;
console.log(jour1.loup);
// → false
```

{{index [quoting, "of object properties"], "colon character"}}

À l'intérieur des accolades, on trouve une liste de propriétés séparées
par des virgules. Chaque propriété a un nom suivi de deux points et
d'une valeur. Lorsqu'un objet est écrit sur plusieurs lignes, l'indentation
comme dans l'exemple aide à la lisibilité. Les propriétés dont le nom
n'est pas un nom de liaison valide doivent être entouré d'accolades.

```
let descriptions = {
  travail: "Je suis allé au travail",
  "touché arbre": "J'ai touché un arbre"
};
```

{{index [braces, object]}}


Cela signifie que les accolades ont _deux_ significations en JavaScript. Sur
au début d'une ((déclaration)), elles commencent un ((bloc)) de déclarations.
Sur toute autre position, elles décrivent un objet. Heureusement, il est
rarement utile de commencer une instruction par un objet entre accolades,
l'ambiguïté entre ces deux éléments n'est pas un problème majeur.

{{index undefined}}

La lecture d'une propriété qui n'existe pas vous donnera la valeur
`undefined`.

{{index [property, assignment], mutability, "= operator"}}

Il est possible d'attribuer une valeur à une expression de propriété à
l'aide de l'opérateur `=`. Cela va remplacer la valeur de la propriété
si elle existait déjà ou créera une nouvelle propriété sur l'objet si elle
n'existait pas.

{{index "tentacle (analogy)", [property, "model of"], [binding, "model of"]}}

Pour revenir brièvement à notre modèle tentaculaire de liaisons de propriété
les liaisons sont similaires. Elles _s'emparent_ des valeurs, mais d'autres
liaisons et propriétés peuvent s'accrocher à ces mêmes valeurs. Vous pouvez
considérer les objets comme des pieuvres avec un nombre quelconque de
tentacules, chacune d'entre elles ayant un nom tatoué dessus.

{{index "delete operator", [property, deletion]}}

L'opérateur `delete` coupe un tentacule d'une telle pieuvre. Il s'agit
un opérateur unaire qui, lorsqu'il est appliqué à une propriété de l'objet,
supprimera la propriété en question de l'objet. Ce n'est pas une chose
courante à faire, mais c'est possible.

```
let unObjet = {gauche: 1, droite: 2};
console.log(unObjet.left);
// → 1
delete unObjet.gauche;
console.log(unObjet.gauche);
// → undefined
console.log("gauche" in unObjet);
// → false
console.log("droite" in unObjet);
// → true
```

{{index "in operator", [property, "testing for"], object}}

L'opérateur binaire `in`, lorsqu'il est appliqué à une chaîne de caractères
et à un objet, vous indique si cet objet possède une propriété portant ce
nom. La différence entre mettre une propriété à `undefined` et la supprimer
réellement est que, dans le premier cas, l'objet _a toujours_ la propriété
(elle n'a simplement pas de valeur très intéressante), alors que dans le
second cas la propriété n'est plus présente et `in` retournera `false`.

{{index "Object.keys function"}}

Pour connaître les propriétés d'un objet, vous pouvez utiliser la fonction
fonction `Objet.keys`. Vous lui donnez un objet, et elle retourne un tableau
de chaînes de caractères - les noms des propriétés de l'objet.

```
console.log(Objet.keys({x: 0, y: 0, z: 2}));
// → ["x", "y", "z"]
```


Il existe une fonction `Object.assign` qui copie toutes les propriétés d'un
objet dans un autre objet.

```
let objetA = {a: 1, b: 2};
Object.assign(objetA, {b: 3, c: 4});
console.log(objetA);
// → {a: 1, b: 3, c: 4}
```

{{index array, collection}}

Les tableaux ne sont donc qu'un type d'objet spécialisé dans le stockage de
séquences de choses. Si vous évaluez `typeof []`, cela donne `"object"`. Vous
pouvez les voir comme des pieuvres longues et plates avec tous leurs
tentacules en une rangée bien ordonnée, étiquetés avec des nombres.

{{index journal, "weresquirrel example"}}

Nous allons représenter le journal que Jacques tient comme un tableau d'objets.

```{test: wrap}
let journal = [
  {evenements: ["travail", "touché arbre", "pizza",
            "jogging", "television"],
   ecureuil: false},
  {evenements: ["travail", "glace", "chou-fleur",
            "lasagne", "touché arbre", "brossé dents"],
   ecureuil: false},
  {evenements: ["weekend", "vélo", "pause", "cacahuètes",
            "bière"],
   ecureuil: true},
  /* et ainsi de suite... */
];
```

## Mutabilité

Nous allons passer à la programmation proprement dite _bientôt_. D'abord,
il y a encore un peu de théorie à comprendre.

{{index mutability, "side effect", number, string, Boolean, [object, mutability]}}

Nous avons vu que les valeurs des objets peuvent être modifiées. Les types
de valeurs discutés dans les chapitres précédents, comme les nombres, les
chaînes de caractères et les booléens, sont toutes _((immuables))_ - il est
impossible de modifier les valeurs de ces types. Vous pouvez les combiner
et dériver de nouvelles valeurs à partir d'elles, mais lorsque vous prenez
une valeur de chaîne de caractères spécifique, cette valeur ne peut être modifiée.
Le texte qu'elle contient ne peut pas être modifié. Si vous avez une chaîne de
caractères qui contient " chat ", il n'est pas possible pour un autre code de
modifier un caractère de votre chaîne pour qu'elle s'écrive "rat".

Les objets fonctionnent différemment. Vous _pouvez_ modifier leurs propriétés,
ce qui fait qu'une même valeur d'objet peut avoir un contenu différent à
différents moments.

{{index [object, identity], identity, [memory, organization], mutability}}

Lorsque nous avons deux nombres, 120 et 120, nous pouvons les considérer
comme précisément le même nombre, qu'ils se réfèrent ou non aux mêmes bits
physiques. Avec les objets, il y a une différence entre avoir deux références
au même objet et le fait d'avoir deux objets différents qui contiennent les mêmes
propriétés. Considérons le code suivant :

```
let objet1 = {value: 10};
let objet2 = objet1;
let objet3 = {value: 10};

console.log(objet1 == objet2);
// → true
console.log(objet1 == objec3);
// → false

objet1.value = 15;
console.log(objet2.value);
// → 15
console.log(objet3.value);
// → 10
```

{{index "tentacle (analogy)", [binding, "model of"]}}

Les liaisons `objet1` et `objet2` saisissent le _même_ objet, c'est pourquoi
changer `objet1` change aussi la valeur de `objet2`. On dit qu'ils
ont la même _identité_. La liaison `objet3` pointe vers un objet différent,
qui contient initialement les mêmes propriétés que `objet1` mais qui vit
une vie séparée.

{{index "const keyword", "let keyword", [binding, "as state"]}}

Les liaisons peuvent également être modifiables ou constantes, mais ceci est
distinct de la façon dont leurs valeurs se comportent. Même si les valeurs
numériques ne changent pas, vous pouvez utiliser une liaison `let` pour suivre
l'évolution d'un nombre en modifiant la valeur sur laquelle pointe la liaison.
De même, bien qu'une liaison `const` d'un objet ne peut pas être modifié et
continuera à pointer sur le même objet, le _contenu_ de cet objet peut changer.

```{test: no}
const score = {visiteurs: 0, domicile: 0};
// C'est correct
score.visiteurs = 1;
// Cela n'est pas correct
score = {visitors: 1, home: 1};
```

{{index "== operator", [comparison, "of objects"], "deep comparison"}}

Lorsque vous comparez des objets avec l'opérateur `==` de JavaScript, il
compare par identité : il ne produira `vrai` que si les deux objets sont
précisément la même valeur. La comparaison d'objets différents renverra
`false`, même s'ils ont des propriétés identiques. Il n'existe pas
d'opération de comparaison "profonde" en JavaScript, qui compare les objets
par leur contenu, mais il est possible de l'écrire soi-même (ce qui est
l'un des objectifs de l'exercice) [exercices](data#exercise_deep_compare) à
la fin de ce chapitre).

## Le journal de bord du lycanthrope

{{index "weresquirrel example", lycanthropy, "addEntry function"}}

Donc, Jacques démarre son interpréteur JavaScript et met en place
l'environnement dont il a besoin pour tenir son ((journal)).

```{includeCode: true}
let journal = [];

function ajouteEntree(evenements, ecureuil) {
  journal.push({evenements, ecureuil});
}
```

{{index [braces, object], "{} (object)", [property, definition]}}

Notez que l'objet ajouté au journal a un aspect un peu bizarre. Au lieu de
de déclarer des propriétés comme `events : events`, il donne juste un nom
de propriété. C'est un raccourci qui signifie la même chose : si un nom de
propriété dans la notation en accolade n'est pas suivi d'une valeur la valeur
est prise dans la liaison portant le même nom.

Ainsi, tous les soirs à 22 heures, ou parfois le lendemain matin, après
avoir descendu de l'étagère supérieure de son bureau, Jacques enregistre
la journée.

```
ajouteEntree(["travail", "touché arbre", "pizza", "jogging",
          "television"], false);
ajouteEntree(["travail", "glace", "chou-fleur", "lasagne",
          "touché arbre", "brossé dents"], false);
ajouteEntree(["weekend", "vélo", "pause", "cacahuètes",
          "bière"], true);
```


Une fois qu'il aura assez de points de données, il a l'intention d'utiliser
les statistiques pour trouver lesquels de ces événements peuvent être liés
aux écureuils.

{{index correlation}}

La _corrélation_ est une mesure de ((dépendance)) entre les variables
statistiques. Une variable statistique n'est pas tout à fait la même chose
qu'une variable de programmation. En statistiques, vous disposez généralement
d'un ensemble de mesures, les individus, et chaque variable est mesurée
pour chaque individu. La corrélation entre les variables est généralement
exprimée sous la forme d'une valeur allant de -1 à 1. Une corrélation nulle
signifie que les variables ne sont pas liées. Une corrélation de 1 indique
que les deux variables sont parfaitement liées : si vous en connaissez une,
vous connaissez aussi l'autre. Une corrélation négative de 1 négative signifie
également que les variables sont parfaitement liées, mais qu'elles sont
opposées: quand l'une est vraie, l'autre est fausse.

{{index "phi coefficient"}}

Pour calculer la mesure de la corrélation entre deux variables booléennes,
on peut utiliser le "coefficient phi" (_ϕ_). Il s'agit d'une formule dont
est un ((tableau de fréquence)) contenant le nombre de fois que les différentes
combinaisons différentes des variables ont été observées. La sortie de la
formule est un nombre compris entre -1 et 1 qui décrit la corrélation.

Nous pourrions prendre l'événement consistant à manger de la ((pizza)) et
le placer dans une ((table de fréquence)) comme celui-ci, où chaque chiffre
indique le nombre de fois que cette combinaison est apparue dans nos mesures :

{{figure {url: "img/pizza-squirrel.svg", alt: "Eating pizza versus turning into a squirrel", width: "7cm"}}}

Si nous appelons cette table _n_, nous pouvons calculer _ϕ_ à l'aide de la formule suivante :

{{if html

<div>
<table style="border-collapse: collapse; margin-left: 1em;"><tr>
  <td style="vertical-align: middle"><em>ϕ</em> =</td>
  <td style="padding-left: .5em">
    <div style="border-bottom: 1px solid black; padding: 0 7px;"><em>n</em><sub>11</sub><em>n</em><sub>00</sub> −
      <em>n</em><sub>10</sub><em>n</em><sub>01</sub></div>
    <div style="padding: 0 7px;">√<span style="border-top: 1px solid black; position: relative; top: 2px;">
      <span style="position: relative; top: -4px"><em>n</em><sub>1•</sub><em>n</em><sub>0•</sub><em>n</em><sub>•1</sub><em>n</em><sub>•0</sub></span>
    </span></div>
  </td>
</tr></table>
</div>

if}}

{{if tex

[\begin{equation}\varphi = \frac{n_{11}n_{00}-n_{10}n_{01}}{\sqrt{n_{1\bullet}n_{0\bullet}n_{\bullet1}n_{\bullet0}}}\end{equation}]{latex}

if}}

(Si à ce stade, vous posez le livre pour vous concentrer sur un terrible
terrible flashback du cours de maths de seconde - attendez ! Je n'ai pas
l'intention de vous torturer avec des pages interminables de notations
cryptiques - il s'agit juste de cette formule pour le moment. Et même avec
celle-ci, tout ce que nous faisons est de la transformer en JavaScript).

La notation [_n_~01~]{if html}[[$n_{01}$]{latex}]{if tex} indique
le nombre de mesures pour lesquelles la première variable (écrasement) est
est fausse (0) et la deuxième variable (pizza) est vraie (1). Dans le tableau
de la pizza la valeur [_n_~01~]{if html}[[$n_{01}$]{latex}]{if tex} est 9.

La valeur [_n_~1-~]{if html}[[$n_{1\bullet}$]{latex}]{if tex} désigne
la somme de toutes les mesures où la première variable est vraie, soit 5
dans le tableau de l'exemple. De même,
[_n_~•0~]{if html}[[$n_{\bullet0}$]{latex}]{if tex} fait référence à la somme des
mesures où la deuxième variable est fausse.

{{index correlation, "phi coefficient"}}

Ainsi, pour la table de pizza, la partie au-dessus de la ligne de division
(le dividende) serait 1×76-4×9 = 40, et la partie en dessous (le diviseur)
serait la racine carrée de 5×85×10×80, ou [√340000]{if html}[[$\sqrt{340000}$]{latex}]{if tex}. Cela donne un résultat de _ϕ_ ≈
0,069, ce qui est minuscule. Manger ((pizza)) ne semble pas avoir d'influence
influence sur les transformations.

## Calculer la corrélation

{{index [array, "as table"], [nesting, "of arrays"]}}

Nous pouvons représenter un _tableau_ deux par deux en JavaScript avec un
tableau à quatre éléments (`[76, 9, 4, 1]`). Nous pouvons également utiliser
d'autres représentations, telles qu'un tableau contenant deux tableaux à
deux éléments (`[[76, 9], [4, 1]]`) ou un objet avec des noms de propriétés
comme `"11"` et `"01"`, mais le tableau plat est simple et permet de raccourcir
agréablement les expressions qui accèdent au tableau sont courtes. Nous allons
interpréter les indices du tableau comme deux-((bit)) ((nombre binaire))s,
où le chiffre le plus à gauche (le plus significatif) fait référence à la
variable écureuil et le plus à droite (le moins significatif) fait référence
à la variable de l'événement. Par exemple, le nombre binaire `10` fait
référence au cas où Jacques s'est transformé en écureuil, mais l'événement
(disons "pizza") n'a pas eu lieu. Cela s'est produit quatre fois. Et comme
le nombre binaire `10` est égal à 2 en notation décimale, nous allons
stocker ce nombre à l'indice 2 du tableau.

{{index "phi coefficient", "phi function"}}

{{id phi_function}}

Voici la fonction qui calcule le coefficient _ϕ_ à partir d'un tel tableau.
tableau :

```{includeCode: strip_log, test: clip}
function phi(tableau) {
  return (tableau[3] * tableau[0] - tableau[2] * tableau[1]) /
    Math.sqrt((tableau[2] + tableau[3]) *
              (tableau[0] + tableau[1]) *
              (tableau[1] + tableau[3]) *
              (tableau[0] + tableau[2]));
}

console.log(phi([76, 9, 4, 1]));
// → 0.068599434
```

{{index "square root", "Math.sqrt function"}}

Il s'agit d'une traduction directe de la formule _ϕ_ en JavaScript.
`Math.sqrt` est la fonction racine carrée, telle que fournie par l'objet `Math`
dans un environnement JavaScript standard. Nous devons ajouter deux champs
de la table pour obtenir des champs comme
[n~1•~]{if html}[[$n_{1\bullet}$]{latex}]{if tex} parce que les sommes des
lignes ou des colonnes ne sont pas stockées directement dans notre structure
de données.

{{index "JOURNAL data set"}}


Jacques a tenu son journal pendant trois mois. Le ((jeu de données)) résultant
est disponible dans le [coding sandbox](https://eloquentjavascript.net/code#4) pour ce chapitre[
([_https://eloquentjavascript.net/code#4_](https://eloquentjavascript.net/code#4))]{if
book}, où il est stocké dans la liaison `JOURNAL` et dans un fichier
téléchargeable [fichier](https://eloquentjavascript.net/code/journal.js).

{{index "tableFor function"}}

Pour extraire une ((table)) deux par deux pour un événement spécifique du
journal, nous devons boucler sur toutes les entrées et compter combien de fois
l'événement se produit en relation avec les transformations de l'écureuil.

```{includeCode: strip_log}
function tableauPour(evenement, journal) {
  let tableau = [0, 0, 0, 0];
  for (let i = 0; i < journal.length; i++) {
    let entree = journal[i], index = 0;
    if (entree.events.includes(evenement)) index += 1;
    if (entree.ecureuil) index += 2;
    tableau[index] += 1;
  }
  return tableau;
}

console.log(tableauPour("pizza", JOURNAL));
// → [76, 9, 4, 1]
```

{{index [array, searching], "includes method"}}

Les tableaux possèdent une méthode `includes` qui vérifie si une valeur
donnée existe dans le tableau. La fonction utilise cette méthode pour
déterminer si le nom de l'événement qui l'intéresse fait partie de la
liste des événements pour un jour donné.

{{index [array, indexing]}}

Le corps de la boucle dans `tableauPour` détermine dans quelle case de la table
chaque entrée du journal arrive, en vérifiant si l'entrée contient l'événement
spécifique qui l'intéresse et si l'événement se produit en même temps qu'un
incident d'écureuil. La boucle ajoute ensuite une entrée dans la bonne case
dans le tableau.

Nous avons maintenant les outils nécessaires pour calculer les ((corrélation))s
individuelles. La seule étape restante est de trouver une corrélation pour
chaque type d'événement enregistré et voir si quelque chose ressort.

{{id for_of_loop}}

## Boucles de tableau

{{index "for loop", loop, [array, iteration]}}

Dans la fonction `tableauPour`, il y a une boucle comme celle-ci :

```
for (let i = 0; i < JOURNAL.length; i++) {
  let entree = JOURNAL[i];
  // Do something with entry
}
```

Ce type de boucle est commun dans le JavaScript classique - passer sur des
tableaux un élément à la fois est quelque chose qui revient souvent, et pour
ce faire vous exécutez un compteur sur la longueur du tableau et choisissez
chaque élément à tour de rôle.

Il existe un moyen plus simple d'écrire de telles boucles en JavaScript
moderne.

```
for (let entree of JOURNAL) {
  console.log(`${entree.events.length} evenements.`);
}
```

{{index "for/of loop"}}

Quand une boucle `for` ressemble à ça, avec le mot `of` après une définition
de variable, elle va boucler sur les éléments de la valeur donnée après
`of`. Cela fonctionne non seulement pour les tableaux, mais aussi pour les
chaînes et certaines d'autres structures de données. Nous verrons _comment_
cela fonctionne dans le [Chapitre?](object).

{{id analysis}}

## L'analyse finale

{{index journal, "weresquirrel example", "journalEvents function"}}

Nous devons calculer une corrélation pour chaque type d'événement qui se
produit dans l'ensemble des données. Pour ce faire, nous devons d'abord
_trouver_ chaque type d'événement.

{{index "includes method", "push method"}}

```{includeCode: "strip_log"}
function evenementsJournal(journal) {
  let evenements = [];
  for (let entree of journal) {
    for (let evenement of entree.evenements) {
      if (!evenements.includes(evenement)) {
        evenements.push(evenement);
      }
    }
  }
  return evenements;
}

console.log(evenementsJournal(JOURNAL));
// → ["carotte", "exercice", "weekend", "pain", …]
```

En passant en revue tous les événements et en ajoutant ceux qui ne sont pas
déjà dans le tableau `evenements`, la fonction collecte tous les types
d'événements.

Avec cela, nous pouvons voir toutes les ((corrélation))s.

```{test: no}
for (let evenement of evenementsJournal(JOURNAL)) {
  console.log(evenement + ":", phi(tableauPour(evenement, JOURNAL)));
}
// → carotte:   0.0140970969
// → exercice: 0.0685994341
// → weekend:  0.1371988681
// → pain:   -0.0757554019
// → gateau: -0.0648203724
// et ainsi de suite...
```

La plupart des corrélations semblent être proches de zéro. Manger des
carottes, du pain, ou du gateau ne déclenche apparemment pas la
lycanthropie de l'écureuil. Cela semble se produire un peu plus souvent
le week-end. Filtrons les résultats pour ne montrer que les corrélations
supérieures à 0,1 ou inférieures à -0,1.

```{test: no, startCode: true}
for (let evenement of evenementsJournal(JOURNAL)) {
  let correlation = phi(tableauPour(evenement, JOURNAL));
  if (correlation > 0.1 || correlation < -0.1) {
    console.log(evenement + ":", correlation);
  }
}
// → weekend:        0.1371988681
// → brossé dents:  -0.3805211953
// → bonbons:        0.1296407447
// → travail:       -0.1371988681
// → spaghetti:      0.2425356250
// → lire:           0.1106828054
// → cacahuètes:     0.5902679812
```

Aha ! Il y a deux facteurs avec une ((corrélation)) qui est clairement
plus forte que les autres. Manger des ((cacahuètes)) a un fort effet
positif sur la probabilité de se transformer en écureuil, tandis que se
brosser les dents a un effet négatif significatif.

Intéressant. Essayons quelque chose.

```
for (let entree of JOURNAL) {
  if (entree.events.includes("cacahuètes") &&
     !entree.events.includes("brossé dents")) {
    entree.events.push("cacahuètes dents");
  }
}
console.log(phi(tableauPour("cacahuètes dents", JOURNAL)));
// → 1
```

C'est un résultat important. Le phénomène se produit précisément lorsque
Jacques mange des ((cacahuètes)) et ne se brosse pas les dents. Si
seulement il n'était pas flemmard de l'hygiène dentaire, il n'aurait
jamais remarqué son malheur.

Sachant cela, Jacques arrête de manger des cacahuètes et constate que
que ses transformations ne reviennent pas.

{{index "weresquirrel example"}}

Pendant quelques années, tout va bien pour Jacques. Mais à un moment donné,
il perd son emploi. Parce qu'il vit dans un pays méchant où ne pas avoir
de travail signifie ne pas avoir de services médicaux, il est obligé de
prendre un emploi dans un ((cirque)) où il se produit sous le nom de
_L'incroyable homme écureuil_, se bourrant la bouche de beurre de cacahuète
avant chaque spectacle.

Un jour, lassé de cette existence pitoyable, Jacques ne parvient pas à
reprendre sa forme humaine saute par une fissure du chapiteau du cirque et
et disparaît dans la forêt. On ne le reverra plus jamais.

## Davantage de tableaulogie

{{index [array, methods], [method, array]}}

Avant de terminer ce chapitre, je voudrais vous présenter quelques autres
concepts liés aux objets. Je vais commencer par vous présenter quelques
méthodes de tableau généralement utiles.

{{index "push method", "pop method", "shift method", "unshift method"}}


Nous avons vu `push` et `pop`, qui ajoutent et suppriment des éléments à la
à la fin d'un tableau, [plus tôt](data#array_methods) dans ce chapitre.
Les méthodes correspondantes pour ajouter et supprimer des éléments au
début d'un tableau sont appelées `unshift` et `shift`.

```
let listeDeTaches = [];
function memoriser(tache) {
  listeDeTaches.push(tache);
}
function prendTache() {
  return listeDeTaches.shift();
}
function memoriserUrgence(tache) {
  listeDeTaches.unshift(tache);
}
```

{{index "task management example"}}

Ce programme gère une file d'attente de tâches. Vous ajoutez des tâches à la
fin de la file d'attente en appelant `memoriser("courses")`, et lorsque vous
êtes prêt à faire quelque chose, vous appelez `prendTache()` pour récupérer
(et supprimer) l'élément de tête de la file d'attente. La fonction
`memoriserUrgence` ajoute également une tâche mais l'ajoute à l'avant et
non à l'arrière de la file d'attente.

{{index [array, searching], "indexOf method", "lastIndexOf method"}}

Pour rechercher une valeur spécifique, les tableaux fournissent une méthode
`indexOf`. Cette méthode recherche dans le tableau du début à la fin et renvoie
l'indice auquel la valeur demandée a été trouvée - ou -1 si elle n'a pas été
trouvée. Pour effectuer une recherche à partir de la fin plutôt que du début,
il existe une méthode similaire appelée `lastIndexOf`.

```
console.log([1, 2, 3, 2, 1].indexOf(2));
// → 1
console.log([1, 2, 3, 2, 1].lastIndexOf(2));
// → 3
```

`indexOf` et `lastIndexOf` prennent toute deux un second argument facultatif
qui indique où commencer la recherche.

{{index "slice method", [array, indexing]}}

Une autre méthode de tableau fondamentale est `slice`, qui prend les indices
de début et de fin et renvoie un tableau qui ne contient que les éléments
situés entre eux. L'indice de début est inclusif, l'indice de fin est exclusif.

```
console.log([0, 1, 2, 3, 4].slice(2, 4));
// → [2, 3]
console.log([0, 1, 2, 3, 4].slice(2));
// → [2, 3, 4]
```

{{index [string, indexing]}}

Si l'indice de fin n'est pas donné, `slice` prendra tous les éléments qui se
trouvent après l'index de début. Vous pouvez également omettre l'indice de
début pour copier le tableau entier.

{{index concatenation, "concat method"}}

La méthode `concat` peut être utilisée pour coller des tableaux ensemble pour
créer un nouveau tableau, de la même manière que l'opérateur `+` le fait pour
les chaînes de caractères.

L'exemple suivant montre les méthodes `concat` et `slice` en action. Il prend
un tableau et un index, et renvoie un nouveau tableau qui est une copie du
tableau d'origine avec l'élément à l'indice donné supprimé.

```
function retirer(tableau, index) {
  return tableau.slice(0, index)
    .concat(tableau.slice(index + 1));
}
console.log(retirer(["a", "b", "c", "d", "e"], 2));
// → ["a", "b", "d", "e"]
```

Si vous passez à `concat` un argument qui n'est pas un tableau, cette valeur
sera ajoutée au nouveau tableau comme s'il s'agissait d'un tableau à un
élément.

## Les chaines et leurs propriétés

{{index [string, properties]}}

Nous pouvons lire des propriétés comme `length` et `toUpperCase` à partir de
valeurs de chaînes de caractères. Mais si vous essayez d'ajouter une nouvelle
propriété, elle ne s'ajoute pas.

```
let kim = "Kim";
kim.age = 88;
console.log(kim.age);
// → undefined
```

Les valeurs de type chaîne de caractères, nombre et booléen ne sont pas des
objets, et bien que le langage ne se plaint pas si vous tentez de leur
attribuer de nouvelles propriétés, il ne stocke pas réellement ces propriétés.
Comme mentionné précédemment ces valeurs sont immuables et ne peuvent pas
être modifiées.

{{index [string, methods], "slice method", "indexOf method", [string, searching]}}

Mais ces types ont des propriétés intégrées. Chaque valeur de chaîne possède un
nombre de méthodes. Certaines très utiles sont `slice` et `indexOf`, qui
ressemblent aux méthodes de tableau du même nom.

```
console.log("coconuts".slice(4, 7));
// → nut
console.log("coconut".indexOf("u"));
// → 5
```


Une des différences est que le `indexOf` d'une chaîne peut rechercher une
chaîne contenant plus d'un caractère, alors que la méthode correspondante
pour les tableaux ne recherche qu'un seul élément.

```
console.log("one two three".indexOf("ee"));
// → 11
```

{{index [whitespace, trimming], "trim method"}}

La méthode `trim` supprime les espaces (espaces, nouvelles lignes, tabulations
et caractères similaires) au début et à la fin d'une chaîne.

```
console.log("  okay \n ".trim());
// → okay
```

La fonction `zeroPad` du [chapitre précédent](fonctions) existe aussi en
tant que méthode. Elle s'appelle `padStart` et prend comme arguments la
longueur souhaitée et le caractère de remplissage comme arguments.

```
console.log(String(6).padStart(3, "0"));
// → 006
```

{{id split}}

Vous pouvez séparer une chaîne sur chaque occurrence d'une autre chaîne avec
`split` et la joindre à nouveau avec `join`.

```
let phrase = "Les messagers sagittaire piétinent";
let mots = phrase.split(" ");
console.log(mots);
// → ["Les", "messagers", "sagittaire", "piétinent"]
console.log(mots.join(". "));
// → Les. messagers. sagittaire. piétinent
```

{{index "repeat method"}}

Une chaîne de caractères peut être répétée à l'aide de la méthode `repeat`,
qui crée une nouvelle chaîne de caractères contenant plusieurs copies de
la chaîne d'origine, collées entre ensemble.

```
console.log("LA".repeat(3));
// → LALALA
```

{{index ["length property", "for string"], [string, indexing]}}

Nous avons déjà vu la propriété `length` du type string. Accéder à
aux caractères individuels d'une chaîne de caractères ressemble à l'accès
aux éléments d'un tableau (avec une mise en garde que nous aborderons dans
le [chapitre ?](higher_order#code_units)).

```
let chaine = "abc";
console.log(chaine.length);
// → 3
console.log(chaine[1]);
// → b
```

{{id rest_parameters}}

## Paramètres restants

{{index "Math.max function"}}

Il peut être utile pour une fonction d'accepter un nombre quelconque
d'((argument))s. Par exemple, `Math.max` calcule le maximum de _tous_
les arguments qui lui sont donnés.

{{index "period character", "max example", spread}}

Pour écrire une telle fonction, il faut mettre trois points avant le
dernier ((paramètre) de la fonction, comme ceci :

```{includeCode: strip_log}
function max(...nombres) {
  let resultat = -Infinity;
  for (let nombre of nombres) {
    if (nombre > resultat) resultat = nombre;
  }
  return resultat;
}
console.log(max(4, 1, 9, -2));
// → 9
```

Lorsqu'une telle fonction est appelée, les _((paramètres restants))_
sont liés à un tableau contenant tous les autres arguments. S'il y a
d'autres paramètres avant lui, leurs valeurs ne font pas partie de ce
tableau. Lorsque, comme dans `max`, ils sont les seuls paramètres, il
contiendra tous les arguments.

{{index [function, application]}}

Vous pouvez utiliser une notation similaire à trois points pour _appeler_
une fonction avec un tableau d'arguments.

```
let nombres = [5, 1, 7];
console.log(max(...nombres));
// → 7
```


Cela "((étends))" le tableau dans l'appel de fonction, en passant ses
éléments comme des arguments séparés. Il est possible d'inclure un tableau
comme cela avec d'autres arguments, comme dans `max(9, ...nombres, 2)`.

{{index [array, "of rest arguments"], "square brackets"}}

La notation des tableaux entre crochets permet de la même façon à l'opérateur
triple point d'étendre un autre tableau dans le nouveau tableau.

```
let mots = ["jamais", "completement"];
console.log(["ne va", ...mots, "comprendre"]);
// → ["ne va", "jamais", "completement", "comprendre"]
```

## L'objet Math

{{index "Math object", "Math.min function", "Math.max function", "Math.sqrt function", minimum, maximum, "square root"}}

Comme nous l'avons vu, `Math` est un ensemble de fonctions utilitaires
liées aux nombres, telles que `Math.max` (maximum), `Math.min` (minimum),
et `Math.sqrt` (racine carrée).

{{index namespace, [object, property]}}

{{id namespace_pollution}}

L'objet `Math` est utilisé comme un conteneur pour regrouper un ensemble de
fonctionnalité. Il n'existe qu'un seul objet `Math`, et il n'est presque
jamais utile en tant que valeur. Il fournit plutôt un _espace de noms_ pour
que toutes ces fonctions et valeurs n'aient pas à être des liaisons globales.

{{index [binding, naming]}}

Le fait d'avoir trop de liaisons globales "pollue" l'espace de noms. Plus
le nombre de noms ont été pris, plus vous êtes susceptible d'écraser
accidentellement la valeur d'une liaison existante. Par exemple, il n'est pas
improbable de vouloir nommer quelque chose `max` dans l'un de vos programmes.
Puisque la fonction intégrée `max` de JavaScript se trouve en sécurité dans
l'objet l'objet `Math`, nous n'avons pas à nous soucier de l'écraser.

{{index "let keyword", "const keyword"}}

De nombreuses langues vous arrêteront, ou du moins vous avertiront, lorsque
vous definissez une liaison avec un nom qui est déjà pris. JavaScript vous
avertira pour les liaisons que vous avez déclarées avec `let` ou `const`
mais - paradoxalement - pas pour les liaisons standard ni pour les
liaisons déclarées avec `var` ou `function`.

{{index "Math.cos function", "Math.sin function", "Math.tan function", "Math.acos function", "Math.asin function", "Math.atan function", "Math.PI constant", cosine, sine, tangent, "PI constant", pi}}

Revenons à l'objet `Math`. Si vous avez besoin de faire de la
((trigonométrie)), `Math` peut vous aider. Il contient les fonctions `cos`
(cosinus), `sin` (sinus), et `tan`(tangente), ainsi que leurs fonctions
inverses, `acos`, `asin`, et `atan`, respectivement. Le nombre π (pi) -
ou du moins l'approximation la plus proche qui tient dans une fenêtre
JavaScript `Math.PI`. Il existe une vieille tradition de programmation qui
consiste à écrire les noms des valeurs ((constantes)) en majuscules.

```{test: no}
function pointAleatoireSurUnCercle(rayon) {
  let angle = Math.random() * 2 * Math.PI;
  return {x: rayon * Math.cos(angle),
          y: rayon * Math.sin(angle)};
}
console.log(pointAleatoireSurUnCercle(2));
// → {x: 0.3667, y: 1.966}
```

Si les sinus et les cosinus ne vous sont pas familiers, ne vous inquiétez pas.
Lorsqu'ils sont utilisés dans ce livre, dans le [Chapitre ?](dom#sin_cos), je
les expliquerai.

{{index "Math.random function", "random number"}}

L'exemple précédent utilisait `Math.random`. Il s'agit d'une fonction qui
renvoie un nouveau nombre pseudo-aléatoire compris entre zéro (inclus) et un
(exclus) à chaque fois que vous l'appelez.


```{test: no}
console.log(Math.random());
// → 0.36993729369714856
console.log(Math.random());
// → 0.727367032552138
console.log(Math.random());
// → 0.40180766698904335
```

{{index "pseudorandom number", "random number"}}

Bien que les ordinateurs soient des machines déterministes - ils réagissent
toujours de la même manière si on leur donne la même entrée, il est possible
de leur faire produire des nombres qui semblent aléatoires. Pour ce faire,
la machine garde une valeur cachée, et à chaque fois que vous demandez un
nouveau nombre aléatoire, elle effectue des calculs compliqués sur cette
valeur cachée pour créer une nouvelle valeur. Ainsi, il peut produire des
nombres toujours nouveaux et difficiles à prévoir d'une manière qui
_semble_ aléatoire.

{{index rounding, "Math.floor function"}}

Si nous voulons un nombre aléatoire entier au lieu d'un nombre fractionnaire,
nous pouvons utiliser `Math.floor` (qui arrondit à l'entier inférieur) sur
le résultat de `Math.random`.

```{test: no}
console.log(Math.floor(Math.random() * 10));
// → 2
```

En multipliant le nombre aléatoire par 10, on obtient un nombre supérieur ou
égal à 0 et inférieur à 10. Étant donné que `Math.floor` arrondit à
l'inférieur, cette expression produira, avec autant de chance, n'importe quel
nombre de 0 à 9.

{{index "Math.ceil function", "Math.round function", "Math.abs function", "absolute value"}}

Il existe également les fonctions `Math.ceil` (pour "plafond", qui arrondit
au nombre entier supérieur), `Math.round` (au nombre entier le plus proche), et
`Math.abs`, qui prend la valeur absolue d'un nombre, ce qui signifie qu'elle
positive les valeurs négatives mais laisse les valeurs positives telles quelles.

## Destructurer

{{index "phi function"}}

Revenons un instant à la fonction `phi`.

```{test: wrap}
function phi(tableau) {
  return (tableau[3] * tableau[0] - tableau[2] * tableau[1]) /
    Math.sqrt((tableau[2] + tableau[3]) *
              (tableau[0] + tableau[1]) *
              (tableau[1] + tableau[3]) *
              (tableau[0] + tableau[2]));
}
```

{{index "destructuring binding", parameter}}

L'une des raisons pour lesquelles cette fonction est difficile à lire est que
nous avons une liaison pointant vers notre tableau, mais nous préférerions de
loin avoir des liaisons pour les _éléments_ du tableau, c'est-à-dire
`let n00 = tableau[0]` et ainsi de suite. Heureusement, il existe un moyen
succinct de faire cela en JavaScript.

```
function phi([n00, n01, n10, n11]) {
  return (n11 * n00 - n10 * n01) /
    Math.sqrt((n10 + n11) * (n00 + n01) *
              (n01 + n11) * (n00 + n10));
}
```

{{index "let keyword", "var keyword", "const keyword", [binding, destructuring]}}

Cela fonctionne également pour les liaisons créées avec `let`, `var`, ou
`const`. Si vous savez que la valeur que vous liez est un tableau, vous
pouvez utiliser des ((crochets)) pour "regarder à l'intérieur" de la valeur
et lier son contenu.

{{index [object, property], [braces, object]}}

Une astuce similaire fonctionne pour les objets, en utilisant des accolades
au lieu des crochets.

```
let {nom} = {nom: "Faraji", age: 23};
console.log(nom);
// → Faraji
```

{{index null, undefined}}

Notez que si vous essayez de déstructurer `null` ou `undefined`, vous obtenez
une erreur, tout comme si vous essayiez d'accéder directement à une propriété
de ces valeurs.

## JSON

{{index [array, representation], [object, representation], "data format", [memory, organization]}}

Parce que les propriétés ne font que saisir leur valeur, au lieu de la
contenir, les objets et les tableaux sont stockés dans la mémoire de
l'ordinateur en tant que séquences de bits contenant les _((adresses))_ -
l'emplacement en mémoire - de leur contenu. Ainsi, un tableau avec un autre
tableau à l'intérieur consiste en (au moins) une région de mémoire pour
le tableau interne, et d'une autre pour le tableau externe, contenant
(entre autres) un nombre binaire qui représente la position du tableau
interne.

Si vous souhaitez enregistrer des données dans un fichier pour les consulter
ultérieurement ou les envoyer à un autre ordinateur sur le réseau, vous devez
d'une manière ou d'une autre convertir ces enchevêtrements d'adresses mémoire
en une description qui peut être stockée ou envoyée. Vous pourriez envoyer
la totalité de la mémoire de votre ordinateur avec l'adresse de la valeur qui
vous intéresse, je suppose, mais cela ne semble pas être la meilleure approche.

{{indexsee "JavaScript Object Notation", JSON}}

{{index serialization, "World Wide Web"}}

Ce que nous pouvons faire, c'est _sérialiser_ les données. Cela signifie
qu'elles sont converties en une description plate. Un format de sérialisation
populaire est appelé _((JSON))_ (prononcez "Jason"), qui signifie
JavaScript Object Notation. Il est largement utilisé comme format de stockage
et de communication de données sur le Web, même dans des langages autres
que JavaScript.

{{index [array, notation], [object, creation], [quoting, "in JSON"], comment}}

JSON ressemble à la façon dont JavaScript écrit les tableaux et les objets,
avec quelques restrictions. Tous les noms de propriétés doivent être entourés
de guillemets doubles, et seules les expressions de données simples sont
autorisées, pas d'appels de fonctions, de liaisons, ou quoi que ce soit qui
implique des calcul. Les commentaires ne sont pas autorisés dans JSON.

Une entrée de journal peut ressembler à ceci lorsqu'elle est représentée
sous forme de données JSON :

```{lang: "application/json"}
{
  "ecureuil": false,
  "evenements": ["travail", "touché arbre", "pizza", "jogging"]
}
```

{{index "JSON.stringify function", "JSON.parse function", serialization, deserialization, parsing}}

JavaScript nous donne les fonctions `JSON.stringify` et `JSON.parse` pour
convertir les données depuis et vers ce format. La première prend une valeur
JavaScript et renvoie une chaîne encodée en JSON. La seconde prend une telle
chaîne et la convertit en la valeur qu'elle encode.

```
let chaine = JSON.stringify({ecureuil: false,
                             evenement: ["weekend"]});
console.log(chaine);
// → {"ecureuil":false,"evenement":["weekend"]}
console.log(JSON.parse(chaine).evenement);
// → ["weekend"]
```

## Résumé

Les objets et les tableaux (qui sont un type spécifique d'objet) fournissent
des moyens de regrouper plusieurs valeurs en une seule. D'un point de vue
conceptuel, cela permet de mettre un tas d'objets connexes dans un sac et
de se promener avec le sac, au lieu d'enrouler nos bras autour de choses
individuelles et d'essayer de s'y accrocher séparément.

La plupart des valeurs en JavaScript ont des propriétés, les exceptions
étant `null` et `undefined`. On accède aux propriétés en utilisant
`valeur.prop` ou `valeur["prop"]`. Les objets ont tendance à utiliser des
noms pour leurs propriétés et stockent plus ou moins un ensemble fixe
d'entre elles. Les tableaux, par contre, contiennent généralement des
quantités variables de valeurs conceptuellement identiques et utilisent
des nombres (en commençant par 0) comme noms de leurs propriétés.

Il y a des propriétés nommées dans les tableaux, telles que `length` et
un certain nombre de méthodes. Les méthodes sont des fonctions qui vivent
dans les propriétés et (généralement) agissent sur la valeur dont elles
sont une propriété.

Vous pouvez itérer sur des tableaux en utilisant un type spécial de
boucle `for` - `for (let élément du tableau)`.

## Exercices

### La somme d'une série

{{index "summing (exercise)"}}

L'[introduction](intro) de ce livre faisait allusion à ce qui suit comme une
comme une bonne façon de calculer la somme d'une série de nombres :

```{test: no}
console.log(sum(serie(1, 10)));
```

{{index "range function", "sum function"}}

Ecrivez une fonction `serie` qui prend deux arguments, `début` et `fin`,
et retourne un tableau contenant tous les nombres de `début` jusqu'à
(et incluant) `fin`.

Ensuite, écrivez une fonction `somme` qui prend un tableau de nombres et
renvoie la somme de ces nombres. Exécutez le programme d'exemple et voyez
s'il renvoie effectivement 55.

{{index "optional argument"}}

En guise de devoir bonus, modifiez votre fonction `serie` pour qu'elle
prenne un troisième argument facultatif qui indique la valeur du pas
utilisée lors de l'exécution de la fonction et de la construction du tableau.
Si aucun pas n'est donné, les éléments sont incrémentés par incréments de
un, ce qui correspond à l'ancien comportement. L'appel de la fonction
`serie(1, 10, 2)` devrait retourner `[1, 3, 5, 7, 9]`. Assurez-vous qu'elle
fonctionne également avec des valeurs de pas négatives, de sorte que
`serie(5, 2, -1)` produise `[5, 4, 3, 2]`.

{{if interactive

```{test: no}
// Votre code ici.

console.log(serie(1, 10));
// → [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
console.log(serie(5, 2, -1));
// → [5, 4, 3, 2]
console.log(somme(serie(1, 10)));
// → 55
```

if}}

{{hint

{{index "summing (exercise)", [array, creation], "square brackets"}}

La construction d'un tableau se fait le plus facilement en initialisant
d'abord une liaison à `[]` (un tableau frais et vide) et en appelant de
façon répétée sa méthode `push` pour ajouter une valeur. N'oubliez pas de
retourner le tableau à la fin de la fonction.

{{index [array, indexing], comparison}}

Comme la limite de fin est inclusive, vous devrez utiliser l'opérateur `<=`
plutôt que `<` pour vérifier la fin de votre boucle.

{{index "arguments object"}}

Le paramètre step peut être un paramètre optionnel qui prend la valeur par
défaut (en utilisant l'opérateur `=`) à 1.

{{index "range function", "for loop"}}

La meilleure façon de faire en sorte que `serie` comprenne des valeurs de pas
négatives est probablement d'écrire deux boucles séparées - une pour compter
vers le haut et une autre pour compter vers le bas parce que la comparaison
qui vérifie que la boucle est terminée doit être doit être `>=` plutôt que
`<=` lors du décompte.

Il peut également être intéressant d'utiliser un pas par défaut différent,
à savoir -1, lorsque la fin de l'intervalle est plus petite que le début.
De cette façon, `serie(5, 2)` renvoie quelque chose de significatif, plutôt
que de rester coincé dans une ((boucle infinie)). Il est possible de faire
référence à des paramètres dans la valeur par défaut d'un paramètre.

hint}}

### Inverser un tableau

{{index "reversing (exercise)", "reverse method", [array, methods]}}

Les tableaux ont une méthode `reverse` qui modifie le tableau en
inversant l'ordre d'apparition de ses éléments. Pour cet exercice,
écrivez deux fonctions, `inverseTableau` et `inverseTableauEnPlace`. La
première, `inverseTableau`, prend un tableau comme argument et produit
un _nouveau_ tableau qui contient les mêmes éléments dans l'ordre inverse.
La seconde, `inverseTableauEnPlace`, fait ce que la méthode `reverse`
fait : elle _modifie_ le tableau donné en argument en inversant ses
éléments. Ni l'une ni l'autre ne peut utiliser la méthode standard
`reverse`.

{{index efficiency, "pure function", "side effect"}}

En repensant aux notes sur les effets de bord et les fonctions pures dans
le [chapitre précédent](functions#pure), quelle variante devrait selon vous être
être utile dans plus de situations ? Laquelle fonctionne le plus rapidement ?

{{if interactive

```{test: no}
// Votre code ici.

console.log(inverseTableau(["A", "B", "C"]));
// → ["C", "B", "A"];
let tableau = [1, 2, 3, 4, 5];
inverseTableauEnPlace(tableau);
console.log(tableau);
// → [5, 4, 3, 2, 1]
```

if}}

{{hint

{{index "reversing (exercise)"}}

Il y a deux façons évidentes d'implémenter `inverseTableau`. La première
consiste à parcourir le tableau d'entrée d'avant en arrière et d'utiliser
la méthode `unshift` sur le nouveau tableau pour insérer chaque élément à
son début. La seconde est de boucler sur le tableau d'entrée en arrière
et d'utiliser la méthode `push`. L'itération sur un tableau à l'envers
nécessite une spécification `for`, comme
`(let i = array.length - 1 ; i >= 0 ; i--)`.

{{index "slice method"}}

Inverser le réseau en place est plus difficile. Vous devez faire attention
à ne pas écraser des éléments dont vous aurez besoin plus tard. L'utilisation
de `inverseTableau` ou copier l'ensemble du tableau (`array.slice(0)` est
une bonne manière de copier un tableau) fonctionne mais c'est de la triche.

L'astuce consiste à _échanger_ le premier et le dernier élément, puis le
second et l'avant-dernier, et ainsi de suite. Vous pouvez le faire en bouclant
sur la moitié de la longueur du tableau (utilisez `Math.floor` pour arrondir à
l'inférieur - vous n'avez pas besoin de toucher l'élément central d'un tableau
avec un nombre impair d'éléments) et en échangeant l'élément à la position
`i` avec celui à la position `array.length - 1 - i`. Vous pouvez utiliser une
liaison locale pour conserver brièvement l'un des éléments, remplacer cet
élément par son image miroir, puis placer la valeur de la liaison locale
à l'emplacement où se trouvait l'image miroir.

hint}}

{{id list}}

### A list

{{index ["data structure", list], "list (exercise)", "linked list", array, collection}}

Les objets, en tant que blobs génériques de valeurs, peuvent être utilisés pour
construire toutes sortes de structures de données. Une structure de données
commune est la _liste_ (à ne pas confondre avec le tableau). Une liste est un
ensemble imbriqué d'objets, le premier objet faisant référence au second, le
second au premier objet contenant une référence au second, le second au
troisième, et ainsi de suite.

```{includeCode: true}
let liste = {
  valeur: 1,
  reste: {
    valeur: 2,
    reste: {
      valeur: 3,
      reste: null
    }
  }
};
```

Les objets résultants forment une chaîne, comme ceci :

{{figure {url: "img/linked-list.svg", alt: "A linked list",width: "8cm"}}}

{{index "structure sharing", [memory, structure sharing]}}

Ce qui est bien avec les listes, c'est qu'elles peuvent partager des parties
de leur structure. Par exemple, si je crée deux nouvelles valeurs
`{valeur : 0, reste : liste}` et `{valeur : -1, reste : liste}` (avec `list`
faisant référence à la liaison définie précédemment), ce sont toutes deux des
listes indépendantes, mais elles partagent la structure qui constitue leurs
trois derniers éléments. La liste originale est toujours une liste valide à
trois éléments.

Ecrivez une fonction `tableauVersListe` qui construit une structure de liste
telle que celle montrée lorsqu'on lui donne `[1, 2, 3]` comme argument.
Ecrivez aussi une fonction `listeVersTableau` qui produit un tableau à partir
d'une liste. Ensuite, ajoutez une fonction d'aide `prepend`, qui prend un
élément et une liste et crée une nouvelle liste en ajoutant l'élément au début
de la liste d'entrée, et `nieme`, qui prend une liste et un nombre et retourne
l'élément qui se trouve à la position donnée dans la liste (zéro faisant
référence au premier élément) ou `undefined` si cet élément n'existe pas.

{{index recursion}}

Si vous ne l'avez pas encore fait, écrivez aussi une version récursive de `nieme`.

{{if interactive

```{test: no}
// Votre code ici.

console.log(tableauVersListe([10, 20]));
// → {value: 10, rest: {value: 20, rest: null}}
console.log(listeVersTableau(arrayToList([10, 20, 30])));
// → [10, 20, 30]
console.log(prepend(10, prepend(20, null)));
// → {value: 10, rest: {value: 20, rest: null}}
console.log(nieme(tableauVersListe([10, 20, 30]), 1));
// → 20
```

if}}

{{hint

{{index "list (exercise)", "linked list"}}

La construction d'une liste est plus facile lorsqu'elle est faite d'arrière en
avant. Ainsi, `tableauVersListe` pourrait itérer sur le tableau à l'envers
(voir l'exercice précédent) et, pour chaque élément, ajouter un objet à la
liste. Vous pouvez utiliser une liaison locale pour contenir la partie de la
liste qui a été construite jusqu'ici et utiliser une affectation
comme `liste = {valeur : X, reste : liste}` pour ajouter un élément.

{{index "for loop"}}

Pour parcourir une liste (dans `listeVersTableau` et `nieme`), une
spécification de boucle `for` comme celle-ci peut être utilisée :

```
for (let noeud = liste; noeud; noeud = noeud.reste) {}
```

Vous voyez comment ça marche ? À chaque itération de la boucle, `noeud`
pointe vers la sous-liste courante, et le corps peut lire sa propriété
`valeur` pour pour obtenir l'élément courant. A la fin d'une itération,
`noeud` passe à la sous-liste suivante. Lorsque cette dernière est nulle,
nous avons atteint la fin de la liste, et la boucle est terminée.

{{index recursion}}

La version récursive de `nieme` va, de la même manière, regarder une partie
de plus en plus petite de la "queue" de la liste et en même temps compter vers
le bas pour alors renvoyer la propriété `valeur` du noeud qu'il regarde. Pour
obtenir le zeroieme d'une liste, il suffit de prendre la propriété `valeur`
de son noeud de tête. Pour obtenir l'élément _N_ + 1, vous prenez
le *N* ième élément de la liste qui se trouve dans la propriété `rest` de
cette liste.

hint}}

{{id exercise_deep_compare}}

### Comparaison profonde

{{index "deep comparison (exercise)", [comparison, deep], "deep comparison", "== operator"}}

L'opérateur `==` compare les objets par identité. Mais parfois, vous
préférer comparer les valeurs de leurs propriétés réelles.

Ecrivez une fonction `profondementEgal` qui prend deux valeurs et retourne
vrai seulement s'il s'agit de la même valeur ou d'objets ayant les mêmes
propriétés, et dans ce cas si les valeurs des propriétés sont égales
lorsqu'elles sont comparées avec un appel récursif à `profondementEgal`.

{{index null, "=== operator", "typeof operator"}}

Pour savoir si les valeurs doivent être comparées directement (utilisez
l'opérateur `===`) ou si leurs propriétés doivent être comparées, vous
pouvez utiliser l'opérateur `typeof`. S'il produit `"object"` pour les
deux valeurs, vous devez effectuer une comparaison approfondie. Mais vous
devez tenir compte d'une exception stupide: à cause d'un accident historique,
`typeof null` produit aussi "object".

{{index "Object.keys function"}}

La fonction `Object.keys` vous sera utile lorsque vous aurez besoin de passer
en revue les propriétés des objets pour les comparer.

{{if interactive

```{test: no}
// Votre code ici.

let obj = {voici: {donc: "un"}, objet: 2};
console.log(profondementEgal(obj, obj));
// → true
console.log(profondementEgal(obj, {donc: "un", objet: 2}));
// → false
console.log(profondementEgal(obj, {voici: {donc: "un"}, objet: 2}));
// → true
```

if}}

{{hint

{{index "deep comparison (exercise)", [comparison, deep], "typeof operator", "=== operator"}}

Votre test pour savoir si vous avez affaire à un objet réel ressemblera à
quelque chose comme `typeof x == "object" && x != null`. Faites attention à
comparer des propriétés uniquement lorsque _les deux_ arguments sont des
objets. Dans tous les autres cas, vous pouvez simplement renvoyer le résultat
de l'application de `===`.

{{index "Object.keys function"}}

Utilisez `Object.keys` pour passer en revue les propriétés. Vous devez tester
si les deux objets possèdent le même ensemble de noms de propriétés et si ces
propriétés ont des valeurs identiques. Une façon de le faire est de s'assurer
que les deux objets ont le même nombre de propriétés (la longueur des listes
de propriétés est la même). Ensuite, lorsque vous effectuez une boucle sur
l'une des propriétés de l'objet pour les comparer, vérifiez toujours d'abord
que l'autre objet possède effectivement une propriété de ce nom. S'ils ont
le même nombre de propriétés et que toutes les propriétés de l'un existent
aussi dans l'autre, ils ont le même ensemble de propriétés.

{{index "return value"}}

La meilleure façon de renvoyer la valeur correcte de la fonction est de
retourner immédiatement false lorsqu'une erreur est détectée et en
retournant vrai à la fin de la fonction.

hint}}

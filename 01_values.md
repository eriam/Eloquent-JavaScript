{{meta {docid: values}}}

# Valeurs Types et Opérateurs

{{quote {author: "Master Yuan-Ma", title: "The Book of Programming", chapter: true}

Sous la surface de la machine, le programme se déplace. Sans effort, il se
dilate et se contracte. Dans une grande harmonie, les électrons se dispersent et
se regroupent. Les formes sur l'écran ne sont que des ondulations sur l'eau.
L'essence reste invisiblement en dessous.

quote}}

{{index "Yuan-Ma", "Book of Programming"}}

{{figure {url: "img/chapter_picture_1.jpg", alt: "Picture of a sea of bits", chapter: framed}}}

{{index "binary data", data, bit, memory}}

Dans le monde de l'ordinateur, il n'y a que des données. Vous pouvez lire
des données, modifier des données, créer de nouvelles données, mais ce qui
n'est pas des données ne peut pas être être mentionné. Toutes ces données
sont stockées sous forme de longues séquences de bits et sont donc  
fondamentalement identiques.

{{index CD, signal}}

Les _bits_ sont des éléments à deux valeurs, généralement décrits comme des
zéros et des uns. À l'intérieur de l'ordinateur, ils prennent la forme d'une
charge électrique élevée ou faible, un signal fort ou faible, ou une tache
brillante ou terne sur la surface d'un CD. Tout élément d'information discret
peut être réduit à une séquence de zéros et de uns et donc représentée par
des bits.

{{index "binary number", radix, "decimal number"}}

Par exemple, nous pouvons exprimer le nombre 13 en bits. Cela fonctionne de la
même manière qu'en numération décimale, mais au lieu de 10 ((chiffres))
différents, vous n'en avez que 2, et le poids de chacun d'eux augmente d'un
facteur 2 de la droite vers la gauche. Voici les bits qui composent le nombre
13, avec les poids des chiffres indiqués en dessous.

```{lang: null}
   0   0   0   0   1   1   0   1
 128  64  32  16   8   4   2   1
```

Il s'agit donc du nombre binaire 00001101. Ses chiffres non nuls représentent
8, 4, et 1, et donnent un total de 13.

## Valeurs

{{index [memory, organization], "volatile data storage", "hard drive"}}

Imaginez une mer de bits - un océan de bits. Un ordinateur moderne typique
possède plus de 30 milliards de bits dans sa mémoire volatile (mémoire de
travail). Le stockage non-volatile (le disque dur ou équivalent) a tendance
à disposer de quelques ordres de grandeur supplémentaires.

Pour pouvoir travailler avec de telles quantités de bits sans se perdre,
nous devons les séparer en morceaux qui représentent des éléments d'information.
Dans un environnement JavaScript, ces morceaux sont appelés _((valeur))s_.
Bien que toutes les valeurs soient constituées de bits, elles jouent des rôles différents. Chaque valeur possède un ((type)) qui détermine son rôle. Certaines
valeurs sont des nombres, certaines sont des morceaux de texte, certaines
sont des fonctions, et ainsi de suite.

{{index "garbage collection"}}

Pour créer une valeur, il suffit d'invoquer son nom. C'est pratique. Vous
n'avez pas besoin de rassembler des matériaux de construction pour vos valeurs
ou de les payer. Il vous suffit d'en demander une, et _boum_, vous l'avez.
Elles ne sont pas vraiment créées de toutes pièces, bien sûr. Chaque valeur
doit être stockée quelque part, et si vous voulez en utiliser une quantité
gigantesque en même temps, vous risquez de manquer de mémoire. Heureusement,
ce n'est un problème que si vous avez besoin de toutes les valeurs
simultanément. Dès que vous n'utilisez, elle se dissipe, laissant derrière
elle ses bits qui seront recyclés comme matériau de construction pour la
prochaine génération de valeurs.

Ce chapitre présente les éléments atomiques des programmes JavaScript,
c'est-à-dire les types de valeurs simples et les opérateurs qui peuvent agir
sur ces valeurs.

## Nombres

{{index [syntax, number], number, [number, notation]}}


Les valeurs du type _number_ sont, sans surprise, des valeurs numériques. Dans
un programme JavaScript, elles s'écrivent comme suit :

```
13
```

{{index "binary number"}}

Utilisez-le dans un programme, et il fera en sorte que le modèle binaire pour
le nombre 13 existe dans la mémoire de l'ordinateur.

{{index [number, representation], bit}}

JavaScript utilise un nombre fixe de bits, 64, pour stocker une valeur
numérique unique. Il n'y a qu'un nombre limité de motifs que vous pouvez
faire avec 64 bits, ce qui signifie que le nombre de nombres différents qui
peuvent être représentés est limité. Avec _N_ ((chiffre)) décimaux, vous pouvez représenter 10^N^ nombres. De même, avec 64 chiffres binaires chiffres
binaires, vous pouvez représenter 2^64^ nombres différents, soit environ 18
quintillion (un 18 suivi de 18 zéros). C'est beaucoup.

Autrefois, la mémoire des ordinateurs était beaucoup plus petite, et les gens
avaient tendance à utiliser groupes de 8 ou 16 bits pour représenter leurs
nombres. Il était facile de dépasser accidentellement de si petits
nombres ( _((overflow))_) - pour se retrouver avec un nombre qui ne tenait
pas dans le nombre de bits donné. Aujourd'hui, même les ordinateurs qui
tiennent dans la poche ont beaucoup de mémoire, donc vous êtes libre d'utiliser
des blocs de 64 bits, et vous n'avez à vous soucier du dépassement de capacité
que lorsque vous traitez avec des nombres vraiment astronomiques.

{{index sign, "floating-point number", "sign bit"}}

Cependant tous les nombres entiers inférieurs à 18 quintillions ne rentrent
pas dans un nombre JavaScript. Ces bits stockent également les nombres
négatifs, donc un bit indique le signe du nombre. Un problème plus important
est que les nombres non entiers (à virgules) doivent également être représentés.
Pour ce  faire, certains des bits sont utilisés pour stocker la position de
la virgule. Le nombre entier maximal réel qui peut être stocké est plutôt de
l'ordre de 9 quadrillions (15 zéros), ce qui reste agréablement énorme.

{{index [number, notation], "fractional number"}}

Les nombres fractionnaires s'écrivent à l'aide d'un point.

```
9.81
```

{{index exponent, "scientific notation", [number, notation]}}

Pour les très grands ou très petits nombres, vous pouvez également utiliser
la notation scientifique en ajoutant un _e_ (pour _exponent_) suivi de
l'exposant du nombre.

```
2.998e8
```

Il s'agit de 2.998 × 10^8^ = 299,800,000.

{{index pi, [number, "precision of"], "floating-point number"}}

Les calculs avec des nombres entiers (également appelés _((integer))s_) plus
petits que les 9 quadrillions mentionnés sont garantis d'être toujours
précis. Malheureusement, les calculs avec des nombres fractionnaires ne
le sont généralement pas. Tout comme π (pi) ne peut pas être exprimé
précisément par un nombre fini de chiffres décimaux, de nombreux nombres
perdent un peu de précision lorsque seuls 64 bits sont disponibles pour
les stocker. C'est dommage, mais cela pose des problèmes pratiques que dans
des situations spécifiques. L'important est d'en être conscient et de traiter
les nombres numériques fractionnaires comme des approximations, et non comme
des valeurs précises.

### Arithmétique

{{index [syntax, operator], operator, "binary operator", arithmetic, addition, multiplication}}

La principale chose à faire avec les nombres est l'arithmétique. Les opérations arithmétiques telles que l'addition ou la multiplication prennent deux valeurs numériques et produisent un nouveau nombre à partir de celles-ci. Voici à quoi
elles ressemblent en JavaScript :

```
100 + 4 * 11
```

{{index [operator, application], asterisk, "plus character", "* operator", "+ operator"}}

Les symboles `+` et `*` sont appelés _opérateurs_. Le premier représente
l'addition, et le second la multiplication. En plaçant un opérateur
entre deux valeurs, il sera appliqué à ces valeurs et produira une nouvelle
valeur.

{{index grouping, parentheses, precedence}}

Mais l'exemple signifie-t-il "additionner 4 et 100, et multiplier le résultat par 11,"
ou la multiplication se fait-elle avant l'addition ? Comme vous l'avez peut-être
deviné, la multiplication se fait en premier. Mais comme en mathématiques, vous pouvez changer cela en mettant l'addition entre parenthèses.

```
(100 + 4) * 11
```

{{index "hyphen character", "slash character", division, subtraction, minus, "- operator", "/ operator"}}

Pour la soustraction, il y a l'opérateur `-`, et la division peut être faite
avec l'opérateur `/`.

Lorsque les opérateurs apparaissent ensemble sans parenthèses, l'ordre dans
lequel ils sont  appliqués est déterminé par la _((précédence))_ des opérateurs.
L'exemple montre que la multiplication précède l'addition. L'opérateur `/` a
la même précédence que `*`. De même, pour `+` et `-`. Lorsque plusieurs
opérateurs ayant la même précédence sont appliqués, comme dans `1 - 2 + 1`, ils
sont appliqués de gauche à droite : `(1 - 2) + 1`.

Ne vous souciez pas trop des règles de précédence. En cas de doute, il suffit
d'ajouter des parenthèses.

{{index "modulo operator", division, "remainder operator", "% operator"}}

Il existe un autre opérateur arithmétique, que vous ne reconnaîtrez peut-être
pas immédiatement. Le symbole `%` est utilisé pour représenter l'opération
_reste_. `X % Y` est le reste de la division de `X` par `Y`. Par exemple,
`314 % 100` donne `14`, et `144 % 12` donne `0`.
La précédence de l'opérateur de reste est la même que celle de la
multiplication et de la division. Vous verrez aussi souvent cet opérateur
désigné par le terme _modulo_.

### Nombres spéciaux

{{index [number, "special values"]}}

Il existe trois valeurs spéciales en JavaScript qui sont considérées comme
des nombres mais qui ne se comportent pas comme des nombres normaux.

{{index infinity}}

Les deux premières sont `Infinity` et `-Infinity`, qui représentent l'infini
positif et l'infini négatif. `Infinity - 1` est toujours `Infinity`,
et ainsi de suite. Ne faites pas trop confiance au calcul basé sur l'infini,
cependant. Ce n'est pas mathématiquement correct, et cela vous mènera
rapidement au prochain nombre spécial : `NaN`.

{{index NaN, "not a number", "division by zero"}}

`NaN` signifie "not a number" (pas un nombre), même s'il _est_ une valeur
de type nombre. Vous obtiendrez ce résultat lorsque, par exemple, vous
essayez de calculer `0 / 0` (zéro divisé par zéro), `Infini - Infini`, ou
encore toute autre opération numérique qui ne donne pas de résultat
significatif.

## Chaînes de caractères

{{indexsee "grave accent", backtick}}

{{index [syntax, string], text, character, [string, notation], "single-quote character", "double-quote character", "quotation mark", backtick}}

Le type de données de base suivant est la _((chaîne de caractère))_. Les
chaînes de caractères sont utilisées pour représenter du texte. Elles sont
écrites en mettant leur contenu entre guillemets.

```
`Down on the sea`
"Lie on the ocean"
'Float on the ocean'
```


Vous pouvez utiliser des guillemets simples, doubles ou inversés pour marquer
les chaînes de caractères, à condition que les guillemets au début et à la
fin de la chaîne de caractères correspondent.

{{index "line break", "newline character"}}

Presque tout peut être mis entre guillemets, et JavaScript en fera une
valeur de chaîne de caractères. Mais quelques caractères sont plus difficiles.
Vous pouvez imaginer comment mettre des guillemets entre guillemets peut
être difficile. Les _retours a la ligne_ (les caractères que vous obtenez
lorsque vous appuyez sur [enter]{keyname}) peuvent être incluses sans
échappement uniquement lorsque la chaîne est citée avec des guillemets inversés.
(`` ` ``).

{{index [escaping, "in strings"], ["backslash character", "in strings"]}}

Pour permettre d'inclure de tels caractères dans une chaîne, la notation
suivante est utilisée suivante : chaque fois qu'une barre oblique inverse
(`\`) se trouve à l'intérieur d'un texte texte entre guillemets, cela
signifie que le caractère qui le suit a une sinigifcation spéciale. C'est
ce qu'on appelle l'_échappement_ du caractère. Un guillemet qui est
précédée d'une barre oblique inverse ne terminera pas la chaîne de caractères
mais en fera partie. Lorsqu'un caractère `n` apparaît après une barre oblique
inverse, il est interprété comme une nouvelle ligne. De même, un `t` après
une barre oblique inverse signifie un ((caractère de tabulation)).
Prenons la chaîne suivante :

```
"Voila la première ligne\nEt la seconde"
```

Le texte contenu est le suivant :

```{lang: null}
Voila la première ligne
Et la seconde
```

Il y a, bien sûr, des situations où vous voulez qu'une barre oblique inverse
dans une soit juste une barre oblique inversée, et non un code spécial. Si
deux barres obliques inversées se suivent, elles fusionneront et il n'en
restera qu'une seule dans la chaîne de caractères résultante. C'est ainsi que
la chaîne de caractères "_Un caractère de nouvelle ligne
s'écrit comme `"`\n`"`._" peut être exprimée :

```
"Un caractère de nouvelle ligne s'écrit comme \"\\n\"."
```

{{id unicode}}

{{index [string, representation], Unicode, character}}

Les chaînes de caractères, elles aussi, doivent être modélisées comme une
série de bits pour pouvoir exister dans l'ordinateur. La façon dont JavaScript
fait cela est basée sur la norme _((Unicode))_. Cette norme attribue un
numéro à pratiquement tous les caractères dont vous pourriez avoir besoin,
y compris les caractères du grec, de l'arabe, du japonais, de l'arménien,
et ainsi de suite. Si nous avons un numéro pour chaque caractère, une chaîne
de caractères peut être décrite par une séquence de nombres.

{{index "UTF-16", emoji}}

Et c'est ce que fait JavaScript. Mais il y a une complication : la
représentation de JavaScript utilise 16 bits par élément de chaîne, qui peut
décrire jusqu'à 2^16^ caractères différents. Mais Unicode définit plus de
caractères que cela - environ deux fois plus, à ce stade. Ainsi, certains
caractères, tels que de nombreux emoji, occupent deux "positions de caractères"
dans les chaînes JavaScript. Nous reviendrons sur ce point au [chapitre
?](higher_order#code_units).

{{index "+ operator", concatenation}}

Les chaînes de caractères ne peuvent pas être divisées, multipliées ou
soustraites, mais l'opérateur "+" peut être utilisé sur elles. Il n'ajoute
pas, mais il _colle_ deux chaînes de caractères ensemble. La ligne suivante
produira la chaîne `"concaténer"` :

```
"con" + "cat" + "é" + "ner"
```

Les chaînes de caractères ont un certain nombre de fonctions associées
(_méthodes_) qui peuvent être utilisées pour effectuer d'autres opérations
sur elles.  J'en dirai plus dans le [Chapitre ?](data#methods).

{{index interpolation, backtick}}

Les chaînes de caractères écrites avec des guillemets simples ou doubles
se comportent presque de la même manière. La seule différence réside dans
le type de guillemet que vous devez échapper à l'intérieur de celles-ci.
Les chaînes de caractères entre guillemets inversés, généralement appelées
_((template literals))_, ont des capacités supplémentaires. Outre la
possibilité de s'étendre sur plusieurs lignes, elles peuvent également
intégrer d'autres valeurs.

```
`la moitié de 100 est ${100 / 2}`
```

Lorsque vous écrivez quelque chose à l'intérieur de `${}` dans un template
literals, son résultat sera calculé, converti en une chaîne de caractères,
et inclus à cette position. L'exemple produit "_la moitié de 100 est 50_".

## Opérateurs unaires

{{index operator, "typeof operator", type}}

Tous les opérateurs ne sont pas des symboles. Certains s'écrivent comme des
mots. Un exemple est l'opérateur `typeof`, qui produit une chaîne de
caractères désignant le type de la valeur que vous lui donnez.

```
console.log(typeof 4.5)
// → number
console.log(typeof "x")
// → string
```

{{index "console.log", output, "JavaScript console"}}

{{id "console.log"}}

Nous utiliserons `console.log` dans le code d'exemple pour indiquer que
nous voulons voir le résultat de l'évaluation de quelque chose. Plus
d'informations à ce sujet dans le [prochain chapitre] (program_structure).

{{index negation, "- operator", "binary operator", "unary operator"}}

Les autres opérateurs présentés opèrent tous sur deux valeurs, mais `typeof`
n'en prend qu'une seule. Les opérateurs qui utilisent deux valeurs sont appelés opérateurs _binaires_ tandis que ceux qui n'en prennent qu'une sont appelés
opérateurs _unaires_. L'opérateur moins peut être utilisé à la fois comme
opérateur binaire et comme opérateur unaire.

```
console.log(- (10 - 2))
// → -8
```

## Valeurs booléennes

{{index Boolean, operator, true, false, bit}}


Il est souvent utile d'avoir une valeur qui ne distingue que deux possibilités,
comme "oui" et "non" ou "on" et "off". À cette fin, JavaScript dispose d'un
type _Boolean_, qui ne possède que deux valeurs, true et false, qui s'écrivent
comme ces mots.

### Comparaison

{{index comparison}}

Voici une façon de produire des valeurs booléennes :

```
console.log(3 > 2)
// → true
console.log(3 < 2)
// → false
```

{{index [comparison, "of numbers"], "> operator", "< operator", "greater than", "less than"}}

Les signes `>` et `<` sont les symboles traditionnels pour "est plus grand
plus grand que" et "plus petit que", respectivement. Ce sont des opérateurs
binaires. En les appliquant, on obtient une valeur booléenne qui indique
s'ils sont vrais dans ce cas.

Les chaînes de caractères peuvent être comparées de la même manière.

```
console.log("Aardvark" < "Zoroaster")
// → true
```

{{index [comparison, "of strings"]}}

La façon dont les chaînes de caractères sont ordonnées est à peu près
alphabétique mais pas vraiment ce que ce que l'on s'attend à voir dans
un dictionnaire : les lettres majuscules sont toujours "inférieures"
aux lettres minuscules, donc `"Z" < "a"`, et les caractères non
alphabétiques ( !, -, etc.) sont aussi inclus dans l'ordre. Lors de la
comparaison des chaînes de caractères JavaScript procède de gauche à droite,
en comparant les codes ((Unicode)) un par un.

{{index equality, ">= operator", "<= operator", "== operator", "!= operator"}}

D'autres opérateurs similaires sont `>=` (plus grand que ou égal à), `<=`
(inférieur ou égal à), `==` (égal à) et `!=` (non égal à).

```
console.log("Itchy" != "Scratchy")
// → true
console.log("Pomme" == "Orange")
// → false
```

{{index [comparison, "of NaN"], NaN}}

Il n'y a qu'une seule valeur en JavaScript qui n'est pas égale à elle-même,
il s'agit de `NaN` ("not a number").

```
console.log(NaN == NaN)
// → false
```

"NaN" est censé désigner le résultat d'un calcul absurde, et en tant que tel,
il n'est pas égal au résultat de n'importe quel _autre_ calcul absurde.

### Opérateurs logiques

{{index reasoning, "logical operators"}}


Il existe également certaines opérations qui peuvent être appliquées aux
valeurs booléennes elles-mêmes. JavaScript prend en charge trois opérateurs
logiques : _and_, _or_, et _not_. Ils peuvent être utilisés pour "raisonner"
sur les booléens.

{{index "&& operator", "logical and"}}

L'opérateur `&&` représente le _and_ logique. C'est un opérateur binaire,
et son résultat n'est vrai que si les deux valeurs qui lui sont données
sont vraies.

```
console.log(true && false)
// → false
console.log(true && true)
// → true
```

{{index "|| operator", "logical or"}}

L'opérateur `||` dénote un _or_ logique. Il produit vrai si l'une ou l'autre des
valeurs qui lui sont données est vraie.

```
console.log(false || true)
// → true
console.log(false || false)
// → false
```

{{index negation, "! operator"}}

_Not_ s'écrit comme un point d'exclamation (`!`). C'est un opérateur unaire
qui renverse la valeur qui lui est donnée - `!true` produit `false`, et
`!false` donne `true`.

{{index precedence}}

Lorsque l'on mélange ces opérateurs booléens avec les opérateurs arithmétiques
et autres il n'est pas toujours évident de savoir quand les parenthèses sont
nécessaires. Dans la pratique, il suffit généralement de savoir que, parmi
les opérateurs que nous avons vus jusqu'à présent, `||` a la plus faible
priorité, puis vient `&&`, puis les opérateurs de comparaison (`>`, `==`,
et ainsi de suite), et enfin les autres. Cet ordre a été choisi de telle sorte
que, dans les expressions typiques comme celle qui suit, le moins de parenthèses possible soient nécessaires :

```
1 + 1 == 2 && 10 * 10 > 50
```

{{index "conditional execution", "ternary operator", "?: operator", "conditional operator", "colon character", "question mark"}}

Le dernier opérateur logique dont je vais parler n'est pas unaire, ni binaire, mais
_ternaire_, opérant sur trois valeurs. Il s'écrit avec un point d'interrogation
et un deux-points, comme ceci :

```
console.log(true ? 1 : 2);
// → 1
console.log(false ? 1 : 2);
// → 2
```

Celui-ci est appelé l'opérateur _conditionnel_ (ou parfois seulement
l'opérateur _ternaire_ puisqu'il s'agit du seul opérateur de ce type
dans le langage). La valeur qui se trouve à gauche du point d'interrogation
"choisit" laquelle des les deux autres valeurs qui sortiront. Lorsqu'elle
est vraie, elle choisit la valeur du milieu, et quand elle est fausse,
elle choisit la valeur de droite.

## Valeur nulle on indéfinie

{{index undefined, null}}

Il existe deux valeurs spéciales, écrites `null` et `undefined`, qui sont
utilisées pour indiquer l'absence d'une valeur _significative_. Ces valeurs
sont des valeurs elle même, mais elles ne portent aucune information.

De nombreuses opérations dans le langage qui ne produisent pas de valeur
significative (vous en verrez quelques unes plus tard) produisent des
`undefined` simplement parce qu'elles doivent produire _une_ valeur quelle
qu'elle soit.

La différence de signification entre `undefined` et `null` est un accident
de conception de JavaScript, et elle n'a pas d'importance la plupart du temps.
Dans les cas cas où vous devez réellement vous préoccuper de ces valeurs,
je recommande de les traiter comme des valeurs interchangeables.

## Automatic type conversion

{{index NaN, "type coercion"}}

Dans l'introduction, j'ai mentionné que JavaScript fait tout son possible
pour accepter presque tous les programmes que vous lui donnez, même les
programmes qui font des bizarreries. Ceci est bien démontré par les expressions suivantes :

```
console.log(8 * null)
// → 0
console.log("5" - 1)
// → 4
console.log("5" + 1)
// → 51
console.log("five" * 2)
// → NaN
console.log(false == 0)
// → true
```

{{index "+ operator", arithmetic, "* operator", "- operator"}}

Lorsqu'un opérateur est appliqué au "mauvais" type de valeur, JavaScript
va tranquillement convertir cette valeur dans le type dont il a besoin, en
utilisant un ensemble de règles qui ne sont pas souvent ce que vous voulez
ou attendez. Ce phénomène est appelé _((coercition de type))_. Le `null` de
la première expression devient `0`, et le `"5"` de la deuxième expression
devient `5` (de chaîne de caractères à nombre). Pourtant, dans la troisième
expression, `+` essaie de concaténer les chaînes de caractères avant l'addition
numérique, donc le `1` est converti en `"1"` (d'un nombre à une
chaîne de caractères).

{{index "type coercion", [number, "conversion to"]}}

Lorsque quelque chose qui ne correspond pas à un nombre de manière évidente
(comme par exemple `"five"` ou `undefined`) est converti en un nombre, vous
obtenez la valeur `NaN`. D'autres opérations arithmétiques sur `NaN`
continuent à produire `NaN`, donc si vous obtenez l'une de ces valeurs à un
endroit inattendu, recherchez les conversions de type accidentelles.

{{index null, undefined, [comparison, "of undefined values"], "== operator"}}

Lorsque l'on compare des valeurs du même type en utilisant `==`, le résultat
est facile à prédire : vous devriez obtenir true lorsque les deux valeurs sont
identiques, sauf dans le cas de `NaN`. Mais lorsque les types diffèrent, JavaScript utilise un ensemble compliqué et confus de règles pour déterminer ce qu'il
faut faire. Dans la plupart des cas, il essaie simplement de convertir l'une
des valeurs en type de l'autre valeur. Cependant, lorsque `null` ou
`undefined` se trouve de part et d'autre de l'opérateur, il ne produit un
résultat vrai que si les deux côtés sont `null` ou `undefined`.

```
console.log(null == undefined);
// → true
console.log(null == 0);
// → false
```

Ce comportement est souvent utile. Lorsque vous voulez tester si une valeur
a une valeur réelle plutôt que `null` ou `undefined`, vous pouvez la comparer
à `null` avec l'opérateur `==` (ou `!=`).

{{index "type coercion", [Boolean, "conversion to"], "=== operator", "!== operator", comparison}}

Mais que faire si vous voulez tester si quelque chose se réfère à la valeur
exacte précise `false` ? Des expressions comme `0 == false` et `"" == false`
sont également vraies à cause de la conversion automatique des types. Lorsque
vous ne voulez _pas_ que des conversions de type se produisent, il existe deux
opérateurs supplémentaires : `===` et `!==`. Le premier teste si une valeur est _précisément_ égale à une autre à l'autre, et le second teste si elle n'est pas précisément égale.

Ainsi, `"" === false` est faux comme prévu.

Je recommande d'utiliser les opérateurs de comparaison à trois caractères
de manière défensive pour éviter que des conversions de types inattendues
ne vous fassent trébucher. Mais lorsque vous êtes certain que les types des
deux côtés seront les mêmes, il n'y a pas de problème à l'utilisation
d'opérateurs plus courts.

### Court-circuiter les opérateurs logiques

{{index "type coercion", [Boolean, "conversion to"], operator}}

Les opérateurs logiques `&&` et `||` traitent des valeurs de types différents
d'une manière particulière. Ils convertissent la valeur de leur côté gauche
en un type booléen afin de décider de ce qu'il faut faire, mais selon l'opérateur
et du résultat de cette conversion, ils renverront soit la valeur de gauche
valeur de gauche _originale_ ou la valeur de droite.

{{index "|| operator"}}


L'opérateur `||`, par exemple, retournera la valeur à sa gauche quand
elle peut être convertie en true et retournera la valeur à sa droite
sinon. Ceci a l'effet attendu lorsque les valeurs sont booléennes
et fait quelque chose d'analogue pour les valeurs d'autres types.

```
console.log(null || "user")
// → user
console.log("Agnes" || "user")
// → Agnes
```

{{index "default value"}}

Nous pouvons utiliser cette fonctionnalité comme un moyen de revenir à une
valeur par défaut. Si vous avez une valeur qui pourrait être vide, vous
pouvez mettre `||` après avec une valeur de remplacement. Si la valeur
initiale peut être convertie en false, vous obtiendrez la valeur de
remplacement. Les règles de conversion des chaînes de caractères et les
nombres en valeurs booléennes stipulent que `0`, `NaN` et la chaîne vide
(`""`) sont considérés comme des `false`, tandis que toutes les autres
valeurs sont considérées comme des `true`. Donc `0 || -1` produit `-1`,
et `"" || " !?"` donne `" !?"`.

{{index "&& operator"}}

L'opérateur `&&` fonctionne de manière similaire, mais dans l'autre sens.
Lorsque la valeur gauche est quelque chose qui se convertit en faux, il
retourne cette valeur, et sinon, il renvoie la valeur à sa droite.

Une autre propriété importante de ces deux opérateurs est que la partie à
leur droite n'est évaluée que lorsque cela est nécessaire. Dans le cas de `true |||
X`, peu importe ce qu'est `X` - même si c'est un morceau de programme qui fait
quelque chose de _terrible_, le résultat sera vrai, et `X` n'est jamais évalué.
Il en va de même pour `false && X`, qui est faux et ignorera `X`. Cela
s'appelle _((court-circuit d'évaluation))_.

{{index "ternary operator", "?: operator", "conditional operator"}}

L'opérateur conditionnel fonctionne de manière similaire. Parmi les deuxième et
troisième valeur, seule celle qui est sélectionnée est évaluée.

## Résumé

Nous avons étudié quatre types de valeurs JavaScript dans ce chapitre : les
nombres, les chaînes de caractères, les booléens et les valeurs indéfinies.

Ces valeurs sont créées en tapant leur nom (`true`, `null`) ou leur valeur
(`13`, `"abc"`). Vous pouvez combiner et transformer des valeurs avec des
opérateurs. Nous avons vu les opérateurs binaires pour l'arithmétique
(`+`, `-`, `*`, `/`, et `%`), la concaténation de chaînes de caractères
(`+`), la comparaison (`==`, `!=`, `===`, `!==`, `<`, `>`, `<=`, `>=`) et
la logique (`&&`, `||`), ainsi que plusieurs opérateurs unaires (`-` pour
annuler un nombre, `!` pour annuler logiquement et `typeof` pour trouver le
type d'une valeur) et un opérateur ternaire (`?:`) pour choisir une des deux
valeurs en fonction d'une troisième valeur.

Cela vous donne suffisamment d'informations pour utiliser JavaScript comme
une calculatrice de poche, mais pas plus. Le chapitre [suivant](program_structure) commencera à relier ces expressions ensemble dans des programmes de base.

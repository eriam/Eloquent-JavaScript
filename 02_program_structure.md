# Structure d'un programme

{{quote {author: "_why", title: "Why's (Poignant) Guide to Ruby", chapter: true}

Et mon coeur brille d'un rouge vif sous ma peau pelliculaire et translucide et
ils doivent m'administrer 10cc de JavaScript pour me faire revenir. (Je
réagis bien aux toxines dans le sang). Mec, ce truc va faire sortir les
les pêches directement de vos branchies !

quote}}

{{index why, "Poignant Guide"}}

{{figure {url: "img/chapter_picture_2.jpg", alt: "Picture of tentacles holding objects", chapter: framed}}}

Dans ce chapitre, nous allons commencer à faire des choses que l'on peut
réellement appeler de la _programmation_. Nous allons étendre notre maîtrise
du langage JavaScript au-delà des noms et des fragments de phrases que nous
avons vus jusqu'à présent, jusqu'au point où nous pouvons exprimer une
prose significative.

## Expressions et instructions

{{index grammar, [syntax, expression], [code, "structure of"], grammar, [JavaScript, syntax]}}

Dans le [Chapitre ?](values), nous avons créé des valeurs et nous leur
avons appliqué des opérateurs pour obtenir de nouvelles valeurs. La création
de valeurs comme celle-ci est la substance principale de tout programme
JavaScript. Mais cette substance doit être encadrée dans une structure plus
large pour être utile. C'est donc ce que nous allons aborder maintenant.

{{index "literal expression", [parentheses, expression]}}

Un fragment de code qui produit une valeur est appelé une
_((expression))_. Chaque valeur qui est écrite littéralement (comme `22`
ou `"psychanalyse"`) est une expression. Une expression entre
parenthèses est également une expression, tout comme un ((opérateur binaire))
appliqué à deux expressions ou un ((opérateur unaire)) appliqué à une seule.

{{index [nesting, "of expressions"], "human language"}}

Cela montre une partie de la beauté d'une interface basée sur le langage.
Les expressions peuvent contenir d'autres expressions de la même manière
que les sous-entendus dans les langues humaines sont imbriqués - un
sous-entendu peut contenir ses propres sous-entendus, et ainsi de suite.
Cela nous permet de construire des expressions qui décrivent des calculs
arbitrairement complexes.

{{index statement, semicolon, program}}

Si une expression correspond à un fragment de phrase, une _instruction_
JavaScript correspond à une phrase complète. Un programme est une liste de
d'instructions.

{{index [syntax, statement]}}

Le type d'instruction le plus simple est une expression suivie d'un
point-virgule. Ceci est un programme :

```
1;
!false;
```

Mais c'est un programme inutile. Une ((expression)) peut juste produire une
valeur, qui peut ensuite être utilisée par un code qui l'englobe. Une
((instruction)) se suffit à elle-même, elle n'a de sens que si elle affecte
le monde. Elle peut afficher quelque chose à l'écran - cela compte comme
un changement du monde - ou bien elle peut changer l'état interne de la
machine d'une manière qui affectera les déclarations qui suivent. Ces
changements sont appelés _((effets de bord))_. Les instructions de
l'exemple précédent ne font que produire les valeurs `1` et `true` et
puis les oublient immédiatement. Cela ne laisse aucune impression sur
le monde. Lorsque vous exécutez ce programme, rien d'observable ne
se produit.

{{index "programming style", "automatic semicolon insertion", semicolon}}

Dans certains cas, JavaScript vous permet d'omettre le point-virgule à la
fin d'une déclaration. Dans d'autres cas, il doit être présent, sinon la
((ligne)) suivante sera traitée comme faisant partie de la même déclaration.
Les règles qui déterminent quand le point virgule peut être omis en toute
sécurité sont quelque peu complexes et sujettes à erreur. Dans ce livre,
chaque instruction nécessitant un point-virgule en recevra toujours un. Je
vous recommande de faire de même, au moins jusqu'à ce que vous en sachiez
plus sur les subtilités des points-virgules manquants.

## Liaisons

{{indexsee variable, binding}}
{{index [syntax, statement], [binding, definition], "side effect", [memory, organization], [state, in binding]}}

Comment un programme conserve-t-il un état interne ? Comment se souvient-il
des choses ? Nous avons vu comment produire de nouvelles valeurs à partir
d'anciennes valeurs, mais cela ne change pas les anciennes valeurs, et la
nouvelle valeur doit être immédiatement utilisée ou elle sera oubliée à
nouveau. Pour attraper et retenir des valeurs, JavaScript fournit une
chose appelée _liaison_, ou _variable_ :

```
let caught = 5 * 5;
```

{{index "let keyword"}}

C'est un deuxième type d'((instruction)). Le (_((mot-clé))_) `let` indique
que cette phrase va définir une liaison. Il est suivi du nom de la liaison
et, si on veut lui donner immédiatement une valeur, par un opérateur `=`
et une expression.

L'instruction précédente crée une liaison appelée `caught` et l'utilise
pour saisir le nombre obtenu en multipliant 5 par 5.

Une fois qu'une liaison a été définie, son nom peut être utilisé en tant
qu'((expression)). La valeur d'une telle expression est la valeur que la
liaison détient actuellement. Voici un exemple :

```
let ten = 10;
console.log(ten * ten);
// → 100
```

{{index "= operator", assignment, [binding, assignment]}}

Lorsqu'une liaison indique une valeur, cela ne signifie pas qu'elle est liée
à cette valeur pour toujours. L'opérateur `=` peut être utilisé à tout moment
sur des liaisons existantes pour les déconnecter de leur valeur actuelle et
les faire indiquer vers une nouvelle valeur.

```
let mood = "light";
console.log(mood);
// → light
mood = "dark";
console.log(mood);
// → dark
```

{{index [binding, "model of"], "tentacle (analogy)"}}

Vous devez imaginer les liaisons comme des tentacules, plutôt que comme des
boîtes. Elles ne _contiennent pas_ les valeurs ; elles les _attrapent_ - deux
liaisons peuvent se référer à la même valeur. Un programme ne peut accéder
qu'aux valeurs auxquelles il a encore une référence. Quand vous avez besoin
de vous souvenir de quelque chose, vous faites pousser un tentacule
pour vous y accrocher ou vous rattachez l'une de vos tentacules existantes.

Prenons un autre exemple. Pour vous souvenir du nombre de dollars que
Luigi vous doit encore, vous créez une liaison. Et quand il vous rembourse
35 dollars, vous donnez à cette liaison une nouvelle valeur.

```
let detteLuigi = 140;
detteLuigi = detteLuigi - 35;
console.log(detteLuigi);
// → 105
```

{{index undefined}}

Lorsque vous définissez une liaison sans lui donner de valeur, le tentacule
n'a rien à attraper, donc il se retrouve dans l'air. Si vous demandez la
valeur d'une liaison vide, vous obtiendrez la valeur `undefined`.

{{index "let keyword"}}

Une seule instruction `let` peut définir plusieurs liaisons. Les définitions
doivent être séparées par des virgules.

```
let one = 1, two = 2;
console.log(one + two);
// → 3
```

Les mots `var` et `const` peuvent aussi être utilisés pour créer des liens, de
manière similaire à `let`.

```
var nom = "Ayda";
const salutation = "Bonjour ";
console.log(salutation + nom);
// → Bonjour Ayda
```

{{index "var keyword"}}

La première, `var` (abréviation de "variable"), est la manière dont les
liaisons étaient déclarées dans le JavaScript d'avant 2015. Je reviendrai
sur la manière précise dont elle diffère de `let` dans le [prochain chapitre](fonctions). Pour l'instant, rappelez-vous qu'il fait la même
chose, mais que nous l'utiliserons rarement dans ce livre car il possède
des propriétés déroutantes.

{{index "const keyword", naming}}

Le mot `const` signifie _((constante))_. Il définit une liaison constante
qui pointe vers la même valeur tant qu'elle vit. Ceci est utile pour les
liaisons qui donnent un nom à une valeur afin de pouvoir facilement y
faire référence plus tard.

## Noms des liaisons

{{index "underscore character", "dollar sign", [binding, naming]}}

Les noms de liaison peuvent être n'importe quel mot. Les chiffres peuvent
faire partie des noms de liaison - "catch22" est un nom valide, par
exemple - mais le nom ne doit pas commencer par un chiffre. Un nom de
liaison peut inclure des signes de dollar (`$`) ou des tirets bas (`_`).
underscores (`_`) mais aucune autre ponctuation ou caractères spéciaux.

{{index [syntax, identifier], "implements (reserved word)", "interface (reserved word)", "package (reserved word)", "private (reserved word)", "protected (reserved word)", "public (reserved word)", "static (reserved word)", "void operator", "yield (reserved word)", "enum (reserved word)", "reserved word", [binding, naming]}}

Les mots ayant une signification particulière, tels que `let`, sont des
_((mot-clé))s_ et ne peuvent pas être utilisés comme noms de liaison.
Il existe également un certain nombre de mots qui sont "réservés pour
une utilisation" dans les ((futures)) versions de JavaScript, qui ne peuvent
pas non plus être utilisés comme noms de liaison. La liste complète
des mots-clés et des mots réservés est assez longue.

```{lang: "text/plain"}
break case catch class const continue debugger default
delete do else enum export extends false finally for
function if implements import interface in instanceof let
new package private protected public return static super
switch this throw true try typeof var void while with yield
```

{{index [syntax, error]}}

Ne vous souciez pas de mémoriser cette liste. Lorsque la création d'une
liaison produit une erreur de syntaxe inattendue, vérifiez si vous n'essayez
pas de définir un mot réservé.

## L'environnement

{{index "standard environment", [browser, environment]}}

L'ensemble des liaisons et de leurs valeurs qui existent à un moment donné
s'appelle l'_((environnement))_. Au démarrage d'un programme, cet
environnement n'est pas vide. Il contient toujours des liaisons qui font
partie du langage ((standard)), et la plupart du temps, il contient également
des liaisons qui fournissent des moyens d'interagir avec le système
environnant. Par exemple, dans un navigateur, il y a des fonctions pour
interagir avec le site Web actuellement chargé et pour lire les
entrées ((souris)) et ((clavier)).

## Fonctions

{{indexsee "application (of functions)", [function, application]}}
{{indexsee "invoking (of functions)", [function, application]}}
{{indexsee "calling (of functions)", [function, application]}}
{{index output, function, [function, application], [browser, environment]}}

Un grand nombre de valeurs fournies dans l'environnement par défaut ont
le type _((fonction))_. Une fonction est un morceau de programme enveloppé
dans une valeur. Ces valeurs peuvent être _appliquées_ afin d'exécuter le
programme enveloppé. Par exemple, dans un environnement de navigateur, la
liaison `prompt` contient une fonction qui affiche une petite
((boîte de dialogue)) demandant à l'utilisateur de saisir des données.
Cette liaison ou fonction est utilisée comme ceci :

```
prompt("Entrez mot de passe");
```

{{figure {url: "img/prompt.png", alt: "A prompt dialog", width: "8cm"}}}

{{index parameter, [function, application], [parentheses, arguments]}}

L'exécution d'une fonction est appelée _invoquer_, _appeller_ ou _appliquer_.
Vous pouvez appeler une fonction en mettant des parenthèses après une
expression qui produit une valeur de fonction. En général, vous utiliserez
directement le nom de la liaison qui contient la fonction. Les valeurs entre
les parenthèses sont données au programme à l'intérieur de la fonction. Dans
l'exemple exemple, la fonction `prompt` utilise la chaîne de caractères
que nous lui donnons comme texte à afficher dans la boîte de dialogue. Les
valeurs données aux fonctions sont appelées _((argument))s_. Des fonctions
différentes peuvent avoir besoin d'un nombre et de types différent d'arguments.

La fonction `prompt` n'est pas beaucoup utilisée dans la programmation web
moderne, principalement parce que vous n'avez aucun contrôle sur l'aspect de
la boîte de dialogue par contre elle peut être utile dans les programmes
tests et les expériences.

## La fonction console.log

{{index "JavaScript console", "developer tools", "Node.js", "console.log", output, [browser, environment]}}

Dans les exemples, j'ai utilisé `console.log` pour afficher les valeurs. La
plupart des systèmes JavaScript (y compris tous les navigateurs web modernes
et Node.js) fournissent une fonction `console.log` qui écrit ses arguments
sur une sortie texte quelconque. Dans les navigateurs, la sortie se trouve
dans la ((console JavaScript)). Cette partie de l'interface du navigateur
est cachée par défaut, mais la plupart des navigateurs l'ouvrent lorsque
vous appuyez sur F12 ou, sur un Mac, sur [command]{keyname}-[option]{keyname}-I.
Si cela ne fonctionne pas, recherchez dans les menus un élément nommé
Outils Developpeur ou similaire.

{{if interactive

Lors de l'exécution des exemples (ou de votre propre code) sur les pages de ce
livre, la sortie `console.log` s'affichera après l'exemple, au lieu de
dans la console JavaScript du navigateur.

```
let x = 30;
console.log("la valeur de x est", x);
// → la valeur de x est 30
```

if}}

{{index [object, property], [property, access]}}

Bien que les noms de liaison ne puissent pas contenir de ((caractère de
point))s, `console.log` en a un. Cela est dû au fait que `console.log`
n'est pas une simple liaison. C'est en fait une expression qui récupère
la propriété `log` à partir de la valeur contenue dans le binding
`console`. Nous verrons ce que cela signifie exactement au [Chapitre ?](data#properties).

{{id return_values}}
## Valeurs de retour

{{index [comparison, "of numbers"], "return value", "Math.max function", maximum}}

L'affichage d'une boîte de dialogue ou l'écriture de texte à l'écran est
un _((effet de bord))_. De nombreuses fonctions sont utiles en raison
des effets de bord qu'elles produisent. Les fonctions peuvent également
produire des valeurs et dans ce cas, elles n'ont pas besoin d'avoir un
effet de bord pour être utiles. Par exemple, la fonction `Math.max` prend
n'importe quel nombre d'arguments numériques et renvoie le plus grand.

```
console.log(Math.max(2, 4));
// → 4
```

{{index [function, application], minimum, "Math.min function"}}

Lorsqu'une fonction produit une valeur, on dit qu'elle _renvoie_ cette
valeur. Tout ce qui produit une valeur est une ((expression)) en JavaScript,
ce qui signifie que les appels de fonction peuvent être utilisés dans des
expressions plus larges. Ici un appel à `Math.min`, qui est l'opposé
de `Math.max`, est utilisé dans une partie d'une expression addition :

```
console.log(Math.min(2, 4) + 100);
// → 102
```

Le [chapitre suivant](functions) explique comment écrire vos propres fonctions.
fonctions.

## Structure de contrôle

{{index "execution order", program, "control flow"}}

Lorsque votre programme contient plus d'une ((instruction)), les instructions
sont exécutées comme s'il s'agissait d'une histoire, de haut en bas. Cet
exemple contient deux instructions. La première demande à l'utilisateur un
nombre, et la seconde, qui est exécutée après la première, montre le
((carré)) de ce nombre.

```
let unNombre = Number(prompt("Saisissez un nombre"));
console.log("Votre nombre est la racine de " +
            unNombre * unNombre);
```

{{index [number, "conversion to"], "type coercion", "Number function", "String function", "Boolean function", [Boolean, "conversion to"]}}

La fonction `Number` convertit une valeur en un nombre. Nous avons besoin
de cette conversion parce que le résultat de `prompt` est une chaîne de
caractères, et nous voulons un nombre. Il existe des fonctions similaires
appelées `String` et `Boolean` qui convertissent les valeurs en ces types.

Voici la représentation schématique plutôt triviale de la structure de
contrôle:

{{figure {url: "img/controlflow-straight.svg", alt: "Trivial control flow", width: "4cm"}}}

## Execution conditionnelle

{{index Boolean, ["control flow", conditional]}}

Tous les programmes ne sont pas des chemins tout droits. Nous pouvons, par
exemple, vouloir créer une route qui se ramifie, où le programme prend
la branche appropriée en fonction de la situation. C'est ce qu'on appelle
l'_((exécution conditionnelle))_.

{{figure {url: "img/controlflow-if.svg", alt: "Conditional control flow",width: "4cm"}}}

{{index [syntax, statement], "Number function", "if keyword"}}

L'exécution conditionnelle est créée avec le mot-clé `if` en JavaScript.
Dans le cas simple, nous voulons qu'un code soit exécuté si, et seulement si,
une certaine condition est remplie. Nous pouvons, par exemple, vouloir afficher le
carré de l'entrée seulement si l'entrée est réellement un nombre.

```{test: wrap}
let unNombre = Number(prompt("Saisissez un nombre"));
if (!Number.isNaN(unNombre)) {
  console.log("Votre nombre est la racine de " +
              unNombre * unNombre);
}
```

Avec cette modification, si vous entrez "perroquet", aucune sortie
n'est affichée.

{{index [parentheses, statement]}}

Le mot-clé "if" exécute ou saute une instruction en fonction de la valeur
d'une expression booléenne. L'expression décisive est écrite après le mot-clé
entre parenthèses, suivie de l'instruction à exécuter.

{{index "Number.isNaN function"}}

La fonction `Number.isNaN` est une fonction standard de JavaScript qui
renvoie "vrai" uniquement si l'argument qui lui est donné est "NaN". La fonction `Number` renvoie `NaN` lorsque vous lui donnez une chaîne de caractères qui
qui ne représente pas un nombre valide. Ainsi, la condition se traduit par
"à moins que `theNumber` soit not-a-number, faites ceci".

{{index grouping, "{} (block)", [braces, "block"]}}

L'instruction après le `if` est entourée de crochets (`{` et
`}`) dans cet exemple. Les crochets peuvent être utilisées pour regrouper
un nombre quelconque d'instructions en une seule instruction, appelée
_((bloc))_. Vous auriez pu également les omettre dans ce cas, puisqu'elles
ne contiennent qu'une seule déclaration. Mais pour éviter d'avoir à se
demander si elles sont nécessaires, la plupart des programmeurs JavaScript
les utilisent dans chaque déclaration enveloppée comme celle-ci. Nous
suivrons principalement cette convention dans ce livre, sauf pour
l'occasionnel one-liner.

```
if (1 + 1 == 2) console.log("C'est vrai");
// → It's true
```

{{index "else keyword"}}

Souvent, vous n'aurez pas seulement du code qui s'exécute quand une
condition est vraie, mais aussi du code qui gère l'autre cas. Ce chemin
alternatif est représentée par la deuxième flèche du diagramme. Vous pouvez
utiliser le mot-clé `else`, ainsi que le mot-clé `if`, pour créer deux chemins d'exécution alternatifs distincts.


```{test: wrap}
let unNombre = Number(prompt("Saisissez un nombre"));
if (!Number.isNaN(unNombre)) {
  console.log("Votre nombre est la racine de " +
              unNombre * unNombre);
} else {
  console.log("Hey. Pourquoi ne pas me donner un nombre?");
}
```

{{index ["if keyword", chaining]}}

Si vous avez plus de deux chemins à choisir, vous pouvez "enchaîner" plusieurs
paires de `if`/`else` ensemble. En voici un exemple :

```
let num = Number(prompt("Saisissez un nombre"));

if (num < 10) {
  console.log("Petit");
} else if (num < 100) {
  console.log("Moyen");
} else {
  console.log("Grand");
}
```

Le programme va d'abord vérifier si `num` est inférieur à 10. Si c'est le
cas, il choisit cette branche, affiche "Petit", et a terminé. Si ce n'est
pas le cas, il prend la branche `else`, qui contient elle-même un second `if`.
Si la deuxième condition (`< 100`) se vérifie, cela signifie que le nombre
est au moins 10 mais inférieur à 100, et "Moyen" est affiché. Si ce n'est
pas le cas, la deuxième et dernière branche `else` est choisie.

Le schéma de ce programme ressemble à ceci :

{{figure {url: "img/controlflow-nested-if.svg", alt: "Nested if control flow", width: "4cm"}}}

{{id loops}}
## Boucles do et while

Considérons un programme qui produit tous les ((nombre pair))s de 0 à 12.
Une manière d'écrire ce programme est la suivante :

```
console.log(0);
console.log(2);
console.log(4);
console.log(6);
console.log(8);
console.log(10);
console.log(12);
```

{{index ["control flow", loop]}}

Ça marche, mais l'idée d'écrire un programme est de faire en sorte que
d'avoir _moins de travail_, pas plus. Si nous avions besoin de tous les
nombres pairs inférieurs à 1 000, cette approche serait irréalisable. Ce
dont nous avons besoin est un moyen d'exécuter un un morceau de code
plusieurs fois. Cette forme de flux de contrôle s'appelle une _((boucle))_.

{{figure {url: "img/controlflow-loop.svg", alt: "Loop control flow",width: "4cm"}}}

{{index [syntax, statement], "counter variable"}}

Le flux de contrôle en boucle nous permet de revenir à un point du
programme où nous étions auparavant et de le répéter avec l'état actuel
du programme. Si nous combinons cela avec une liaison qui compte, nous
pouvons faire quelque chose comme ceci :

```
let nombre = 0;
while (nombre <= 12) {
  console.log(nombre);
  nombre = nombre + 2;
}
// → 0
// → 2
//   … etcetera
```

{{index "while loop", Boolean, [parentheses, statement]}}

Une ((instruction)) commençant par le mot-clé `while` crée une boucle.
Le mot "while" est suivi d'une ((expression)) entre parenthèses et
puis d'une instruction, pareillement au mot "if". La boucle continue à
entrer dans cette l'instruction tant que l'expression produit une valeur
qui donne `vrai` lorsqu'elle est convertie en booléen.

{{index [state, in binding], [binding, as state]}}

La liaison `nombre` démontre la manière dont une ((liaison)) peut suivre
la progression d'un programme. A chaque fois que la boucle se répète,
`nombre` reçoit une valeur qui est 2 de plus que sa valeur précédente.
Au début de chaque répétition, il est comparé au nombre 12 pour décider
si le travail du programme est terminé.

{{index exponentiation}}

A titre d'exemple plus parlant, nous pouvons  maintenant écrire un programme
qui calcule et affiche la valeur de 2^10^ (2 à la 10ème puissance). Nous
utilisons deux liaisons : une pour garder la trace de notre résultat et une
pour compter le nombre de fois où nous avons multiplié ce résultat par 2.
La boucle teste si la deuxième liaison a déjà atteint 10 et, si ce n'est
pas le cas, met à jour les deux liaisons.

```
let resultat = 1;
let compteur = 0;
while (compteur < 10) {
  resultat = resultat * 2;
  compteur = compteur + 1;
}
console.log(resultat);
// → 1024
```

Le compteur aurait également pu commencer à 1 et vérifier si le nombre de
pièces était inférieur à 10, mais pour des raisons qui apparaîtront dans
le [chapitre ?](data#array_indexing), c'est une bonne idée de s'habituer
à compter à partir de 0.

{{index "loop body", "do loop", ["control flow", loop]}}

Une boucle `do` est une structure de contrôle similaire à une boucle `while`.
Elle diffère seulement sur un point : une boucle `do` exécute toujours au
moins une fois son corps, et elle commence à tester si elle doit s'arrêter
seulement après cette première exécution. Pour refléter cela, le test
apparaît après le corps de la boucle.

```
let votreNom;
do {
  votreNom = prompt("Qui es-tu?");
} while (!votreNom);
console.log(votreNom);
```

{{index [Boolean, "conversion to"], "! operator"}}

Ce programme vous obligera à entrer un nom. Il vous le demandera encore et
encore jusqu'à ce qu'il obtienne quelque chose qui n'est pas une chaîne vide.
Appliquer l'opérateur `!` convertira une valeur en type booléen avant de la
négater et toutes les chaînes de caractères sauf `""` sont converties en
`vrai`. Cela signifie que la boucle continue à tourner jusqu'à ce que vous
fournissiez un nom non vide.

## Indentation du code

{{index [code, "structure of"], [whitespace, indentation], "programming style"}}

Dans les exemples, j'ai ajouté des espaces devant les déclarations qui
qui font partie d'un énoncé plus large. Ces espaces ne sont pas nécessaires,
l'ordinateur acceptera le programme sans eux. En fait, même les
((retours a la ligne)) dans les programmes sont facultatifs. Vous pouvez
écrire un programme comme une seule longue ligne si vous en aviez envie.

Le rôle de cette ((indentation)) à l'intérieur des ((blocs)) est de faire
ressortir la structure du code. Dans un code où de nouveaux blocs sont ouverts
à l'intérieur d'autres blocs, il peut devenir difficile de voir où un bloc se
termine et un autre commence. Avec une indentation appropriée, la forme
visuelle d'un programme correspond à la forme des blocs. J'aime utiliser
deux espaces pour chaque bloc ouvert, mais les goûts diffèrent, certaines
personnes utilisent quatre espaces, et d'autres des ((caractère de tabulation))s.
L'important est que chaque nouveau bloc ajoute la même quantité d'espace.

```
if (false != true) {
  console.log("Oui n'est-ce pas.");
  if (1 < 2) {
    console.log("Et ce n'est pas surprenant.");
  }
}
```

La plupart des ((éditeurs)) de code[ (y compris celui de ce livre)]{if
interactive} vous aideront en indentant automatiquement les nouvelles lignes
au niveau approprié.

## Boucles for

{{index [syntax, statement], "while loop", "counter variable"}}

De nombreuses boucles suivent le modèle montré dans les exemples `while`.
Tout d'abord, un "compteur" est créé pour suivre la progression de la boucle.
Puis vient une boucle `while`, généralement avec une expression de test qui
vérifie si le compteur a atteint sa valeur finale. À la fin du corps de la
boucle, le compteur est mis à jour pour suivre la progression.

{{index "for loop", loop}}

Parce que ce modèle est si commun, JavaScript et les langages similaires
fournissent une forme légèrement plus courte et plus complète, la
boucle `for`.

```
for (let nombre = 0; nombre <= 12; nombre = nombre + 2) {
  console.log(number);
}
// → 0
// → 2
//   … etcetera
```

{{index ["control flow", loop], state}}

Ce programme est exactement équivalent à l'exemple [précédent](program_structure#loops)
de l'impression des nombres pairs. La seule modification apportée est que
toutes les ((instruction))s qui sont liées à l'"état" de la boucle sont
regroupées après `for`.

{{index [binding, as state], [parentheses, statement]}}

Les parenthèses après un mot-clé `for` doivent contenir deux ((point-virgule))s.
La partie située avant le premier point-virgule _initialise_ la boucle,
généralement en définissant une liaison. La deuxième partie est
l'((expression)) qui _vérifie_ si la boucle doit continuer. La dernière partie
partie _met à jour_ l'état de la boucle après chaque itération. Dans la
plupart des cas, c'est plus court et plus clair qu'une construction `while`.

{{index exponentiation}}

Voici le code qui calcule 2^10^ en utilisant `for` au lieu de `while` :

```{test: wrap}
let resultat = 1;
for (let compteur = 0; compteur < 10; compteur = compteur + 1) {
  resultat = resultat * 2;
}
console.log(resultat);
// → 1024
```

## Sortir d'une boucle

{{index [loop, "termination of"], "break keyword"}}

Le fait que la condition de bouclage produise `false` n'est pas la seule
façon dont une boucle peut se terminer. Il existe une instruction spéciale
appelée `break` qui a pour effet de sortir immédiatement de la boucle
qui l'entoure.

Ce programme illustre l'instruction `break`. Il trouve le premier nombre
qui est à la fois supérieur ou égal à 20 et divisible par 7.

```
for (let actuel = 20; ; actuel = actuel + 1) {
  if (actuel % 7 == 0) {
    console.log(actuel);
    break;
  }
}
// → 21
```

{{index "remainder operator", "% operator"}}

L'utilisation de l'opérateur de reste (`%`) est un moyen simple de tester
si un nombre est divisible par un autre nombre. S'il l'est, le reste de
leur division est égal à zéro.

{{index "for loop"}}

La construction `for` de l'exemple ne comporte pas de partie qui vérifie
la fin de la boucle. Cela signifie que la boucle ne s'arrêtera jamais
sauf si l'instruction `break` qu'elle contient est exécutée.

Si vous supprimez l'instruction `break` ou si vous écrivez accidentellement
une condition de fin qui produit toujours `vrai`, votre programme sera
coincé dans une _((boucle infinie))_. Un programme coincé dans une
boucle infinie ne finira jamais de s'exécuter, ce qui est généralement
pas très sympa.

{{if interactive

Si vous créez une boucle infinie dans l'un des exemples de ces pages,
on vous demandera généralement si vous souhaitez arrêter le script après quelques
quelques secondes. Si cela ne fonctionne pas, vous devrez fermer l'onglet dans lequel vous travaillez ou, sur certains navigateurs, fermer l'ensemble du navigateur, pour récupérer.

if}}

{{index "continue keyword"}}

Le mot-clé `continue` est similaire à `break`, dans le sens où il influence
la progression d'une boucle. Lorsque `continue` est rencontré dans le corps
d'une boucle, le contrôle saute du corps et continue avec la prochaine
itération de la boucle.

## Mise à jour succincte des liaisons

{{index assignment, "+= operator", "-= operator", "/= operator", "*= operator", [state, in binding], "side effect"}}

Un programme a souvent besoin, en particulier dans une boucle, de "mettre à jour" une liaison pour contenir une valeur basée sur la valeur précédente de cette liaison.

```{test: no}
compteur = compteur + 1;
```
JavaScript fournit un raccourci pour cela.

```{test: no}
compteur += 1;
```

Des raccourcis similaires fonctionnent pour beaucoup d'autres opérateurs,
tels que `resultat *= 2`` pour doubler `resultat` ou `compteur -= 1` pour
compter vers le bas.

Cela nous permet de raccourcir un peu plus notre exemple de comptage.

```
for (let nombre = 0; nombre <= 12; nombre += 2) {
  console.log(nombre);
}
```

{{index "++ operator", "-- operator"}}

Pour `compteur += 1` et `compteur -= 1`, il existe des équivalents encore
plus courts : `counter++` et `counter--`.

## Distribuer sur une valeur avec switch

{{index [syntax, statement], "conditional execution", dispatch, ["if keyword", chaining]}}

Il n'est pas rare que le code ressemble à ceci :

```{test: no}
if (x == "value1") action1();
else if (x == "value2") action2();
else if (x == "value3") action3();
else defaultAction();
```

{{index "colon character", "switch keyword"}}

Il existe une structure appelée `switch` qui est destiné à exprimer une telle
"distribution" (dispatch en Anglais) d'une manière plus directe.
Malheureusement, la syntaxe que JavaScript utilise pour cela (qu'il a hérité
des langages de programmation C/Java) est quelque peu maladroite - une chaîne d'instructions `if` pourrait être plus efficace. Voici un exemple :

```
switch (prompt("Quel temps fait-il?")) {
  case "pluvieux":
    console.log("Pensez au parapluie.");
    break;
  case "ensoleillé":
    console.log("Des habits légers.");
  case "nuageux":
    console.log("Vous pouvez sortir.");
    break;
  default:
    console.log("Météo inconnue!");
    break;
}
```

{{index fallthrough, "break keyword", "case keyword", "default keyword"}}

Vous pouvez mettre un nombre quelconque d'étiquettes `case` à l'intérieur
du bloc ouvert par `switch`. Le programme commencera à s'exécuter au niveau
de l'étiquette qui correspondant à la valeur donnée à `switch`, ou à `default`
si aucune valeur correspondante n'est trouvée. Il continuera à s'exécuter,
même à travers autres étiquettes, jusqu'à ce qu'il atteigne une instruction
`break`. Dans certains cas, comme le cas `"ensoleillé"` dans l'exemple,
cela peut être utilisé pour partager du code entre les cas (il recommande
d'aller dehors par temps ensoleillé et par temps nuageux). Mais attention,
il est facile d'oublier une telle "rupture", ce qui fera que le programme
exécutera du code que vous ne voulez pas exécuter.

## Capitalisation

{{index capitalization, [binding, naming], [whitespace, syntax]}}

Les noms des liaisons ne doivent pas contenir d'espaces, mais il est souvent
utile d'utiliser plusieurs mots pour décrire clairement ce que représente
la liaison. Les choix possibles pour écrire un nom de liaison avec plusieurs
mots dedans sont les suivants :

```{lang: null}
fuzzylittleturtle
fuzzy_little_turtle
FuzzyLittleTurtle
fuzzyLittleTurtle
```

{{index "camel case", "programming style", "underscore character"}}

Le premier style peut être difficile à lire. J'aime plutôt l'aspect des
soulignements bien que ce style soit un peu pénible à taper. Les
fonctions ((standard)) JavaScript, et la plupart des programmeurs JavaScript,
suivent le style du bas : ils mettent une majuscule à chaque mot sauf au
premier. Il n'est pas difficile de s'habituer à ce genre de petites choses,
et le code avec des styles de dénomination mixtes peut être déroutant à lire,
donc nous suivons cette ((convention)).

{{index "Number function", constructor}}

Dans quelques cas, tels que la fonction `Number`, la première lettre d'une
liaison est également mise en majuscule. Cela a été fait pour marquer cette
fonction comme un constructeur. Ce qu'est un constructeur deviendra clair
dans le [Chapitre ?](object#constructors). Pour l'instant, l'important est
de ne pas trop se soucier de ce manque apparent de ((cohérence)).

## Commentaires

{{index readability}}

Souvent, le code brut ne transmet pas toutes les informations que vous
voulez qu'un programme transmette à des lecteurs _humains_, ou bien il les
transmet d'une manière tellement cryptique que les gens ne peuvent pas
le comprendre. Dans d'autres cas, vous pouvez simplement inclure des
réflexions connexes dans votre programme. C'est à cela que servent les _((commentaire))s_.

{{index "slash character", "line comment"}}

Un commentaire est un morceau de texte qui fait partie d'un programme mais
qui est complètement ignoré par l'ordinateur. JavaScript a deux façons
d'écrire des commentaires. Pour écrire un commentaire d'une seule ligne,
vous pouvez utiliser deux barres obliques (`//`), suivis du texte du
commentaire.

```{test: no}
let soldeCompte = calculerSolde(compte);
// C'est un creux vert où chante une rivière.
soldeCompte.ajusteSolde();
// Qui attrape follement des lambeaux blancs dans l'herbe.
let monRapport = new Rapport();
// Où le soleil sur la fière montagne sonne :
monRapport.ajouteSolde(soldeCompte);
// C'est une petite vallée, qui mousse comme la lumière dans un verre.
```

{{index "block comment"}}

Un commentaire `//` ne va que jusqu'à la fin de la ligne. Une section de texte
entre `/*` et `*/` sera ignorée dans son intégralité, qu'elle contienne ou
non des sauts de ligne. Ceci est utile pour ajouter des blocs d'informations
d'informations sur un fichier ou un morceau de programme.

```
/*
  J'ai d'abord trouvé ce nombre gribouillé au dos d'un vieux
  vieux cahier. Depuis lors, il est souvent passé, apparaissant dans des
  des numéros de téléphone et des numéros de série de produits que j'ai
  achetés. Comme il m'aime bien, j'ai décidé de le garder.
*/
const monNombre = 11213;
```

## Résumé

Vous savez maintenant qu'un programme est construit à partir d'instructions,
qui elles-mêmes contiennent parfois d'autres instructions. Les instructions
ont tendance à contenir des expressions, qui peuvent elles-mêmes être
construites à partir de plus petites expressions.

En mettant les instructions les unes à la suite des autres, vous obtenez un
programme qui est exécuté de haut en bas. Vous pouvez introduire des
perturbations dans le contrôle en utilisant des instructions
conditionnelles (`if`, `else`, et `switch`) et des
boucles (`while`, `do`, etc.).

Les liaisons peuvent être utilisées pour classer des morceaux de données
sous un nom, et elles sont utiles pour suivre l'état de votre programme.
L'environnement est l'ensemble de liaisons qui sont définies. Les systèmes
JavaScript placent toujours un certain nombre de liaisons standard utiles
dans votre environnement.

Les fonctions sont des valeurs spéciales qui encapsulent un morceau de
programme. Vous pouvez les invoquer en écrivant `nomDeFonction(argument1, argument2)`. Un tel appel de fonction est une expression et peut produire une valeur.

## Exercices

{{index exercises}}

Si vous ne savez pas comment tester vos solutions aux exercices, reportez-vous
à la section [Introduction](intro).

Chaque exercice commence par une description du problème. Lisez cette
description et essayez de de résoudre l'exercice. Si vous rencontrez des
problèmes, pensez à lire les conseils [après l'exercice]{if interactive}[à la [fin du livre](hints)]{if book}. Les solutions complètes des exercices ne sont
ne sont pas incluses dans ce livre, mais vous pouvez les trouver en ligne à l'adresse suivante [_https://eloquentjavascript.net/code_](https://eloquentjavascript.net/code#2).
Si vous voulez apprendre quelque chose des exercices, je vous recommande de ne regarder les solutions qu'après avoir fait les exercices, ou du moins après l'avoir attaqué  assez longtemps et assez fort pour avoir un léger mal de tête.

### Boucler un triangle

{{index "triangle (exercise)"}}

Ecrivez une ((boucle)) qui fait sept appels à `console.log` pour afficher le triangle suivant
triangle suivant :

```{lang: null}
#
##
###
####
#####
######
#######
```

{{index [string, length]}}

Il peut être utile de savoir que vous pouvez trouver la longueur d'une chaîne en
en écrivant `.length` après celle-ci.

```
let maChaine = "abc";
console.log(maChaine.length);
// → 3
```

{{if interactive

La plupart des exercices contiennent un morceau de code que vous pouvez
modifier pour résoudre l'exercice. N'oubliez pas que vous pouvez cliquer
sur les blocs de code pour les modifier.

```
// Votre code ici.
```
if}}

{{hint

{{index "triangle (exercise)"}}

Vous pouvez commencer par un programme qui imprime les nombres de 1 à 7,
que vous pouvez dériver en apportant quelques modifications à [l'exemple d'impression des nombres pairs](program_structure#loops) donné plus tôt dans le manuel
où la boucle `for` a été introduite.

Considérons maintenant l'équivalence entre les nombres et les chaînes de
caractères dièse. Vous pouvez passer de 1 à 2 en ajoutant 1 (`+= 1`).
Vous pouvez passer de `"#"` à `"##"` en ajoutant un caractère (`+= "#"`).
Ainsi, votre solution peut suivre de près le programme d'impression des
nombres.

hint}}

### FizzBuzz

{{index "FizzBuzz (exercise)", loop, "conditional execution"}}

Ecrivez un programme qui utilise `console.log` pour imprimer tous les
nombres de 1 à 100 avec deux exceptions. Pour les nombres divisibles par 3,
imprimez "Fizz" à la place du nombre, et pour les nombres divisibles par 5
(et non par 3), imprimez "Buzz" à la place.

Lorsque cela fonctionne, modifiez votre programme pour imprimer `"FizzBuzz"`.
pour les nombres qui sont divisibles à la fois par 3 et 5 (et qui affichent toujours
`"Fizz"` ou `"Buzz"` pour les nombres divisibles par un seul d'entre eux).

(Il s'agit en fait d'une ((question d'entretien d'embauche)) dont on a
prétendu qu'elle permettait d'éliminer un pourcentage significatif de
candidats programmeurs. Donc si vous l'avez résolue, votre valeur sur le
marché du travail vient d'augmenter).

{{if interactive
```
// Votre code ici.
```
if}}

{{hint

{{index "FizzBuzz (exercise)", "remainder operator", "% operator"}}

Le passage en revue des chiffres est clairement un travail en boucle, et le
choix de ce qu'il faut imprimer est une question d'exécution conditionnelle.
Souvenez-vous de l'astuce consistant à l'utilisation de l'opérateur de
reste (`%`) pour vérifier si un nombre est divisible par un autre nombre
(dont le reste est égal à zéro).

Dans la première version, il y a trois résultats possibles pour chaque nombre.
vous devrez donc créer une chaîne `if`/ `else if`/ `else`.

{{index "|| operator", ["if keyword", chaining]}}

La deuxième version du programme a une solution simple et une autre
solution astucieuse. La solution simple consiste à ajouter une autre "branche"
conditionnelle pour pour tester précisément la condition donnée. Pour la
solution astucieuse, construisez une chaîne de caractères contenant le ou les
mots à sortir et d'imprimer soit ce mot ou le nombre s'il n'y a pas de mot,
éventuellement en faisant un bon usage de l'opérateur `||`.

hint}}

### Échiquier

{{index "chessboard (exercise)", loop, [nesting, "of loops"], "newline character"}}

Écrivez un programme qui crée une chaîne de caractères représentant une
grille 8×8, en utilisant des caractères de nouvelle ligne pour séparer les
lignes. À chaque position de la grille, il y a soit un espace, soit un
caractère "#". Les caractères doivent former un échiquier.

En passant cette chaîne à `console.log`, on devrait obtenir quelque chose
comme ceci :

```{lang: null}
 # # # #
# # # #
 # # # #
# # # #
 # # # #
# # # #
 # # # #
# # # #
```

Lorsque vous avez un programme qui génère ce modèle, définissez une liaison
`taille = 8` et modifiez le programme de façon à ce qu'il fonctionne pour
n'importe quelle `taille`, en produisant une grille de la largeur et de la
hauteur données.

{{if interactive
```
// Votre code ici.
```
if}}

{{hint

{{index "chess board (exercise)"}}

Vous pouvez construire la chaîne en commençant par une chaîne vide (`""`)
et en ajoutant des caractères de manière répétée. Un caractère de
nouvelle ligne s'écrit `"\n"`.

{{index [nesting, "of loops"], [braces, "block"]}}

Pour travailler avec deux ((dimensions)), vous aurez besoin d'une ((boucle))
à l'intérieur d'une ((boucle)). Mettez des accolades autour des corps des
deux boucles afin de pouvoir pour voir facilement où elles commencent et
se terminent. Essayez d'indenter correctement ces corps. L'ordre des
boucles doit suivre l'ordre dans lequel nous construisons la chaîne de
caractères (ligne par ligne, de gauche à droite, de haut en bas). Ainsi,
la boucle extérieure gère les lignes, et la boucle intérieure gère les
caractères sur une ligne.

{{index "counter variable", "remainder operator", "% operator"}}

Vous aurez besoin de deux liaisons pour suivre votre progression. Pour
savoir s'il faut mettre un espace ou un signe dièse à une position donnée,
vous pouvez tester si la somme des deux compteurs est paire (`% 2`).

Terminer une ligne en ajoutant un caractère de nouvelle ligne doit se faire
après que la ligne ait été construite, donc faites-le après la boucle interne
mais à l'intérieur de la boucle externe.

hint}}

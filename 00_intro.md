{{meta {load_files: ["code/intro.js"]}}}

# Introduction

{{quote {author: "Ellen Ullman", title: "Close to the Machine: Technophilia and its Discontents", chapter: true}

Nous pensons que nous créons le système pour nos propres besoins. Nous pensons
que nous le faisons à notre image... Mais l'ordinateur n'est pas vraiment
comme nous. C'est une projection d'une partie très mince de nous-mêmes : cette
partie consacrée à la logique, l'ordre, la règle et la clarté.

quote}}

{{figure {url: "img/chapter_picture_00.jpg", alt: "Picture of a screwdriver and a circuit board", chapter: "framed"}}}

Il s'agit d'un livre sur l'enseignement des ((ordinateurs)). Les ordinateurs
sont à peu près aussi aussi courants que les tournevis aujourd'hui, mais ils
sont un peu plus complexes, et leur faire faire ce que vous voulez n'est pas
toujours facile.

Si la tâche que vous confiez à votre ordinateur est courante et bien comprise,
comme vous montrer vos e-mails ou agir comme une calculatrice, vous
vous pouvez ouvrir l'((application)) appropriée et vous mettre au travail.
Mais pour des tâches uniques ou ouvertes, il n'y a probablement pas d'application.

C'est là que la ((programmation)) peut intervenir. La _Programmation_ est l'acte de
construire un _programme_, c'est-à-dire un ensemble d'instructions précises indiquant à un ordinateur ce qu'il doit faire. Parce que les ordinateurs sont des bêtes stupides et pédantes, la programmation est fondamentalement fastidieuse et frustrante.

{{index [programming, "joy of"], speed}}

Heureusement, si vous pouvez passer outre ce fait, et peut-être même apprécier
la rigueur de penser en termes que les machines muettes peuvent traiter, la programmation peut être enrichissante. Elle vous permet de faire en quelques
secondes des choses qui prendraient une _éternité_ à la main. C'est un moyen de
faire faire des choses à votre outil informatique à qu'il ne pouvait pas faire
avant. C'est aussi un merveilleux exercice de pensée abstraite.

La plupart des programmes sont réalisés avec des ((langages de programmation)). Un _langage de programmation_ est un langage construit artificiellement utilisé pour instruire les ordinateurs. Il est intéressant de constater que le moyen le plus
efficace que nous ayons trouvé pour communiquer avec un ordinateur emprunte
autant à la manière dont nous communiquons entre nous. Comme les langues
humaines, les langues informatiques permettent aux mots et aux phrases d'être
combinés de nouvelles façons, ce qui rend possible d'exprimer des concepts
toujours nouveaux.

{{index [JavaScript, "availability of"], "casual computing"}}

Il fut un temps où les interfaces basées sur le langage, comme les invites
BASIC et DOS des années 1980 et 1990, étaient la principale méthode
d'interaction avec les ordinateurs. Elles ont été largement remplacées par des interfaces visuelles qui sont plus faciles à apprendre mais offrent moins de
liberté. Les langages informatiques sont toujours là, si vous savez où chercher.
L'un de ces langages, JavaScript, est intégré à tous les navigateurs modernes
et est donc disponible sur presque tous les appareils.

{{indexsee "web browser", browser}}

Ce livre essaiera de vous familiariser suffisamment avec ce langage pour que vous puissiez faire des choses utiles et amusantes avec lui.

## A propos de la programmation

{{index [programming, "difficulty of"]}}

En plus d'expliquer JavaScript, je vais introduire les principes de base
de la programmation. Il s'avère que la programmation est difficile. Les règles fondamentales sont simples et claires, mais les programmes construits au-dessus
de ces règles ont tendance à devenir assez complexes pour introduire leurs
propres règles et leur propre complexité. Vous construisez votre propre
labyrinthe, d'une certaine manière, et vous pourriez vous y perdre.

{{index learning}}

Il y aura des moments où la lecture de ce livre sera terriblement frustrante.
Si débutez la programmation, il y aura beaucoup de nouvelles informations
à assimiler. Une grande partie de ces informations seront ensuite _combinée_ d'une manière qui vous obligera à établir des liens supplémentaires.

C'est à vous de faire les efforts nécessaires. Lorsque vous avez du mal à
à suivre le livre, ne tirez pas de conclusions hâtives sur vos propres capacités.
Tout va bien, tout est parfaitement normal, vous devez simplement persévérer.
Faites une pause, relisez certains documents, et assurez-vous de lire et de
comprendre les programmes d'exemple et les ((exercices)). L'apprentissage est
un travail difficile, mais tout ce que vous apprenez vous appartient et
facilitera votre apprentissage ultérieur.

{{quote {author: "Ursula K. Le Guin", title: "The Left Hand of Darkness"}

{{index "Le Guin, Ursula K."}}

Quand l'action n'est pas rentable, rassemblez des informations ; quand les informations ne sont pas rentables, dormez.

quote}}

{{index [program, "nature of"], data}}

Un programme, c'est beaucoup de choses. C'est un morceau de texte tapé par un programmeur, c'est la force dirigeante qui fait faire à l'ordinateur ce qu'il
fait, ce sont des données dans la mémoire de l'ordinateur, qui elles même
contrôlent les actions effectuées sur cette même mémoire. Les analogies qui
tentent de comparer les programmes à des objets qui nous sont familiers ont
tendance à échouer. Une analogie superficiellement appropriée est celle d'une
machine - beaucoup de composants différents permettent à l'ensemble de fonctionner,
et pour que l'ensemble fonctionne, nous devons tenir compte de la façon dont
ces composants s'interconnectent et contribuent au fonctionnement de l'ensemble.

Un ((ordinateur)) est une machine physique qui sert d'hôte à ces machines
immatérielles. Les ordinateurs eux-mêmes ne peuvent faire que des choses stupidement simples. La raison pour laquelle ils sont si utiles est qu'ils font ces choses à
une ((vitesse)) incroyablement élevée. Un programme peut ingénieusement combiner un
nombre énorme de ces actions simples pour faire des choses très compliquées.

{{index [programming, "joy of"]}}

Un programme est une construction de la pensée. Il est gratuit à construire,
il est léger, et il grandit facilement sous nos mains qui le tapent.

Mais si l'on n'y prend garde, la taille et la ((complexité)) d'un programme
deviendront incontrôlables, même pour la personne qui l'a créé. Garder les programmes sous contrôle est le principal problème de la programmation. Quand un programme fonctionne, il est beau. L'art de la programmation est la capacité
à contrôler la complexité. Le grand programme est maîtrisé - simple dans sa
complexité.

{{index "programming style", "best practices"}}

Certains programmeurs pensent que la meilleure façon de gérer cette complexité est d'utiliser seulement un petit ensemble de techniques bien comprises dans leurs programmes. Ils ont composé des règles strictes ("meilleures pratiques")
prescrivant la forme que les que les programmes doivent avoir et restent ainsi
soigneusement dans cette petite zone des "meilleures pratiques".

{{index experiment}}

Ce n'est pas seulement ennuyeux, c'est aussi inefficace. Les nouveaux problèmes
exigent souvent de nouvelles solutions. Le domaine de la programmation est
jeune et se développe encore rapidement, et il est suffisamment varié pour laisser la place à des approches très différentes. Il y a beaucoup d'erreurs terribles
à faire dans la conception de programmes, et vous devez faire un maximum de ces
erreurs afin de les comprendre. Le sens de ce qu'est un bon programme se
développe dans la pratique, et pas à partir d'une liste de règles.

## Pourquoi le langage est important

{{index "programming language", "machine code", "binary data"}}

Au début, à la naissance de l'informatique, il n'y avait pas de langage
de programmation. Les programmes ressemblaient à quelque chose comme ça :

```{lang: null}
00110001 00000000 00000000
00110001 00000001 00000001
00110011 00000001 00000010
01010001 00001011 00000010
00100010 00000010 00001000
01000011 00000001 00000000
01000001 00000001 00000001
00010000 00000010 00000000
01100010 00000000 00000000
```

{{index [programming, "history of"], "punch card", complexity}}

C'est un programme qui additionne les nombres de 1 à 10 et qui imprime le résultat.
le résultat : `1 + 2 + ... + 10 = 55`. Il pourrait fonctionner sur une simple,
machine hypothétique. Pour programmer les premiers ordinateurs, il était nécessaire de
placer de grandes séries d'interrupteurs dans la bonne position ou percer des trous dans des bandes de carton et les transmettre à l'ordinateur. Vous pouvez probablement
imaginer combien cette procédure était fastidieuse et sujette aux erreurs. Même l'écriture de programmes simples exigeait beaucoup d'ingéniosité et de discipline.
Les programmes complexes étaient presque irréalisables.


{{index bit, "wizard (mighty)"}}

Bien sûr, la saisie manuelle de ces schémas obscurs de bits (les uns
et les zéros) donnait au programmeur le sentiment profond d'être un puissant
magicien. Et cela doit valoir quelque chose en termes de satisfaction
professionnelle.

{{index memory, instruction}}

Chaque ligne du programme précédent contient une seule instruction. Elle
pourrait être écrit en anglais comme ceci :

 1. Stocker le nombre 0 dans l'emplacement mémoire 0.
 2. Enregistrez le numéro 1 dans l'emplacement mémoire 1.
 3. Enregistrez la valeur de l'emplacement mémoire 1 dans l'emplacement mémoire 2.
 4. Soustrayez le nombre 11 de la valeur de l'emplacement mémoire 2.
 5. Si la valeur de l'emplacement mémoire 2 est le nombre 0,
    continuez avec l'instruction 9.
 6. Ajoutez la valeur de l'emplacement mémoire 1 à l'emplacement mémoire 0.
 7. Ajoutez le nombre 1 à la valeur de l'emplacement mémoire 1.
 8. Continuez avec l'instruction 3.
 9. Affichez la valeur de l'emplacement mémoire 0.


{{index readability, naming, binding}}

Bien que ce soit déjà plus lisible que la soupe de bits, c'est encore
encore assez obscur. L'utilisation de noms au lieu de chiffres pour les
instructions et les emplacements mémoire.

```{lang: "text/plain"}
 Set “total” to 0.
 Set “count” to 1.
[loop]
 Set “compare” to “count”.
 Subtract 11 from “compare”.
 If “compare” is zero, continue at [end].
 Add “count” to “total”.
 Add 1 to “count”.
 Continue at [loop].
[end]
 Output “total”.
```

{{index loop, jump, "summing example"}}

Pouvez-vous voir comment le programme fonctionne à ce stade ? Les deux
premières lignes donnent à deux emplacements mémoire leurs valeurs de départ:
`total` sera utilisé pour construire le résultat du calcul, et `count`
gardera une trace du nombre que nous sommes en train de regarder. Les lignes
utilisant `compare` sont probablement les plus étranges. Le programme veut
voir si `count` est égal à 11 pour décider s'il peut arrêter de fonctionner.
Parce que notre machine hypothétique est plutôt primitive, elle peut seulement
tester si un nombre est égal à zéro et prendre une décision basée
sur cette base. Donc elle utilise l'emplacement mémoire nommé `compare` pour
calculer la valeur de `count - 11` et prend une décision en fonction de cette
valeur. Les deux lignes suivantes ajoutent la valeur de `count` au résultat et
incrémentent `count` de 1 chaque fois que le programme a décidé que `count`
n'est pas encore 11.

Voici le même programme en JavaScript:

```
let total = 0, count = 1;
while (count <= 10) {
  total += count;
  count += 1;
}
console.log(total);
// → 55
```

{{index "while loop", loop, [braces, block]}}

Cette version nous apporte quelques améliorations supplémentaires. La plus
importante est qu'il n'est plus nécessaire de spécifier la façon dont nous
voulons que le programme saute d'avant en arrière. La construction `while`
s'en charge. Elle continue l'exécution du bloc (entouré d'accolades) situé
en dessous de lui tant que la condition qui lui a été donnée est vérifiée.
Cette condition est `count <= 10`, ce qui signifie signifie "_count_ est
inférieur ou égal à 10". Nous n'avons plus besoin de créer une valeur
temporaire et la comparer à zéro, ce qui était juste un détail sans intérêt.
Une partie de la puissance des langages de programmation est qu'ils peuvent
s'occuper des détails sans intérêt pour nous.

{{index "console.log"}}

A la fin du programme, après que la construction `while` soit terminée,
l'opération `console.log` est utilisée pour écrire le résultat.

{{index "sum function", "range function", abstraction, function}}

Enfin, voici à quoi pourrait ressembler le programme si nous disposions
des opérations pratiques `range` et `sum`, qui créent respectivement
une ((collection)) de nombres dans une plage et calculent la somme d'une
collection de nombres :

```{startCode: true}
console.log(sum(range(1, 10)));
// → 55
```

{{index readability}}

La morale de cette histoire est que le même programme peut être exprimé
de manière longue et courte, illisible et lisible. La première version du
programme était extrêmement obscure, alors que cette dernière est presque
de l'Anglais : `log` la `sum` de la `range` de nombres de 1 à 10.
(Nous verrons dans [les chapitres suivants](data) comment définir des
opérations comme `sum` et `range`).

{{index ["programming language", "power of"], composability}}

Un bon langage de programmation aide le programmeur en lui permettant de
de parler des actions que l'ordinateur doit effectuer à un niveau supérieur.
Il permet d'omettre les détails, fournit des blocs de construction pratiques
(comme `while` et `console.log`), permet de définir vos propres blocs de
construction (tels que `sum` et `range`), et rend ces blocs faciles à composer.

## Qu'est ce que JavaScript?

{{index history, Netscape, browser, "web application", JavaScript, [JavaScript, "history of"], "World Wide Web"}}

{{indexsee WWW, "World Wide Web"}}

{{indexsee Web, "World Wide Web"}}

JavaScript a été introduit en 1995 comme moyen d'ajouter des programmes
aux pages Web dans le navigateur Netscape Navigator. Le langage a depuis été
adopté par tous les autres principaux navigateurs Web graphiques. Il a
rendu possible les applications web modernes, des applications avec
lesquelles vous pouvez interagir directement sans avoir à recharger la
page à chaque action. JavaScript est également utilisé dans des sites Web
plus traditionnels pour fournir diverses formes d'interactivité et
d'ingéniosité.

{{index Java, naming}}

Il est important de noter que JavaScript n'a presque rien à voir avec
le langage de programmation appelé Java. Le nom similaire a été inspiré par
des considérations marketing plutôt qu'un bon jugement. Lorsque JavaScript
a été introduit, le langage Java a été fortement commercialisé et
gagnait en popularité. Quelqu'un a pensé que c'était une bonne idée
d'essayer de de profiter de ce succès. Maintenant, nous sommes coincés
avec ce nom.

{{index ECMAScript, compatibility}}

Après son adoption en dehors de Netscape, un document ((standard)) a été
écrit pour décrire la façon dont le langage JavaScript devait fonctionner
afin que que les différents logiciels qui prétendaient supporter JavaScript
parlent en fait du même langage. Ce document s'appelle la norme ECMAScript,
d'après l'organisation Ecma International qui a procédé à la normalisation.
En pratique, les termes ECMAScript et JavaScript sont interchangeables,
ce sont deux noms pour le même langage.

{{index [JavaScript, "weaknesses of"], debugging}}

Il y a ceux qui disent des choses _horribles_ sur JavaScript. Beaucoup
de ces choses sont vraies. Quand on m'a demandé d'écrire quelque chose en
JavaScript pour la première fois, j'ai rapidement commencé à le mépriser.
Il acceptait presque tout ce que je tapais mais l'interprétait d'une manière
qui était complètement différente de ce que je voulais dire. Cela avait
beaucoup à voir avec le le fait que je n'avais pas la moindre idée de ce
que je faisais, bien sûr, mais il y a un vrai problème ici: JavaScript est
ridiculement libéral dans ce qu'il ce qu'il permet. L'idée derrière cette
conception était qu'elle rendrait la programmation en JavaScript plus facile
pour les débutants. En réalité, cela rend surtout de trouver des problèmes
dans vos programmes plus difficile parce que le système ne vous les
signalera pas.

{{index [JavaScript, "flexibility of"], flexibility}}

Mais cette flexibilité a aussi ses avantages. Elle laisse de la place pour
beaucoup de techniques qui sont impossibles dans des langages plus rigides,
et comme vous le verrez (par exemple dans le [Chapitre ?](modules)), elle
peut être utilisée pour surmonter certains des défauts de JavaScript. Après
avoir ((appris)) le langage correctement et avoir travaillé avec lui pendant
un certain temps, j'ai appris à _aimer_ JavaScript.

{{index future, [JavaScript, "versions of"], ECMAScript, "ECMAScript 6"}}

Il y a eu plusieurs versions de JavaScript. ECMAScript version 3 était la
version la plus répandue à l'époque de la montée en puissance de JavaScript,
en gros entre 2000 et 2010. Pendant ce temps, des travaux étaient en cours
sur une version 4 ambitieuse, qui prévoyait un certain nombre d'améliorations
et d'extensions radicales du langage. Changer un langage vivant et largement
utilisé de manière aussi radicale s'est avérée politiquement difficile, et
les travaux sur la version 4 ont été abandonnés en 2008 pour produire
une version 5 beaucoup moins ambitieuse, qui n'apportait que quelques
améliorations non controversées, sortie en 2009. Puis, en 2015, la version 6
est sortie, une mise à jour majeure qui incluait certaines des idées prévues
pour la version 4. Depuis lors, nous avons eu de nouvelles petites mises à
jour chaque année.

Le fait que le langage évolue signifie que les navigateurs doivent
constamment suivre le rythme, et si vous utilisez un ancien navigateur, il
se peut qu'il ne prenne pas en charge toutes les fonctionnalités. Les
concepteurs du langage veillent à ne pas apporter de modifications susceptibles
de casser les programmes existants de manière a ce que les nouveaux navigateurs
puissent toujours exécuter les anciens programmes. Dans ce livre, j'utilise
la version 2017 de JavaScript.

{{index [JavaScript, "uses of"]}}

Les navigateurs Web ne sont pas les seules plateformes sur lesquelles
JavaScript est utilisé. Certaines bases de données, comme MongoDB et CouchDB,
utilisent JavaScript comme langage de script et d'interrogation. Plusieurs
plateformes de programmation de bureau et de serveur notamment le projet
((Node.js)) (qui fait l'objet du [Chapitre ?](node)), fournissent
un environnement de programmation JavaScript en dehors du navigateur.

## Le code et que faire avec

{{index "reading code", "writing code"}}

Le _code_ est le texte qui compose les programmes. La plupart des chapitres
de ce livre contiennent beaucoup de code. Je pense que lire du code et écrire
du ((code)) sont des éléments indispensables pour ((apprendre)) à programmer.
Essayez de ne pas vous contenter de survoler les exemples, lisez-les
attentivement et comprenez-les. Cela peut être lent et déroutant au début,
mais je vous promets que vous allez rapidement y arriver. Il en va de même
pour les ((exercices)). Ne supposez  pas que vous les comprenez avant
d'avoir écrit une solution qui fonctionne.

{{index interpretation}}

Je vous recommande d'essayer vos solutions aux exercices dans un véritable
interpréteur JavaScript. De cette façon, vous aurez un retour immédiat sur
si ce que vous faites fonctionne, et, je l'espère, vous serez tentés
d'((expérimenter)) et d'aller au-delà des exercices.

{{if interactive

Lorsque vous lisez ce livre dans votre navigateur, vous pouvez éditer
(et exécuter) tous les programmes d'exemple en cliquant sur le cadre.

if}}

{{if book

{{index download, sandbox, "running code"}}

Le moyen le plus simple d'exécuter les exemples de code du livre et
d'expérimenter est de le consulter dans la version en ligne du livre à
l'adresse suivante [_https://eloquentjavascript.net_] (https://eloquentjavascript.net/). Là-bas, vous pouvez cliquer sur n'importe quel exemple de code pour l'éditer,
l'exécuter et voir la sortie qu'il produit. Pour travailler sur les exercices,
rendez-vous sur [_https://eloquentjavascript.net/code_](https://eloquentjavascript.net/code), qui fournit le code de départ de chaque exercice de programmation et
vous permet de voir les solutions.

if}}

{{index "developer tools", "JavaScript console"}}

Si vous voulez exécuter les programmes définis dans ce livre en dehors du
site Web du livre, vous devrez vous appliquer a choisir votre environment.
De nombreux exemples sont autonomes et devraient fonctionner dans n'importe quel environnement JavaScript. Mais le code des chapitres ultérieurs est souvent
écrit pour un environnement spécifique (le navigateur ou Node.js) et ne
peut s'exécuter que dans cet environnement. En outre, de nombreux chapitres
définissent des programmes plus importants, et les morceaux de code qui
y figurent dépendent les uns des autres ou de fichiers externes. Le site
[sandbox] (https://eloquentjavascript.net/code) sur le site Web fournit des
des liens vers des fichiers Zip contenant tous les scripts et les fichiers
de données nécessaires à l'exécution du code d'un chapitre donné.

## Apercu de ce livre

Ce livre se compose en gros de trois parties. Les 12 premiers chapitres traitent
du langage JavaScript. Les sept chapitres suivants traitent des navigateurs
((navigateurs)) et la façon dont JavaScript est utilisé pour les programmer.
Enfin, deux chapitres sont consacrés à ((Node.js)), un autre environnement
pour programmer avec JavaScript.

Tout au long du livre, il y a cinq _chapitres de projet_, qui décrivent des
programmes d'exemple plus importants pour vous donner un aperçu de la
programmation réelle. Dans l'ordre d'apparition, nous travaillerons à la
construction d'un [robot de livraison](robot), un [langage de programmation](langage), un [jeu de plateforme plate-forme](game), un [programme de peinture en pixels](paint) et un [site Web dynamique](skillsharing).

La partie du livre consacrée au langage commence par quatre chapitres qui
présentent la structure de base du langage JavaScript. Ils introduisent les
[structures de contrôle](program_structure) (comme le mot `while` que vous
avez vu dans cette introduction), les [fonctions](fonctions) (écriture de
vos propres blocs de construction), et les [structures de données](data).
Après cela, vous serez capable d'écrire des programmes de base. Les
chapitres suivants, [?](higher_order) et [?](object) introduisent des techniques d'utilisation des fonctions et des objets pour écrire pour écrire du code plus _abstrait_ et garder la complexité sous contrôle.

Après un [chapitre sur le premier projet](robot), la partie langage du livre
se poursuit avec des chapitres sur [la gestion des erreurs et la correction des bogues](error), les [expressions régulières](regexp) (un outil important pour
travailler avec du texte), [la modularité](modules) (une autre défense contre
la complexité), et la [programmation asynchrone](async) (gestion des événements
qui prennent du temps). Le [deuxième chapitre du projet](language) conclut la
première partie du livre.

La deuxième partie, les chapitres [?](browser) jusqu'à [?](paint), décrivent les
outils auxquels le JavaScript du navigateur a accès. Vous apprendrez à afficher
des choses à l'écran (chapitres [?](dom) et [?](canvas)), à répondre à la
l'entrée de l'utilisateur ([Chapitre ?](event)), et à communiquer sur le réseau
([Chapitre ?](http)). Il y a encore deux chapitres de projet dans cette
partie.

Ensuite, le [chapitre ?](node) décrit Node.js, et le [chapitre ??](skillsharing) construit un petit site Web à l'aide de cet outil.

{{if commercial

Enfin, le [chapitre ?] (fast) décrit certaines des considérations qui
interviennent lors de l'optimisation des programmes JavaScript pour la vitesse.

if}}

## Conventions typographiques

{{index "factorial function"}}

Dans ce livre, le texte écrit dans une police `monospaced`représente des
éléments de programmes - parfois ce sont des fragments autosuffisants, et
parfois ils font simplement référence à une partie d'un programme voisin.
Les programmes (dont dont vous avez déjà vu quelques-uns) sont écrits comme
suit :

```
function factorial(n) {
  if (n == 0) {
    return 1;
  } else {
    return factorial(n - 1) * n;
  }
}
```

{{index "console.log"}}

Parfois, pour montrer la sortie d'un programme, la sortie attendue est écrite
après celle-ci, avec deux barres obliques et une flèche.

```
console.log(factorial(8));
// → 40320
```

Good luck!

# Jeu du pendu en python, étape par étape.


### 1. Choisir un mot :

Il faut pouvoir choisir un mot avant de démarrer le jeu, pour se faire, on peut prendre un mot "aléatoire" provennant du dictionnaire ou bien demander à un second utilisateur de choisir le mot.

Dans l'option 1, le mot aléatoire peut être défini par une liste `["mot1", "mot2"]`... sachant qu'une liste, en python peut être vue comme un dictionnaire où chaque clé est en réalité un indice.
On peut alors voir une liste comme ceci : `{0: "mot1", 1: "mot2"}`, ainsi, si on souhaite accéder au premier élément de la liste, il suffit de faire : `ma_liste[0]`.   
On peut alors aisaiment demandé un numéro aléatoire avec les fonctions du module `Random`. Il suffit alors uniquement de connaître la taille de la liste récupérable avec la fonction `len(ma_liste)`. Pour demander un nombre aléatoire entre 0 et `len(ma_liste)`.


### 2. Savoir si une lettre fait partie du mot : 

Une fois le mot stocké en mémoire (dans une variable `mot_courrant = mots[indice_aleatoire]`) il faut pouvoir faire 2 choses : 
1. Demander à l'utilisateur d'entrer un caractère.
2. Vérifier que ce caractère soit présent dans le mot.

On peut vérifier qu'un caractère est dans un mot en utilisant le mot clé `in` qui renvoie un booléen (`True` ou `False`). 
Dans ce cas, on distingue 3 cas : 
1. Le caractère entré par l'utilisateur n'est pas dans le mot ; dans ce cas, il faut compter une erreur supplémentaire à l'utilisateur.
2. Le caractère entré par l'utilisateur est présent dans le mot ; dans ce cas, il faut alors conserver cette lettre quelque part (une liste, un ensemble...).
3. Le caractère entré par l'utilisateur a déjà été proposé ; dans ce cas, il ne faut rien faire (ou compter cela comme une erreur).

## 3. Boucler jusqu'à ce que le jeu soit terminé :

Maintenant que nous sommes capable de choisir un mot, que nous pouvons demander à l'utilisateur de proposer une caractère et que nous somme capable de distringuer le cas où le caractère est présent dans le mot ou non, il faut boucler jusqu'à ce que le jeu soit terminé.
Dans quels cas le jeu est-il terminé ? On retrouve encore une fois deux cas :
1. Le joueur a trouvé le mot dans le nombre d'essais qui lui étaient impartis.
2. Le joueur a utilisé trop de tentative, il se retrouve alors pendu !

<!-- -->

1. Dans l'étape 2. nous étions capable de récupérer de la part du joueur les caractères qu'il propose. On stockait alors ces caractères dans une structure de données. Il faut alors être câpable de déterminer quand un mot est trouvé. Pour se faire, il existe plusieurs méthodes, voici quelques exemples : 
    1. On peut ranger le mot initial (`mot_courrant`) dans l'ordre alphabétique, et retirer les doublons. Ainsi, lorsqu'on veut vérifier que l'ensemble des lettre données par le joueur correspond à la combinaison, on a juste à ranger dans ce même ordre notre liste et les comparer.
    2. On peut maintenir un ensemble de lettres. Un ensemble est une structure de données qui ressemble aux listes à l'exception que dans un ensemble, on ne peut trouver qu'une seule et unique fois la même occurrence. Si par exemple, on a le mot, `mot_courrant="bonjour"`, on aurait l'ensemble : `{"b", "o", "n", "j", "u", "r"}`, On remarque alors que le "o" n'apparaît qu'une seule fois. Ensuite, il suffira alors, pour chaque proposition du joueur, de vérifier que la lettre apparaît dans le mot. Si oui, on ajoute la lettre dans un autre ensemble, si non, on retire une tentative. Si par exemple, l'utilateur entre dans cet ordre les lettres : "a", "b", "j" on aura un second ensemble qui ressemblera à `{"b", "j"}`.


2. Enfin, nous devons stopper le jeu dans le cas où l'utilisateur s'est trompé trop de fois. Nous avions déjà compté le nombre de fois où le joueur s'est trompé. Avec cette information, nous sommes capâble de demander à la boucle de s'arrêter lorsque nous dépassons un nombre de tentative fixé arbitrairement.

Une fois ces deux conditions réunis, il suffit alors de faire notre boucle `while`, on doit alors lire "Tant que *le mot n'est pas trouvé* **OU** *le nombre de tentative n'est pas dépassé*, alors, on continue de demander une lettre à l'utilisateur.

### 4. Pour aller plus loin :

Si toutes les étapes du dessus ont été réalisé, nous devrions avoir un jeu du pendu fonctionnel, puisque, nous sommes câpable de choisir un mot, lire l'entrée du joueur, vérifier que sa lettre est présente dans le mot. Si elle ne l'est pas, on est câpable de lui compter une erreur. On est également en capacité de detecter la fin de jeu, que ce soit une fin gagnante ou une fin perdante. Cependant, notre jeu manque un peu d'affichage. Je propose donc d'ajouter des informations à l'utilisateur.
Normalement, dans le jeu du pendu, on peut voir la première (et parfois la dernière lettre) ainsi que le nombre de lettre manquante. Je propose donc de refaire cet affichage.

Pour se faire, lorsque le mot est choisit, nous allons récupérer trois informations, la première, la dernière lettre du mot ainsi que sa taille.   
Pour récupérer la première et dernière lettre du mot, il faut voir les chaînes de caractères comme des listes de caractères. Ainsi, lorsque l'on sait cela, on se rend compte qu'on peut accéder à n'importe quel caractère de la même manière qu'on accéderai à un élément d'une liste. Avec les crochets `[]`. Par exemple, pour récupérer la première lettre du mot courrant, on peut faire : `mot_courrant[0]`. Je te laisse voir comment récupérer la dernière lettre ainsi que la taille ;).  
Une fois ces trois informations récupérées. On peut, dans une nouvelle variable, stocker notre chaîne de caractères à afficher à l'utilisateur. Si le mot choisit est "bonjour", on veut afficher "b_____r" à l'utilisateur. Ce qu'on fait en faisant cela, c'est afficher la première lettre, la taille de la chaîne de caractère - 2 et la dernière lettre du mot.   
(*à savoir qu'en python, on peut multiplier les caractères, en faisant*
```py
cri="A" * 3
print(cri)
```
*On obtiendra : `AAA`*).

Maintenant, nous sommes capable d'afficher, en début de partie la première lettre, la dernière et la taille du mot, mais on ne resepcte toujours pas le jeu du pendu, qui veut qu'on affiche les lettres lorsqu'elles sont découvertes par le joueur. 

Pour faire cela, lors que le joueur entre une lettre présente dans le mot, il faut aller chercher l'indice à laquelle cette lettre est présente. On peut faire ça avec la méthode [offerte par Python](https://docs.python.org/3/library/stdtypes.html#str.find) : `find()`. Seulement, nous avons un problème ici, la méthode `find` renvoie uniquement l'indice de la première occurence. Dans notre exemple du mot `bonjour`, on a 2 fois la lettre "o". En faisant `"bonjour".find("o")` on aurait alors `1` en sortie.
Je propose donc de regarder la doc de la méthode afin de constater qu'on a 3 paramètres possibles, le caractère rechercher, l'indice de départ et l'indice de fin de la recherche. Ce troisième paramètre ne nous intéresse pas, car si on ne le donne pas, Python va prendre par défaut le mot jusqu'au bout.

On peut donc jouer avec le deuxième paramètre. Une autre information importante nous est donné dans la documentation ; si le caractère rechercher n'est pas trouvé, la fonction renvoie -1.
Utilisons toutes ces informations à notre avantage afin de modifier la chaîne affiché à l'utilisateur. 
Voici la solution :   
Ecrire une boucle Tant que *indice* différent de -1 ; **chercher la prochaine occurence\*** de la lettre dans le mot et **remplacer le `_` par cette lettre\***.

* **Chercher la prochaine occurence** : Pour se faire, il faut utiliser la méthode find ainsi :
 `indice = mot.find(lettre, indice)`
* **remplacer le `_` par cette lettre** : Pour se faire, tu peux utiliser cette méthode :
  `mot_a_afficher = mot_a_afficher[:indice] + lettre + mot_a_afficher[indice + 1:]`.


<details><summary>Je suis conscient que cette partie peut paraître un peu compliquée, je te propose donc une solution mais je t'invite à chercher par toi-même avant de la regarder !  </summary>
  <pre>
    Tu as vraiment chercher par toi-même ? 🤔
  </pre>
  <details><summary>Très bien, voici ma solution ! </summary>
    <pre>
      if lettre in mot_courrant:
      indice = mot_courrant.find(lettre)
      while indice != -1:
      	mot_a_afficher = mot_a_afficher[:indice] + lettre + mot_a_afficher[indice + 1:]
      	indice = mot_courrant.find(lettre, indice + 1)
    </pre>
  </details>
</details>

Avec ça, tu devrais avoir un jeu du pendu fonctionnel ! 

### 5. Améliorations possibles :

Il reste quelques points d'améliorations que tu peux travailler si tu t'ennuies :
1. Afficher le pendu (en ASCII Art)
2. Contrôler l'input utilisateur. Actuellement, le joueur peut écrire n'importe quoi (des chiffres, des lettres, des caractères spéciaux...) et surtout, de n'importe quelle taille.
3. Gérer la casse (MAJ/min) pour pas que l'utilisateur se retrouve avec des erreurs parce qu'il a écrit en majuscule.
4. Gérer le cas des mots composés.
5. ....

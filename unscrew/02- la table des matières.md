# La gestion de la table des matière

### Le cas général :

De manière générale, on utilise la commande ```\tableofcontents``` qui fonctionne très bien en elle-même. Néammoins, il peut arriver que l'on cherche des effets de style particulier.

>[!TIP]
>De même que le titre peut être mis par défaut en début de document, il peut aussi être intéressabt de mettre une table des matière systématique en fin de document. Pour cela on glissera la commande ```\tableofcontents``` dans un ```\AtEndDocument{...}```

### Pour le cas des rapports

Dans le cas des rapports, on met la table des matières en début de document, ce qui ne pose pas de problème pour la classe ```article``` mais qui est plus ardu pour la classe ```report```. Pour gérer ce soucis, et modifier avec plus de liberté la table des matières, on utilise le package ```tocloft```.

En premier lieu, on cherche à enlever l'entête de la table des matière : le package ```tocloft``` le permet avec le code suivant

>```
> \makeatletter
> \renewcommand{\@cftmaketoctitle}{}
> \makeatother
>```

Ensuite, on va règler l'espacement entre les lignes : ```\setlength\cftparskip{2pt}```

Dans les styles 2 et 3, il est aussi nécessaire de réindenter la table des matières : on le fait avec le code suivant :
>```
>\cftsetindents{section}{1em}{2em}
>\cftsetindents{subsection}{2em}{2em}
>```

Dans le style 1, un problème apparait quand à l'utilisation de ```\chapter{\thetitle}``` au lieu de ```\maketitle```. En effet, ceci entraine l'ajout d'une ligne dans la table des matières car le document considère que l'on commence en chapitre. Cet ajout n'est pas toujours gênant (notamment dans le cas des __polycopiés de cours__) mais ici on ne veut pas de cette ligne. Ainsi, on va locelement modifier la limite de profondeur de la table des matières afin d'ignorer momentanément le ```\chapter``` : mettons cela dans une macro :

>```
>\newcommand{\hidechapter}[0]{
>\addtocontents{toc}{\protect\setcounter{tocdepth}{-10}}
>\chapter{\thetitle}
>\addtocontents{toc}{\protect\setcounter{tocdepth}{4}}
>}
>```

<details>
<summary><b>Détails ligne à ligne</b></summary>

> ```\newcommand{\hidechapter}[0]{``` on commence la définition d'une macro sans paramère

> ```\addtocontents{toc}{\protect\setcounter{tocdepth}{-10}}``` on ajoute à la table des matière la commande ```\setcounter{tocdepth}{-10}``` qui modifie la profondeur de sorte que les chapitres ne soit pas visible. Cependant, la table des matière n'est pas directement manipulé et est stocker dans un fichier annexe caché, donc l'ajout de commande doit être "protéger" pour le transport du préambule au document de table des matières : d'où le ```\protect``` avant la commande.

> ```\chapter{\thetitle}``` on fait le titre comme expliquer dans __01- le titre__

> ```\addtocontents{toc}{\protect\setcounter{tocdepth}{4}}``` on remet la profondeur à la valeur par défault que l'on souhaite

> ```}``` 

</details>

Et finalement, on utilise ```\AtBeginDocument{\hidechapter}``` au lieu d'un simple ```\AtBeginDocument{\chapter{\thetitle}}```.

>[!IMPORTANT]
>On pourrait ici se passer de préciser ```\thetitle``` dans la redéfinition de la commande ```\@makechapterhead```. Par uniformisation des préambules proposés dans ce repo, on le laisse ainsi même si ce n'est utile que si l'on conserve la ligne du chapitre dans la table des matières.

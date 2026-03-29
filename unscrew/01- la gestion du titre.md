# La gestion du titre

### Le cas général :

Au cas général, on utilise la commande ```\maketitle``` en début de document

>[!TIP]
>Pour les plus paresseux, cette commande peut être inséré dans un ```\AtBeginDocument{...}``` afin de s'économiser son écriture à chaque début de document

>[!WARNING]
>Cette commande admet trois paramètre implicites : la date, l'auteur et le titre. Ces derniers sont respectivement défininis dans le préambule par les commandes :
>
> - ```\date{...}``` pour la date
> - ```\author{...}``` pour l'auteur
> - ```\title{...}``` pour le titre
>
>Ces trois commandes ne peuvent être retirées, dans le cas où l'on ne veut pas définir un de ces paramètre, on n'y mettra simplement pas d'argument.

### Pour le cas des *rapports* :

En plus des "auteurs" définis par la commandes dédiée, on veut ici ajouter le nom du directeur de stage. À cet effet, on ajoute la ligne 

> ```\def\thesupervisor{...}```

Son rôle est de définire une variable (`\thesupervisor`) où sera stocké la valeur *nom du directeur de stage*. Cette valeur est ensuite manuellement rajouté au début du document, pour les style 2 et 3 :

>```
> \AtBeginDocument{\maketitle
>\vspace{-15pt}
>{\footnotesize\raggedleft \thesupervisor
>
>}\vspace{10pt}}
>```

>[!NOTE]
>On utilise ici trois commandes de mise en page cruciales :
>
>- ```\vspace{...}``` qui permet le déplacement vertical positif ou négatif
>- ```\raggedleft``` qui aligne le texte à doite
>- ```\footnotesize``` qui ajuste la taille de la police

Pour le style 1, la chose se corse : on ne va pas utiliser de ```\maketitle``` mais plutôt définir notre propre entête en changeant la commande ```\chapter{...}``` 

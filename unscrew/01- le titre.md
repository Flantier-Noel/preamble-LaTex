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

Pour le style 1, la chose se corse : on ne va pas utiliser de ```\maketitle``` mais plutôt définir notre propre entête en changeant la commande ```\chapter{...}```. Détaillons la procédure :

- On commence par récupérer/stocker les infos que l'on veut ajouter dans le titre :

> ```
>\makeatletter
>\let\thetitle\@title
>\let\theauthor\@author
>\let\thedate\@date
>\makeatother
>```

- On modifie la commande ```\@makechapterhead``` afin de créer l'entête de chapitre selon le style souhaité :
>```
>\makeatletter
>\renewcommand{\@makechapterhead}[1]{
>  \vspace*{50\p@}
>  {\parindent \z@ \centering \normalfont
>    \hrule height 3pt \vskip 5\p@
>    \hrule height 2pt \vskip 20\p@
>    \interlinepenalty\@M
>    \Huge\bfseries \thetitle\par\nobreak
>    \vskip 15\p@
>    \hrule height 2pt \vskip 5\p@
>    \raggedright\small\theauthor \\[-0.4cm]
>    \raggedleft\normalfont\small\thesupervisor
>  \vskip 20\p@}}
>\makeatother
>```

<details>
<summary><b>Détails ligne à ligne</b></summary>

> ```\makeatletter``` on s'autorise l'usage du symbole ```@```

> ```\renewcommand{\@makechapterhead}[1]{``` on commence la redéfinition de la commande ```\@makechapterhead```

> ```\vspace*{50\p@}``` on ajuste verticalement

> ```{\parindent \z@ \centering \normalfont``` on centre et ajuste la taille de police

> ```\hrule height 3pt \vskip 5\p@``` on dessine une ligne horizontale
> 
> ```\hrule height 2pt \vskip 20\p@``` on dessine une ligne horizontale

> ```\interlinepenalty\@M``` ?

> ```\Huge\bfseries \thetitle\par\nobreak``` on écrit le titre en gros (```\Huge```) et en gras (```bfseries```)

> ```\vskip 15\p@``` on laisse un petit blanc vertical

> ```\hrule height 2pt \vskip 5\p@``` on dessine une ligne horizontale

> ```\raggedright\small\theauthor \\[-0.4cm] ``` on écrit le nom de l'auteur (```\theautor```) en petit (```\small```) à gauche (```\raggedright```) puis on remonte la prochaine ligne pour y écrire à droite
>
> ```\raggedleft\normalfont\small\thesupervisor ``` on écrit le nom du directeur de stage (```\thesuprevisor```) en petit en police basique (```\normalfont```) à gauche (```raggedleft```)

> ```\vskip 20\p@}}``` on conclue la redéfinition avec un peu d'espace vertical

> ```\makeatother``` on arrête d'utiliser le symbole ```@```

</details>

>[!WARNING]
> La commande ```\@makechapterhead``` n'existe que dans le type de document ```report```

# La gestion du style général de la page

En premier lieu, la taille de la page et celle de la police par défaut est définis dès la ligne :
> ```\documentclass[10pt,a4paper]{...}```
<details>
<summary><b>Détails ligne à ligne</b></summary>

La taille de la police par défaut est ici mise à ```10pt``` et la page à la format A4 (```a4paper```)
</details>

## Les marges :

Deux options s'offrent à nous :

- Le package ```geometry``` (utilisé dans les style 2 et 3 des rapports par exemple). Avec ce dernier, on pourra regler la taille des marges horizontales avec la commande :
> ```\usepackage[left=25mm, right=25mm]{geometry}```

>[!NOTE]
>Pour aller plus loin sur la paramétrisation avec ```geometry``` : [documentation en ligne](https://www.xm1math.net/doculatex/geometry.html)

- La méthode "à la main" (utilisé dans le style 1 des rapports par exemple) : on règle manuellement avec la commande ```\setlength{...}{...}```

> ```
> \setlength{\textwidth}{19cm}
>\setlength{\topmargin}{0.1cm}
>\setlength{\headsep}{0.6cm}
>\setlength{\headheight}{12mm}
>\setlength{\topskip}{0.5cm}
>\setlength{\textheight}{27cm}
>\setlength{\voffset}{-30mm}
>\setlength{\hoffset}{-32mm}
> ```

<details>
<summary><b>Détails ligne à ligne</b></summary>

>```\setlength{\textwidth}{19cm}``` on règle la largeur de la zone de texte

>```\setlength{\topmargin}{0.1cm}``` on règle la largeur de la marge du haut

>```\setlength{\headsep}{0.6cm}``` on règle la distance entre l'entête des pages et le contenu

>```\setlength{\headheight}{12mm}``` on règle la hauteur de l'entête des pages

>```\setlength{\topskip}{0.5cm}``` on règle la distance entre l'entête des pages et le contenu (redondant ?)

>```\setlength{\textheight}{27cm}``` on règle la hauteur de la zone de texte

>v\setlength{\voffset}{-30mm}``` on règle le décalage vertical par défault de la zone de texte

>```\setlength{\hoffset}{-32mm}``` on règle le décalage horizontal par défaut de la zone de texte
</details>

# L'entête de page :

Dans le style 1 des rapports (par exemple), les pages sans titre s'affublent d'une entête précisant certaines métadonnées (titre, date, ...). Dans ce but, nous utilisons le code :

>```
>pagestyle{fancy}
>\renewcommand{\chaptermark}[1]{\markboth{#1}{}}
>\rhead{\textcolor{gris}{\textit{\thedate}}}
>\lhead{\textcolor{gris}{Phasellus laoreet}}
>\chead{\textcolor{gris}{\thetitle}}
>```

<details>
<summary><b>Détails ligne à ligne</b></summary>
  
>```pagestyle{fancy}```

>```\renewcommand{\chaptermark}[1]{\markboth{#1}{}}```

>```\rhead{\textcolor{gris}{\textit{\thedate}}}```

>```\lhead{\textcolor{gris}{Phasellus laoreet}}```

>```\chead{\textcolor{gris}{\thetitle}}```
</details>

>[!WARNING]
> On utilise ici la valeur ```gris``` qui est définis plutôt avec la commande :
> >```\definecolor{gris}{gray}{.5}```

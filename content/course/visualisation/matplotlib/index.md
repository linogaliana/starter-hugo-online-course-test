---
title: "De beaux graphiques avec python: mise en pratique"
date: 2020-09-24T13:00:00Z
draft: false
weight: 10
slug: matplotlibTP
type: book
tags:
  - visualisation
  - matplotlib
  - seaborn
categories:
  - Exercice
summary: |
  Une découverte des fonctionalités graphiques de matplotlib,
  seaborn et plotly pour représenter des statistiques
  sur les décomptes de vélo à Paris
plotly: true
---


<script src="https://d3js.org/d3.v7.min.js"></script>
<script src="https://cdn.plot.ly/plotly-latest.min.js"></script>



<script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.3.6/require.min.js" integrity="sha512-c3Nl8+7g4LMSTdrm621y7kf9v3SDPnhxLNhcjFJbKECVnmZHTdo+IRO05sNLTH/D3vA6u1X32ehoLC7WFVdheg==" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.5.1/jquery.min.js" integrity="sha512-bLT0Qm9VnAYZDflyKcBaQ2gg0hSYNQrJ8RilYldYQ1FxQYoCLtUjuuRuZo+fjqhx/qtq/1itJ0C2ejDxltZVFg==" crossorigin="anonymous"></script>
<script type="application/javascript">define('jquery', [],function() {return window.jQuery;})</script>


<a href="https://github.com/linogaliana/python-datascientist/blob/master/notebooks/course/visualisation/matplotlib.ipynb" class="github"><i class="fab fa-github"></i></a>
[![Download](https://img.shields.io/badge/Download-Notebook-important?logo=Jupyter.png)](https://downgit.github.io/#/home?url=https://github.com/linogaliana/python-datascientist/blob/master/notebooks/course/visualisation/matplotlib.ipynb)
[![nbviewer](https://img.shields.io/badge/Visualize-nbviewer-blue?logo=Jupyter.png)](https://nbviewer.jupyter.org/github/linogaliana/python-datascientist/blob/master/notebooks/course/visualisation/matplotlib.ipynb)
[![Onyxia](https://img.shields.io/badge/SSPcloud-Tester%20via%20SSP--cloud-informational&color=yellow?logo=Python.png)](https://datalab.sspcloud.fr/launcher/inseefrlab-helm-charts-datascience/jupyter?autoLaunch=true&onyxia.friendlyName=%C2%ABpython-datascience%C2%BB&init.personalInit=%C2%ABhttps%3A%2F%2Fraw.githubusercontent.com%2Flinogaliana%2Fpython-datascientist%2Fmaster%2Fsspcloud%2Finit-jupyter.sh%C2%BB&init.personalInitArgs=%C2%ABnotebooks/course/visualisation%20matplotlib.ipynb%C2%BB&security.allowlist.enabled=false)<br>
[![Binder](https://img.shields.io/badge/Launch-Binder-E66581.svg?logo=data:image/png;base64,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.png)](https://mybinder.org/v2/gh/linogaliana/python-datascientist/master?filepath=notebooks/course/visualisation/matplotlib.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](http://colab.research.google.com/github/linogaliana/python-datascientist/blob/master/notebooks/course/visualisation/matplotlib.ipynb)
[![githubdev](https://img.shields.io/static/v1?logo=visualstudiocode&label=&message=Open%20in%20Visual%20Studio%20Code&labelColor=2c2c32&color=007acc&logoColor=007acc.png)](https://github.dev/linogaliana/python-datascientist/notebooks/course/visualisation/matplotlib.ipynb)

La pratique de la visualisation se fera, dans ce cours, en répliquant des graphiques qu'on peut trouver sur
la page de l'*open-data* de la ville de Paris
[ici](https://opendata.paris.fr/explore/dataset/comptage-velo-donnees-compteurs/information/?disjunctive.id_compteur&disjunctive.nom_compteur&disjunctive.id&disjunctive.name).

Ce TP vise à initier:

-   Aux packages [matplotlib](https://matplotlib.org/) et
    [seaborn](https://seaborn.pydata.org/) pour la construction de graphiques figés
-   Au package [plotly](https://plotly.com/python/) pour les graphiques
    dynamiques, au format HTML

Nous verrons par la suite la manière de construire des cartes facilement avec
des formats équivalents.

Un sous-ensemble des données de [paris open data](https://opendata.paris.fr/explore/dataset/comptage-velo-donnees-compteurs/information/?disjunctive.id_compteur&disjunctive.nom_compteur&disjunctive.id&disjunctive.name) a été mis à disposition
sur {{< githubrepo >}} pour faciliter l'import (élimination des colonnes
qui ne nous serviront pas mais ralentissent l'import).

``` python
import matplotlib.pyplot as plt
import seaborn as sns
```

## Premier graphique avec l'API `matplotlib` de `pandas`

{{% box status="exercise" title="Exercice" icon="fas fa-pencil-alt" %}}

**Exercice 1 : Importer les données et produire un premier graphique**

1.  Importer les données de compteurs de vélos. Vous pouvez utiliser l'url <https://github.com/linogaliana/python-datascientist/raw/master/data/bike.csv>. :warning: Il s'agit de données
    compressées au format `gzip`, il faut donc utiliser l'option `compression`

2.  En premier lieu, sans se préoccuper des éléments de style ni des labels des
    graphiques, reproduire les deux premiers graphiques de la
    [page d'analyse des données](https://opendata.paris.fr/explore/dataset/comptage-velo-donnees-compteurs/dataviz/?disjunctive.id_compteur&disjunctive.nom_compteur&disjunctive.id&disjunctive.name):
    *Les 10 compteurs avec la moyenne horaire la plus élevée* et *Les 10 compteurs ayant comptabilisés le plus de vélos*.

![](index_files/figure-gfm/cell-6-output-1.png)

![](index_files/figure-gfm/cell-7-output-1.png)

{{% /box %}}

{{% box status="note" title="Conseil" icon="fa fa-comment" %}}
Pour obtenir un graphique ordonné du plus grand au plus petit, il faut avoir les données ordonnées du plus petit au
plus grand. C'est bizarre mais c'est comme ça...

{{% /box %}}

On peut remarquer plusieurs éléments problématiques (par exemple les labels) mais
aussi des éléments ne correspondant pas (les titres des axes, etc.) ou
manquants (le nom du graphique...)

Comme les graphiques produits par `pandas` suivent la logique très flexible
de `matplotlib`, il est possible de les customiser. Cependant, c'est
souvent beaucoup de travail et il peut être préférable de directement
utiliser *seaborn*, qui offre quelques arguments prêts à l'emploi.

## Utiliser directement `seaborn`

Vous pouvez repartir des deux dataframes précédents. On va suppose qu'ils se
nomment `df1` et `df2`.

{{% box status="exercise" title="Exercice" icon="fas fa-pencil-alt" %}}

**Exercice 2 : Un peu de style !**

Il y a plusieurs manières de faire un *bar* plot en `seaborn`. La plus flexible,
c'est-à-dire celle qui permet le mieux d'interagir avec `matplotlib` est
`catplot`

1.  Réinitialiser l'index des df pour avoir une colonne *'Nom du compteur'*

2.  Refaire le graphique précédent avec la fonction `catplot` de `seaborn`. Pour
    contrôler la taille du graphique vous pouvez utiliser les arguments `height` et
    `aspect`.

3.  Ajouter les titres des axes et le titre du graphique pour le premier graphique

![](index_files/figure-gfm/cell-11-output-1.png)

4.  Refaites l'exercice avec la fonction `sns.barplot`.

![](index_files/figure-gfm/cell-13-output-1.png)

5.  Essayez de colorer en rouge l'axe des `x`. Vous pouvez pré-définir un
    style avec `sns.set_style("ticks", {"xtick.color": "red"})`

![](index_files/figure-gfm/cell-15-output-1.png)

{{% /box %}}

{{% box status="exercise" title="Exercice" icon="fas fa-pencil-alt" %}}

**Exercice 3 : Refaire les graphiques**

1.  Refaire le graphique *Les 10 compteurs ayant comptabilisé le plus de vélos*

![](index_files/figure-gfm/cell-17-output-1.png)

2.  Les graphiques qui suivent vont nécessiter un peu d'agilité dans la gestion des dates. Il faut en effet commencer par créer une variable temporelle (vous pouvez la nommer
    `timestamp`) et la transformer en variable mensuelle (grâce à
    `dt.to_period('M')`) et l'appeler `month`. Vous pouvez essayer de le faire vous même ou cliquer
    ci-dessous pour la solution.

{{< spoiler text="Solution" >}}

``` python
df['timestamp'] = pd.to_datetime(df['Date et heure de comptage'], format='%Y-%m-%dT%H:%M:%SZ', errors='coerce')
df['month'] = df['timestamp'].dt.to_period('M')
```

{{< /spoiler >}}

3.  Refaire le graphique *Moyenne mensuelle des comptages vélos*.

![](index_files/figure-gfm/cell-20-output-1.png)

4.  Refaire le graphique *Moyenne journalière des comptages vélos* (créer d'abord une variable de jour avec `.dt.day`)

![](index_files/figure-gfm/cell-22-output-1.png)

5.  Refaire le graphique *Comptages vélo au cours des 7 derniers jours* (de l'échantillon)

![](index_files/figure-gfm/cell-24-output-1.png)

{{% /box %}}

## Des graphiques dynamiques avec `Plotly`

Le package `Plotly` est une surcouche à la librairie Javascript
`Plotly.js` qui permet de créer et manipuler des objets graphiques de manière
très flexible afin de produire des objets réactifs sans avoir à recourir
à Javascript.

Le point d'entrée recommandé est le module `Plotly Express`
([documentation ici](https://plotly.com/python/plotly-express/)) qui offre une arborescence
riche mais néanmoins intuitive pour construire des graphiques
(objets `plotly.graph_objects.Figure`) pouvant être modifiés *a posteriori*
si besoin (par exemple pour *customiser* les axes).

### Comment visualiser un graphique `plotly` ?

Dans un notebook Jupyter classique, les lignes suivantes de code permettent
d'afficher le résultat d'une commande `Plotly` sous un bloc de code:

``` python
from plotly.offline import init_notebook_mode
init_notebook_mode(connected = True)
```

Pour `JupyterLab`, l'extension `jupyterlab-plotly` s'avère nécessaire:

``` python
jupyter labextension install jupyterlab-plotly
```

Pour les utilisateurs de `python` via l'excellent package `R` `reticulate`, il
est possible d'écrire le résultats dans un fichier `.html` et d'utiliser
`htmltools::includeHTML` pour l'afficher via `R Markdown` (les utilisateurs
de `R` trouveront bien-sûr une technique bien plus simple: utiliser
directement le package `R` `plotly`...)

### Réplication de l'exemple précédent avec `plotly`

Les modules suivants seront nécessaires pour construire des graphiques
avec `plotly`:

``` python
import plotly
import plotly.express as px
from IPython.display import HTML #pour afficher les graphs
# dans une cellule de notebook
```

{{% box status="exercise" title="Exercice" icon="fas fa-pencil-alt" %}}

**Exercice 4 : Premier graphique avec plotly**

L'objectif est de reconstuire le premier diagramme en barre rouge avec `plotly`.

1.  Réalisez le graphique en utilisant la fonction adéquate avec `Plotly Express` et...

-   Ne pas prendre le
    thème par défaut mais un à fond blanc, pour avoir un résultat ressemblant
    à celui proposé sur le site de l'*open-data*.
-   Pour la couleur rouge,
    vous pouvez utiliser l'argument `color_discrete_sequence`.
-   Ne pas oublier de nommer les axes
-   Pensez à la couleur du texte de l'axe inférieur

2.  Tester un autre thème, à fond sombre. Pour les couleurs, faire un
    groupe stockant les trois plus fortes valeurs puis les autres.

{{% /box %}}

La première question permet de construire le graphique suivant:

{{< chart data="plotly1" >}}

Alors qu'avec le thème sombre (question 2), on obtient :

{{< chart data="plotly2" >}}

# Exercices supplémentaires

https://plotly.com/python/v3/3d-network-graph/

---
title: "Requêter via des API avec Python"
date: 2020-09-08T13:00:00Z
draft: false
weight: 80
slug: api
type: book
tags:
  - API
  - JSON
  - openfood
categories:
  - Exercice
summary: |
  Les API (Application Programming Interface) sont un mode d'accès aux
  données en expansion. Grâce aux API, l'automatisation de scripts
  est facilitée puisqu'il n'est plus nécessaire de stocker un fichier,
  et gérer ses différentes versions, mais uniquement de requêter une base
  et laisser au producteur de données le soin de gérer les mises à jour de
  la base.  
---

Requêter via des API avec Python
================
2020-09-08T13:00:00Z

<script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.3.6/require.min.js" integrity="sha512-c3Nl8+7g4LMSTdrm621y7kf9v3SDPnhxLNhcjFJbKECVnmZHTdo+IRO05sNLTH/D3vA6u1X32ehoLC7WFVdheg==" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.5.1/jquery.min.js" integrity="sha512-bLT0Qm9VnAYZDflyKcBaQ2gg0hSYNQrJ8RilYldYQ1FxQYoCLtUjuuRuZo+fjqhx/qtq/1itJ0C2ejDxltZVFg==" crossorigin="anonymous"></script>
<script type="application/javascript">define('jquery', [],function() {return window.jQuery;})</script>


<a href="https://github.com/linogaliana/python-datascientist/blob/master/notebooks/course/manipulation/04c_API_TP.ipynb" class="github"><i class="fab fa-github"></i></a>
[![Download](https://img.shields.io/badge/Download-Notebook-important?logo=Jupyter.png)](https://downgit.github.io/#/home?url=https://github.com/linogaliana/python-datascientist/blob/master/notebooks/course/manipulation/04c_API_TP.ipynb)
[![nbviewer](https://img.shields.io/badge/Visualize-nbviewer-blue?logo=Jupyter.png)](https://nbviewer.jupyter.org/github/linogaliana/python-datascientist/blob/master/notebooks/course/manipulation/04c_API_TP.ipynb)
[![Onyxia](https://img.shields.io/badge/SSPcloud-Tester%20via%20SSP--cloud-informational&color=yellow?logo=Python.png)](https://datalab.sspcloud.fr/launcher/inseefrlab-helm-charts-datascience/jupyter?autoLaunch=true&onyxia.friendlyName=%C2%ABpython-datascience%C2%BB&init.personalInit=%C2%ABhttps%3A%2F%2Fraw.githubusercontent.com%2Flinogaliana%2Fpython-datascientist%2Fmaster%2Fsspcloud%2Finit-jupyter.sh%C2%BB&init.personalInitArgs=%C2%ABnotebooks/course/manipulation%2004c_API_TP.ipynb%C2%BB&security.allowlist.enabled=false)<br>
[![Binder](https://img.shields.io/badge/Launch-Binder-E66581.svg?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAFkAAABZCAMAAABi1XidAAAB8lBMVEX///9XmsrmZYH1olJXmsr1olJXmsrmZYH1olJXmsr1olJXmsrmZYH1olL1olJXmsr1olJXmsrmZYH1olL1olJXmsrmZYH1olJXmsr1olL1olJXmsrmZYH1olL1olJXmsrmZYH1olL1olL0nFf1olJXmsrmZYH1olJXmsq8dZb1olJXmsrmZYH1olJXmspXmspXmsr1olL1olJXmsrmZYH1olJXmsr1olL1olJXmsrmZYH1olL1olLeaIVXmsrmZYH1olL1olL1olJXmsrmZYH1olLna31Xmsr1olJXmsr1olJXmsrmZYH1olLqoVr1olJXmsr1olJXmsrmZYH1olL1olKkfaPobXvviGabgadXmsqThKuofKHmZ4Dobnr1olJXmsr1olJXmspXmsr1olJXmsrfZ4TuhWn1olL1olJXmsqBi7X1olJXmspZmslbmMhbmsdemsVfl8ZgmsNim8Jpk8F0m7R4m7F5nLB6jbh7jbiDirOEibOGnKaMhq+PnaCVg6qWg6qegKaff6WhnpKofKGtnomxeZy3noG6dZi+n3vCcpPDcpPGn3bLb4/Mb47UbIrVa4rYoGjdaIbeaIXhoWHmZYHobXvpcHjqdHXreHLroVrsfG/uhGnuh2bwj2Hxk17yl1vzmljzm1j0nlX1olL3AJXWAAAAbXRSTlMAEBAQHx8gICAuLjAwMDw9PUBAQEpQUFBXV1hgYGBkcHBwcXl8gICAgoiIkJCQlJicnJ2goKCmqK+wsLC4usDAwMjP0NDQ1NbW3Nzg4ODi5+3v8PDw8/T09PX29vb39/f5+fr7+/z8/Pz9/v7+zczCxgAABC5JREFUeAHN1ul3k0UUBvCb1CTVpmpaitAGSLSpSuKCLWpbTKNJFGlcSMAFF63iUmRccNG6gLbuxkXU66JAUef/9LSpmXnyLr3T5AO/rzl5zj137p136BISy44fKJXuGN/d19PUfYeO67Znqtf2KH33Id1psXoFdW30sPZ1sMvs2D060AHqws4FHeJojLZqnw53cmfvg+XR8mC0OEjuxrXEkX5ydeVJLVIlV0e10PXk5k7dYeHu7Cj1j+49uKg7uLU61tGLw1lq27ugQYlclHC4bgv7VQ+TAyj5Zc/UjsPvs1sd5cWryWObtvWT2EPa4rtnWW3JkpjggEpbOsPr7F7EyNewtpBIslA7p43HCsnwooXTEc3UmPmCNn5lrqTJxy6nRmcavGZVt/3Da2pD5NHvsOHJCrdc1G2r3DITpU7yic7w/7Rxnjc0kt5GC4djiv2Sz3Fb2iEZg41/ddsFDoyuYrIkmFehz0HR2thPgQqMyQYb2OtB0WxsZ3BeG3+wpRb1vzl2UYBog8FfGhttFKjtAclnZYrRo9ryG9uG/FZQU4AEg8ZE9LjGMzTmqKXPLnlWVnIlQQTvxJf8ip7VgjZjyVPrjw1te5otM7RmP7xm+sK2Gv9I8Gi++BRbEkR9EBw8zRUcKxwp73xkaLiqQb+kGduJTNHG72zcW9LoJgqQxpP3/Tj//c3yB0tqzaml05/+orHLksVO+95kX7/7qgJvnjlrfr2Ggsyx0eoy9uPzN5SPd86aXggOsEKW2Prz7du3VID3/tzs/sSRs2w7ovVHKtjrX2pd7ZMlTxAYfBAL9jiDwfLkq55Tm7ifhMlTGPyCAs7RFRhn47JnlcB9RM5T97ASuZXIcVNuUDIndpDbdsfrqsOppeXl5Y+XVKdjFCTh+zGaVuj0d9zy05PPK3QzBamxdwtTCrzyg/2Rvf2EstUjordGwa/kx9mSJLr8mLLtCW8HHGJc2R5hS219IiF6PnTusOqcMl57gm0Z8kanKMAQg0qSyuZfn7zItsbGyO9QlnxY0eCuD1XL2ys/MsrQhltE7Ug0uFOzufJFE2PxBo/YAx8XPPdDwWN0MrDRYIZF0mSMKCNHgaIVFoBbNoLJ7tEQDKxGF0kcLQimojCZopv0OkNOyWCCg9XMVAi7ARJzQdM2QUh0gmBozjc3Skg6dSBRqDGYSUOu66Zg+I2fNZs/M3/f/Grl/XnyF1Gw3VKCez0PN5IUfFLqvgUN4C0qNqYs5YhPL+aVZYDE4IpUk57oSFnJm4FyCqqOE0jhY2SMyLFoo56zyo6becOS5UVDdj7Vih0zp+tcMhwRpBeLyqtIjlJKAIZSbI8SGSF3k0pA3mR5tHuwPFoa7N7reoq2bqCsAk1HqCu5uvI1n6JuRXI+S1Mco54YmYTwcn6Aeic+kssXi8XpXC4V3t7/ADuTNKaQJdScAAAAAElFTkSuQmCC.png)](https://mybinder.org/v2/gh/linogaliana/python-datascientist/master?filepath=notebooks/course/manipulation/04c_API_TP.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](http://colab.research.google.com/github/linogaliana/python-datascientist/blob/master/notebooks/course/manipulation/04c_API_TP.ipynb)
[![githubdev](https://img.shields.io/static/v1?logo=visualstudiocode&label=&message=Open%20in%20Visual%20Studio%20Code&labelColor=2c2c32&color=007acc&logoColor=007acc.png)](https://github.dev/linogaliana/python-datascientist/notebooks/course/manipulation/04c_API_TP.ipynb)

# Introduction : Qu'est-ce qu'une API ?

## Définition

Pour expliquer le principe d'une API, je vais reprendre le début de
la fiche dédiée dans la documentation collaborative
[utilitR](https://www.book.utilitr.org/api.html) que je recommande de lire :

> Une *Application Programming Interface* (ou API) est une interface de programmation qui permet d'utiliser une application existante pour restituer des données. Le terme d'API peut être paraître intimidant, mais il s'agit simplement d'une façon de mettre à disposition des données : plutôt que de laisser l'utilisateur consulter directement des bases de données (souvent volumineuses et complexes), l'API lui propose de formuler une requête qui est traitée par le serveur hébergeant la base de données, puis de recevoir des données en réponse à sa requête.
>
> D'un point de vue informatique, une API est une porte d'entrée clairement identifiée par laquelle un logiciel offre des services à d'autres logiciels (ou utilisateurs). L'objectif d'une API est de fournir un point d'accès à une fonctionnalité qui soit facile à utiliser et qui masque les détails de la mise en oeuvre. Par exemple, l'API Sirene permet de récupérer la raison sociale d'une entreprise à partir de son identifiant Siren en interrogeant le référentiel disponible sur Internet directement depuis un script R, sans avoir à connaître tous les détails du répertoire Sirene.
>
> À l'Insee comme ailleurs, la connexion entre les bases de données pour les nouveaux projets tend à se réaliser par des API. L'accès à des données par des API devient ainsi de plus en plus commun et est amené à devenir une compétence de base de tout utilisateur de données.
>
> [`utilitR`](https://www.book.utilitr.org/api.html)

## Avantages des API

A nouveau, citons la documentation [utilitR](https://www.book.utilitr.org/api.html)

Les API présentent de multiples avantages :

> -   Les API rendent les programmes plus reproductibles. En effet, grâce aux API, il est possible de mettre à jour facilement les données utilisées par un programme si celles-ci évoluent. Cette flexibilité accrue pour l'utilisateur évite au producteur de données d'avoir à réaliser de multiples extractions, et réduit le problème de la coexistence de versions différentes des données.
> -   Grâce aux API, l'utilisateur peut extraire facilement une petite partie d'une base de données plus conséquente.
> -   Les API permettent de mettre à disposition des données tout en limitant le nombre de personnes ayant accès aux bases de données elles-mêmes.
> -   Grâce aux API, il est possible de proposer des services sur mesure pour les utilisateurs (par exemple, un accès spécifique pour les gros utilisateurs).
>
> [`utilitR`](https://www.book.utilitr.org/api.html)

L'utilisation accrue d'API dans le cadre de stratégies open-data est l'un
des piliers des 15 feuilles de route ministérielles
en matière d'ouverture, de circulation et de valorisation des données publiques.

## Utilisation des API

Citons encore une fois
la documentation [`utilitR`](https://www.book.utilitr.org/api.html)

> Une API peut souvent être utilisée de deux façons : par une interface Web, et par l'intermédiaire d'un logiciel (R, Python...). Par ailleurs, les API peuvent être proposées avec un niveau de liberté variable pour l'utilisateur :
>
> -   soit en libre accès (l'utilisation n'est pas contrôlée et l'utilisateur peut utiliser le service comme bon lui semble) ;
> -   soit via la génération d'un compte et d'un jeton d'accès qui permettent de sécuriser l'utilisation de l'API et de limiter le nombre de requêtes.
>
> [`utilitR`](https://www.book.utilitr.org/api.html)

De nombreuses API nécessitent une authentification, c'est-à-dire un
compte utilisateur afin de pouvoir accéder aux données.
Dans un premier temps,
nous regarderons exclusivement les API ouvertes sans restriction d'accès.  
Certains exercices et exemples permettront néanmoins d'essayer des API
avec restrictions d'accès.

# Requêter une API

## Principe général

> L'utilisation de l'interface Web est utile dans une démarche exploratoire mais trouve rapidement ses limites, notamment lorsqu'on consulte régulièrement l'API. L'utilisateur va rapidement se rendre compte qu'il est beaucoup plus commode d'utiliser une API via un logiciel de traitement pour automatiser la consultation ou pour réaliser du téléchargement de masse. De plus, l'interface Web n'existe pas systématiquement pour toutes les API.
>
> Le mode principal de consultation d'une API consiste à adresser une requête à cette API via un logiciel adapté (R, Python, Java...). Comme pour l'utilisation d'une fonction, l'appel d'une API comprend des paramètres qui sont détaillées dans la documentation de l'API.
>
> [`utilitR`](https://www.book.utilitr.org/api.html)

Voici les éléments importants à avoir en tête sur les requêtes (j'emprunte encore
à [`utilitR`](https://www.book.utilitr.org/api.html)):

-   Le **point d'entrée** d'un service offert par une API se présente sous la forme d'une URL (adresse web). Chaque service proposé par une API a sa propre URL. Par exemple, dans le cas de l'OpenFood Facts,
    l'URL à utiliser pour obtenir des informations sur un produit particulier (l'identifiant `737628064502`) estg https://world.openfoodfacts.org/api/v0/product/737628064502.json
-   Cette URL doit être complétée avec différents paramètres qui précisent la requête (par exemple l'identifiant Siren). Ces paramètres viennent s'ajouter à l'URL, souvent à la suite de `?`. Chaque service proposé par une API a ses propres paramètres, détaillés dans la documentation.
-   Lorsque l'utilisateur soumet sa requête, l'API lui renvoie une réponse structurée contenant l'ensemble des informations demandées. Le résultat envoyé par une API est majoritairement aux formats JSON ou XML (deux formats dans lesquels les informations sont hiérarchisées de manière emboitée). Plus rarement, certains services proposent une information sous forme plate (de type csv).

Du fait de la dimension hiérarchique des formats JSON ou XML, le résultat n'est pas toujours facile à récupérer mais
`python` propose d'excellents outils pour cela (meilleurs que ceux de `R`). Certains packages, notamment `json`, facilitent l'extraction de champs d'une sortie d'API. Dans certains cas, des packages spécifiques à une API ont été créés pour simplifier l'écriture d'une requête ou la récupération du résultat. Par exemple, le package
[pynsee](https://github.com/InseeFrLab/Py-Insee-Data/tree/master/pynsee)
propose des options qui seront retranscrites automatiquement dans l'URL de
requête pour faciliter le travail sur les données Insee.

## Exemple avec l'API de la Banque Mondiale

Avec l'API de la Banque mondiale, voici comme s'écrit une requête :

> http://api.worldbank.org/v2/countries?incomeLevel=LMC

1.  Le point d'entrée est l'URL <http://api.worldbank.org/v2>
2.  Un filtre est appliqué sur les pays (`countries?`) afin de ne conserver
    que celles telles que `incomeLevel=LMC` (*"Lower middle income"*)

En cliquant sur le lien, le site renvoie des données en XML,
qui ressemblent pas mal à ce qu'on a vu plus tôt avec le scraping : une structure avec des balises qui s'ouvrent et qui se ferment.

Pour obtenir la même information en `Python`, il faut revenir aux fondamentaux : on va avoir besoin du module `requests`. Suivant les API, nous avons soit besoin de rien de plus si nous parvenons directement à obtenir un json, soit devoir utiliser un *parser* comme `BeautifulSoup` dans le cas contraire.

Avec l'API de la banque mondiale, on va utiliser le module `requests` et sa méthode `get` : on lui donne l'url de l'API qui nous intéresse, on lui demande d'en faire un json et le tour est *en apparence* joué.

``` python
import requests
req = requests.get('http://api.worldbank.org/v2/countries?incomeLevel=LMC')
req
```

    <Response [200]>

Prenons par exemple les 1000 premiers caractères du résultat :

``` python
print(req.content[:1000])
```

b'<?xml version="1.0" encoding="utf-8"?><wb:countries page="1" pages="2" per_page="50" total="55" xmlns:wb="http://www.worldbank.org"><wb:country id="AGO">AO</wb:iso2Code>Angola</wb:name><wb:region id="SSF" iso2code="ZG">Sub-Saharan Africa </wb:region><wb:adminregion id="SSA" iso2code="ZF">Sub-Saharan Africa (excluding high income)</wb:adminregion><wb:incomeLevel id="LMC" iso2code="XN">Lower middle income</wb:incomeLevel><wb:lendingType id="IBD" iso2code="XF">IBRD</wb:lendingType>Luanda</wb:capitalCity></wb:longitude></wb:latitude></wb:country><wb:country id="BEN">BJ</wb:iso2Code>Benin</wb:name><wb:region id="SSF" iso2code="ZG">Sub-Saharan Africa </wb:region><wb:adminregion id="SSA" iso2code="ZF">Sub-Saharan Africa (excluding high income)</wb:adminregion>\<wb:incomeLevel id="LMC" iso2code="'

Quand on regarde de plus près, on voit que les informations suivantes apparaissent :

-   Code du pays
-   Nom du pays
-   Région
-   Classification en termes de revenus
-   Les types de prêt pour ces pays
-   La capitale
-   Longitude
-   Latitude

Le format XML est fortement balisé, ce qui n'est pas très pratique.
En utilisant désormais un autre URL, on obtient un JSON, plus pratique pour travailler :

> http://api.worldbank.org/v2/countries?incomeLevel=LMC&format=json

``` python
import requests
import pandas as pd

req = requests.get('http://api.worldbank.org/v2/countries?incomeLevel=LMC&format=json')
```

A nouveau, les premiers caractères sont les suivants:

``` python
print(req.content[:1000])
```

b'\[{"page":1,"pages":2,"per_page":"50","total":55},\[{"id":"AGO","iso2Code":"AO","name":"Angola","region":{"id":"SSF","iso2code":"ZG","value":"Sub-Saharan Africa"},"adminregion":{"id":"SSA","iso2code":"ZF","value":"Sub-Saharan Africa (excluding high income)"},"incomeLevel":{"id":"LMC","iso2code":"XN","value":"Lower middle income"},"lendingType":{"id":"IBD","iso2code":"XF","value":"IBRD"},"capitalCity":"Luanda","longitude":"13.242","latitude":"-8.81155"},{"id":"BEN","iso2Code":"BJ","name":"Benin","region":{"id":"SSF","iso2code":"ZG","value":"Sub-Saharan Africa"},"adminregion":{"id":"SSA","iso2code":"ZF","value":"Sub-Saharan Africa (excluding high income)"},"incomeLevel":{"id":"LMC","iso2code":"XN","value":"Lower middle income"},"lendingType":{"id":"IDX","iso2code":"XI","value":"IDA"},"capitalCity":"Porto-Novo","longitude":"2.6323","latitude":"6.4779"},{"id":"BGD","iso2Code":"BD","name":"Bangladesh","region":{"id":"SAS","iso2code":"8S","value":"South Asia"},"adminregion":{"id":"SAS","iso2'

Cela ressemble déjà plus à un dictionnaire `Python`[^1].

Ici, il n'est même pas nécessaire en première approche
d'utiliser le package `json`, l'information
étant déjà tabulée dans l'écho renvoyé (on a la même information pour tous les pays):

``` python
wb = req.json()
wb = pd.json_normalize(wb[1])
wb.head(5)
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>iso2Code</th>
      <th>name</th>
      <th>capitalCity</th>
      <th>longitude</th>
      <th>latitude</th>
      <th>region.id</th>
      <th>region.iso2code</th>
      <th>region.value</th>
      <th>adminregion.id</th>
      <th>adminregion.iso2code</th>
      <th>adminregion.value</th>
      <th>incomeLevel.id</th>
      <th>incomeLevel.iso2code</th>
      <th>incomeLevel.value</th>
      <th>lendingType.id</th>
      <th>lendingType.iso2code</th>
      <th>lendingType.value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>AGO</td>
      <td>AO</td>
      <td>Angola</td>
      <td>Luanda</td>
      <td>13.242</td>
      <td>-8.81155</td>
      <td>SSF</td>
      <td>ZG</td>
      <td>Sub-Saharan Africa</td>
      <td>SSA</td>
      <td>ZF</td>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IBD</td>
      <td>XF</td>
      <td>IBRD</td>
    </tr>
    <tr>
      <th>1</th>
      <td>BEN</td>
      <td>BJ</td>
      <td>Benin</td>
      <td>Porto-Novo</td>
      <td>2.6323</td>
      <td>6.4779</td>
      <td>SSF</td>
      <td>ZG</td>
      <td>Sub-Saharan Africa</td>
      <td>SSA</td>
      <td>ZF</td>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BGD</td>
      <td>BD</td>
      <td>Bangladesh</td>
      <td>Dhaka</td>
      <td>90.4113</td>
      <td>23.7055</td>
      <td>SAS</td>
      <td>8S</td>
      <td>South Asia</td>
      <td>SAS</td>
      <td>8S</td>
      <td>South Asia</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>3</th>
      <td>BLZ</td>
      <td>BZ</td>
      <td>Belize</td>
      <td>Belmopan</td>
      <td>-88.7713</td>
      <td>17.2534</td>
      <td>LCN</td>
      <td>ZJ</td>
      <td>Latin America &amp; Caribbean</td>
      <td>LAC</td>
      <td>XJ</td>
      <td>Latin America &amp; Caribbean (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IBD</td>
      <td>XF</td>
      <td>IBRD</td>
    </tr>
    <tr>
      <th>4</th>
      <td>BOL</td>
      <td>BO</td>
      <td>Bolivia</td>
      <td>La Paz</td>
      <td>-66.1936</td>
      <td>-13.9908</td>
      <td>LCN</td>
      <td>ZJ</td>
      <td>Latin America &amp; Caribbean</td>
      <td>LAC</td>
      <td>XJ</td>
      <td>Latin America &amp; Caribbean (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IBD</td>
      <td>XF</td>
      <td>IBRD</td>
    </tr>
  </tbody>
</table>
</div>

Cependant, si on regarde la dimension de l'objet obtenu, on obtient un
chiffre rond (50 lignes). Ceci est suspect et un petit tour dans la
documentation de l'API nous apprendrait que c'est le nombre maximal de
retour possible. Il faut donc faire attention à la documentation et
ajouter un paramètre `page=2` pour rattraper les derniers échos:

``` python
wb2 = pd.json_normalize(
    requests.get("http://api.worldbank.org/v2/countries?incomeLevel=LMC&format=json&page=2").json()[1]
    )
pd.concat([wb, wb2])
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>iso2Code</th>
      <th>name</th>
      <th>capitalCity</th>
      <th>longitude</th>
      <th>latitude</th>
      <th>region.id</th>
      <th>region.iso2code</th>
      <th>region.value</th>
      <th>adminregion.id</th>
      <th>adminregion.iso2code</th>
      <th>adminregion.value</th>
      <th>incomeLevel.id</th>
      <th>incomeLevel.iso2code</th>
      <th>incomeLevel.value</th>
      <th>lendingType.id</th>
      <th>lendingType.iso2code</th>
      <th>lendingType.value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>AGO</td>
      <td>AO</td>
      <td>Angola</td>
      <td>Luanda</td>
      <td>13.242</td>
      <td>-8.81155</td>
      <td>SSF</td>
      <td>ZG</td>
      <td>Sub-Saharan Africa</td>
      <td>SSA</td>
      <td>ZF</td>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IBD</td>
      <td>XF</td>
      <td>IBRD</td>
    </tr>
    <tr>
      <th>1</th>
      <td>BEN</td>
      <td>BJ</td>
      <td>Benin</td>
      <td>Porto-Novo</td>
      <td>2.6323</td>
      <td>6.4779</td>
      <td>SSF</td>
      <td>ZG</td>
      <td>Sub-Saharan Africa</td>
      <td>SSA</td>
      <td>ZF</td>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BGD</td>
      <td>BD</td>
      <td>Bangladesh</td>
      <td>Dhaka</td>
      <td>90.4113</td>
      <td>23.7055</td>
      <td>SAS</td>
      <td>8S</td>
      <td>South Asia</td>
      <td>SAS</td>
      <td>8S</td>
      <td>South Asia</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>3</th>
      <td>BLZ</td>
      <td>BZ</td>
      <td>Belize</td>
      <td>Belmopan</td>
      <td>-88.7713</td>
      <td>17.2534</td>
      <td>LCN</td>
      <td>ZJ</td>
      <td>Latin America &amp; Caribbean</td>
      <td>LAC</td>
      <td>XJ</td>
      <td>Latin America &amp; Caribbean (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IBD</td>
      <td>XF</td>
      <td>IBRD</td>
    </tr>
    <tr>
      <th>4</th>
      <td>BOL</td>
      <td>BO</td>
      <td>Bolivia</td>
      <td>La Paz</td>
      <td>-66.1936</td>
      <td>-13.9908</td>
      <td>LCN</td>
      <td>ZJ</td>
      <td>Latin America &amp; Caribbean</td>
      <td>LAC</td>
      <td>XJ</td>
      <td>Latin America &amp; Caribbean (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IBD</td>
      <td>XF</td>
      <td>IBRD</td>
    </tr>
    <tr>
      <th>5</th>
      <td>BTN</td>
      <td>BT</td>
      <td>Bhutan</td>
      <td>Thimphu</td>
      <td>89.6177</td>
      <td>27.5768</td>
      <td>SAS</td>
      <td>8S</td>
      <td>South Asia</td>
      <td>SAS</td>
      <td>8S</td>
      <td>South Asia</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>6</th>
      <td>CIV</td>
      <td>CI</td>
      <td>Cote d'Ivoire</td>
      <td>Yamoussoukro</td>
      <td>-4.0305</td>
      <td>5.332</td>
      <td>SSF</td>
      <td>ZG</td>
      <td>Sub-Saharan Africa</td>
      <td>SSA</td>
      <td>ZF</td>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>7</th>
      <td>CMR</td>
      <td>CM</td>
      <td>Cameroon</td>
      <td>Yaounde</td>
      <td>11.5174</td>
      <td>3.8721</td>
      <td>SSF</td>
      <td>ZG</td>
      <td>Sub-Saharan Africa</td>
      <td>SSA</td>
      <td>ZF</td>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDB</td>
      <td>XH</td>
      <td>Blend</td>
    </tr>
    <tr>
      <th>8</th>
      <td>COG</td>
      <td>CG</td>
      <td>Congo, Rep.</td>
      <td>Brazzaville</td>
      <td>15.2662</td>
      <td>-4.2767</td>
      <td>SSF</td>
      <td>ZG</td>
      <td>Sub-Saharan Africa</td>
      <td>SSA</td>
      <td>ZF</td>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDB</td>
      <td>XH</td>
      <td>Blend</td>
    </tr>
    <tr>
      <th>9</th>
      <td>COM</td>
      <td>KM</td>
      <td>Comoros</td>
      <td>Moroni</td>
      <td>43.2418</td>
      <td>-11.6986</td>
      <td>SSF</td>
      <td>ZG</td>
      <td>Sub-Saharan Africa</td>
      <td>SSA</td>
      <td>ZF</td>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>10</th>
      <td>CPV</td>
      <td>CV</td>
      <td>Cabo Verde</td>
      <td>Praia</td>
      <td>-23.5087</td>
      <td>14.9218</td>
      <td>SSF</td>
      <td>ZG</td>
      <td>Sub-Saharan Africa</td>
      <td>SSA</td>
      <td>ZF</td>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDB</td>
      <td>XH</td>
      <td>Blend</td>
    </tr>
    <tr>
      <th>11</th>
      <td>DJI</td>
      <td>DJ</td>
      <td>Djibouti</td>
      <td>Djibouti</td>
      <td>43.1425</td>
      <td>11.5806</td>
      <td>MEA</td>
      <td>ZQ</td>
      <td>Middle East &amp; North Africa</td>
      <td>MNA</td>
      <td>XQ</td>
      <td>Middle East &amp; North Africa (excluding high inc...</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>12</th>
      <td>DZA</td>
      <td>DZ</td>
      <td>Algeria</td>
      <td>Algiers</td>
      <td>3.05097</td>
      <td>36.7397</td>
      <td>MEA</td>
      <td>ZQ</td>
      <td>Middle East &amp; North Africa</td>
      <td>MNA</td>
      <td>XQ</td>
      <td>Middle East &amp; North Africa (excluding high inc...</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IBD</td>
      <td>XF</td>
      <td>IBRD</td>
    </tr>
    <tr>
      <th>13</th>
      <td>EGY</td>
      <td>EG</td>
      <td>Egypt, Arab Rep.</td>
      <td>Cairo</td>
      <td>31.2461</td>
      <td>30.0982</td>
      <td>MEA</td>
      <td>ZQ</td>
      <td>Middle East &amp; North Africa</td>
      <td>MNA</td>
      <td>XQ</td>
      <td>Middle East &amp; North Africa (excluding high inc...</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IBD</td>
      <td>XF</td>
      <td>IBRD</td>
    </tr>
    <tr>
      <th>14</th>
      <td>FSM</td>
      <td>FM</td>
      <td>Micronesia, Fed. Sts.</td>
      <td>Palikir</td>
      <td>158.185</td>
      <td>6.91771</td>
      <td>EAS</td>
      <td>Z4</td>
      <td>East Asia &amp; Pacific</td>
      <td>EAP</td>
      <td>4E</td>
      <td>East Asia &amp; Pacific (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>15</th>
      <td>GHA</td>
      <td>GH</td>
      <td>Ghana</td>
      <td>Accra</td>
      <td>-0.20795</td>
      <td>5.57045</td>
      <td>SSF</td>
      <td>ZG</td>
      <td>Sub-Saharan Africa</td>
      <td>SSA</td>
      <td>ZF</td>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>16</th>
      <td>HND</td>
      <td>HN</td>
      <td>Honduras</td>
      <td>Tegucigalpa</td>
      <td>-87.4667</td>
      <td>15.1333</td>
      <td>LCN</td>
      <td>ZJ</td>
      <td>Latin America &amp; Caribbean</td>
      <td>LAC</td>
      <td>XJ</td>
      <td>Latin America &amp; Caribbean (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>17</th>
      <td>HTI</td>
      <td>HT</td>
      <td>Haiti</td>
      <td>Port-au-Prince</td>
      <td>-72.3288</td>
      <td>18.5392</td>
      <td>LCN</td>
      <td>ZJ</td>
      <td>Latin America &amp; Caribbean</td>
      <td>LAC</td>
      <td>XJ</td>
      <td>Latin America &amp; Caribbean (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>18</th>
      <td>IDN</td>
      <td>ID</td>
      <td>Indonesia</td>
      <td>Jakarta</td>
      <td>106.83</td>
      <td>-6.19752</td>
      <td>EAS</td>
      <td>Z4</td>
      <td>East Asia &amp; Pacific</td>
      <td>EAP</td>
      <td>4E</td>
      <td>East Asia &amp; Pacific (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IBD</td>
      <td>XF</td>
      <td>IBRD</td>
    </tr>
    <tr>
      <th>19</th>
      <td>IND</td>
      <td>IN</td>
      <td>India</td>
      <td>New Delhi</td>
      <td>77.225</td>
      <td>28.6353</td>
      <td>SAS</td>
      <td>8S</td>
      <td>South Asia</td>
      <td>SAS</td>
      <td>8S</td>
      <td>South Asia</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IBD</td>
      <td>XF</td>
      <td>IBRD</td>
    </tr>
    <tr>
      <th>20</th>
      <td>IRN</td>
      <td>IR</td>
      <td>Iran, Islamic Rep.</td>
      <td>Tehran</td>
      <td>51.4447</td>
      <td>35.6878</td>
      <td>MEA</td>
      <td>ZQ</td>
      <td>Middle East &amp; North Africa</td>
      <td>MNA</td>
      <td>XQ</td>
      <td>Middle East &amp; North Africa (excluding high inc...</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IBD</td>
      <td>XF</td>
      <td>IBRD</td>
    </tr>
    <tr>
      <th>21</th>
      <td>KEN</td>
      <td>KE</td>
      <td>Kenya</td>
      <td>Nairobi</td>
      <td>36.8126</td>
      <td>-1.27975</td>
      <td>SSF</td>
      <td>ZG</td>
      <td>Sub-Saharan Africa</td>
      <td>SSA</td>
      <td>ZF</td>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDB</td>
      <td>XH</td>
      <td>Blend</td>
    </tr>
    <tr>
      <th>22</th>
      <td>KGZ</td>
      <td>KG</td>
      <td>Kyrgyz Republic</td>
      <td>Bishkek</td>
      <td>74.6057</td>
      <td>42.8851</td>
      <td>ECS</td>
      <td>Z7</td>
      <td>Europe &amp; Central Asia</td>
      <td>ECA</td>
      <td>7E</td>
      <td>Europe &amp; Central Asia (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>23</th>
      <td>KHM</td>
      <td>KH</td>
      <td>Cambodia</td>
      <td>Phnom Penh</td>
      <td>104.874</td>
      <td>11.5556</td>
      <td>EAS</td>
      <td>Z4</td>
      <td>East Asia &amp; Pacific</td>
      <td>EAP</td>
      <td>4E</td>
      <td>East Asia &amp; Pacific (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>24</th>
      <td>KIR</td>
      <td>KI</td>
      <td>Kiribati</td>
      <td>Tarawa</td>
      <td>172.979</td>
      <td>1.32905</td>
      <td>EAS</td>
      <td>Z4</td>
      <td>East Asia &amp; Pacific</td>
      <td>EAP</td>
      <td>4E</td>
      <td>East Asia &amp; Pacific (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>25</th>
      <td>LAO</td>
      <td>LA</td>
      <td>Lao PDR</td>
      <td>Vientiane</td>
      <td>102.177</td>
      <td>18.5826</td>
      <td>EAS</td>
      <td>Z4</td>
      <td>East Asia &amp; Pacific</td>
      <td>EAP</td>
      <td>4E</td>
      <td>East Asia &amp; Pacific (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>26</th>
      <td>LKA</td>
      <td>LK</td>
      <td>Sri Lanka</td>
      <td>Colombo</td>
      <td>79.8528</td>
      <td>6.92148</td>
      <td>SAS</td>
      <td>8S</td>
      <td>South Asia</td>
      <td>SAS</td>
      <td>8S</td>
      <td>South Asia</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IBD</td>
      <td>XF</td>
      <td>IBRD</td>
    </tr>
    <tr>
      <th>27</th>
      <td>LSO</td>
      <td>LS</td>
      <td>Lesotho</td>
      <td>Maseru</td>
      <td>27.7167</td>
      <td>-29.5208</td>
      <td>SSF</td>
      <td>ZG</td>
      <td>Sub-Saharan Africa</td>
      <td>SSA</td>
      <td>ZF</td>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>28</th>
      <td>MAR</td>
      <td>MA</td>
      <td>Morocco</td>
      <td>Rabat</td>
      <td>-6.8704</td>
      <td>33.9905</td>
      <td>MEA</td>
      <td>ZQ</td>
      <td>Middle East &amp; North Africa</td>
      <td>MNA</td>
      <td>XQ</td>
      <td>Middle East &amp; North Africa (excluding high inc...</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IBD</td>
      <td>XF</td>
      <td>IBRD</td>
    </tr>
    <tr>
      <th>29</th>
      <td>MMR</td>
      <td>MM</td>
      <td>Myanmar</td>
      <td>Naypyidaw</td>
      <td>95.9562</td>
      <td>21.914</td>
      <td>EAS</td>
      <td>Z4</td>
      <td>East Asia &amp; Pacific</td>
      <td>EAP</td>
      <td>4E</td>
      <td>East Asia &amp; Pacific (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>30</th>
      <td>MNG</td>
      <td>MN</td>
      <td>Mongolia</td>
      <td>Ulaanbaatar</td>
      <td>106.937</td>
      <td>47.9129</td>
      <td>EAS</td>
      <td>Z4</td>
      <td>East Asia &amp; Pacific</td>
      <td>EAP</td>
      <td>4E</td>
      <td>East Asia &amp; Pacific (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IBD</td>
      <td>XF</td>
      <td>IBRD</td>
    </tr>
    <tr>
      <th>31</th>
      <td>MRT</td>
      <td>MR</td>
      <td>Mauritania</td>
      <td>Nouakchott</td>
      <td>-15.9824</td>
      <td>18.2367</td>
      <td>SSF</td>
      <td>ZG</td>
      <td>Sub-Saharan Africa</td>
      <td>SSA</td>
      <td>ZF</td>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>32</th>
      <td>NGA</td>
      <td>NG</td>
      <td>Nigeria</td>
      <td>Abuja</td>
      <td>7.48906</td>
      <td>9.05804</td>
      <td>SSF</td>
      <td>ZG</td>
      <td>Sub-Saharan Africa</td>
      <td>SSA</td>
      <td>ZF</td>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDB</td>
      <td>XH</td>
      <td>Blend</td>
    </tr>
    <tr>
      <th>33</th>
      <td>NIC</td>
      <td>NI</td>
      <td>Nicaragua</td>
      <td>Managua</td>
      <td>-86.2734</td>
      <td>12.1475</td>
      <td>LCN</td>
      <td>ZJ</td>
      <td>Latin America &amp; Caribbean</td>
      <td>LAC</td>
      <td>XJ</td>
      <td>Latin America &amp; Caribbean (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>34</th>
      <td>NPL</td>
      <td>NP</td>
      <td>Nepal</td>
      <td>Kathmandu</td>
      <td>85.3157</td>
      <td>27.6939</td>
      <td>SAS</td>
      <td>8S</td>
      <td>South Asia</td>
      <td>SAS</td>
      <td>8S</td>
      <td>South Asia</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>35</th>
      <td>PAK</td>
      <td>PK</td>
      <td>Pakistan</td>
      <td>Islamabad</td>
      <td>72.8</td>
      <td>30.5167</td>
      <td>SAS</td>
      <td>8S</td>
      <td>South Asia</td>
      <td>SAS</td>
      <td>8S</td>
      <td>South Asia</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDB</td>
      <td>XH</td>
      <td>Blend</td>
    </tr>
    <tr>
      <th>36</th>
      <td>PHL</td>
      <td>PH</td>
      <td>Philippines</td>
      <td>Manila</td>
      <td>121.035</td>
      <td>14.5515</td>
      <td>EAS</td>
      <td>Z4</td>
      <td>East Asia &amp; Pacific</td>
      <td>EAP</td>
      <td>4E</td>
      <td>East Asia &amp; Pacific (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IBD</td>
      <td>XF</td>
      <td>IBRD</td>
    </tr>
    <tr>
      <th>37</th>
      <td>PNG</td>
      <td>PG</td>
      <td>Papua New Guinea</td>
      <td>Port Moresby</td>
      <td>147.194</td>
      <td>-9.47357</td>
      <td>EAS</td>
      <td>Z4</td>
      <td>East Asia &amp; Pacific</td>
      <td>EAP</td>
      <td>4E</td>
      <td>East Asia &amp; Pacific (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDB</td>
      <td>XH</td>
      <td>Blend</td>
    </tr>
    <tr>
      <th>38</th>
      <td>PSE</td>
      <td>PS</td>
      <td>West Bank and Gaza</td>
      <td></td>
      <td></td>
      <td></td>
      <td>MEA</td>
      <td>ZQ</td>
      <td>Middle East &amp; North Africa</td>
      <td>MNA</td>
      <td>XQ</td>
      <td>Middle East &amp; North Africa (excluding high inc...</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>LNX</td>
      <td>XX</td>
      <td>Not classified</td>
    </tr>
    <tr>
      <th>39</th>
      <td>SEN</td>
      <td>SN</td>
      <td>Senegal</td>
      <td>Dakar</td>
      <td>-17.4734</td>
      <td>14.7247</td>
      <td>SSF</td>
      <td>ZG</td>
      <td>Sub-Saharan Africa</td>
      <td>SSA</td>
      <td>ZF</td>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>40</th>
      <td>SLB</td>
      <td>SB</td>
      <td>Solomon Islands</td>
      <td>Honiara</td>
      <td>159.949</td>
      <td>-9.42676</td>
      <td>EAS</td>
      <td>Z4</td>
      <td>East Asia &amp; Pacific</td>
      <td>EAP</td>
      <td>4E</td>
      <td>East Asia &amp; Pacific (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>41</th>
      <td>SLV</td>
      <td>SV</td>
      <td>El Salvador</td>
      <td>San Salvador</td>
      <td>-89.2073</td>
      <td>13.7034</td>
      <td>LCN</td>
      <td>ZJ</td>
      <td>Latin America &amp; Caribbean</td>
      <td>LAC</td>
      <td>XJ</td>
      <td>Latin America &amp; Caribbean (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IBD</td>
      <td>XF</td>
      <td>IBRD</td>
    </tr>
    <tr>
      <th>42</th>
      <td>STP</td>
      <td>ST</td>
      <td>Sao Tome and Principe</td>
      <td>Sao Tome</td>
      <td>6.6071</td>
      <td>0.20618</td>
      <td>SSF</td>
      <td>ZG</td>
      <td>Sub-Saharan Africa</td>
      <td>SSA</td>
      <td>ZF</td>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>43</th>
      <td>SWZ</td>
      <td>SZ</td>
      <td>Eswatini</td>
      <td>Mbabane</td>
      <td>31.4659</td>
      <td>-26.5225</td>
      <td>SSF</td>
      <td>ZG</td>
      <td>Sub-Saharan Africa</td>
      <td>SSA</td>
      <td>ZF</td>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IBD</td>
      <td>XF</td>
      <td>IBRD</td>
    </tr>
    <tr>
      <th>44</th>
      <td>TJK</td>
      <td>TJ</td>
      <td>Tajikistan</td>
      <td>Dushanbe</td>
      <td>68.7864</td>
      <td>38.5878</td>
      <td>ECS</td>
      <td>Z7</td>
      <td>Europe &amp; Central Asia</td>
      <td>ECA</td>
      <td>7E</td>
      <td>Europe &amp; Central Asia (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>45</th>
      <td>TLS</td>
      <td>TL</td>
      <td>Timor-Leste</td>
      <td>Dili</td>
      <td>125.567</td>
      <td>-8.56667</td>
      <td>EAS</td>
      <td>Z4</td>
      <td>East Asia &amp; Pacific</td>
      <td>EAP</td>
      <td>4E</td>
      <td>East Asia &amp; Pacific (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDB</td>
      <td>XH</td>
      <td>Blend</td>
    </tr>
    <tr>
      <th>46</th>
      <td>TUN</td>
      <td>TN</td>
      <td>Tunisia</td>
      <td>Tunis</td>
      <td>10.21</td>
      <td>36.7899</td>
      <td>MEA</td>
      <td>ZQ</td>
      <td>Middle East &amp; North Africa</td>
      <td>MNA</td>
      <td>XQ</td>
      <td>Middle East &amp; North Africa (excluding high inc...</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IBD</td>
      <td>XF</td>
      <td>IBRD</td>
    </tr>
    <tr>
      <th>47</th>
      <td>TZA</td>
      <td>TZ</td>
      <td>Tanzania</td>
      <td>Dodoma</td>
      <td>35.7382</td>
      <td>-6.17486</td>
      <td>SSF</td>
      <td>ZG</td>
      <td>Sub-Saharan Africa</td>
      <td>SSA</td>
      <td>ZF</td>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>48</th>
      <td>UKR</td>
      <td>UA</td>
      <td>Ukraine</td>
      <td>Kiev</td>
      <td>30.5038</td>
      <td>50.4536</td>
      <td>ECS</td>
      <td>Z7</td>
      <td>Europe &amp; Central Asia</td>
      <td>ECA</td>
      <td>7E</td>
      <td>Europe &amp; Central Asia (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IBD</td>
      <td>XF</td>
      <td>IBRD</td>
    </tr>
    <tr>
      <th>49</th>
      <td>UZB</td>
      <td>UZ</td>
      <td>Uzbekistan</td>
      <td>Tashkent</td>
      <td>69.269</td>
      <td>41.3052</td>
      <td>ECS</td>
      <td>Z7</td>
      <td>Europe &amp; Central Asia</td>
      <td>ECA</td>
      <td>7E</td>
      <td>Europe &amp; Central Asia (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDB</td>
      <td>XH</td>
      <td>Blend</td>
    </tr>
    <tr>
      <th>0</th>
      <td>VNM</td>
      <td>VN</td>
      <td>Vietnam</td>
      <td>Hanoi</td>
      <td>105.825</td>
      <td>21.0069</td>
      <td>EAS</td>
      <td>Z4</td>
      <td>East Asia &amp; Pacific</td>
      <td>EAP</td>
      <td>4E</td>
      <td>East Asia &amp; Pacific (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IBD</td>
      <td>XF</td>
      <td>IBRD</td>
    </tr>
    <tr>
      <th>1</th>
      <td>VUT</td>
      <td>VU</td>
      <td>Vanuatu</td>
      <td>Port-Vila</td>
      <td>168.321</td>
      <td>-17.7404</td>
      <td>EAS</td>
      <td>Z4</td>
      <td>East Asia &amp; Pacific</td>
      <td>EAP</td>
      <td>4E</td>
      <td>East Asia &amp; Pacific (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>2</th>
      <td>WSM</td>
      <td>WS</td>
      <td>Samoa</td>
      <td>Apia</td>
      <td>-171.752</td>
      <td>-13.8314</td>
      <td>EAS</td>
      <td>Z4</td>
      <td>East Asia &amp; Pacific</td>
      <td>EAP</td>
      <td>4E</td>
      <td>East Asia &amp; Pacific (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ZMB</td>
      <td>ZM</td>
      <td>Zambia</td>
      <td>Lusaka</td>
      <td>28.2937</td>
      <td>-15.3982</td>
      <td>SSF</td>
      <td>ZG</td>
      <td>Sub-Saharan Africa</td>
      <td>SSA</td>
      <td>ZF</td>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDX</td>
      <td>XI</td>
      <td>IDA</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ZWE</td>
      <td>ZW</td>
      <td>Zimbabwe</td>
      <td>Harare</td>
      <td>31.0672</td>
      <td>-17.8312</td>
      <td>SSF</td>
      <td>ZG</td>
      <td>Sub-Saharan Africa</td>
      <td>SSA</td>
      <td>ZF</td>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>LMC</td>
      <td>XN</td>
      <td>Lower middle income</td>
      <td>IDB</td>
      <td>XH</td>
      <td>Blend</td>
    </tr>
  </tbody>
</table>
</div>

Si on regarde l'information présente dans le DataFrame, on voit qu'elle se
présente sous forme `lendingType.value`. C'est parce que `pandas` a
concaténé les différents niveaux de notre dictionnaire. Si on désire
s'en assurer, on peut regarder sur un exemple:

``` python
req.json()[1][0]['incomeLevel']['value'] == wb.loc[0, 'incomeLevel.value'] 
```

    True

## Un catalogue incomplet d'API existantes

De plus en plus de sites mettent des API à disposition des développeurs et autres curieux.

Pour en citer quelques-unes très connues :

-   Twitter <i class="fab fa-twitter"></i> : https://dev.twitter.com/rest/public
-   Facebook <i class="fab fa-facebook"></i> : https://developers.facebook.com/
-   Instagram <i class="fab fa-instagram"></i> : https://www.instagram.com/developer/
-   Spotify <i class="fab fa-spotify"></i> : https://developer.spotify.com/web-api/

Cependant, il est intéressant de ne pas se restreindre à celles-ci dont les
données ne sont pas toujours les plus intéressantes. Beaucoup
de producteurs de données, privés comme publics, mettent à disposition
leurs données sous forme d'API

-   [API gouv](https://api.gouv.fr/): beaucoup d'API officielles de l'Etat français
    et accès à de la documentation
-   Insee: https://api.insee.fr/catalogue/ et [`pynsee`](https://github.com/InseeFrLab/Py-Insee-Data/tree/master/pynsee)
-   Pole Emploi : https://www.emploi-store-dev.fr/portail-developpeur-cms/home.html
-   SNCF : https://data.sncf.com/api
-   Banque Mondiale : https://datahelpdesk.worldbank.org/knowledgebase/topics/125589

# L'API DVF : accéder à des données de transactions immobilières simplement

Le site `DVF` (demandes de valeurs foncières) permet de visualiser toutes les données relatives aux mutations à titre onéreux (ventes de maisons, appartements, garages...) réalisées durant les 5 dernières années.

Un site de visualisation est disponible sur <https://app.dvf.etalab.gouv.fr/>.

Ce site est très complet quand il s'agit de connaître le prix moyen au mètre
carré d'un quartier ou de comparer des régions entre elles.
L'API DVF permet d'aller plus loin afin de récupérer les résultats dans
un logiciel de traitement de données. Elle a été réalisée par
[Christian Quest](https://github.com/cquest) et le code
source est disponible sur Github <a href="https://github.com/cquest/dvf_as_api" class="github"><i class="fab fa-github"></i></a>.

Les critères de recherche sont les suivants :
- `code_commune` = code INSEE de la commune (ex: 94068)
- `section` = section cadastrale (ex: 94068000CQ)
- `numero_plan` = identifiant de la parcelle, (ex: 94068000CQ0110)
- `lat` + `lon` + `dist` (optionnel): pour une recherche géographique, dist est par défaut un rayon de 500m
- `code_postal`

Les filtres de sélection complémentaires :
- `nature_mutation` (Vente, etc)
- `type_local` (Maison, Appartement, Local, Dépendance)

{{% box status="exercise" title="Exercice" icon="fas fa-pencil-alt" %}}

**Exercice 1 : Exploiter l'API DVF**

:one:
Rechercher toutes les transactions existantes dans DVF à Plogoff (code commune `29168`, en Bretagne).
Afficher les clés du JSON et en déduire le nombre de transactions répertoriées.

:two:
N'afficher que les transactions portant sur des maisons. Le résultat devrait
ressembler au DataFrame suivant:

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>code_service_ch</th>
      <th>reference_document</th>
      <th>articles_1</th>
      <th>articles_2</th>
      <th>articles_3</th>
      <th>articles_4</th>
      <th>articles_5</th>
      <th>numero_disposition</th>
      <th>date_mutation</th>
      <th>nature_mutation</th>
      <th>...</th>
      <th>identifiant_local</th>
      <th>surface_relle_bati</th>
      <th>nombre_pieces_principales</th>
      <th>nature_culture</th>
      <th>nature_culture_speciale</th>
      <th>surface_terrain</th>
      <th>lat</th>
      <th>lon</th>
      <th>geom.type</th>
      <th>geom.coordinates</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>000001</td>
      <td>2015-06-25</td>
      <td>Vente</td>
      <td>...</td>
      <td>None</td>
      <td>90</td>
      <td>4</td>
      <td>S</td>
      <td>None</td>
      <td>277</td>
      <td>48.042047</td>
      <td>-4.705626</td>
      <td>Point</td>
      <td>[-4.705626, 48.042047]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>000001</td>
      <td>2015-09-12</td>
      <td>Vente</td>
      <td>...</td>
      <td>None</td>
      <td>90</td>
      <td>4</td>
      <td>S</td>
      <td>None</td>
      <td>615</td>
      <td>48.038356</td>
      <td>-4.709215</td>
      <td>Point</td>
      <td>[-4.709215, 48.038356]</td>
    </tr>
    <tr>
      <th>2</th>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>000001</td>
      <td>2015-05-23</td>
      <td>Vente</td>
      <td>...</td>
      <td>None</td>
      <td>50</td>
      <td>3</td>
      <td>S</td>
      <td>None</td>
      <td>170</td>
      <td>48.038782</td>
      <td>-4.709152</td>
      <td>Point</td>
      <td>[-4.709152, 48.038782]</td>
    </tr>
    <tr>
      <th>3</th>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>000001</td>
      <td>2018-09-28</td>
      <td>Vente</td>
      <td>...</td>
      <td>None</td>
      <td>67</td>
      <td>3</td>
      <td>S</td>
      <td>None</td>
      <td>610</td>
      <td>48.038467</td>
      <td>-4.708496</td>
      <td>Point</td>
      <td>[-4.708496, 48.038467]</td>
    </tr>
    <tr>
      <th>4</th>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>000001</td>
      <td>2016-03-19</td>
      <td>Vente</td>
      <td>...</td>
      <td>None</td>
      <td>108</td>
      <td>5</td>
      <td>S</td>
      <td>None</td>
      <td>251</td>
      <td>48.038626</td>
      <td>-4.708192</td>
      <td>Point</td>
      <td>[-4.708192, 48.038626]</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>129</th>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>000001</td>
      <td>2019-03-22</td>
      <td>Vente</td>
      <td>...</td>
      <td>None</td>
      <td>77</td>
      <td>3</td>
      <td>S</td>
      <td>None</td>
      <td>273</td>
      <td>48.039692</td>
      <td>-4.702070</td>
      <td>Point</td>
      <td>[-4.70207, 48.039692]</td>
    </tr>
    <tr>
      <th>130</th>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>000001</td>
      <td>2018-09-15</td>
      <td>Vente</td>
      <td>...</td>
      <td>None</td>
      <td>70</td>
      <td>6</td>
      <td>S</td>
      <td>None</td>
      <td>672</td>
      <td>48.039420</td>
      <td>-4.699823</td>
      <td>Point</td>
      <td>[-4.699823, 48.03942]</td>
    </tr>
    <tr>
      <th>131</th>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>000001</td>
      <td>2018-09-26</td>
      <td>Vente</td>
      <td>...</td>
      <td>None</td>
      <td>98</td>
      <td>7</td>
      <td>S</td>
      <td>None</td>
      <td>455</td>
      <td>48.038956</td>
      <td>-4.700808</td>
      <td>Point</td>
      <td>[-4.700808, 48.038956]</td>
    </tr>
    <tr>
      <th>132</th>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>000001</td>
      <td>2015-07-11</td>
      <td>Vente</td>
      <td>...</td>
      <td>None</td>
      <td>48</td>
      <td>4</td>
      <td>S</td>
      <td>None</td>
      <td>625</td>
      <td>48.037184</td>
      <td>-4.700004</td>
      <td>Point</td>
      <td>[-4.700004, 48.037184]</td>
    </tr>
    <tr>
      <th>133</th>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>000001</td>
      <td>2015-09-01</td>
      <td>Vente</td>
      <td>...</td>
      <td>None</td>
      <td>70</td>
      <td>4</td>
      <td>S</td>
      <td>None</td>
      <td>555</td>
      <td>48.037312</td>
      <td>-4.712316</td>
      <td>Point</td>
      <td>[-4.712316, 48.037312]</td>
    </tr>
  </tbody>
</table>
<p>134 rows × 47 columns</p>
</div>

:three: Utiliser l'[API geo](https://api.gouv.fr/documentation/api-geo) pour
récupérer le découpage communal de la ville de Plogoff

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>nom</th>
      <th>code</th>
      <th>codeDepartement</th>
      <th>codeRegion</th>
      <th>population</th>
      <th>geometry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Plogoff</td>
      <td>29168</td>
      <td>29</td>
      <td>53</td>
      <td>1230</td>
      <td>MULTIPOLYGON (((-4.72457 48.03243, -4.72454 48...</td>
    </tr>
  </tbody>
</table>
</div>

:four:
Représenter l'histogramme des prix de vente

N'hésitez pas à aller plus loin en jouant sur des variables de
groupes par exemple

:five:
On va faire une carte des ventes en affichant le prix de l'achat.

Supposons que le DataFrame des ventes s'appelle `ventes`. Il faut d'abord le
convertir
en objet `geopandas`.

``` python
ventes = ventes.dropna(subset = ['lat','lon'])
ventes = gpd.GeoDataFrame(ventes, geometry=gpd.points_from_xy(ventes.lon, ventes.lat))
ventes
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>code_service_ch</th>
      <th>reference_document</th>
      <th>articles_1</th>
      <th>articles_2</th>
      <th>articles_3</th>
      <th>articles_4</th>
      <th>articles_5</th>
      <th>numero_disposition</th>
      <th>date_mutation</th>
      <th>nature_mutation</th>
      <th>...</th>
      <th>nombre_pieces_principales</th>
      <th>nature_culture</th>
      <th>nature_culture_speciale</th>
      <th>surface_terrain</th>
      <th>lat</th>
      <th>lon</th>
      <th>geom.type</th>
      <th>geom.coordinates</th>
      <th>geom</th>
      <th>geometry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>000001</td>
      <td>2017-09-29</td>
      <td>Vente</td>
      <td>...</td>
      <td>0.0</td>
      <td>None</td>
      <td>None</td>
      <td>NaN</td>
      <td>48.037810</td>
      <td>-4.717967</td>
      <td>Point</td>
      <td>[-4.717967, 48.03781]</td>
      <td>NaN</td>
      <td>POINT (-4.71797 48.03781)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>000001</td>
      <td>2018-07-29</td>
      <td>Vente</td>
      <td>...</td>
      <td>0.0</td>
      <td>None</td>
      <td>None</td>
      <td>NaN</td>
      <td>48.037810</td>
      <td>-4.717967</td>
      <td>Point</td>
      <td>[-4.717967, 48.03781]</td>
      <td>NaN</td>
      <td>POINT (-4.71797 48.03781)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>000001</td>
      <td>2014-10-30</td>
      <td>Vente</td>
      <td>...</td>
      <td>NaN</td>
      <td>T</td>
      <td>None</td>
      <td>1240.0</td>
      <td>48.042296</td>
      <td>-4.709488</td>
      <td>Point</td>
      <td>[-4.709488, 48.042296]</td>
      <td>NaN</td>
      <td>POINT (-4.70949 48.04230)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>000001</td>
      <td>2014-10-30</td>
      <td>Vente</td>
      <td>...</td>
      <td>NaN</td>
      <td>T</td>
      <td>None</td>
      <td>630.0</td>
      <td>48.043125</td>
      <td>-4.706963</td>
      <td>Point</td>
      <td>[-4.706963, 48.043125]</td>
      <td>NaN</td>
      <td>POINT (-4.70696 48.04313)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>000001</td>
      <td>2015-06-25</td>
      <td>Vente</td>
      <td>...</td>
      <td>NaN</td>
      <td>J</td>
      <td>None</td>
      <td>78.0</td>
      <td>48.042232</td>
      <td>-4.705553</td>
      <td>Point</td>
      <td>[-4.705553, 48.042232]</td>
      <td>NaN</td>
      <td>POINT (-4.70555 48.04223)</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>434</th>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>000001</td>
      <td>2015-09-01</td>
      <td>Vente</td>
      <td>...</td>
      <td>NaN</td>
      <td>T</td>
      <td>None</td>
      <td>1595.0</td>
      <td>48.037084</td>
      <td>-4.712427</td>
      <td>Point</td>
      <td>[-4.712427, 48.037084]</td>
      <td>NaN</td>
      <td>POINT (-4.71243 48.03708)</td>
    </tr>
    <tr>
      <th>435</th>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>000001</td>
      <td>2015-09-01</td>
      <td>Vente</td>
      <td>...</td>
      <td>4.0</td>
      <td>S</td>
      <td>None</td>
      <td>555.0</td>
      <td>48.037312</td>
      <td>-4.712316</td>
      <td>Point</td>
      <td>[-4.712316, 48.037312]</td>
      <td>NaN</td>
      <td>POINT (-4.71232 48.03731)</td>
    </tr>
    <tr>
      <th>436</th>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>000001</td>
      <td>2015-09-01</td>
      <td>Vente</td>
      <td>...</td>
      <td>0.0</td>
      <td>S</td>
      <td>None</td>
      <td>555.0</td>
      <td>48.037312</td>
      <td>-4.712316</td>
      <td>Point</td>
      <td>[-4.712316, 48.037312]</td>
      <td>NaN</td>
      <td>POINT (-4.71232 48.03731)</td>
    </tr>
    <tr>
      <th>437</th>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>000001</td>
      <td>2015-09-01</td>
      <td>Vente</td>
      <td>...</td>
      <td>NaN</td>
      <td>T</td>
      <td>None</td>
      <td>595.0</td>
      <td>48.037271</td>
      <td>-4.711856</td>
      <td>Point</td>
      <td>[-4.711856, 48.037271]</td>
      <td>NaN</td>
      <td>POINT (-4.71186 48.03727)</td>
    </tr>
    <tr>
      <th>438</th>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>000001</td>
      <td>2014-10-30</td>
      <td>Vente</td>
      <td>...</td>
      <td>NaN</td>
      <td>L</td>
      <td>None</td>
      <td>850.0</td>
      <td>48.033956</td>
      <td>-4.716009</td>
      <td>Point</td>
      <td>[-4.716009, 48.033956]</td>
      <td>NaN</td>
      <td>POINT (-4.71601 48.03396)</td>
    </tr>
  </tbody>
</table>
<p>431 rows × 49 columns</p>
</div>

Avant de faire une carte, on va convertir
les limites de la commune de Plogoff en geoJSON pour faciliter
sa représentation avec `folium`
([voir la doc `geopandas` à ce propos](https://geopandas.readthedocs.io/en/latest/gallery/polygon_plotting_with_folium.html#Add-polygons-to-map)):

``` python
geo_j = plgf.to_json()
```

Pour représenter graphiquement, on peut utiliser le code suivant (essayez de
le comprendre et pas uniquement de l'exécuter).

``` python
import folium
import numpy as np

ventes['map_color'] = pd.qcut(ventes['valeur_fonciere'], [0,0.8,1], labels = ['lightblue','red'])
ventes['icon'] = np.where(ventes['type_local']== 'Maison', "home", "")
ventes['num_voie_clean'] = np.where(ventes['numero_voie'].isnull(), "", ventes['numero_voie'])
ventes['text'] = ventes.apply(lambda s: "Adresse: {num} {voie} <br>Vente en {annee} <br>Prix {prix:.0f} €".format(
                        num = s['num_voie_clean'],
                        voie = s["voie"],
                        annee = s['date_mutation'].split("-")[0],
                        prix = s["valeur_fonciere"]),
             axis=1)
             
center = ventes[['lat', 'lon']].mean().values.tolist()
sw = ventes[['lat', 'lon']].min().values.tolist()
ne = ventes[['lat', 'lon']].max().values.tolist()

m = folium.Map(location = center, tiles='Stamen Toner')

# I can add marker one by one on the map
for i in range(0,len(ventes)):
    folium.Marker([ventes.iloc[i]['lat'], ventes.iloc[i]['lon']],
                  popup=ventes.iloc[i]['text'],
                  icon=folium.Icon(color=ventes.iloc[i]['map_color'], icon=ventes.iloc[i]['icon'])).add_to(m)

m.fit_bounds([sw, ne])
```

``` python
# Afficher la carte
m
```

{{% /box %}}

{{< rawhtml >}}

<div style="width:100%;"><div style="position:relative;width:100%;height:0;padding-bottom:60%;"><span style="color:#565656">Make this Notebook Trusted to load map: File -> Trust Notebook</span><iframe srcdoc="&lt;!DOCTYPE html&gt;
&lt;head&gt;    
    &lt;meta http-equiv=&quot;content-type&quot; content=&quot;text/html; charset=UTF-8&quot; /&gt;
    
        &lt;script&gt;
            L_NO_TOUCH = false;
            L_DISABLE_3D = false;
        &lt;/script&gt;
    
    &lt;style&gt;html, body {width: 100%;height: 100%;margin: 0;padding: 0;}&lt;/style&gt;
    &lt;style&gt;#map {position:absolute;top:0;bottom:0;right:0;left:0;}&lt;/style&gt;
    &lt;script src=&quot;https://cdn.jsdelivr.net/npm/leaflet@1.6.0/dist/leaflet.js&quot;&gt;&lt;/script&gt;
    &lt;script src=&quot;https://code.jquery.com/jquery-1.12.4.min.js&quot;&gt;&lt;/script&gt;
    &lt;script src=&quot;https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/js/bootstrap.min.js&quot;&gt;&lt;/script&gt;
    &lt;script src=&quot;https://cdnjs.cloudflare.com/ajax/libs/Leaflet.awesome-markers/2.0.2/leaflet.awesome-markers.js&quot;&gt;&lt;/script&gt;
    &lt;link rel=&quot;stylesheet&quot; href=&quot;https://cdn.jsdelivr.net/npm/leaflet@1.6.0/dist/leaflet.css&quot;/&gt;
    &lt;link rel=&quot;stylesheet&quot; href=&quot;https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css&quot;/&gt;
    &lt;link rel=&quot;stylesheet&quot; href=&quot;https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css&quot;/&gt;
    &lt;link rel=&quot;stylesheet&quot; href=&quot;https://maxcdn.bootstrapcdn.com/font-awesome/4.6.3/css/font-awesome.min.css&quot;/&gt;
    &lt;link rel=&quot;stylesheet&quot; href=&quot;https://cdnjs.cloudflare.com/ajax/libs/Leaflet.awesome-markers/2.0.2/leaflet.awesome-markers.css&quot;/&gt;
    &lt;link rel=&quot;stylesheet&quot; href=&quot;https://cdn.jsdelivr.net/gh/python-visualization/folium/folium/templates/leaflet.awesome.rotate.min.css&quot;/&gt;
    
            &lt;meta name=&quot;viewport&quot; content=&quot;width=device-width,
                initial-scale=1.0, maximum-scale=1.0, user-scalable=no&quot; /&gt;
            &lt;style&gt;
                #map_115b72cdcb5fe41fbc0524ad7e0caf27 {
                    position: relative;
                    width: 100.0%;
                    height: 100.0%;
                    left: 0.0%;
                    top: 0.0%;
                }
            &lt;/style&gt;
        
&lt;/head&gt;
&lt;body&gt;    
    
            &lt;div class=&quot;folium-map&quot; id=&quot;map_115b72cdcb5fe41fbc0524ad7e0caf27&quot; &gt;&lt;/div&gt;
        
&lt;/body&gt;
&lt;script&gt;    
    
            var map_115b72cdcb5fe41fbc0524ad7e0caf27 = L.map(
                &quot;map_115b72cdcb5fe41fbc0524ad7e0caf27&quot;,
                {
                    center: [48.03477472157772, -4.671743032482598],
                    crs: L.CRS.EPSG3857,
                    zoom: 10,
                    zoomControl: true,
                    preferCanvas: false,
                }
            );

            

        
    
            var tile_layer_d387ed039618d1d66c1a9e6d16ff0786 = L.tileLayer(
                &quot;https://stamen-tiles-{s}.a.ssl.fastly.net/toner/{z}/{x}/{y}.png&quot;,
                {&quot;attribution&quot;: &quot;Map tiles by \u003ca href=\&quot;http://stamen.com\&quot;\u003eStamen Design\u003c/a\u003e, under \u003ca href=\&quot;http://creativecommons.org/licenses/by/3.0\&quot;\u003eCC BY 3.0\u003c/a\u003e. Data by \u0026copy; \u003ca href=\&quot;http://openstreetmap.org\&quot;\u003eOpenStreetMap\u003c/a\u003e, under \u003ca href=\&quot;http://www.openstreetmap.org/copyright\&quot;\u003eODbL\u003c/a\u003e.&quot;, &quot;detectRetina&quot;: false, &quot;maxNativeZoom&quot;: 18, &quot;maxZoom&quot;: 18, &quot;minZoom&quot;: 0, &quot;noWrap&quot;: false, &quot;opacity&quot;: 1, &quot;subdomains&quot;: &quot;abc&quot;, &quot;tms&quot;: false}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var marker_76e27df8f7dc173bebaa6f0200c3930b = L.marker(
                [48.03781, -4.717967],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_fc5c531c8fa3a1b25957528952856f2b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_76e27df8f7dc173bebaa6f0200c3930b.setIcon(icon_fc5c531c8fa3a1b25957528952856f2b);
        
    
        var popup_bbf9e85fd7656814d89a43cd54c947e9 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_304af936cbecbf3d25468902d5b830e0 = $(`&lt;div id=&quot;html_304af936cbecbf3d25468902d5b830e0&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5215 LA POINTE DU RAZ &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 176000 €&lt;/div&gt;`)[0];
            popup_bbf9e85fd7656814d89a43cd54c947e9.setContent(html_304af936cbecbf3d25468902d5b830e0);
        

        marker_76e27df8f7dc173bebaa6f0200c3930b.bindPopup(popup_bbf9e85fd7656814d89a43cd54c947e9)
        ;

        
    
    
            var marker_5f455844929322adadc9250873bce9bf = L.marker(
                [48.03781, -4.717967],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_1907b2115da36f6cf3946a0338dfd727 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_5f455844929322adadc9250873bce9bf.setIcon(icon_1907b2115da36f6cf3946a0338dfd727);
        
    
        var popup_b4afb3019907f16221ba4f850c6a3133 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_4e4696d3e66b6c5644bbe6e067a994ff = $(`&lt;div id=&quot;html_4e4696d3e66b6c5644bbe6e067a994ff&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5215 LA POINTE DU RAZ &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 85000 €&lt;/div&gt;`)[0];
            popup_b4afb3019907f16221ba4f850c6a3133.setContent(html_4e4696d3e66b6c5644bbe6e067a994ff);
        

        marker_5f455844929322adadc9250873bce9bf.bindPopup(popup_b4afb3019907f16221ba4f850c6a3133)
        ;

        
    
    
            var marker_9ebd7a42a188cf42e8ce50986f8337c3 = L.marker(
                [48.042296, -4.709488],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_e7766ef034287b5c4a196a37c38e4d26 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_9ebd7a42a188cf42e8ce50986f8337c3.setIcon(icon_e7766ef034287b5c4a196a37c38e4d26);
        
    
        var popup_d34db0d3e6ec63f75766e0b8b9d97316 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9263882ffb49b0714e2bfe0ffbc49b1e = $(`&lt;div id=&quot;html_9263882ffb49b0714e2bfe0ffbc49b1e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LAOUAL &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 897 €&lt;/div&gt;`)[0];
            popup_d34db0d3e6ec63f75766e0b8b9d97316.setContent(html_9263882ffb49b0714e2bfe0ffbc49b1e);
        

        marker_9ebd7a42a188cf42e8ce50986f8337c3.bindPopup(popup_d34db0d3e6ec63f75766e0b8b9d97316)
        ;

        
    
    
            var marker_639f6528a9a0ad9a5eaac91e8b806408 = L.marker(
                [48.043125, -4.706963],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_72f37fda98db8475a920886328b9f301 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_639f6528a9a0ad9a5eaac91e8b806408.setIcon(icon_72f37fda98db8475a920886328b9f301);
        
    
        var popup_92e79f54482d5d4810a4ccb3eb193629 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_5aacdfc8bcac92ae98f841c5adb841bb = $(`&lt;div id=&quot;html_5aacdfc8bcac92ae98f841c5adb841bb&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LAOUAL &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 897 €&lt;/div&gt;`)[0];
            popup_92e79f54482d5d4810a4ccb3eb193629.setContent(html_5aacdfc8bcac92ae98f841c5adb841bb);
        

        marker_639f6528a9a0ad9a5eaac91e8b806408.bindPopup(popup_92e79f54482d5d4810a4ccb3eb193629)
        ;

        
    
    
            var marker_1b11cdf095e6645b478506431b8c02fd = L.marker(
                [48.042232, -4.705553],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_88410a299c12fc0aff7f8603729f99c6 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_1b11cdf095e6645b478506431b8c02fd.setIcon(icon_88410a299c12fc0aff7f8603729f99c6);
        
    
        var popup_0c75e822a98e401d709f0c6209add748 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8bdfe4b81316cc925fa954270643cb7d = $(`&lt;div id=&quot;html_8bdfe4b81316cc925fa954270643cb7d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LAOUAL &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 120000 €&lt;/div&gt;`)[0];
            popup_0c75e822a98e401d709f0c6209add748.setContent(html_8bdfe4b81316cc925fa954270643cb7d);
        

        marker_1b11cdf095e6645b478506431b8c02fd.bindPopup(popup_0c75e822a98e401d709f0c6209add748)
        ;

        
    
    
            var marker_f9e1a719306743a7c4833a66c67dce3a = L.marker(
                [48.042047, -4.705626],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_ab72885b4afee2c09557b4dc2dd47f22 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_f9e1a719306743a7c4833a66c67dce3a.setIcon(icon_ab72885b4afee2c09557b4dc2dd47f22);
        
    
        var popup_4c89ce62a05c485eff14d73b651f34b3 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ab69fa9f0b00d312d13cfb6059567b5a = $(`&lt;div id=&quot;html_ab69fa9f0b00d312d13cfb6059567b5a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 183 LAOUAL &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 120000 €&lt;/div&gt;`)[0];
            popup_4c89ce62a05c485eff14d73b651f34b3.setContent(html_ab69fa9f0b00d312d13cfb6059567b5a);
        

        marker_f9e1a719306743a7c4833a66c67dce3a.bindPopup(popup_4c89ce62a05c485eff14d73b651f34b3)
        ;

        
    
    
            var marker_9cd4d7e94fa870b60fbab99cb33c535f = L.marker(
                [48.038236, -4.709329],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_acb1442df2ebbba4008109b63c991e93 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_9cd4d7e94fa870b60fbab99cb33c535f.setIcon(icon_acb1442df2ebbba4008109b63c991e93);
        
    
        var popup_502ceb24d6879f1bf40995288482b6f5 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_6cbe570eddfdf00095bdbcfe52ec7bd6 = $(`&lt;div id=&quot;html_6cbe570eddfdf00095bdbcfe52ec7bd6&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESCOFF &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 1500 €&lt;/div&gt;`)[0];
            popup_502ceb24d6879f1bf40995288482b6f5.setContent(html_6cbe570eddfdf00095bdbcfe52ec7bd6);
        

        marker_9cd4d7e94fa870b60fbab99cb33c535f.bindPopup(popup_502ceb24d6879f1bf40995288482b6f5)
        ;

        
    
    
            var marker_492f02a192e5e4534cfe27e6106ccf67 = L.marker(
                [48.038356, -4.709215],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_e24bf76173376d708450dae5bce8b354 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_492f02a192e5e4534cfe27e6106ccf67.setIcon(icon_e24bf76173376d708450dae5bce8b354);
        
    
        var popup_b1d92610ecf36cc94d85fa69643633ba = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ce689873152a0b88ce2302bbaa2e7b61 = $(`&lt;div id=&quot;html_ce689873152a0b88ce2302bbaa2e7b61&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 220 KREIZ AN AVEL &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 105000 €&lt;/div&gt;`)[0];
            popup_b1d92610ecf36cc94d85fa69643633ba.setContent(html_ce689873152a0b88ce2302bbaa2e7b61);
        

        marker_492f02a192e5e4534cfe27e6106ccf67.bindPopup(popup_b1d92610ecf36cc94d85fa69643633ba)
        ;

        
    
    
            var marker_3370aad0b5f92002bb5015297b918520 = L.marker(
                [48.039437, -4.710305],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d1ddc39d6d92b860733c37f75c99b3d6 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_3370aad0b5f92002bb5015297b918520.setIcon(icon_d1ddc39d6d92b860733c37f75c99b3d6);
        
    
        var popup_3a91ae91c0f23f5d86811d8c340b574f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_92865600026c8709b243d230f6bbfa6f = $(`&lt;div id=&quot;html_92865600026c8709b243d230f6bbfa6f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESCOFF &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 1000 €&lt;/div&gt;`)[0];
            popup_3a91ae91c0f23f5d86811d8c340b574f.setContent(html_92865600026c8709b243d230f6bbfa6f);
        

        marker_3370aad0b5f92002bb5015297b918520.bindPopup(popup_3a91ae91c0f23f5d86811d8c340b574f)
        ;

        
    
    
            var marker_c226c50bd273af9ec2cea9508ca8913a = L.marker(
                [48.038782, -4.709152],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_46c67cbf572d8bba9a758dbd7c7ca9ac = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_c226c50bd273af9ec2cea9508ca8913a.setIcon(icon_46c67cbf572d8bba9a758dbd7c7ca9ac);
        
    
        var popup_d1d9e01a56a1962886e7e64e93f98a13 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_063e55d5be47f2b8b789e7604cf3391b = $(`&lt;div id=&quot;html_063e55d5be47f2b8b789e7604cf3391b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 215 AR VEL &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 85000 €&lt;/div&gt;`)[0];
            popup_d1d9e01a56a1962886e7e64e93f98a13.setContent(html_063e55d5be47f2b8b789e7604cf3391b);
        

        marker_c226c50bd273af9ec2cea9508ca8913a.bindPopup(popup_d1d9e01a56a1962886e7e64e93f98a13)
        ;

        
    
    
            var marker_46a3f4cd2e6e5d230f4576a8c346a74d = L.marker(
                [48.038442, -4.709021],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_4d56033a001300de9d0718b2b5479f0c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_46a3f4cd2e6e5d230f4576a8c346a74d.setIcon(icon_4d56033a001300de9d0718b2b5479f0c);
        
    
        var popup_68afd6f07cc6cf79dec596154becb18b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d3a734a7f925a48f271e48aa81944042 = $(`&lt;div id=&quot;html_d3a734a7f925a48f271e48aa81944042&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESCOFF &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 105000 €&lt;/div&gt;`)[0];
            popup_68afd6f07cc6cf79dec596154becb18b.setContent(html_d3a734a7f925a48f271e48aa81944042);
        

        marker_46a3f4cd2e6e5d230f4576a8c346a74d.bindPopup(popup_68afd6f07cc6cf79dec596154becb18b)
        ;

        
    
    
            var marker_f8a1f39d9a1254a0278fb278a8b99c7b = L.marker(
                [48.038467, -4.708496],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_10609a7dd1fb87d83fe9c456a70de533 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_f8a1f39d9a1254a0278fb278a8b99c7b.setIcon(icon_10609a7dd1fb87d83fe9c456a70de533);
        
    
        var popup_4db517b45168e747c56422ed892cbcb2 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_fad82e33bc4a5919d1d2e2affcac0c3e = $(`&lt;div id=&quot;html_fad82e33bc4a5919d1d2e2affcac0c3e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 208 LESCOFF &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 130000 €&lt;/div&gt;`)[0];
            popup_4db517b45168e747c56422ed892cbcb2.setContent(html_fad82e33bc4a5919d1d2e2affcac0c3e);
        

        marker_f8a1f39d9a1254a0278fb278a8b99c7b.bindPopup(popup_4db517b45168e747c56422ed892cbcb2)
        ;

        
    
    
            var marker_46c7438a43e023f0d4dc059510fe4c69 = L.marker(
                [48.038626, -4.708192],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_cd897185fddf5ba42abf34e4a9df4bf1 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_46c7438a43e023f0d4dc059510fe4c69.setIcon(icon_cd897185fddf5ba42abf34e4a9df4bf1);
        
    
        var popup_7c1b5d713576664fb48521a13d459b16 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_841fc7e6563a6609afe517ea8046c9ea = $(`&lt;div id=&quot;html_841fc7e6563a6609afe517ea8046c9ea&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 206 DES LANGOUSTIERS &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 65000 €&lt;/div&gt;`)[0];
            popup_7c1b5d713576664fb48521a13d459b16.setContent(html_841fc7e6563a6609afe517ea8046c9ea);
        

        marker_46c7438a43e023f0d4dc059510fe4c69.bindPopup(popup_7c1b5d713576664fb48521a13d459b16)
        ;

        
    
    
            var marker_debeca91cc132d344ccff112381bdb08 = L.marker(
                [48.03872, -4.707889],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_ea220bacaac3e58c0b68256e7267a1bb = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_debeca91cc132d344ccff112381bdb08.setIcon(icon_ea220bacaac3e58c0b68256e7267a1bb);
        
    
        var popup_26c48fdc63136eaf033a5d7af734a397 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_75d16364f6b21881be38bb2f63bb7bc6 = $(`&lt;div id=&quot;html_75d16364f6b21881be38bb2f63bb7bc6&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESCOFF &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 65000 €&lt;/div&gt;`)[0];
            popup_26c48fdc63136eaf033a5d7af734a397.setContent(html_75d16364f6b21881be38bb2f63bb7bc6);
        

        marker_debeca91cc132d344ccff112381bdb08.bindPopup(popup_26c48fdc63136eaf033a5d7af734a397)
        ;

        
    
    
            var marker_fa08999dcc2263b426684a771e03b5cd = L.marker(
                [48.039763, -4.706615],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_9215d9f48b3288d74ee62b6267fca7f4 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_fa08999dcc2263b426684a771e03b5cd.setIcon(icon_9215d9f48b3288d74ee62b6267fca7f4);
        
    
        var popup_ff81a3b6c8ae02ba1e1e96e515420cd0 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_43872d1adc31f9d44c907cb24a9b36e9 = $(`&lt;div id=&quot;html_43872d1adc31f9d44c907cb24a9b36e9&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESCOFF &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 10000 €&lt;/div&gt;`)[0];
            popup_ff81a3b6c8ae02ba1e1e96e515420cd0.setContent(html_43872d1adc31f9d44c907cb24a9b36e9);
        

        marker_fa08999dcc2263b426684a771e03b5cd.bindPopup(popup_ff81a3b6c8ae02ba1e1e96e515420cd0)
        ;

        
    
    
            var marker_1cd8c93a2c0b79ecdc9a97500499dad7 = L.marker(
                [48.039617, -4.706066],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_3eac32e3342858f0a77acc7fa2fb24a7 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_1cd8c93a2c0b79ecdc9a97500499dad7.setIcon(icon_3eac32e3342858f0a77acc7fa2fb24a7);
        
    
        var popup_afc9c22728992144935fa2851a8df1c7 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a5b0b9de05f711fea194a76d21b1f496 = $(`&lt;div id=&quot;html_a5b0b9de05f711fea194a76d21b1f496&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 198 DES LANGOUSTIERS &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 90000 €&lt;/div&gt;`)[0];
            popup_afc9c22728992144935fa2851a8df1c7.setContent(html_a5b0b9de05f711fea194a76d21b1f496);
        

        marker_1cd8c93a2c0b79ecdc9a97500499dad7.bindPopup(popup_afc9c22728992144935fa2851a8df1c7)
        ;

        
    
    
            var marker_190750958234fab5e7b81ad2acd70e34 = L.marker(
                [48.039813, -4.706178],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_ed962a141363b57d2e7ef6b2706292bb = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_190750958234fab5e7b81ad2acd70e34.setIcon(icon_ed962a141363b57d2e7ef6b2706292bb);
        
    
        var popup_859946382d0b78090ed4978193633228 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_bc3422c87bc2af836caca730fdfbc097 = $(`&lt;div id=&quot;html_bc3422c87bc2af836caca730fdfbc097&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESCOFF &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 90000 €&lt;/div&gt;`)[0];
            popup_859946382d0b78090ed4978193633228.setContent(html_bc3422c87bc2af836caca730fdfbc097);
        

        marker_190750958234fab5e7b81ad2acd70e34.bindPopup(popup_859946382d0b78090ed4978193633228)
        ;

        
    
    
            var marker_d84e4a51fc938ee4ecae02ecf49b3300 = L.marker(
                [48.039813, -4.706178],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_8a9c38e5f1e1651948f42f8a1b10a4f6 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_d84e4a51fc938ee4ecae02ecf49b3300.setIcon(icon_8a9c38e5f1e1651948f42f8a1b10a4f6);
        
    
        var popup_00b7e884dc1cde38723a4a9229a55222 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e0204f216c73fc2f768918406d039161 = $(`&lt;div id=&quot;html_e0204f216c73fc2f768918406d039161&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESCOFF &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 90000 €&lt;/div&gt;`)[0];
            popup_00b7e884dc1cde38723a4a9229a55222.setContent(html_e0204f216c73fc2f768918406d039161);
        

        marker_d84e4a51fc938ee4ecae02ecf49b3300.bindPopup(popup_00b7e884dc1cde38723a4a9229a55222)
        ;

        
    
    
            var marker_732aa34ed39dca18c97a129aafea385b = L.marker(
                [48.039561, -4.705858],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_0e4ae1c1d3794f4763104ea366f246ae = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_732aa34ed39dca18c97a129aafea385b.setIcon(icon_0e4ae1c1d3794f4763104ea366f246ae);
        
    
        var popup_51644340e8a0fdac4ca7f2d6dcfa10f8 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ae86189f9f4d18ac49d4fca3f3d4abb5 = $(`&lt;div id=&quot;html_ae86189f9f4d18ac49d4fca3f3d4abb5&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 197 LESCOFF &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 62000 €&lt;/div&gt;`)[0];
            popup_51644340e8a0fdac4ca7f2d6dcfa10f8.setContent(html_ae86189f9f4d18ac49d4fca3f3d4abb5);
        

        marker_732aa34ed39dca18c97a129aafea385b.bindPopup(popup_51644340e8a0fdac4ca7f2d6dcfa10f8)
        ;

        
    
    
            var marker_8deb508b417e34055c3bad7349304e9c = L.marker(
                [48.039599, -4.70426],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_228fce2217bafdf5a853957d61fa6058 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_8deb508b417e34055c3bad7349304e9c.setIcon(icon_228fce2217bafdf5a853957d61fa6058);
        
    
        var popup_81e81eab9f5988e6f6812a39bbebec42 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7616a538bba0ff1ca4760846c023787f = $(`&lt;div id=&quot;html_7616a538bba0ff1ca4760846c023787f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 236 LESCOFF &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 27500 €&lt;/div&gt;`)[0];
            popup_81e81eab9f5988e6f6812a39bbebec42.setContent(html_7616a538bba0ff1ca4760846c023787f);
        

        marker_8deb508b417e34055c3bad7349304e9c.bindPopup(popup_81e81eab9f5988e6f6812a39bbebec42)
        ;

        
    
    
            var marker_d131ed92e80625a15eb6259ec1c33d3e = L.marker(
                [48.039585, -4.704422],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_2c97714c929930cde4f621f04a3f88e5 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_d131ed92e80625a15eb6259ec1c33d3e.setIcon(icon_2c97714c929930cde4f621f04a3f88e5);
        
    
        var popup_05956f5e27a3b50d91c7221ed87629ec = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ba2ce92fae71120a3169615695f264ed = $(`&lt;div id=&quot;html_ba2ce92fae71120a3169615695f264ed&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 235 DES LANGOUSTIERS &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 130000 €&lt;/div&gt;`)[0];
            popup_05956f5e27a3b50d91c7221ed87629ec.setContent(html_ba2ce92fae71120a3169615695f264ed);
        

        marker_d131ed92e80625a15eb6259ec1c33d3e.bindPopup(popup_05956f5e27a3b50d91c7221ed87629ec)
        ;

        
    
    
            var marker_1f33d119c61cf87ad581942fc3cccadb = L.marker(
                [48.039474, -4.704727],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_f1289557ef109a8478402947385d0866 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_1f33d119c61cf87ad581942fc3cccadb.setIcon(icon_f1289557ef109a8478402947385d0866);
        
    
        var popup_4265733984386dfbaced11dec6e8ef65 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c24313ff47f2fb62df6f7ff5307108ad = $(`&lt;div id=&quot;html_c24313ff47f2fb62df6f7ff5307108ad&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 234 LESCOFF &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 130000 €&lt;/div&gt;`)[0];
            popup_4265733984386dfbaced11dec6e8ef65.setContent(html_c24313ff47f2fb62df6f7ff5307108ad);
        

        marker_1f33d119c61cf87ad581942fc3cccadb.bindPopup(popup_4265733984386dfbaced11dec6e8ef65)
        ;

        
    
    
            var marker_ceb72ffe74b85135612dc72e2c218772 = L.marker(
                [48.036863, -4.709276],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_07e85983af00d22cd034ca270f156cec = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ceb72ffe74b85135612dc72e2c218772.setIcon(icon_07e85983af00d22cd034ca270f156cec);
        
    
        var popup_a3c543ce6359fd922a62d5b696d2bd8d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_f583ea3cbd118ec55423b1eafc2f5b45 = $(`&lt;div id=&quot;html_f583ea3cbd118ec55423b1eafc2f5b45&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESCOFF &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 183000 €&lt;/div&gt;`)[0];
            popup_a3c543ce6359fd922a62d5b696d2bd8d.setContent(html_f583ea3cbd118ec55423b1eafc2f5b45);
        

        marker_ceb72ffe74b85135612dc72e2c218772.bindPopup(popup_a3c543ce6359fd922a62d5b696d2bd8d)
        ;

        
    
    
            var marker_d9bf1789beb0b4dedf6743401d436615 = L.marker(
                [48.036781, -4.709462],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_b77077799ac6379d1478a147d3782932 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_d9bf1789beb0b4dedf6743401d436615.setIcon(icon_b77077799ac6379d1478a147d3782932);
        
    
        var popup_37bd9c9658b6f5aefa2ac6fc5cb0943e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a1f04f36aeef747a1dc157de353abb9b = $(`&lt;div id=&quot;html_a1f04f36aeef747a1dc157de353abb9b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESCOFF &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 183000 €&lt;/div&gt;`)[0];
            popup_37bd9c9658b6f5aefa2ac6fc5cb0943e.setContent(html_a1f04f36aeef747a1dc157de353abb9b);
        

        marker_d9bf1789beb0b4dedf6743401d436615.bindPopup(popup_37bd9c9658b6f5aefa2ac6fc5cb0943e)
        ;

        
    
    
            var marker_695199e875ea1fa2c01eeb3b47c15692 = L.marker(
                [48.036899, -4.709473],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_a32579293c0b43643ee6de4cded53f18 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_695199e875ea1fa2c01eeb3b47c15692.setIcon(icon_a32579293c0b43643ee6de4cded53f18);
        
    
        var popup_56ed8f6bdef5972a323f9abba3d5e0c0 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ca29ed3437b0450dfba13ae8c9eef060 = $(`&lt;div id=&quot;html_ca29ed3437b0450dfba13ae8c9eef060&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 278 DU SOLDAT DUVAL &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 183000 €&lt;/div&gt;`)[0];
            popup_56ed8f6bdef5972a323f9abba3d5e0c0.setContent(html_ca29ed3437b0450dfba13ae8c9eef060);
        

        marker_695199e875ea1fa2c01eeb3b47c15692.bindPopup(popup_56ed8f6bdef5972a323f9abba3d5e0c0)
        ;

        
    
    
            var marker_a63d40bda2356e40602683ea1ad4ea0d = L.marker(
                [48.038238, -4.707333],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_188d833c447d7fa49515e748cd73f1b8 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_a63d40bda2356e40602683ea1ad4ea0d.setIcon(icon_188d833c447d7fa49515e748cd73f1b8);
        
    
        var popup_6560e4d2fee38300871c84b1cfbbe1c0 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_36b0d4f14e6ebf9e94e305d7cb01f722 = $(`&lt;div id=&quot;html_36b0d4f14e6ebf9e94e305d7cb01f722&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 268 LESCOFF &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 70000 €&lt;/div&gt;`)[0];
            popup_6560e4d2fee38300871c84b1cfbbe1c0.setContent(html_36b0d4f14e6ebf9e94e305d7cb01f722);
        

        marker_a63d40bda2356e40602683ea1ad4ea0d.bindPopup(popup_6560e4d2fee38300871c84b1cfbbe1c0)
        ;

        
    
    
            var marker_36423d99fc70d31fc9596ff1637c59db = L.marker(
                [48.038774, -4.708101],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_9d2cea70c4d2856da01620c3c1408163 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_36423d99fc70d31fc9596ff1637c59db.setIcon(icon_9d2cea70c4d2856da01620c3c1408163);
        
    
        var popup_6bcbaf3fb7e2cf39c1d0c58dcc2c56cb = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ed6f0b83b23d7ee9df0b57e1fb9889b9 = $(`&lt;div id=&quot;html_ed6f0b83b23d7ee9df0b57e1fb9889b9&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESCOFF &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 65000 €&lt;/div&gt;`)[0];
            popup_6bcbaf3fb7e2cf39c1d0c58dcc2c56cb.setContent(html_ed6f0b83b23d7ee9df0b57e1fb9889b9);
        

        marker_36423d99fc70d31fc9596ff1637c59db.bindPopup(popup_6bcbaf3fb7e2cf39c1d0c58dcc2c56cb)
        ;

        
    
    
            var marker_fba2f86f3330a81089d7ed1ed28ceb2b = L.marker(
                [48.039593, -4.703711],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_7b1e956297ebdef70cb169c876ec9f0b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_fba2f86f3330a81089d7ed1ed28ceb2b.setIcon(icon_7b1e956297ebdef70cb169c876ec9f0b);
        
    
        var popup_1a0c912554afc103d011164191d9c6dc = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_3a5d2ad934713f0031909ec8144ac2fc = $(`&lt;div id=&quot;html_3a5d2ad934713f0031909ec8144ac2fc&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESCOFF &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 123000 €&lt;/div&gt;`)[0];
            popup_1a0c912554afc103d011164191d9c6dc.setContent(html_3a5d2ad934713f0031909ec8144ac2fc);
        

        marker_fba2f86f3330a81089d7ed1ed28ceb2b.bindPopup(popup_1a0c912554afc103d011164191d9c6dc)
        ;

        
    
    
            var marker_ee98ec335559cf039f58ecb6de38fbd8 = L.marker(
                [48.039118, -4.709662],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_28cd7f8cb26bfdc2fa1cddc8c0a20f5f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ee98ec335559cf039f58ecb6de38fbd8.setIcon(icon_28cd7f8cb26bfdc2fa1cddc8c0a20f5f);
        
    
        var popup_c934e4efaef8c0beaa47bcee1c82ec74 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a1a380f10afdb89a852ddef72d0d5c51 = $(`&lt;div id=&quot;html_a1a380f10afdb89a852ddef72d0d5c51&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESCOFF &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 1268 €&lt;/div&gt;`)[0];
            popup_c934e4efaef8c0beaa47bcee1c82ec74.setContent(html_a1a380f10afdb89a852ddef72d0d5c51);
        

        marker_ee98ec335559cf039f58ecb6de38fbd8.bindPopup(popup_c934e4efaef8c0beaa47bcee1c82ec74)
        ;

        
    
    
            var marker_6a158afd5689abb4146f6d1be6246cd2 = L.marker(
                [48.039244, -4.709273],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_2167767d304e82d1a69bcd2ddfcb9f48 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_6a158afd5689abb4146f6d1be6246cd2.setIcon(icon_2167767d304e82d1a69bcd2ddfcb9f48);
        
    
        var popup_45fcdfc41e2e1acce0e76e0de6da701d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_64b24252f39050fc171c8751607d485d = $(`&lt;div id=&quot;html_64b24252f39050fc171c8751607d485d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESCOFF &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 1238 €&lt;/div&gt;`)[0];
            popup_45fcdfc41e2e1acce0e76e0de6da701d.setContent(html_64b24252f39050fc171c8751607d485d);
        

        marker_6a158afd5689abb4146f6d1be6246cd2.bindPopup(popup_45fcdfc41e2e1acce0e76e0de6da701d)
        ;

        
    
    
            var marker_5a6da92d06ce1713dd000c8532dff807 = L.marker(
                [48.04302, -4.702863],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_80a7e8dd7e6f10a2d7cef6f8fce5cbd1 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_5a6da92d06ce1713dd000c8532dff807.setIcon(icon_80a7e8dd7e6f10a2d7cef6f8fce5cbd1);
        
    
        var popup_a621d7fc00dd42bb5701c8329017fa2b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_fd4ed64b2faf6d184f8cf655057d60a8 = $(`&lt;div id=&quot;html_fd4ed64b2faf6d184f8cf655057d60a8&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LAOUAL &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 84 €&lt;/div&gt;`)[0];
            popup_a621d7fc00dd42bb5701c8329017fa2b.setContent(html_fd4ed64b2faf6d184f8cf655057d60a8);
        

        marker_5a6da92d06ce1713dd000c8532dff807.bindPopup(popup_a621d7fc00dd42bb5701c8329017fa2b)
        ;

        
    
    
            var marker_1f8b309d5c1c0496222e4ad006cfbf29 = L.marker(
                [48.041793, -4.705125],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_c6cba6f68534cb8409f1403af3534ced = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_1f8b309d5c1c0496222e4ad006cfbf29.setIcon(icon_c6cba6f68534cb8409f1403af3534ced);
        
    
        var popup_94dadc99b579928667955fea3c89d22f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_09ec44e7f5499180f73cde6ec39bddd6 = $(`&lt;div id=&quot;html_09ec44e7f5499180f73cde6ec39bddd6&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LAOUAL &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 291 €&lt;/div&gt;`)[0];
            popup_94dadc99b579928667955fea3c89d22f.setContent(html_09ec44e7f5499180f73cde6ec39bddd6);
        

        marker_1f8b309d5c1c0496222e4ad006cfbf29.bindPopup(popup_94dadc99b579928667955fea3c89d22f)
        ;

        
    
    
            var marker_7fbddd3d3848cb7e87cf454d5990fc67 = L.marker(
                [48.041517, -4.70501],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d140d4a9080e5ebf1782d3a61d16e803 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_7fbddd3d3848cb7e87cf454d5990fc67.setIcon(icon_d140d4a9080e5ebf1782d3a61d16e803);
        
    
        var popup_7a3889e75258fc51982467588d0b0743 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_6bfde037caffa2c3564ff486e8540187 = $(`&lt;div id=&quot;html_6bfde037caffa2c3564ff486e8540187&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LAOUAL &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 213 €&lt;/div&gt;`)[0];
            popup_7a3889e75258fc51982467588d0b0743.setContent(html_6bfde037caffa2c3564ff486e8540187);
        

        marker_7fbddd3d3848cb7e87cf454d5990fc67.bindPopup(popup_7a3889e75258fc51982467588d0b0743)
        ;

        
    
    
            var marker_d91e5f730feeda3b6ef51d6113b4debd = L.marker(
                [48.040483, -4.697976],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_906998f6fda2b712f73f5db21b604e78 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_d91e5f730feeda3b6ef51d6113b4debd.setIcon(icon_906998f6fda2b712f73f5db21b604e78);
        
    
        var popup_cfda792ffd999a0b0a9162d4b0a53c92 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_689ac8ecc313e17fffaddc37f9708112 = $(`&lt;div id=&quot;html_689ac8ecc313e17fffaddc37f9708112&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHERNEAU &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 1665 €&lt;/div&gt;`)[0];
            popup_cfda792ffd999a0b0a9162d4b0a53c92.setContent(html_689ac8ecc313e17fffaddc37f9708112);
        

        marker_d91e5f730feeda3b6ef51d6113b4debd.bindPopup(popup_cfda792ffd999a0b0a9162d4b0a53c92)
        ;

        
    
    
            var marker_3a94f75ceab2049608d08ef8e8138f38 = L.marker(
                [48.041406, -4.700591],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_9069d46de2c8f4350ecee57932b8905f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_3a94f75ceab2049608d08ef8e8138f38.setIcon(icon_9069d46de2c8f4350ecee57932b8905f);
        
    
        var popup_e9fb892d34031dff25b232dfb9677ec9 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_788f901f203737eddb28640a79c3bc35 = $(`&lt;div id=&quot;html_788f901f203737eddb28640a79c3bc35&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 137 KERHERNEAU &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 125000 €&lt;/div&gt;`)[0];
            popup_e9fb892d34031dff25b232dfb9677ec9.setContent(html_788f901f203737eddb28640a79c3bc35);
        

        marker_3a94f75ceab2049608d08ef8e8138f38.bindPopup(popup_e9fb892d34031dff25b232dfb9677ec9)
        ;

        
    
    
            var marker_571825ae1f44da76c42e9109419e0a3a = L.marker(
                [48.041625, -4.700293],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_323391a29e28e93dce99fdbf4c798180 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_571825ae1f44da76c42e9109419e0a3a.setIcon(icon_323391a29e28e93dce99fdbf4c798180);
        
    
        var popup_108421af3b6a364a65e048b2a6def79e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_282eb4264b783041411a45bf7ed95f7f = $(`&lt;div id=&quot;html_282eb4264b783041411a45bf7ed95f7f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 138 KERHERNEAU &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 178675 €&lt;/div&gt;`)[0];
            popup_108421af3b6a364a65e048b2a6def79e.setContent(html_282eb4264b783041411a45bf7ed95f7f);
        

        marker_571825ae1f44da76c42e9109419e0a3a.bindPopup(popup_108421af3b6a364a65e048b2a6def79e)
        ;

        
    
    
            var marker_4c3cd36374097667e218f498f5f2d400 = L.marker(
                [48.039985, -4.703074],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_755d51d5b36b5346d6d968073685b682 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_4c3cd36374097667e218f498f5f2d400.setIcon(icon_755d51d5b36b5346d6d968073685b682);
        
    
        var popup_2263c6ebd381dbc256d5a0b32474531a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7f54e2c8b6faf5e9c72ed09aeb52c360 = $(`&lt;div id=&quot;html_7f54e2c8b6faf5e9c72ed09aeb52c360&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 155 DES LANGOUSTIERS &lt;br&gt;Vente en 2019 &lt;br&gt;Prix 172790 €&lt;/div&gt;`)[0];
            popup_2263c6ebd381dbc256d5a0b32474531a.setContent(html_7f54e2c8b6faf5e9c72ed09aeb52c360);
        

        marker_4c3cd36374097667e218f498f5f2d400.bindPopup(popup_2263c6ebd381dbc256d5a0b32474531a)
        ;

        
    
    
            var marker_e16027c0e8d9c7e20152e99ead33a005 = L.marker(
                [48.039985, -4.703074],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_e20535cb7cfa30558f33ccea955bab08 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_e16027c0e8d9c7e20152e99ead33a005.setIcon(icon_e20535cb7cfa30558f33ccea955bab08);
        
    
        var popup_782e786cb0bef72188f3ca4f4cbcaa07 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8f88ff3a09ec064f4a7c0173b10ef755 = $(`&lt;div id=&quot;html_8f88ff3a09ec064f4a7c0173b10ef755&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 155 DES LANGOUSTIERS &lt;br&gt;Vente en 2019 &lt;br&gt;Prix 172790 €&lt;/div&gt;`)[0];
            popup_782e786cb0bef72188f3ca4f4cbcaa07.setContent(html_8f88ff3a09ec064f4a7c0173b10ef755);
        

        marker_e16027c0e8d9c7e20152e99ead33a005.bindPopup(popup_782e786cb0bef72188f3ca4f4cbcaa07)
        ;

        
    
    
            var marker_9af4c2269ab8aaf3475d22578331f8ea = L.marker(
                [48.040302, -4.703544],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_2a35dc7c2a0284b1d755d83870e05815 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_9af4c2269ab8aaf3475d22578331f8ea.setIcon(icon_2a35dc7c2a0284b1d755d83870e05815);
        
    
        var popup_bfef50d9fa55f50eff20b38d4b64a65c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_dc384cbac9f23fbb689a3e0367d6d7fa = $(`&lt;div id=&quot;html_dc384cbac9f23fbb689a3e0367d6d7fa&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESCOFF &lt;br&gt;Vente en 2019 &lt;br&gt;Prix 1467 €&lt;/div&gt;`)[0];
            popup_bfef50d9fa55f50eff20b38d4b64a65c.setContent(html_dc384cbac9f23fbb689a3e0367d6d7fa);
        

        marker_9af4c2269ab8aaf3475d22578331f8ea.bindPopup(popup_bfef50d9fa55f50eff20b38d4b64a65c)
        ;

        
    
    
            var marker_e56635a360c66e0d11487c1ed95db21c = L.marker(
                [48.0401, -4.703612],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_cced218efb782bbcc411f6262eed4edd = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_e56635a360c66e0d11487c1ed95db21c.setIcon(icon_cced218efb782bbcc411f6262eed4edd);
        
    
        var popup_96fa1d9b9bc7ddf9c7f6c2de4b629aac = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c1d879918d227a6eb953fbf14d29cfa9 = $(`&lt;div id=&quot;html_c1d879918d227a6eb953fbf14d29cfa9&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 162 LESCOFF &lt;br&gt;Vente en 2019 &lt;br&gt;Prix 1467 €&lt;/div&gt;`)[0];
            popup_96fa1d9b9bc7ddf9c7f6c2de4b629aac.setContent(html_c1d879918d227a6eb953fbf14d29cfa9);
        

        marker_e56635a360c66e0d11487c1ed95db21c.bindPopup(popup_96fa1d9b9bc7ddf9c7f6c2de4b629aac)
        ;

        
    
    
            var marker_0d8b221bd1c9a282c018f1c8cd92b5ed = L.marker(
                [48.04055, -4.699342],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_18e2d3eaceb981f74dffb42953722cff = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_0d8b221bd1c9a282c018f1c8cd92b5ed.setIcon(icon_18e2d3eaceb981f74dffb42953722cff);
        
    
        var popup_36889b7e1f29f7cf2c63698ad1f9581f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_084e2d9fb6a4fa974b344ede10f5c233 = $(`&lt;div id=&quot;html_084e2d9fb6a4fa974b344ede10f5c233&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 144 D IROISE &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 75000 €&lt;/div&gt;`)[0];
            popup_36889b7e1f29f7cf2c63698ad1f9581f.setContent(html_084e2d9fb6a4fa974b344ede10f5c233);
        

        marker_0d8b221bd1c9a282c018f1c8cd92b5ed.bindPopup(popup_36889b7e1f29f7cf2c63698ad1f9581f)
        ;

        
    
    
            var marker_d6fd894a4d1f23d7617b25a953db5813 = L.marker(
                [48.039907, -4.703508],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_2e17749a9235b60c5b96336f5d014941 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_d6fd894a4d1f23d7617b25a953db5813.setIcon(icon_2e17749a9235b60c5b96336f5d014941);
        
    
        var popup_15b727c2b4c40928ccf56d3b3dd81fda = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1d8a992b57ee333e2cba9cb2135ff96a = $(`&lt;div id=&quot;html_1d8a992b57ee333e2cba9cb2135ff96a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 161 DES LANGOUSTIERS &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 123000 €&lt;/div&gt;`)[0];
            popup_15b727c2b4c40928ccf56d3b3dd81fda.setContent(html_1d8a992b57ee333e2cba9cb2135ff96a);
        

        marker_d6fd894a4d1f23d7617b25a953db5813.bindPopup(popup_15b727c2b4c40928ccf56d3b3dd81fda)
        ;

        
    
    
            var marker_1b4fb054205cc702dab252647bf0f08a = L.marker(
                [48.039851, -4.703561],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_7e5f888d80efd631d8e08a24b10ddacb = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_1b4fb054205cc702dab252647bf0f08a.setIcon(icon_7e5f888d80efd631d8e08a24b10ddacb);
        
    
        var popup_6564b6f4258ade3c9ce77afa5f05d40a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_caf188c0074a77874b5b5a0b12a3d2ef = $(`&lt;div id=&quot;html_caf188c0074a77874b5b5a0b12a3d2ef&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESCOFF &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 123000 €&lt;/div&gt;`)[0];
            popup_6564b6f4258ade3c9ce77afa5f05d40a.setContent(html_caf188c0074a77874b5b5a0b12a3d2ef);
        

        marker_1b4fb054205cc702dab252647bf0f08a.bindPopup(popup_6564b6f4258ade3c9ce77afa5f05d40a)
        ;

        
    
    
            var marker_8bae3779f29a0c0bd8c130d77263a173 = L.marker(
                [48.041159, -4.705031],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_f4f0f2416ec3d64b411af72ee1c121bc = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_8bae3779f29a0c0bd8c130d77263a173.setIcon(icon_f4f0f2416ec3d64b411af72ee1c121bc);
        
    
        var popup_64128df607557c9a0f76ddc6a8ae6900 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a740ba1b82543029cf95cc413a6225e9 = $(`&lt;div id=&quot;html_a740ba1b82543029cf95cc413a6225e9&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5233 DES AJONCS D OR &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 245030 €&lt;/div&gt;`)[0];
            popup_64128df607557c9a0f76ddc6a8ae6900.setContent(html_a740ba1b82543029cf95cc413a6225e9);
        

        marker_8bae3779f29a0c0bd8c130d77263a173.bindPopup(popup_64128df607557c9a0f76ddc6a8ae6900)
        ;

        
    
    
            var marker_cd9626af4adc0eafabeb3b593235b6e3 = L.marker(
                [48.041159, -4.705031],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_66b9985746bb57c1bfa1f6fd34bcdaa8 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_cd9626af4adc0eafabeb3b593235b6e3.setIcon(icon_66b9985746bb57c1bfa1f6fd34bcdaa8);
        
    
        var popup_f7f08718faf72f4f53e1b372d0782eed = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ffae8762ca2ffdee361f8620e9ecb3ee = $(`&lt;div id=&quot;html_ffae8762ca2ffdee361f8620e9ecb3ee&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5233 DES AJONCS D OR &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 245030 €&lt;/div&gt;`)[0];
            popup_f7f08718faf72f4f53e1b372d0782eed.setContent(html_ffae8762ca2ffdee361f8620e9ecb3ee);
        

        marker_cd9626af4adc0eafabeb3b593235b6e3.bindPopup(popup_f7f08718faf72f4f53e1b372d0782eed)
        ;

        
    
    
            var marker_2e44e63f98774f0a0a65de90011ba45a = L.marker(
                [48.041286, -4.705006],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_77709e976257a298faea1d5aacebe171 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_2e44e63f98774f0a0a65de90011ba45a.setIcon(icon_77709e976257a298faea1d5aacebe171);
        
    
        var popup_660d44466777ccad89f0c3a0b79c0e18 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e03b74f6e9c0a59f397ed2c2bc8f59c7 = $(`&lt;div id=&quot;html_e03b74f6e9c0a59f397ed2c2bc8f59c7&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5233 DES AJONCS D OR &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 245030 €&lt;/div&gt;`)[0];
            popup_660d44466777ccad89f0c3a0b79c0e18.setContent(html_e03b74f6e9c0a59f397ed2c2bc8f59c7);
        

        marker_2e44e63f98774f0a0a65de90011ba45a.bindPopup(popup_660d44466777ccad89f0c3a0b79c0e18)
        ;

        
    
    
            var marker_913695fdb22be1a353877f5942d4460a = L.marker(
                [48.041188, -4.70479],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_304968efbd413c50315239fc14d5a9be = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_913695fdb22be1a353877f5942d4460a.setIcon(icon_304968efbd413c50315239fc14d5a9be);
        
    
        var popup_e799b438c65f0be7b3e6c01ad88a1478 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2ee75edca951551b42767eb98a15e0e0 = $(`&lt;div id=&quot;html_2ee75edca951551b42767eb98a15e0e0&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5233 DES AJONCS D OR &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 245030 €&lt;/div&gt;`)[0];
            popup_e799b438c65f0be7b3e6c01ad88a1478.setContent(html_2ee75edca951551b42767eb98a15e0e0);
        

        marker_913695fdb22be1a353877f5942d4460a.bindPopup(popup_e799b438c65f0be7b3e6c01ad88a1478)
        ;

        
    
    
            var marker_4a9eb9865887e5dc99dc9c38e35b48d3 = L.marker(
                [48.041079, -4.70486],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_fdc60d1c4045b28e8e722845cf447e77 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_4a9eb9865887e5dc99dc9c38e35b48d3.setIcon(icon_fdc60d1c4045b28e8e722845cf447e77);
        
    
        var popup_ead11a7cd3817eda74558db4e22be337 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9484a560d73431c16782e41bac772677 = $(`&lt;div id=&quot;html_9484a560d73431c16782e41bac772677&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5233 DES AJONCS D OR &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 245030 €&lt;/div&gt;`)[0];
            popup_ead11a7cd3817eda74558db4e22be337.setContent(html_9484a560d73431c16782e41bac772677);
        

        marker_4a9eb9865887e5dc99dc9c38e35b48d3.bindPopup(popup_ead11a7cd3817eda74558db4e22be337)
        ;

        
    
    
            var marker_adc9243fe6478020a5fd1d429dfcbb75 = L.marker(
                [48.041902, -4.705415],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_6b936cfc0590df01172e3e7ab56f6abf = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_adc9243fe6478020a5fd1d429dfcbb75.setIcon(icon_6b936cfc0590df01172e3e7ab56f6abf);
        
    
        var popup_54efae91889018f3f4ea3e9771180010 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_eada0385c5a969d23dbd246ef4fe73e5 = $(`&lt;div id=&quot;html_eada0385c5a969d23dbd246ef4fe73e5&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LAOUAL &lt;br&gt;Vente en 2019 &lt;br&gt;Prix 50 €&lt;/div&gt;`)[0];
            popup_54efae91889018f3f4ea3e9771180010.setContent(html_eada0385c5a969d23dbd246ef4fe73e5);
        

        marker_adc9243fe6478020a5fd1d429dfcbb75.bindPopup(popup_54efae91889018f3f4ea3e9771180010)
        ;

        
    
    
            var marker_c003a6bbf9599db348397af54191bc15 = L.marker(
                [48.040589, -4.690298],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_4d8d61e0bc254c1b0b82d18db29072d3 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_c003a6bbf9599db348397af54191bc15.setIcon(icon_4d8d61e0bc254c1b0b82d18db29072d3);
        
    
        var popup_00aabd7b123b0225c779bac0943ccf41 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_f3bc9b23094478805a61f8266d8df58b = $(`&lt;div id=&quot;html_f3bc9b23094478805a61f8266d8df58b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGADALEN &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 62000 €&lt;/div&gt;`)[0];
            popup_00aabd7b123b0225c779bac0943ccf41.setContent(html_f3bc9b23094478805a61f8266d8df58b);
        

        marker_c003a6bbf9599db348397af54191bc15.bindPopup(popup_00aabd7b123b0225c779bac0943ccf41)
        ;

        
    
    
            var marker_87bc6a6ee3b29e4347658ffb170d0876 = L.marker(
                [48.040075, -4.69014],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_9f384ef481acb7a4e72f1a0c05d163b1 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_87bc6a6ee3b29e4347658ffb170d0876.setIcon(icon_9f384ef481acb7a4e72f1a0c05d163b1);
        
    
        var popup_f3c454ca1de3f3dc9686a15b465b50f9 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_dfbea101f6cc900e6a27cd6c094667e1 = $(`&lt;div id=&quot;html_dfbea101f6cc900e6a27cd6c094667e1&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 110 KERGADALEN &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 62000 €&lt;/div&gt;`)[0];
            popup_f3c454ca1de3f3dc9686a15b465b50f9.setContent(html_dfbea101f6cc900e6a27cd6c094667e1);
        

        marker_87bc6a6ee3b29e4347658ffb170d0876.bindPopup(popup_f3c454ca1de3f3dc9686a15b465b50f9)
        ;

        
    
    
            var marker_266ce2f4ae3dbbdee6e940958959d730 = L.marker(
                [48.041337, -4.691061],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_543f1c6877c87566968943edf300b7d0 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_266ce2f4ae3dbbdee6e940958959d730.setIcon(icon_543f1c6877c87566968943edf300b7d0);
        
    
        var popup_97ba798a7b8a56b7664efefac839fa1d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8daec230a43fd6944114522505d33d37 = $(`&lt;div id=&quot;html_8daec230a43fd6944114522505d33d37&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGADALEN &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_97ba798a7b8a56b7664efefac839fa1d.setContent(html_8daec230a43fd6944114522505d33d37);
        

        marker_266ce2f4ae3dbbdee6e940958959d730.bindPopup(popup_97ba798a7b8a56b7664efefac839fa1d)
        ;

        
    
    
            var marker_c6350109e189c50a9607618bc3ef1b85 = L.marker(
                [48.040514, -4.691955],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_836f98b4409355d04a7954245130aad8 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_c6350109e189c50a9607618bc3ef1b85.setIcon(icon_836f98b4409355d04a7954245130aad8);
        
    
        var popup_e8beaddae3b867f1739efb117b8a1c8a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_45ed56258ebf88488a87066eeda6af6e = $(`&lt;div id=&quot;html_45ed56258ebf88488a87066eeda6af6e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGADALEN &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_e8beaddae3b867f1739efb117b8a1c8a.setContent(html_45ed56258ebf88488a87066eeda6af6e);
        

        marker_c6350109e189c50a9607618bc3ef1b85.bindPopup(popup_e8beaddae3b867f1739efb117b8a1c8a)
        ;

        
    
    
            var marker_68c353a3b44f1b13569d5148e24c76ea = L.marker(
                [48.040574, -4.691787],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_6a9eddb1d428dba7d52b093475a161d2 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_68c353a3b44f1b13569d5148e24c76ea.setIcon(icon_6a9eddb1d428dba7d52b093475a161d2);
        
    
        var popup_3060f39d9fde1ddf40910f58fd117866 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d007908a15837283c89f6b511ad8c930 = $(`&lt;div id=&quot;html_d007908a15837283c89f6b511ad8c930&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGADALEN &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_3060f39d9fde1ddf40910f58fd117866.setContent(html_d007908a15837283c89f6b511ad8c930);
        

        marker_68c353a3b44f1b13569d5148e24c76ea.bindPopup(popup_3060f39d9fde1ddf40910f58fd117866)
        ;

        
    
    
            var marker_1931159d4f812998ce2faf963824b0c1 = L.marker(
                [48.040049, -4.690408],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_6aaacf3087cd3e99342170a373b82290 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_1931159d4f812998ce2faf963824b0c1.setIcon(icon_6aaacf3087cd3e99342170a373b82290);
        
    
        var popup_2cfbac00ce04d2fc61b106d20192d9da = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_3d8f84f41ef1d842cb4f484f350869f9 = $(`&lt;div id=&quot;html_3d8f84f41ef1d842cb4f484f350869f9&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 111 KERGADALEN &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 50000 €&lt;/div&gt;`)[0];
            popup_2cfbac00ce04d2fc61b106d20192d9da.setContent(html_3d8f84f41ef1d842cb4f484f350869f9);
        

        marker_1931159d4f812998ce2faf963824b0c1.bindPopup(popup_2cfbac00ce04d2fc61b106d20192d9da)
        ;

        
    
    
            var marker_6f2702c5b2186dbad9efff7d35d48cc5 = L.marker(
                [48.039988, -4.683359],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_f1a9305da1f1d0fd501c59b5379c407f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_6f2702c5b2186dbad9efff7d35d48cc5.setIcon(icon_f1a9305da1f1d0fd501c59b5379c407f);
        
    
        var popup_10de9515fbf36ad661bc3a5b94f29901 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_df58109f1050df3ed7f0c80672f0f929 = $(`&lt;div id=&quot;html_df58109f1050df3ed7f0c80672f0f929&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 98 TRIGUEN &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 62000 €&lt;/div&gt;`)[0];
            popup_10de9515fbf36ad661bc3a5b94f29901.setContent(html_df58109f1050df3ed7f0c80672f0f929);
        

        marker_6f2702c5b2186dbad9efff7d35d48cc5.bindPopup(popup_10de9515fbf36ad661bc3a5b94f29901)
        ;

        
    
    
            var marker_b946e993c38b5f1c88edd858aaa3d1be = L.marker(
                [48.040099, -4.68336],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_c0def23c57c57365c3be1b4fc1e2684c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_b946e993c38b5f1c88edd858aaa3d1be.setIcon(icon_c0def23c57c57365c3be1b4fc1e2684c);
        
    
        var popup_ec96acabaddb9b43cac3d72bd4d921f9 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c62d4352d37e1b11feec5cff949ba680 = $(`&lt;div id=&quot;html_c62d4352d37e1b11feec5cff949ba680&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  TRIGUEN &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 62000 €&lt;/div&gt;`)[0];
            popup_ec96acabaddb9b43cac3d72bd4d921f9.setContent(html_c62d4352d37e1b11feec5cff949ba680);
        

        marker_b946e993c38b5f1c88edd858aaa3d1be.bindPopup(popup_ec96acabaddb9b43cac3d72bd4d921f9)
        ;

        
    
    
            var marker_ed9f8ad637675a0501479b4c7124535f = L.marker(
                [48.040522, -4.688371],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_e83b60f10299ff49d054b6966af2f8fb = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ed9f8ad637675a0501479b4c7124535f.setIcon(icon_e83b60f10299ff49d054b6966af2f8fb);
        
    
        var popup_deb4a2852751de27faf20e4c3ead872d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_28aee01ff40cb91e601446ca84c3ef6a = $(`&lt;div id=&quot;html_28aee01ff40cb91e601446ca84c3ef6a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGADALEN &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 60000 €&lt;/div&gt;`)[0];
            popup_deb4a2852751de27faf20e4c3ead872d.setContent(html_28aee01ff40cb91e601446ca84c3ef6a);
        

        marker_ed9f8ad637675a0501479b4c7124535f.bindPopup(popup_deb4a2852751de27faf20e4c3ead872d)
        ;

        
    
    
            var marker_5b062ee04afe3dad572fb7c19bac57fb = L.marker(
                [48.040618, -4.68813],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_f8950815a48712a726c6fecd41dbeeed = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_5b062ee04afe3dad572fb7c19bac57fb.setIcon(icon_f8950815a48712a726c6fecd41dbeeed);
        
    
        var popup_40d6080031304671891dc02e9f4fbedd = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_baeff2e9555c23ae3f55d8ea922340c1 = $(`&lt;div id=&quot;html_baeff2e9555c23ae3f55d8ea922340c1&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGADALEN &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 60000 €&lt;/div&gt;`)[0];
            popup_40d6080031304671891dc02e9f4fbedd.setContent(html_baeff2e9555c23ae3f55d8ea922340c1);
        

        marker_5b062ee04afe3dad572fb7c19bac57fb.bindPopup(popup_40d6080031304671891dc02e9f4fbedd)
        ;

        
    
    
            var marker_69a020f65298e7e4807dfe34e473f83c = L.marker(
                [48.040487, -4.688305],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_da8140fb4c3111ca1767df1dbfe5fb44 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_69a020f65298e7e4807dfe34e473f83c.setIcon(icon_da8140fb4c3111ca1767df1dbfe5fb44);
        
    
        var popup_af9b94c6ec98b3f03184de4e6b984d16 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8333445389c63721ee4905879b6a3056 = $(`&lt;div id=&quot;html_8333445389c63721ee4905879b6a3056&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 453 TRIGUEN &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 60000 €&lt;/div&gt;`)[0];
            popup_af9b94c6ec98b3f03184de4e6b984d16.setContent(html_8333445389c63721ee4905879b6a3056);
        

        marker_69a020f65298e7e4807dfe34e473f83c.bindPopup(popup_af9b94c6ec98b3f03184de4e6b984d16)
        ;

        
    
    
            var marker_810095ca7c53e60ed18c33a5d1d6d141 = L.marker(
                [48.040086, -4.683292],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_82d84a5a044fc4a938324072b9cdaf1f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_810095ca7c53e60ed18c33a5d1d6d141.setIcon(icon_82d84a5a044fc4a938324072b9cdaf1f);
        
    
        var popup_bbe38d0a93ad0dc42198694260844d67 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d637d11cd68af4b3a1e63e0ed69ed44d = $(`&lt;div id=&quot;html_d637d11cd68af4b3a1e63e0ed69ed44d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  TRIGUEN &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 62000 €&lt;/div&gt;`)[0];
            popup_bbe38d0a93ad0dc42198694260844d67.setContent(html_d637d11cd68af4b3a1e63e0ed69ed44d);
        

        marker_810095ca7c53e60ed18c33a5d1d6d141.bindPopup(popup_bbe38d0a93ad0dc42198694260844d67)
        ;

        
    
    
            var marker_bbb8049d0d615c734a5d9873e78a297f = L.marker(
                [48.040086, -4.683292],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_613529e5bc57096b1cd23d5aa463a049 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_bbb8049d0d615c734a5d9873e78a297f.setIcon(icon_613529e5bc57096b1cd23d5aa463a049);
        
    
        var popup_504a330d7249486102734bf36a34216e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e0091bdec58d26277c27ea47300a8c9e = $(`&lt;div id=&quot;html_e0091bdec58d26277c27ea47300a8c9e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  TRIGUEN &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 62000 €&lt;/div&gt;`)[0];
            popup_504a330d7249486102734bf36a34216e.setContent(html_e0091bdec58d26277c27ea47300a8c9e);
        

        marker_bbb8049d0d615c734a5d9873e78a297f.bindPopup(popup_504a330d7249486102734bf36a34216e)
        ;

        
    
    
            var marker_5acf989f82d81f494d230eefaab73367 = L.marker(
                [48.04061, -4.688259],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_89352c367eb49c408b8dd34eec33053c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_5acf989f82d81f494d230eefaab73367.setIcon(icon_89352c367eb49c408b8dd34eec33053c);
        
    
        var popup_5bed4a7d0bcf4ad453952bbd25a6c60c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_678958e3289f63e6ac585526eb2b73db = $(`&lt;div id=&quot;html_678958e3289f63e6ac585526eb2b73db&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGADALEN &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 60000 €&lt;/div&gt;`)[0];
            popup_5bed4a7d0bcf4ad453952bbd25a6c60c.setContent(html_678958e3289f63e6ac585526eb2b73db);
        

        marker_5acf989f82d81f494d230eefaab73367.bindPopup(popup_5bed4a7d0bcf4ad453952bbd25a6c60c)
        ;

        
    
    
            var marker_8b45dc2d53e126bd8ee5ec0743a10dc6 = L.marker(
                [48.042198, -4.6794],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_a917487b6424cf64454575ad97ccc78c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_8b45dc2d53e126bd8ee5ec0743a10dc6.setIcon(icon_a917487b6424cf64454575ad97ccc78c);
        
    
        var popup_88d5a67f6c0018b4eb22cc0e7492c13c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d25c26a9c8cc7446bc46435342712dc7 = $(`&lt;div id=&quot;html_d25c26a9c8cc7446bc46435342712dc7&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE MANOIR &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 1055 €&lt;/div&gt;`)[0];
            popup_88d5a67f6c0018b4eb22cc0e7492c13c.setContent(html_d25c26a9c8cc7446bc46435342712dc7);
        

        marker_8b45dc2d53e126bd8ee5ec0743a10dc6.bindPopup(popup_88d5a67f6c0018b4eb22cc0e7492c13c)
        ;

        
    
    
            var marker_028bd7e2825cf058279da1f3ad45709b = L.marker(
                [48.041142, -4.681685],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_75c4c78f346b867508a46eba47ba0133 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_028bd7e2825cf058279da1f3ad45709b.setIcon(icon_75c4c78f346b867508a46eba47ba0133);
        
    
        var popup_86126af44cf3971c30fe178f557faee2 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_275a7dbcab182742a3ab33facfe2f1ca = $(`&lt;div id=&quot;html_275a7dbcab182742a3ab33facfe2f1ca&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE MANOIR &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 90000 €&lt;/div&gt;`)[0];
            popup_86126af44cf3971c30fe178f557faee2.setContent(html_275a7dbcab182742a3ab33facfe2f1ca);
        

        marker_028bd7e2825cf058279da1f3ad45709b.bindPopup(popup_86126af44cf3971c30fe178f557faee2)
        ;

        
    
    
            var marker_dc07f20a6f85836483cf3ac0800f75a2 = L.marker(
                [48.041191, -4.681444],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_e48557361023feb07694d1afc2efa2d6 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_dc07f20a6f85836483cf3ac0800f75a2.setIcon(icon_e48557361023feb07694d1afc2efa2d6);
        
    
        var popup_e61f0a98ec80e183044aae4154d8f555 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_59e0d0fd2d8d9437426c6d582c78973e = $(`&lt;div id=&quot;html_59e0d0fd2d8d9437426c6d582c78973e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE MANOIR &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 90000 €&lt;/div&gt;`)[0];
            popup_e61f0a98ec80e183044aae4154d8f555.setContent(html_59e0d0fd2d8d9437426c6d582c78973e);
        

        marker_dc07f20a6f85836483cf3ac0800f75a2.bindPopup(popup_e61f0a98ec80e183044aae4154d8f555)
        ;

        
    
    
            var marker_1c998889620356b75f40a9b1b272a17d = L.marker(
                [48.037833, -4.67416],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_5ff4b925c9ae0dc575d99f401253ad1c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_1c998889620356b75f40a9b1b272a17d.setIcon(icon_5ff4b925c9ae0dc575d99f401253ad1c);
        
    
        var popup_c76df40e63e81e2635de7a3654b5b28e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_bd47a3658fe52ff73899a4993179aaa7 = $(`&lt;div id=&quot;html_bd47a3658fe52ff73899a4993179aaa7&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 66 ST YVES &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 1000 €&lt;/div&gt;`)[0];
            popup_c76df40e63e81e2635de7a3654b5b28e.setContent(html_bd47a3658fe52ff73899a4993179aaa7);
        

        marker_1c998889620356b75f40a9b1b272a17d.bindPopup(popup_c76df40e63e81e2635de7a3654b5b28e)
        ;

        
    
    
            var marker_3298c48d92d8e3142f51922189d5823e = L.marker(
                [48.037833, -4.67416],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_393756ddf1947ecb4c39761a678535c0 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_3298c48d92d8e3142f51922189d5823e.setIcon(icon_393756ddf1947ecb4c39761a678535c0);
        
    
        var popup_7639f807b62cfb64391f810d252ca786 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_03f680a0724f0eb199b883df8b092c6d = $(`&lt;div id=&quot;html_03f680a0724f0eb199b883df8b092c6d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 66 ST YVES &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 1000 €&lt;/div&gt;`)[0];
            popup_7639f807b62cfb64391f810d252ca786.setContent(html_03f680a0724f0eb199b883df8b092c6d);
        

        marker_3298c48d92d8e3142f51922189d5823e.bindPopup(popup_7639f807b62cfb64391f810d252ca786)
        ;

        
    
    
            var marker_1c8df16d6f2268bee089faec40d7de78 = L.marker(
                [48.037833, -4.67416],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_69501eb65073d22091e47b264aec61a2 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_1c8df16d6f2268bee089faec40d7de78.setIcon(icon_69501eb65073d22091e47b264aec61a2);
        
    
        var popup_68c74250c00bebe37e7a6bf9413e1ef9 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_3c7554b24d2433073ad1749bb502803e = $(`&lt;div id=&quot;html_3c7554b24d2433073ad1749bb502803e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 66 ST YVES &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 75000 €&lt;/div&gt;`)[0];
            popup_68c74250c00bebe37e7a6bf9413e1ef9.setContent(html_3c7554b24d2433073ad1749bb502803e);
        

        marker_1c8df16d6f2268bee089faec40d7de78.bindPopup(popup_68c74250c00bebe37e7a6bf9413e1ef9)
        ;

        
    
    
            var marker_59e9515dbef3b87a447c79a21edbcb31 = L.marker(
                [48.037833, -4.67416],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_e35d0540fed4e3be98594e309b7057aa = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_59e9515dbef3b87a447c79a21edbcb31.setIcon(icon_e35d0540fed4e3be98594e309b7057aa);
        
    
        var popup_a5942ed239ebf2014dfab90238cdd9a1 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_29ab1bc55cb5bc67e578a0e20159277f = $(`&lt;div id=&quot;html_29ab1bc55cb5bc67e578a0e20159277f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 66 ST YVES &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 75000 €&lt;/div&gt;`)[0];
            popup_a5942ed239ebf2014dfab90238cdd9a1.setContent(html_29ab1bc55cb5bc67e578a0e20159277f);
        

        marker_59e9515dbef3b87a447c79a21edbcb31.bindPopup(popup_a5942ed239ebf2014dfab90238cdd9a1)
        ;

        
    
    
            var marker_2f965d1d1b24c6ecf9b465504a541ce2 = L.marker(
                [48.037827, -4.674444],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_1c146881d9621baaffc5f4c21d92ae10 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_2f965d1d1b24c6ecf9b465504a541ce2.setIcon(icon_1c146881d9621baaffc5f4c21d92ae10);
        
    
        var popup_411b35342a575d9a0ba0eadc0791cd4e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_4487d9a2799b04f5c9146a52b8a17f80 = $(`&lt;div id=&quot;html_4487d9a2799b04f5c9146a52b8a17f80&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 66 ST YVES &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 75000 €&lt;/div&gt;`)[0];
            popup_411b35342a575d9a0ba0eadc0791cd4e.setContent(html_4487d9a2799b04f5c9146a52b8a17f80);
        

        marker_2f965d1d1b24c6ecf9b465504a541ce2.bindPopup(popup_411b35342a575d9a0ba0eadc0791cd4e)
        ;

        
    
    
            var marker_01f962c07d6d53977f24aff272097848 = L.marker(
                [48.037735, -4.675296],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_1f12616f652c0f0529c21147df78cb6f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_01f962c07d6d53977f24aff272097848.setIcon(icon_1f12616f652c0f0529c21147df78cb6f);
        
    
        var popup_9ec1aec266758350e1606715682ff957 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ab08b3dc6ef6b8279dadd50cc5ef2ff4 = $(`&lt;div id=&quot;html_ab08b3dc6ef6b8279dadd50cc5ef2ff4&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 69 ST YVES &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 85000 €&lt;/div&gt;`)[0];
            popup_9ec1aec266758350e1606715682ff957.setContent(html_ab08b3dc6ef6b8279dadd50cc5ef2ff4);
        

        marker_01f962c07d6d53977f24aff272097848.bindPopup(popup_9ec1aec266758350e1606715682ff957)
        ;

        
    
    
            var marker_ad33294fcee64c965ec3f2b3ef469b7c = L.marker(
                [48.037735, -4.675296],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_a764de1906e27a3e4b6d7517cd3aefcd = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ad33294fcee64c965ec3f2b3ef469b7c.setIcon(icon_a764de1906e27a3e4b6d7517cd3aefcd);
        
    
        var popup_16d3b07d846ba14514708378c6605cfd = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c49de61b4361ebf764ec472176d550c7 = $(`&lt;div id=&quot;html_c49de61b4361ebf764ec472176d550c7&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 69 ST YVES &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 85000 €&lt;/div&gt;`)[0];
            popup_16d3b07d846ba14514708378c6605cfd.setContent(html_c49de61b4361ebf764ec472176d550c7);
        

        marker_ad33294fcee64c965ec3f2b3ef469b7c.bindPopup(popup_16d3b07d846ba14514708378c6605cfd)
        ;

        
    
    
            var marker_ff0732d5e74134fe1682bc1b410ff327 = L.marker(
                [48.038092, -4.67556],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_306d4c13f5e595571c98f63107fc2e16 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ff0732d5e74134fe1682bc1b410ff327.setIcon(icon_306d4c13f5e595571c98f63107fc2e16);
        
    
        var popup_dd33b08e700c2d96deef4b2d0bcacf10 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_966072bace74e0bab351a8178d35e00d = $(`&lt;div id=&quot;html_966072bace74e0bab351a8178d35e00d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  ST YVES &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 85000 €&lt;/div&gt;`)[0];
            popup_dd33b08e700c2d96deef4b2d0bcacf10.setContent(html_966072bace74e0bab351a8178d35e00d);
        

        marker_ff0732d5e74134fe1682bc1b410ff327.bindPopup(popup_dd33b08e700c2d96deef4b2d0bcacf10)
        ;

        
    
    
            var marker_efa4b5686462cfbb5ad1006160de15ee = L.marker(
                [48.040436, -4.678833],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_435fbf51e22aa1782d2a29fa8bc329a3 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_efa4b5686462cfbb5ad1006160de15ee.setIcon(icon_435fbf51e22aa1782d2a29fa8bc329a3);
        
    
        var popup_e08b4024b31d67aca4dacb6783d67d5e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_47c3d94ae80b75a300687a4dacde50bf = $(`&lt;div id=&quot;html_47c3d94ae80b75a300687a4dacde50bf&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE MANOIR &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 110000 €&lt;/div&gt;`)[0];
            popup_e08b4024b31d67aca4dacb6783d67d5e.setContent(html_47c3d94ae80b75a300687a4dacde50bf);
        

        marker_efa4b5686462cfbb5ad1006160de15ee.bindPopup(popup_e08b4024b31d67aca4dacb6783d67d5e)
        ;

        
    
    
            var marker_a8c40f54fdc03cbafe754cce6f51ea35 = L.marker(
                [48.040259, -4.679053],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_2f56d3abb9c17babfd45f9dac68d59ee = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_a8c40f54fdc03cbafe754cce6f51ea35.setIcon(icon_2f56d3abb9c17babfd45f9dac68d59ee);
        
    
        var popup_331506ca633624330a4fded856034486 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_129eebf2c40ae6d32e6f175786d4e97b = $(`&lt;div id=&quot;html_129eebf2c40ae6d32e6f175786d4e97b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE MANOIR &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 110000 €&lt;/div&gt;`)[0];
            popup_331506ca633624330a4fded856034486.setContent(html_129eebf2c40ae6d32e6f175786d4e97b);
        

        marker_a8c40f54fdc03cbafe754cce6f51ea35.bindPopup(popup_331506ca633624330a4fded856034486)
        ;

        
    
    
            var marker_90c5f1f4ffedd25e1e54fc09618d36dd = L.marker(
                [48.040209, -4.679209],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_03434444aaaac70437b65b49a7016bce = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_90c5f1f4ffedd25e1e54fc09618d36dd.setIcon(icon_03434444aaaac70437b65b49a7016bce);
        
    
        var popup_82ea9ea8f4b434f833dcb3cb4c7d323b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_faffc0de24b3cd17e69c783dd275cb10 = $(`&lt;div id=&quot;html_faffc0de24b3cd17e69c783dd275cb10&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5061 JEAN FRANCOIS CARVAL &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 110000 €&lt;/div&gt;`)[0];
            popup_82ea9ea8f4b434f833dcb3cb4c7d323b.setContent(html_faffc0de24b3cd17e69c783dd275cb10);
        

        marker_90c5f1f4ffedd25e1e54fc09618d36dd.bindPopup(popup_82ea9ea8f4b434f833dcb3cb4c7d323b)
        ;

        
    
    
            var marker_5f6442e22800fc36e041d7de233d1416 = L.marker(
                [48.040547, -4.679162],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_09b049ba857d2e7d74013936d53f4cc2 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_5f6442e22800fc36e041d7de233d1416.setIcon(icon_09b049ba857d2e7d74013936d53f4cc2);
        
    
        var popup_edc8d9bf4bb947254aa1e577286822f5 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_64e290a3f1c607e9db0e003a51f2486e = $(`&lt;div id=&quot;html_64e290a3f1c607e9db0e003a51f2486e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE MANOIR &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 110000 €&lt;/div&gt;`)[0];
            popup_edc8d9bf4bb947254aa1e577286822f5.setContent(html_64e290a3f1c607e9db0e003a51f2486e);
        

        marker_5f6442e22800fc36e041d7de233d1416.bindPopup(popup_edc8d9bf4bb947254aa1e577286822f5)
        ;

        
    
    
            var marker_aba1df4b4423e2ec1750bd23aebaeac8 = L.marker(
                [48.040569, -4.679556],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_26b59bdcb592beb54f003ae03ba24f5c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_aba1df4b4423e2ec1750bd23aebaeac8.setIcon(icon_26b59bdcb592beb54f003ae03ba24f5c);
        
    
        var popup_8a3e1b4cd9304a8f2141e1a09533d6ce = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_b0309ca389157f25d8dee398140c8e69 = $(`&lt;div id=&quot;html_b0309ca389157f25d8dee398140c8e69&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE MANOIR &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 75000 €&lt;/div&gt;`)[0];
            popup_8a3e1b4cd9304a8f2141e1a09533d6ce.setContent(html_b0309ca389157f25d8dee398140c8e69);
        

        marker_aba1df4b4423e2ec1750bd23aebaeac8.bindPopup(popup_8a3e1b4cd9304a8f2141e1a09533d6ce)
        ;

        
    
    
            var marker_dc9e301c510f4c5ed8c8990c26b0d31e = L.marker(
                [48.040599, -4.67922],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_690f0abcf8df6dbb69fc47a67ff7487f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_dc9e301c510f4c5ed8c8990c26b0d31e.setIcon(icon_690f0abcf8df6dbb69fc47a67ff7487f);
        
    
        var popup_159162a148cfbe1b9ad4bdda9c1052ee = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_556a4f4780419f3bf3ed3cd6ec5d9be1 = $(`&lt;div id=&quot;html_556a4f4780419f3bf3ed3cd6ec5d9be1&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE MANOIR &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 110000 €&lt;/div&gt;`)[0];
            popup_159162a148cfbe1b9ad4bdda9c1052ee.setContent(html_556a4f4780419f3bf3ed3cd6ec5d9be1);
        

        marker_dc9e301c510f4c5ed8c8990c26b0d31e.bindPopup(popup_159162a148cfbe1b9ad4bdda9c1052ee)
        ;

        
    
    
            var marker_2efa41f18badd1cf4b3583a8b0c04763 = L.marker(
                [48.040654, -4.679536],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_db90e49dafb2bfd45cf907babf54bb78 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_2efa41f18badd1cf4b3583a8b0c04763.setIcon(icon_db90e49dafb2bfd45cf907babf54bb78);
        
    
        var popup_ff255573c636e3096e8d54eb4d757c81 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_4df442fd8cd080e19488a4fdc70fbf21 = $(`&lt;div id=&quot;html_4df442fd8cd080e19488a4fdc70fbf21&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 85 JEAN FRANCOIS CARVAL &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 75000 €&lt;/div&gt;`)[0];
            popup_ff255573c636e3096e8d54eb4d757c81.setContent(html_4df442fd8cd080e19488a4fdc70fbf21);
        

        marker_2efa41f18badd1cf4b3583a8b0c04763.bindPopup(popup_ff255573c636e3096e8d54eb4d757c81)
        ;

        
    
    
            var marker_6c825b101c9c4edbbe7c829a01860d0d = L.marker(
                [48.038994, -4.678002],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_7941fb9779fd5a02e9fc6504cdb0e847 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_6c825b101c9c4edbbe7c829a01860d0d.setIcon(icon_7941fb9779fd5a02e9fc6504cdb0e847);
        
    
        var popup_4bd595149b2dad7be1ecde59d301d039 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1d4bdc8503e6405bc39546432b81dac0 = $(`&lt;div id=&quot;html_1d4bdc8503e6405bc39546432b81dac0&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE MANOIR &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 554 €&lt;/div&gt;`)[0];
            popup_4bd595149b2dad7be1ecde59d301d039.setContent(html_1d4bdc8503e6405bc39546432b81dac0);
        

        marker_6c825b101c9c4edbbe7c829a01860d0d.bindPopup(popup_4bd595149b2dad7be1ecde59d301d039)
        ;

        
    
    
            var marker_7571640baeff8b0222ee75bd2c2a6287 = L.marker(
                [48.039681, -4.67822],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_5d8cae7163e3112f875c425f16857970 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_7571640baeff8b0222ee75bd2c2a6287.setIcon(icon_5d8cae7163e3112f875c425f16857970);
        
    
        var popup_3337be7aab9f06cf4274dc997e7b42e1 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_67ee1a66f96b627f6c26d12453d35d86 = $(`&lt;div id=&quot;html_67ee1a66f96b627f6c26d12453d35d86&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE MANOIR &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 344 €&lt;/div&gt;`)[0];
            popup_3337be7aab9f06cf4274dc997e7b42e1.setContent(html_67ee1a66f96b627f6c26d12453d35d86);
        

        marker_7571640baeff8b0222ee75bd2c2a6287.bindPopup(popup_3337be7aab9f06cf4274dc997e7b42e1)
        ;

        
    
    
            var marker_da09f66d33b1d8a3166dc82c23c89cff = L.marker(
                [48.037644, -4.666085],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_44cf4a6b5d83c6d5ebaa26931872e779 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_da09f66d33b1d8a3166dc82c23c89cff.setIcon(icon_44cf4a6b5d83c6d5ebaa26931872e779);
        
    
        var popup_006a782df33aacb6a9eca78a5e630059 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_4baab85560feb07da01ce0e37b23dc9b = $(`&lt;div id=&quot;html_4baab85560feb07da01ce0e37b23dc9b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 27 LE BOURG &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 105000 €&lt;/div&gt;`)[0];
            popup_006a782df33aacb6a9eca78a5e630059.setContent(html_4baab85560feb07da01ce0e37b23dc9b);
        

        marker_da09f66d33b1d8a3166dc82c23c89cff.bindPopup(popup_006a782df33aacb6a9eca78a5e630059)
        ;

        
    
    
            var marker_3c3e07f8839f900ee47ee390d5a1bee9 = L.marker(
                [48.036503, -4.665601],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_635f9224554e8f1e204cd66e28280306 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_3c3e07f8839f900ee47ee390d5a1bee9.setIcon(icon_635f9224554e8f1e204cd66e28280306);
        
    
        var popup_e76e52830e565dcde94f99897a8e428a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_aa3322aef37286b23ff84ce75a30dd73 = $(`&lt;div id=&quot;html_aa3322aef37286b23ff84ce75a30dd73&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESTRIVIN &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 87500 €&lt;/div&gt;`)[0];
            popup_e76e52830e565dcde94f99897a8e428a.setContent(html_aa3322aef37286b23ff84ce75a30dd73);
        

        marker_3c3e07f8839f900ee47ee390d5a1bee9.bindPopup(popup_e76e52830e565dcde94f99897a8e428a)
        ;

        
    
    
            var marker_b8ca91c69dd3b7289db928fc825bc411 = L.marker(
                [48.036537, -4.665724],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_8248a0c755280526078e41dd369c5f5f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_b8ca91c69dd3b7289db928fc825bc411.setIcon(icon_8248a0c755280526078e41dd369c5f5f);
        
    
        var popup_46089ccaae591ba6b16b3e607ce39a11 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ed321a5458d2ad14f22f95e504860e82 = $(`&lt;div id=&quot;html_ed321a5458d2ad14f22f95e504860e82&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 7 LESTRIVIN &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 87500 €&lt;/div&gt;`)[0];
            popup_46089ccaae591ba6b16b3e607ce39a11.setContent(html_ed321a5458d2ad14f22f95e504860e82);
        

        marker_b8ca91c69dd3b7289db928fc825bc411.bindPopup(popup_46089ccaae591ba6b16b3e607ce39a11)
        ;

        
    
    
            var marker_2fb815a61285bc1e8eaaa96e92cf6844 = L.marker(
                [48.036532, -4.666032],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_54caf4c620212a1f7f7d640848dd913f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_2fb815a61285bc1e8eaaa96e92cf6844.setIcon(icon_54caf4c620212a1f7f7d640848dd913f);
        
    
        var popup_0f72977ecdd1d384dd4eb03660f501b2 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_77f82c3981ddcac225e907680690241f = $(`&lt;div id=&quot;html_77f82c3981ddcac225e907680690241f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5 LESTRIVIN &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 110000 €&lt;/div&gt;`)[0];
            popup_0f72977ecdd1d384dd4eb03660f501b2.setContent(html_77f82c3981ddcac225e907680690241f);
        

        marker_2fb815a61285bc1e8eaaa96e92cf6844.bindPopup(popup_0f72977ecdd1d384dd4eb03660f501b2)
        ;

        
    
    
            var marker_4d47e5297f1bfb818c0e509fda1e163b = L.marker(
                [48.036532, -4.666032],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_5d5338ad031903f27e1a2fbe9381b5cd = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_4d47e5297f1bfb818c0e509fda1e163b.setIcon(icon_5d5338ad031903f27e1a2fbe9381b5cd);
        
    
        var popup_4c70818d63453dbc393a6320e37bcdcc = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_35289bfd0e5641cd8efde73a394dba9a = $(`&lt;div id=&quot;html_35289bfd0e5641cd8efde73a394dba9a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5 LESTRIVIN &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 105000 €&lt;/div&gt;`)[0];
            popup_4c70818d63453dbc393a6320e37bcdcc.setContent(html_35289bfd0e5641cd8efde73a394dba9a);
        

        marker_4d47e5297f1bfb818c0e509fda1e163b.bindPopup(popup_4c70818d63453dbc393a6320e37bcdcc)
        ;

        
    
    
            var marker_d6137b7b26e48b3e89f706294f0801c7 = L.marker(
                [48.036741, -4.666059],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_166d061a7065607c0cfc160cfa500b81 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_d6137b7b26e48b3e89f706294f0801c7.setIcon(icon_166d061a7065607c0cfc160cfa500b81);
        
    
        var popup_9c67bd4e8cba57f540de814881e57fcb = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2acc13171d7a37cc5850771eef764055 = $(`&lt;div id=&quot;html_2acc13171d7a37cc5850771eef764055&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESTRIVIN &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 110000 €&lt;/div&gt;`)[0];
            popup_9c67bd4e8cba57f540de814881e57fcb.setContent(html_2acc13171d7a37cc5850771eef764055);
        

        marker_d6137b7b26e48b3e89f706294f0801c7.bindPopup(popup_9c67bd4e8cba57f540de814881e57fcb)
        ;

        
    
    
            var marker_6126418f84e295b729694e996cd8e71e = L.marker(
                [48.036741, -4.666059],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_f29bfbcf0f3c6773e507ef546eebcf3f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_6126418f84e295b729694e996cd8e71e.setIcon(icon_f29bfbcf0f3c6773e507ef546eebcf3f);
        
    
        var popup_8048700a86e0c7976996b71489a407dd = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_56bac9d2282cc996e48aeba74aed502b = $(`&lt;div id=&quot;html_56bac9d2282cc996e48aeba74aed502b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESTRIVIN &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 105000 €&lt;/div&gt;`)[0];
            popup_8048700a86e0c7976996b71489a407dd.setContent(html_56bac9d2282cc996e48aeba74aed502b);
        

        marker_6126418f84e295b729694e996cd8e71e.bindPopup(popup_8048700a86e0c7976996b71489a407dd)
        ;

        
    
    
            var marker_b4c7347c2cc5233786381c55f3f7d681 = L.marker(
                [48.03823, -4.666243],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_5675d34033961f49a2d8081c9b0a6260 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_b4c7347c2cc5233786381c55f3f7d681.setIcon(icon_5675d34033961f49a2d8081c9b0a6260);
        
    
        var popup_3ec4c1bf535e780b5b55abb3812595a4 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_87e63e1d4a44d7e6762f320bc4fe23ac = $(`&lt;div id=&quot;html_87e63e1d4a44d7e6762f320bc4fe23ac&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 23 PONT YANN &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 32000 €&lt;/div&gt;`)[0];
            popup_3ec4c1bf535e780b5b55abb3812595a4.setContent(html_87e63e1d4a44d7e6762f320bc4fe23ac);
        

        marker_b4c7347c2cc5233786381c55f3f7d681.bindPopup(popup_3ec4c1bf535e780b5b55abb3812595a4)
        ;

        
    
    
            var marker_af85a547db3c8e058bc7c6cc0cdf13ce = L.marker(
                [48.037832, -4.666753],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_640ccea8a718a4f0de4f1377e0d8459e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_af85a547db3c8e058bc7c6cc0cdf13ce.setIcon(icon_640ccea8a718a4f0de4f1377e0d8459e);
        
    
        var popup_b0a7f4f17a2080699f9b3b8e4dbd80b7 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_96e1bd1604087ed4b9062823f0f866ec = $(`&lt;div id=&quot;html_96e1bd1604087ed4b9062823f0f866ec&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 12 DE LA LIBERTE &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 49000 €&lt;/div&gt;`)[0];
            popup_b0a7f4f17a2080699f9b3b8e4dbd80b7.setContent(html_96e1bd1604087ed4b9062823f0f866ec);
        

        marker_af85a547db3c8e058bc7c6cc0cdf13ce.bindPopup(popup_b0a7f4f17a2080699f9b3b8e4dbd80b7)
        ;

        
    
    
            var marker_26949ce0a4ec00cef60fb71a1bd3b6c2 = L.marker(
                [48.038023, -4.666074],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_2d251ae342fd605d1df05d335d13f59e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_26949ce0a4ec00cef60fb71a1bd3b6c2.setIcon(icon_2d251ae342fd605d1df05d335d13f59e);
        
    
        var popup_67997ec8e11d07c7b4c10fbc7f4b3244 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_0fc4f5e21705d6516e8bd234f19b661b = $(`&lt;div id=&quot;html_0fc4f5e21705d6516e8bd234f19b661b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5222 DE LA LIBERTE &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 88000 €&lt;/div&gt;`)[0];
            popup_67997ec8e11d07c7b4c10fbc7f4b3244.setContent(html_0fc4f5e21705d6516e8bd234f19b661b);
        

        marker_26949ce0a4ec00cef60fb71a1bd3b6c2.bindPopup(popup_67997ec8e11d07c7b4c10fbc7f4b3244)
        ;

        
    
    
            var marker_e4769ce387bed55a98ccd88836f00236 = L.marker(
                [48.038023, -4.666074],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_243b142fceb195a02ba74e34f41e1adb = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_e4769ce387bed55a98ccd88836f00236.setIcon(icon_243b142fceb195a02ba74e34f41e1adb);
        
    
        var popup_53178d52fcaf36ceebe161606b8a708b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c47ef4bb1c6cf9bbfbcaacad4dd801fe = $(`&lt;div id=&quot;html_c47ef4bb1c6cf9bbfbcaacad4dd801fe&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5222 DE LA LIBERTE &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 88000 €&lt;/div&gt;`)[0];
            popup_53178d52fcaf36ceebe161606b8a708b.setContent(html_c47ef4bb1c6cf9bbfbcaacad4dd801fe);
        

        marker_e4769ce387bed55a98ccd88836f00236.bindPopup(popup_53178d52fcaf36ceebe161606b8a708b)
        ;

        
    
    
            var marker_434572b13a43806113a41c5e4313daf0 = L.marker(
                [48.036936, -4.665258],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_4ba6d46549f8fce4bfb642ca44061a99 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_434572b13a43806113a41c5e4313daf0.setIcon(icon_4ba6d46549f8fce4bfb642ca44061a99);
        
    
        var popup_ad9894a4487eadccfd2754e8b439d9b0 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2e249d925a22b67300935a435fd37dcb = $(`&lt;div id=&quot;html_2e249d925a22b67300935a435fd37dcb&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5267 DES DEMOISELLES &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 114000 €&lt;/div&gt;`)[0];
            popup_ad9894a4487eadccfd2754e8b439d9b0.setContent(html_2e249d925a22b67300935a435fd37dcb);
        

        marker_434572b13a43806113a41c5e4313daf0.bindPopup(popup_ad9894a4487eadccfd2754e8b439d9b0)
        ;

        
    
    
            var marker_3953333a65739eaf8a72d0934faa9f11 = L.marker(
                [48.036618, -4.661793],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_8f8cf79ca25f816332a0214bc3a6c4c4 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_3953333a65739eaf8a72d0934faa9f11.setIcon(icon_8f8cf79ca25f816332a0214bc3a6c4c4);
        
    
        var popup_1dea9a54fd0a1d7b07952c6e21cfb7ae = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9ac27a886e7a0afa2263ffa2ed7fd133 = $(`&lt;div id=&quot;html_9ac27a886e7a0afa2263ffa2ed7fd133&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 670 DU CHENE VERT &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 137000 €&lt;/div&gt;`)[0];
            popup_1dea9a54fd0a1d7b07952c6e21cfb7ae.setContent(html_9ac27a886e7a0afa2263ffa2ed7fd133);
        

        marker_3953333a65739eaf8a72d0934faa9f11.bindPopup(popup_1dea9a54fd0a1d7b07952c6e21cfb7ae)
        ;

        
    
    
            var marker_24b64ba5fbe0a50cddb07315f320d036 = L.marker(
                [48.036618, -4.661793],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_a3761773b7b94cbd4f04635fb7959e7c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_24b64ba5fbe0a50cddb07315f320d036.setIcon(icon_a3761773b7b94cbd4f04635fb7959e7c);
        
    
        var popup_8e72c49df6d427bde570310393e5c170 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_20c6efd1db7801b11259a2d812cf6764 = $(`&lt;div id=&quot;html_20c6efd1db7801b11259a2d812cf6764&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 670 DU CHENE VERT &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 137000 €&lt;/div&gt;`)[0];
            popup_8e72c49df6d427bde570310393e5c170.setContent(html_20c6efd1db7801b11259a2d812cf6764);
        

        marker_24b64ba5fbe0a50cddb07315f320d036.bindPopup(popup_8e72c49df6d427bde570310393e5c170)
        ;

        
    
    
            var marker_f50aa13f809115875a0ebc4b56e92b35 = L.marker(
                [48.034854, -4.659846],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_30f9ba5b7d0fb448473d3bb43b99d0a9 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_f50aa13f809115875a0ebc4b56e92b35.setIcon(icon_30f9ba5b7d0fb448473d3bb43b99d0a9);
        
    
        var popup_b77d64c57f5530e38c95be7b4511b1f8 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a6d26204a0cf5c0528e975bc84925dee = $(`&lt;div id=&quot;html_a6d26204a0cf5c0528e975bc84925dee&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERLAER &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 3500 €&lt;/div&gt;`)[0];
            popup_b77d64c57f5530e38c95be7b4511b1f8.setContent(html_a6d26204a0cf5c0528e975bc84925dee);
        

        marker_f50aa13f809115875a0ebc4b56e92b35.bindPopup(popup_b77d64c57f5530e38c95be7b4511b1f8)
        ;

        
    
    
            var marker_af0214bd3354e983de94417b013819c7 = L.marker(
                [48.035471, -4.66189],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_90346dfac01d17d9737905587e9bd3b9 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_af0214bd3354e983de94417b013819c7.setIcon(icon_90346dfac01d17d9737905587e9bd3b9);
        
    
        var popup_644050ae42871f00bab5d8d4573656ea = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_72663d7bbad612e1c6e34146109e6a5e = $(`&lt;div id=&quot;html_72663d7bbad612e1c6e34146109e6a5e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  CROAS AVEL &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 90000 €&lt;/div&gt;`)[0];
            popup_644050ae42871f00bab5d8d4573656ea.setContent(html_72663d7bbad612e1c6e34146109e6a5e);
        

        marker_af0214bd3354e983de94417b013819c7.bindPopup(popup_644050ae42871f00bab5d8d4573656ea)
        ;

        
    
    
            var marker_c69e1ef02b5ce1fe99b809a380f3b8cc = L.marker(
                [48.035471, -4.66189],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_e92629a86173cc48f1e5f943c6895e05 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_c69e1ef02b5ce1fe99b809a380f3b8cc.setIcon(icon_e92629a86173cc48f1e5f943c6895e05);
        
    
        var popup_966ff4549981c7db77a66ece0e109a49 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_62c027b845aa8440b46aa746689c53f6 = $(`&lt;div id=&quot;html_62c027b845aa8440b46aa746689c53f6&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  CROAS AVEL &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 115000 €&lt;/div&gt;`)[0];
            popup_966ff4549981c7db77a66ece0e109a49.setContent(html_62c027b845aa8440b46aa746689c53f6);
        

        marker_c69e1ef02b5ce1fe99b809a380f3b8cc.bindPopup(popup_966ff4549981c7db77a66ece0e109a49)
        ;

        
    
    
            var marker_1a26a782ff229007b1821b0a82ad47ed = L.marker(
                [48.035608, -4.662291],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_3a54a99ee63335dd1b59616cc06fd14b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_1a26a782ff229007b1821b0a82ad47ed.setIcon(icon_3a54a99ee63335dd1b59616cc06fd14b);
        
    
        var popup_3238e2599abe35a1e9667497766d95a7 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2147baada6f6adab79843a6d9f63abee = $(`&lt;div id=&quot;html_2147baada6f6adab79843a6d9f63abee&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  CROAS AVEL &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 90000 €&lt;/div&gt;`)[0];
            popup_3238e2599abe35a1e9667497766d95a7.setContent(html_2147baada6f6adab79843a6d9f63abee);
        

        marker_1a26a782ff229007b1821b0a82ad47ed.bindPopup(popup_3238e2599abe35a1e9667497766d95a7)
        ;

        
    
    
            var marker_daa899468eb341cf3ba21a96ca4e9105 = L.marker(
                [48.035608, -4.662291],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d02e39c8cdc7a6b7992082582d81482e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_daa899468eb341cf3ba21a96ca4e9105.setIcon(icon_d02e39c8cdc7a6b7992082582d81482e);
        
    
        var popup_e818bbcd7ada9b699b2d84ebe0d34ca5 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_6a753b0690732704af8aa85daee104d7 = $(`&lt;div id=&quot;html_6a753b0690732704af8aa85daee104d7&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  CROAS AVEL &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 115000 €&lt;/div&gt;`)[0];
            popup_e818bbcd7ada9b699b2d84ebe0d34ca5.setContent(html_6a753b0690732704af8aa85daee104d7);
        

        marker_daa899468eb341cf3ba21a96ca4e9105.bindPopup(popup_e818bbcd7ada9b699b2d84ebe0d34ca5)
        ;

        
    
    
            var marker_3ebc83008f99ed53e941db578a10f2f5 = L.marker(
                [48.035755, -4.662397],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_7fc2b56b7871df849bba3cb97eea5b7f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_3ebc83008f99ed53e941db578a10f2f5.setIcon(icon_7fc2b56b7871df849bba3cb97eea5b7f);
        
    
        var popup_b9ad95820f1ca6fd7f8456c8ebe2e42b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_15b197147d8c8d536a3c7f594dfd162c = $(`&lt;div id=&quot;html_15b197147d8c8d536a3c7f594dfd162c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 667 PIERRE BROSSOLETTE &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 90000 €&lt;/div&gt;`)[0];
            popup_b9ad95820f1ca6fd7f8456c8ebe2e42b.setContent(html_15b197147d8c8d536a3c7f594dfd162c);
        

        marker_3ebc83008f99ed53e941db578a10f2f5.bindPopup(popup_b9ad95820f1ca6fd7f8456c8ebe2e42b)
        ;

        
    
    
            var marker_311a31bf0dd4cc7f90ce5e99eeb358a0 = L.marker(
                [48.035755, -4.662397],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_bf822d738b2cec335c1209fc1540ab69 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_311a31bf0dd4cc7f90ce5e99eeb358a0.setIcon(icon_bf822d738b2cec335c1209fc1540ab69);
        
    
        var popup_89f3a2900d7433a1f78f3439bb597314 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9f999f521365290739479d46cc1bb642 = $(`&lt;div id=&quot;html_9f999f521365290739479d46cc1bb642&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 667 PIERRE BROSSOLETTE &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 115000 €&lt;/div&gt;`)[0];
            popup_89f3a2900d7433a1f78f3439bb597314.setContent(html_9f999f521365290739479d46cc1bb642);
        

        marker_311a31bf0dd4cc7f90ce5e99eeb358a0.bindPopup(popup_89f3a2900d7433a1f78f3439bb597314)
        ;

        
    
    
            var marker_c395ac1c69b84c4c9e31b80560bf331b = L.marker(
                [48.035054, -4.664085],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_5f3447c6c24e5c14b15714dd216de2b0 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_c395ac1c69b84c4c9e31b80560bf331b.setIcon(icon_5f3447c6c24e5c14b15714dd216de2b0);
        
    
        var popup_2ba9e2c325fa8f65c9c3aa684d640f2e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_f35cf24885bf92421eb653c5ed407c76 = $(`&lt;div id=&quot;html_f35cf24885bf92421eb653c5ed407c76&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 547 DU STADE &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 80000 €&lt;/div&gt;`)[0];
            popup_2ba9e2c325fa8f65c9c3aa684d640f2e.setContent(html_f35cf24885bf92421eb653c5ed407c76);
        

        marker_c395ac1c69b84c4c9e31b80560bf331b.bindPopup(popup_2ba9e2c325fa8f65c9c3aa684d640f2e)
        ;

        
    
    
            var marker_4642efdef2ade301e529616661e394c8 = L.marker(
                [48.035054, -4.664085],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_a18bd073b2874071bbb503638becd7f3 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_4642efdef2ade301e529616661e394c8.setIcon(icon_a18bd073b2874071bbb503638becd7f3);
        
    
        var popup_b4992648a146d4e186a6bbb042c8b166 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_81ff0bca487ddfd40033281e59e4df32 = $(`&lt;div id=&quot;html_81ff0bca487ddfd40033281e59e4df32&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 547 DU STADE &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 80000 €&lt;/div&gt;`)[0];
            popup_b4992648a146d4e186a6bbb042c8b166.setContent(html_81ff0bca487ddfd40033281e59e4df32);
        

        marker_4642efdef2ade301e529616661e394c8.bindPopup(popup_b4992648a146d4e186a6bbb042c8b166)
        ;

        
    
    
            var marker_d037338d4e94bf05513763251de0de5c = L.marker(
                [48.034369, -4.663451],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_749cdf49146b8f7461664a424b981adc = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_d037338d4e94bf05513763251de0de5c.setIcon(icon_749cdf49146b8f7461664a424b981adc);
        
    
        var popup_0684100499c7260e8bedd10f7e7be9fc = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_15f3d91877bc48c5c999b22f9f1ecaa6 = $(`&lt;div id=&quot;html_15f3d91877bc48c5c999b22f9f1ecaa6&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 553 DU STADE &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 70000 €&lt;/div&gt;`)[0];
            popup_0684100499c7260e8bedd10f7e7be9fc.setContent(html_15f3d91877bc48c5c999b22f9f1ecaa6);
        

        marker_d037338d4e94bf05513763251de0de5c.bindPopup(popup_0684100499c7260e8bedd10f7e7be9fc)
        ;

        
    
    
            var marker_9b6d8efe8447fc0d0c866b8e0cd781c6 = L.marker(
                [48.035872, -4.665043],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_11a8ea0fca987f3700bc97a670eeb035 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_9b6d8efe8447fc0d0c866b8e0cd781c6.setIcon(icon_11a8ea0fca987f3700bc97a670eeb035);
        
    
        var popup_597cdc6082be8534d89f3b2c6e25e0a6 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_37498037db7b7f111bedec51c2a6b733 = $(`&lt;div id=&quot;html_37498037db7b7f111bedec51c2a6b733&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 539 DU STADE &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 180000 €&lt;/div&gt;`)[0];
            popup_597cdc6082be8534d89f3b2c6e25e0a6.setContent(html_37498037db7b7f111bedec51c2a6b733);
        

        marker_9b6d8efe8447fc0d0c866b8e0cd781c6.bindPopup(popup_597cdc6082be8534d89f3b2c6e25e0a6)
        ;

        
    
    
            var marker_48ee1d6202790bf2ddf996cc5d7e63de = L.marker(
                [48.035915, -4.665145],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_7059129ae68ad017dea32d87fdacc713 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_48ee1d6202790bf2ddf996cc5d7e63de.setIcon(icon_7059129ae68ad017dea32d87fdacc713);
        
    
        var popup_8ad98d5a8283243df9a7dac4627a30c1 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_b01a4c791b81ef568da7618d3b3ffaca = $(`&lt;div id=&quot;html_b01a4c791b81ef568da7618d3b3ffaca&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 366 LESTRIVIN &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 158000 €&lt;/div&gt;`)[0];
            popup_8ad98d5a8283243df9a7dac4627a30c1.setContent(html_b01a4c791b81ef568da7618d3b3ffaca);
        

        marker_48ee1d6202790bf2ddf996cc5d7e63de.bindPopup(popup_8ad98d5a8283243df9a7dac4627a30c1)
        ;

        
    
    
            var marker_5b1e98e4b4196ed3e8c9a105bbb7eddc = L.marker(
                [48.035314, -4.661167],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_84157a7604154b80d8f38e05de644634 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_5b1e98e4b4196ed3e8c9a105bbb7eddc.setIcon(icon_84157a7604154b80d8f38e05de644634);
        
    
        var popup_eaebf321dc7d24ba9fac697221927870 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_fe98ba17198e166ee9953ed47796fcd9 = $(`&lt;div id=&quot;html_fe98ba17198e166ee9953ed47796fcd9&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  CROAS AVEL &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 18000 €&lt;/div&gt;`)[0];
            popup_eaebf321dc7d24ba9fac697221927870.setContent(html_fe98ba17198e166ee9953ed47796fcd9);
        

        marker_5b1e98e4b4196ed3e8c9a105bbb7eddc.bindPopup(popup_eaebf321dc7d24ba9fac697221927870)
        ;

        
    
    
            var marker_6ce54061846943c7915108a9c7792e98 = L.marker(
                [48.036232, -4.662645],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_e2dbb9a419c40657d78244f8272fbb89 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_6ce54061846943c7915108a9c7792e98.setIcon(icon_e2dbb9a419c40657d78244f8272fbb89);
        
    
        var popup_713b2f3d69d6f983db21b81663a52d42 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e4bba0dfdf0a43f0551e3de6a395bbdb = $(`&lt;div id=&quot;html_e4bba0dfdf0a43f0551e3de6a395bbdb&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5180 PIERRE BROSSOLETTE &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 215000 €&lt;/div&gt;`)[0];
            popup_713b2f3d69d6f983db21b81663a52d42.setContent(html_e4bba0dfdf0a43f0551e3de6a395bbdb);
        

        marker_6ce54061846943c7915108a9c7792e98.bindPopup(popup_713b2f3d69d6f983db21b81663a52d42)
        ;

        
    
    
            var marker_8caf280e37e27c4cbcf13b870ef4ba1b = L.marker(
                [48.036232, -4.662645],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_5282e30e7f0b1f1692b6cbcb71c546ea = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_8caf280e37e27c4cbcf13b870ef4ba1b.setIcon(icon_5282e30e7f0b1f1692b6cbcb71c546ea);
        
    
        var popup_faf84415eff90473c18f53fc667f1318 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_dddd2eb862cdd05b1f84a9725a64dc77 = $(`&lt;div id=&quot;html_dddd2eb862cdd05b1f84a9725a64dc77&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5180 PIERRE BROSSOLETTE &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 215000 €&lt;/div&gt;`)[0];
            popup_faf84415eff90473c18f53fc667f1318.setContent(html_dddd2eb862cdd05b1f84a9725a64dc77);
        

        marker_8caf280e37e27c4cbcf13b870ef4ba1b.bindPopup(popup_faf84415eff90473c18f53fc667f1318)
        ;

        
    
    
            var marker_9e7b4e7f590d4c7e39d523506a785c4e = L.marker(
                [48.035181, -4.663474],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_576122fc962baa37affac860ffc59ec5 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_9e7b4e7f590d4c7e39d523506a785c4e.setIcon(icon_576122fc962baa37affac860ffc59ec5);
        
    
        var popup_d6596a42a206d77e0c0f22eda3d92726 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_453256b1bb77540045dfcec8bb108185 = $(`&lt;div id=&quot;html_453256b1bb77540045dfcec8bb108185&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESTRIVIN &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 80000 €&lt;/div&gt;`)[0];
            popup_d6596a42a206d77e0c0f22eda3d92726.setContent(html_453256b1bb77540045dfcec8bb108185);
        

        marker_9e7b4e7f590d4c7e39d523506a785c4e.bindPopup(popup_d6596a42a206d77e0c0f22eda3d92726)
        ;

        
    
    
            var marker_67c229746b6d20f7121c1061aef9a3c2 = L.marker(
                [48.036215, -4.662535],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d2899dcf0668d71e266727913b781e45 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_67c229746b6d20f7121c1061aef9a3c2.setIcon(icon_d2899dcf0668d71e266727913b781e45);
        
    
        var popup_3da2de0a96020840de3cc81df91dfb73 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d08d2d104093ce7992da7adefb771e51 = $(`&lt;div id=&quot;html_d08d2d104093ce7992da7adefb771e51&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  CROAS AVEL &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 215000 €&lt;/div&gt;`)[0];
            popup_3da2de0a96020840de3cc81df91dfb73.setContent(html_d08d2d104093ce7992da7adefb771e51);
        

        marker_67c229746b6d20f7121c1061aef9a3c2.bindPopup(popup_3da2de0a96020840de3cc81df91dfb73)
        ;

        
    
    
            var marker_44c02af6433f5f0b0a86087d6462f2ab = L.marker(
                [48.0343, -4.663426],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_2a03ac9b958d0416ade662c1939975cf = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_44c02af6433f5f0b0a86087d6462f2ab.setIcon(icon_2a03ac9b958d0416ade662c1939975cf);
        
    
        var popup_97a4add39d82df09e4051957e24398b8 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_6b5e556e0f896ea8ebe7c2944161b1d7 = $(`&lt;div id=&quot;html_6b5e556e0f896ea8ebe7c2944161b1d7&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  CROAS AVEL &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 70000 €&lt;/div&gt;`)[0];
            popup_97a4add39d82df09e4051957e24398b8.setContent(html_6b5e556e0f896ea8ebe7c2944161b1d7);
        

        marker_44c02af6433f5f0b0a86087d6462f2ab.bindPopup(popup_97a4add39d82df09e4051957e24398b8)
        ;

        
    
    
            var marker_63ef39d06de5e5faeaf151e58e4fe183 = L.marker(
                [48.036046, -4.662337],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_2af49e3d24fc4edc55bf1f6912b37acb = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_63ef39d06de5e5faeaf151e58e4fe183.setIcon(icon_2af49e3d24fc4edc55bf1f6912b37acb);
        
    
        var popup_4aad97ed25872c81f647903f5649b98c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_3cdc404634eb75fa460a1fe53fa0b65d = $(`&lt;div id=&quot;html_3cdc404634eb75fa460a1fe53fa0b65d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5195 PIERRE BROSSOLETTE &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 90000 €&lt;/div&gt;`)[0];
            popup_4aad97ed25872c81f647903f5649b98c.setContent(html_3cdc404634eb75fa460a1fe53fa0b65d);
        

        marker_63ef39d06de5e5faeaf151e58e4fe183.bindPopup(popup_4aad97ed25872c81f647903f5649b98c)
        ;

        
    
    
            var marker_cae313defd29ce476bd476a89e7df346 = L.marker(
                [48.036173, -4.662448],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_fd263344e396a40041a44c03e3ec1841 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_cae313defd29ce476bd476a89e7df346.setIcon(icon_fd263344e396a40041a44c03e3ec1841);
        
    
        var popup_6b7fca31388a31b610f96d16069cfc58 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9d496d5f3e0d9322e5c8332fbe42c35a = $(`&lt;div id=&quot;html_9d496d5f3e0d9322e5c8332fbe42c35a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  CROAS AVEL &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 215000 €&lt;/div&gt;`)[0];
            popup_6b7fca31388a31b610f96d16069cfc58.setContent(html_9d496d5f3e0d9322e5c8332fbe42c35a);
        

        marker_cae313defd29ce476bd476a89e7df346.bindPopup(popup_6b7fca31388a31b610f96d16069cfc58)
        ;

        
    
    
            var marker_c92970c541cba605127e571f0ba91a26 = L.marker(
                [48.035448, -4.661123],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_2f138687071e0663997b1d3ef88f44f0 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_c92970c541cba605127e571f0ba91a26.setIcon(icon_2f138687071e0663997b1d3ef88f44f0);
        
    
        var popup_d56504de038105bd8a2dfab79fa362c0 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_724e80a464de8c54ba6fe74a04db890e = $(`&lt;div id=&quot;html_724e80a464de8c54ba6fe74a04db890e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  CROAS AVEL &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 6109 €&lt;/div&gt;`)[0];
            popup_d56504de038105bd8a2dfab79fa362c0.setContent(html_724e80a464de8c54ba6fe74a04db890e);
        

        marker_c92970c541cba605127e571f0ba91a26.bindPopup(popup_d56504de038105bd8a2dfab79fa362c0)
        ;

        
    
    
            var marker_56c630c91df8be180178f016ad90a822 = L.marker(
                [48.035284, -4.661045],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_14af7f70cf88845a8feeb68be66cae0d = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_56c630c91df8be180178f016ad90a822.setIcon(icon_14af7f70cf88845a8feeb68be66cae0d);
        
    
        var popup_8e5a4a2dbd3f95c932cba67f39994056 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_702a1d3cc46d0276bb2ead6909806554 = $(`&lt;div id=&quot;html_702a1d3cc46d0276bb2ead6909806554&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  CROAS AVEL &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 6109 €&lt;/div&gt;`)[0];
            popup_8e5a4a2dbd3f95c932cba67f39994056.setContent(html_702a1d3cc46d0276bb2ead6909806554);
        

        marker_56c630c91df8be180178f016ad90a822.bindPopup(popup_8e5a4a2dbd3f95c932cba67f39994056)
        ;

        
    
    
            var marker_5fa748cf53ffe99383839cd166b996d4 = L.marker(
                [48.039444, -4.65788],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_70be2a112a2b95577eea1501d56ac109 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_5fa748cf53ffe99383839cd166b996d4.setIcon(icon_70be2a112a2b95577eea1501d56ac109);
        
    
        var popup_cd09748cd6b5ca0aa452c6ba558b6dc8 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_069af278194c60983e921b187dfc4461 = $(`&lt;div id=&quot;html_069af278194c60983e921b187dfc4461&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PONT QUILLIOC &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 30500 €&lt;/div&gt;`)[0];
            popup_cd09748cd6b5ca0aa452c6ba558b6dc8.setContent(html_069af278194c60983e921b187dfc4461);
        

        marker_5fa748cf53ffe99383839cd166b996d4.bindPopup(popup_cd09748cd6b5ca0aa452c6ba558b6dc8)
        ;

        
    
    
            var marker_721f6ae603a9aa1518feb1c52d2b5913 = L.marker(
                [48.039855, -4.656933],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_7f95906d6c1235dd0be7f387a4a26419 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_721f6ae603a9aa1518feb1c52d2b5913.setIcon(icon_7f95906d6c1235dd0be7f387a4a26419);
        
    
        var popup_c7f8143ebb3547c738df50eb136c2a3f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7b7471307ed2ec30e2ad0eb246772eea = $(`&lt;div id=&quot;html_7b7471307ed2ec30e2ad0eb246772eea&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PONT QUILLIOC &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 30500 €&lt;/div&gt;`)[0];
            popup_c7f8143ebb3547c738df50eb136c2a3f.setContent(html_7b7471307ed2ec30e2ad0eb246772eea);
        

        marker_721f6ae603a9aa1518feb1c52d2b5913.bindPopup(popup_c7f8143ebb3547c738df50eb136c2a3f)
        ;

        
    
    
            var marker_492edc21d061fef8d57961a30213f412 = L.marker(
                [48.040807, -4.655411],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_97532728d3a50dffd01e03065448639e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_492edc21d061fef8d57961a30213f412.setIcon(icon_97532728d3a50dffd01e03065448639e);
        
    
        var popup_e88384788b01b95e24258b0b7ce4251b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c1da5622d9e84f30d2a7f6861c4e66bc = $(`&lt;div id=&quot;html_c1da5622d9e84f30d2a7f6861c4e66bc&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PONT QUILLIOC &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 30500 €&lt;/div&gt;`)[0];
            popup_e88384788b01b95e24258b0b7ce4251b.setContent(html_c1da5622d9e84f30d2a7f6861c4e66bc);
        

        marker_492edc21d061fef8d57961a30213f412.bindPopup(popup_e88384788b01b95e24258b0b7ce4251b)
        ;

        
    
    
            var marker_4e76ede598a6a2d1ccbf276f9d648b98 = L.marker(
                [48.040194, -4.655155],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_5bacd56b804590a1a942080aa14e3729 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_4e76ede598a6a2d1ccbf276f9d648b98.setIcon(icon_5bacd56b804590a1a942080aa14e3729);
        
    
        var popup_f8b90c5ec7c33e62f885a784a5df5ca5 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2db73964d57fb6bd5f39fb383519059e = $(`&lt;div id=&quot;html_2db73964d57fb6bd5f39fb383519059e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PONT QUILLIOC &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 30500 €&lt;/div&gt;`)[0];
            popup_f8b90c5ec7c33e62f885a784a5df5ca5.setContent(html_2db73964d57fb6bd5f39fb383519059e);
        

        marker_4e76ede598a6a2d1ccbf276f9d648b98.bindPopup(popup_f8b90c5ec7c33e62f885a784a5df5ca5)
        ;

        
    
    
            var marker_637871803ed0e079f1de2bc1f3a30102 = L.marker(
                [48.038705, -4.656586],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_91e02b909cd9fe15eb711496dd9fa937 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_637871803ed0e079f1de2bc1f3a30102.setIcon(icon_91e02b909cd9fe15eb711496dd9fa937);
        
    
        var popup_ae76115be866f0422f1c62a5eb78b0aa = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_697839bdc580bbfbae3dca4dc8cbfbca = $(`&lt;div id=&quot;html_697839bdc580bbfbae3dca4dc8cbfbca&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PONT QUILLIOC &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 30500 €&lt;/div&gt;`)[0];
            popup_ae76115be866f0422f1c62a5eb78b0aa.setContent(html_697839bdc580bbfbae3dca4dc8cbfbca);
        

        marker_637871803ed0e079f1de2bc1f3a30102.bindPopup(popup_ae76115be866f0422f1c62a5eb78b0aa)
        ;

        
    
    
            var marker_6fa27214cd24d9ad2a61c31fd4c10bea = L.marker(
                [48.038894, -4.657775],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_805dc211c8d043dc8f9de8be5638454a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_6fa27214cd24d9ad2a61c31fd4c10bea.setIcon(icon_805dc211c8d043dc8f9de8be5638454a);
        
    
        var popup_c651f56fcaf9d306b52846064546fc8e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_3cd6f0650c0c7888cf8eae0cef568f70 = $(`&lt;div id=&quot;html_3cd6f0650c0c7888cf8eae0cef568f70&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PONT QUILLIOC &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 30500 €&lt;/div&gt;`)[0];
            popup_c651f56fcaf9d306b52846064546fc8e.setContent(html_3cd6f0650c0c7888cf8eae0cef568f70);
        

        marker_6fa27214cd24d9ad2a61c31fd4c10bea.bindPopup(popup_c651f56fcaf9d306b52846064546fc8e)
        ;

        
    
    
            var marker_b9a92123684e59b37be10b820d7e89e0 = L.marker(
                [48.040666, -4.657822],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d97c22bdee15cf94db7dc835b7761729 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_b9a92123684e59b37be10b820d7e89e0.setIcon(icon_d97c22bdee15cf94db7dc835b7761729);
        
    
        var popup_cd8ebe0e847f8975fde74c9f4c8f74a9 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_426ff814e2a7ce8544d685258a5d07a8 = $(`&lt;div id=&quot;html_426ff814e2a7ce8544d685258a5d07a8&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PONT QUILLIOC &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 30500 €&lt;/div&gt;`)[0];
            popup_cd8ebe0e847f8975fde74c9f4c8f74a9.setContent(html_426ff814e2a7ce8544d685258a5d07a8);
        

        marker_b9a92123684e59b37be10b820d7e89e0.bindPopup(popup_cd8ebe0e847f8975fde74c9f4c8f74a9)
        ;

        
    
    
            var marker_ce3942cfdb3b4efff2e3b9bc6cf1a17d = L.marker(
                [48.041186, -4.658173],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_6cfe38ffe3b02f78513b872f739f5668 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ce3942cfdb3b4efff2e3b9bc6cf1a17d.setIcon(icon_6cfe38ffe3b02f78513b872f739f5668);
        
    
        var popup_bf1b3985957318ce1793f59ab443bbe4 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_31d8d3a0bf73ea01cdbdd70fd849bfed = $(`&lt;div id=&quot;html_31d8d3a0bf73ea01cdbdd70fd849bfed&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PONT QUILLIOC &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 30500 €&lt;/div&gt;`)[0];
            popup_bf1b3985957318ce1793f59ab443bbe4.setContent(html_31d8d3a0bf73ea01cdbdd70fd849bfed);
        

        marker_ce3942cfdb3b4efff2e3b9bc6cf1a17d.bindPopup(popup_bf1b3985957318ce1793f59ab443bbe4)
        ;

        
    
    
            var marker_32e7c4f981f91cc902668adccdeef9c7 = L.marker(
                [48.040056, -4.661341],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_a9c230205cc03047a2554d7a21d117c7 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_32e7c4f981f91cc902668adccdeef9c7.setIcon(icon_a9c230205cc03047a2554d7a21d117c7);
        
    
        var popup_088976c2729ba0a387f24ad7c6fc367a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_add9fecd9fbbd1e9194c1c59b2bce8ca = $(`&lt;div id=&quot;html_add9fecd9fbbd1e9194c1c59b2bce8ca&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  TY RHU &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 1500 €&lt;/div&gt;`)[0];
            popup_088976c2729ba0a387f24ad7c6fc367a.setContent(html_add9fecd9fbbd1e9194c1c59b2bce8ca);
        

        marker_32e7c4f981f91cc902668adccdeef9c7.bindPopup(popup_088976c2729ba0a387f24ad7c6fc367a)
        ;

        
    
    
            var marker_b0ce7c704fd9ddadb376b1069db0fc1f = L.marker(
                [48.039981, -4.661334],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_789e2fe27c62de9da0fd8213e2c0ef97 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_b0ce7c704fd9ddadb376b1069db0fc1f.setIcon(icon_789e2fe27c62de9da0fd8213e2c0ef97);
        
    
        var popup_35fdabd01f9b1e35c315b7fd295c94c3 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ec9af7953258aebb7c18aa454085baa8 = $(`&lt;div id=&quot;html_ec9af7953258aebb7c18aa454085baa8&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  TY RHU &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 1500 €&lt;/div&gt;`)[0];
            popup_35fdabd01f9b1e35c315b7fd295c94c3.setContent(html_ec9af7953258aebb7c18aa454085baa8);
        

        marker_b0ce7c704fd9ddadb376b1069db0fc1f.bindPopup(popup_35fdabd01f9b1e35c315b7fd295c94c3)
        ;

        
    
    
            var marker_c88d86a4331684291c42ac099a5a94e5 = L.marker(
                [48.035011, -4.652971],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_5aac4ed1e1ad982eb415f65ac8c2b2a8 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_c88d86a4331684291c42ac099a5a94e5.setIcon(icon_5aac4ed1e1ad982eb415f65ac8c2b2a8);
        
    
        var popup_d781f13a44c0627ebbf30068e836e899 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2f39614c23c8843a01af5a9931ff8d4e = $(`&lt;div id=&quot;html_2f39614c23c8843a01af5a9931ff8d4e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 689 KERSTRAT &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 130000 €&lt;/div&gt;`)[0];
            popup_d781f13a44c0627ebbf30068e836e899.setContent(html_2f39614c23c8843a01af5a9931ff8d4e);
        

        marker_c88d86a4331684291c42ac099a5a94e5.bindPopup(popup_d781f13a44c0627ebbf30068e836e899)
        ;

        
    
    
            var marker_307254cda5ba5441b5b6c55d8fb852fc = L.marker(
                [48.034606, -4.648016],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_6e0f2aa3effb92b76908f6a81680da3c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_307254cda5ba5441b5b6c55d8fb852fc.setIcon(icon_6e0f2aa3effb92b76908f6a81680da3c);
        
    
        var popup_d533c3bce883f0774c16a85d3bef8519 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9cdd3ae38b460d74b3cccab9a373bdc3 = $(`&lt;div id=&quot;html_9cdd3ae38b460d74b3cccab9a373bdc3&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 719 CLUCAREC &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 105000 €&lt;/div&gt;`)[0];
            popup_d533c3bce883f0774c16a85d3bef8519.setContent(html_9cdd3ae38b460d74b3cccab9a373bdc3);
        

        marker_307254cda5ba5441b5b6c55d8fb852fc.bindPopup(popup_d533c3bce883f0774c16a85d3bef8519)
        ;

        
    
    
            var marker_29134a0200d033a44cd316d1f9abc5d8 = L.marker(
                [48.034506, -4.647731],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_58844e91959bee529a113c174778cfa9 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_29134a0200d033a44cd316d1f9abc5d8.setIcon(icon_58844e91959bee529a113c174778cfa9);
        
    
        var popup_09ae870d5b37ae405367c3210ddb6209 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ae758aabe43f8ec35dde1607389cc6c8 = $(`&lt;div id=&quot;html_ae758aabe43f8ec35dde1607389cc6c8&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  CLUCAREC &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 60000 €&lt;/div&gt;`)[0];
            popup_09ae870d5b37ae405367c3210ddb6209.setContent(html_ae758aabe43f8ec35dde1607389cc6c8);
        

        marker_29134a0200d033a44cd316d1f9abc5d8.bindPopup(popup_09ae870d5b37ae405367c3210ddb6209)
        ;

        
    
    
            var marker_81ea5c80e1d150e5f7fd0092fcd6605f = L.marker(
                [48.03418, -4.646578],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_2912bc4d80b7a1dd2700e6c4eb945222 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_81ea5c80e1d150e5f7fd0092fcd6605f.setIcon(icon_2912bc4d80b7a1dd2700e6c4eb945222);
        
    
        var popup_a9a582838565d9e8486d03180098d908 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_5631a6ff8069fc68a9cc721c1699ac85 = $(`&lt;div id=&quot;html_5631a6ff8069fc68a9cc721c1699ac85&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 720 CLUCAREC &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 120000 €&lt;/div&gt;`)[0];
            popup_a9a582838565d9e8486d03180098d908.setContent(html_5631a6ff8069fc68a9cc721c1699ac85);
        

        marker_81ea5c80e1d150e5f7fd0092fcd6605f.bindPopup(popup_a9a582838565d9e8486d03180098d908)
        ;

        
    
    
            var marker_790f7644b9a028dd539f8a59143f3731 = L.marker(
                [48.03418, -4.646578],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_b8181fc9b6ab36bcfc293f957152be4a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_790f7644b9a028dd539f8a59143f3731.setIcon(icon_b8181fc9b6ab36bcfc293f957152be4a);
        
    
        var popup_2720f716ecca19b592916238c9f5b560 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_5ffa9024116847cd892be1bc1617e909 = $(`&lt;div id=&quot;html_5ffa9024116847cd892be1bc1617e909&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 720 CLUCAREC &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 120000 €&lt;/div&gt;`)[0];
            popup_2720f716ecca19b592916238c9f5b560.setContent(html_5ffa9024116847cd892be1bc1617e909);
        

        marker_790f7644b9a028dd539f8a59143f3731.bindPopup(popup_2720f716ecca19b592916238c9f5b560)
        ;

        
    
    
            var marker_4ec6752fd8edb9735a82e74aec3360ed = L.marker(
                [48.034233, -4.646737],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_e1576d051d99f3cce7cb4e3e16eae17c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_4ec6752fd8edb9735a82e74aec3360ed.setIcon(icon_e1576d051d99f3cce7cb4e3e16eae17c);
        
    
        var popup_38cd460a5896f922e36ebdc03e166b0e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_462a8567340ba8e3eecd7545fdedb56b = $(`&lt;div id=&quot;html_462a8567340ba8e3eecd7545fdedb56b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  CLUCAREC &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 120000 €&lt;/div&gt;`)[0];
            popup_38cd460a5896f922e36ebdc03e166b0e.setContent(html_462a8567340ba8e3eecd7545fdedb56b);
        

        marker_4ec6752fd8edb9735a82e74aec3360ed.bindPopup(popup_38cd460a5896f922e36ebdc03e166b0e)
        ;

        
    
    
            var marker_eae2a0932d84c558b35898b696a7faa9 = L.marker(
                [48.034233, -4.646737],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_bccd1f8da0ff0c5ae3a11f09c8f27f70 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_eae2a0932d84c558b35898b696a7faa9.setIcon(icon_bccd1f8da0ff0c5ae3a11f09c8f27f70);
        
    
        var popup_f12104c1a8bf84e6b2c264c9838ab793 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e9ab055d299e21d250fd51323ce8b7b2 = $(`&lt;div id=&quot;html_e9ab055d299e21d250fd51323ce8b7b2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  CLUCAREC &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 120000 €&lt;/div&gt;`)[0];
            popup_f12104c1a8bf84e6b2c264c9838ab793.setContent(html_e9ab055d299e21d250fd51323ce8b7b2);
        

        marker_eae2a0932d84c558b35898b696a7faa9.bindPopup(popup_f12104c1a8bf84e6b2c264c9838ab793)
        ;

        
    
    
            var marker_8d67c977cd08bb03a8ee3ad25f07cb17 = L.marker(
                [48.033976, -4.64739],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_8e134509c3f6ef1c51e7e1ca5397667c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_8d67c977cd08bb03a8ee3ad25f07cb17.setIcon(icon_8e134509c3f6ef1c51e7e1ca5397667c);
        
    
        var popup_1eed806238ad9f05e11681fd15898d1a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_de801a31dcc567e8346d2a4009cd830b = $(`&lt;div id=&quot;html_de801a31dcc567e8346d2a4009cd830b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  CLUCAREC &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 60000 €&lt;/div&gt;`)[0];
            popup_1eed806238ad9f05e11681fd15898d1a.setContent(html_de801a31dcc567e8346d2a4009cd830b);
        

        marker_8d67c977cd08bb03a8ee3ad25f07cb17.bindPopup(popup_1eed806238ad9f05e11681fd15898d1a)
        ;

        
    
    
            var marker_4bef8da08d76f1e78c0ecb3308458bdb = L.marker(
                [48.03423, -4.647783],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_63bcd5414ea46436193a470044c966f6 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_4bef8da08d76f1e78c0ecb3308458bdb.setIcon(icon_63bcd5414ea46436193a470044c966f6);
        
    
        var popup_10fb01a3e68711142ca7b81a511a0695 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8961515a05138215f17777db10fb963f = $(`&lt;div id=&quot;html_8961515a05138215f17777db10fb963f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 728 CLUCAREC &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 60000 €&lt;/div&gt;`)[0];
            popup_10fb01a3e68711142ca7b81a511a0695.setContent(html_8961515a05138215f17777db10fb963f);
        

        marker_4bef8da08d76f1e78c0ecb3308458bdb.bindPopup(popup_10fb01a3e68711142ca7b81a511a0695)
        ;

        
    
    
            var marker_a83c6b7af7f86cf9666c96a12137c216 = L.marker(
                [48.033912, -4.647668],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_4365a3807468faa437e42a8642d51f81 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_a83c6b7af7f86cf9666c96a12137c216.setIcon(icon_4365a3807468faa437e42a8642d51f81);
        
    
        var popup_81d61ae572307014591e082d42e4362a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_0897e3b60eda318db4c5d042b0910b49 = $(`&lt;div id=&quot;html_0897e3b60eda318db4c5d042b0910b49&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  CLUCAREC &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 60000 €&lt;/div&gt;`)[0];
            popup_81d61ae572307014591e082d42e4362a.setContent(html_0897e3b60eda318db4c5d042b0910b49);
        

        marker_a83c6b7af7f86cf9666c96a12137c216.bindPopup(popup_81d61ae572307014591e082d42e4362a)
        ;

        
    
    
            var marker_78042705a15b3bf1f97271aa5965d0f1 = L.marker(
                [48.033771, -4.647744],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_408c4a69b4599aaeb60aa36d8447ea44 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_78042705a15b3bf1f97271aa5965d0f1.setIcon(icon_408c4a69b4599aaeb60aa36d8447ea44);
        
    
        var popup_89a5fff35eb791535e8f0cd48d87816d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_0864dda6717e72984aeaef8cb17624c7 = $(`&lt;div id=&quot;html_0864dda6717e72984aeaef8cb17624c7&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  CLUCAREC &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 60000 €&lt;/div&gt;`)[0];
            popup_89a5fff35eb791535e8f0cd48d87816d.setContent(html_0864dda6717e72984aeaef8cb17624c7);
        

        marker_78042705a15b3bf1f97271aa5965d0f1.bindPopup(popup_89a5fff35eb791535e8f0cd48d87816d)
        ;

        
    
    
            var marker_84fe04dba512062368d1126751bd12c1 = L.marker(
                [48.0349, -4.653065],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_a753383abd5915fd3db8ed72cf476b39 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_84fe04dba512062368d1126751bd12c1.setIcon(icon_a753383abd5915fd3db8ed72cf476b39);
        
    
        var popup_7ceb86f2b15195b5b53b9298421afc71 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_da41e80b73eb2ef54db58d95953b5b32 = $(`&lt;div id=&quot;html_da41e80b73eb2ef54db58d95953b5b32&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERSTRAT &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 130000 €&lt;/div&gt;`)[0];
            popup_7ceb86f2b15195b5b53b9298421afc71.setContent(html_da41e80b73eb2ef54db58d95953b5b32);
        

        marker_84fe04dba512062368d1126751bd12c1.bindPopup(popup_7ceb86f2b15195b5b53b9298421afc71)
        ;

        
    
    
            var marker_d0d49887580fa38d7c5eefbea600aa4f = L.marker(
                [48.035251, -4.652811],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_516616229f0899402cac2cd3318a0d33 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_d0d49887580fa38d7c5eefbea600aa4f.setIcon(icon_516616229f0899402cac2cd3318a0d33);
        
    
        var popup_b0af29de30d173ad1d9ce5674f94a39f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_6c9dd92e3fb05a85d23c5d08f380a1fc = $(`&lt;div id=&quot;html_6c9dd92e3fb05a85d23c5d08f380a1fc&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERSTRAT &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 130000 €&lt;/div&gt;`)[0];
            popup_b0af29de30d173ad1d9ce5674f94a39f.setContent(html_6c9dd92e3fb05a85d23c5d08f380a1fc);
        

        marker_d0d49887580fa38d7c5eefbea600aa4f.bindPopup(popup_b0af29de30d173ad1d9ce5674f94a39f)
        ;

        
    
    
            var marker_1483c7d52d468bc2e65213974db10073 = L.marker(
                [48.034188, -4.641871],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_4a6c64cd727d2e50f361737104e05943 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_1483c7d52d468bc2e65213974db10073.setIcon(icon_4a6c64cd727d2e50f361737104e05943);
        
    
        var popup_8f4a9c140aec6805c2ad5092abc0c3c6 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_dc863e062d0e6d2b5e304732d4933c81 = $(`&lt;div id=&quot;html_dc863e062d0e6d2b5e304732d4933c81&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 1 SAINT ANDRE &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 150000 €&lt;/div&gt;`)[0];
            popup_8f4a9c140aec6805c2ad5092abc0c3c6.setContent(html_dc863e062d0e6d2b5e304732d4933c81);
        

        marker_1483c7d52d468bc2e65213974db10073.bindPopup(popup_8f4a9c140aec6805c2ad5092abc0c3c6)
        ;

        
    
    
            var marker_aeccf2dac4827ba86e66199157113bc8 = L.marker(
                [48.034458, -4.641992],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_2d40b0f8f6f6577978a385050eb5c35e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_aeccf2dac4827ba86e66199157113bc8.setIcon(icon_2d40b0f8f6f6577978a385050eb5c35e);
        
    
        var popup_4492a6d2028a898c7efb673dca61ae31 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1a956cdca01cf273db6c6b525807d3eb = $(`&lt;div id=&quot;html_1a956cdca01cf273db6c6b525807d3eb&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 1 SAINT ANDRE &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 150000 €&lt;/div&gt;`)[0];
            popup_4492a6d2028a898c7efb673dca61ae31.setContent(html_1a956cdca01cf273db6c6b525807d3eb);
        

        marker_aeccf2dac4827ba86e66199157113bc8.bindPopup(popup_4492a6d2028a898c7efb673dca61ae31)
        ;

        
    
    
            var marker_ec354e5c7dd6d39d2b968338090b8bd6 = L.marker(
                [48.035168, -4.64322],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_1b4a3c57478e873b1c89c3ecc3543e03 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ec354e5c7dd6d39d2b968338090b8bd6.setIcon(icon_1b4a3c57478e873b1c89c3ecc3543e03);
        
    
        var popup_97e2511ab3c56590f5028b95a3996350 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7723f364f7b67ad2fd92cdeee934b4c8 = $(`&lt;div id=&quot;html_7723f364f7b67ad2fd92cdeee934b4c8&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LANDRER &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 185000 €&lt;/div&gt;`)[0];
            popup_97e2511ab3c56590f5028b95a3996350.setContent(html_7723f364f7b67ad2fd92cdeee934b4c8);
        

        marker_ec354e5c7dd6d39d2b968338090b8bd6.bindPopup(popup_97e2511ab3c56590f5028b95a3996350)
        ;

        
    
    
            var marker_945254d26eb0028270b3e8e6cafcf765 = L.marker(
                [48.035168, -4.64322],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_c6a466d73dc0819f891f76616c07de53 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_945254d26eb0028270b3e8e6cafcf765.setIcon(icon_c6a466d73dc0819f891f76616c07de53);
        
    
        var popup_50ce6c97a064b8b510a6a7203a59e78d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_802ae8ea73ca99611231f0e9a4650ef5 = $(`&lt;div id=&quot;html_802ae8ea73ca99611231f0e9a4650ef5&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LANDRER &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 185000 €&lt;/div&gt;`)[0];
            popup_50ce6c97a064b8b510a6a7203a59e78d.setContent(html_802ae8ea73ca99611231f0e9a4650ef5);
        

        marker_945254d26eb0028270b3e8e6cafcf765.bindPopup(popup_50ce6c97a064b8b510a6a7203a59e78d)
        ;

        
    
    
            var marker_ddb36d8491db0817c110ef3a431a2638 = L.marker(
                [48.034718, -4.641516],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_b3f75cb031e65146fb3a4870a92500b1 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ddb36d8491db0817c110ef3a431a2638.setIcon(icon_b3f75cb031e65146fb3a4870a92500b1);
        
    
        var popup_fb2eb4a3f4879f59cbeacada33a1e456 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_f601b681ac26f03b16c41d294fd9d13d = $(`&lt;div id=&quot;html_f601b681ac26f03b16c41d294fd9d13d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 883 LANDRER &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 70000 €&lt;/div&gt;`)[0];
            popup_fb2eb4a3f4879f59cbeacada33a1e456.setContent(html_f601b681ac26f03b16c41d294fd9d13d);
        

        marker_ddb36d8491db0817c110ef3a431a2638.bindPopup(popup_fb2eb4a3f4879f59cbeacada33a1e456)
        ;

        
    
    
            var marker_dfba34b28806ba0a53cff73d168dfec7 = L.marker(
                [48.034035, -4.63992],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_9d47c5522d7107807f2ccc3f50318cd0 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_dfba34b28806ba0a53cff73d168dfec7.setIcon(icon_9d47c5522d7107807f2ccc3f50318cd0);
        
    
        var popup_d2cde5a5d6f53b77b20aa7a1503c2828 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_db8d8cdfa52521e1976ae27a69fad8ce = $(`&lt;div id=&quot;html_db8d8cdfa52521e1976ae27a69fad8ce&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LANDRER &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 6000 €&lt;/div&gt;`)[0];
            popup_d2cde5a5d6f53b77b20aa7a1503c2828.setContent(html_db8d8cdfa52521e1976ae27a69fad8ce);
        

        marker_dfba34b28806ba0a53cff73d168dfec7.bindPopup(popup_d2cde5a5d6f53b77b20aa7a1503c2828)
        ;

        
    
    
            var marker_a4e29369c8c39df5f62579ec58ee0915 = L.marker(
                [48.033365, -4.641745],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_b2aeef9afdaea5c7d7cdb9da76fcbbe1 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_a4e29369c8c39df5f62579ec58ee0915.setIcon(icon_b2aeef9afdaea5c7d7cdb9da76fcbbe1);
        
    
        var popup_df4e689f41f10d081a1b821de386d39a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_07cc539c014f9d697ce03052c77affed = $(`&lt;div id=&quot;html_07cc539c014f9d697ce03052c77affed&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LANDRER &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 8000 €&lt;/div&gt;`)[0];
            popup_df4e689f41f10d081a1b821de386d39a.setContent(html_07cc539c014f9d697ce03052c77affed);
        

        marker_a4e29369c8c39df5f62579ec58ee0915.bindPopup(popup_df4e689f41f10d081a1b821de386d39a)
        ;

        
    
    
            var marker_ebac931796be61c10e1bf1ae8e17dd66 = L.marker(
                [48.03465, -4.641562],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_aea0b3ab23d22226b43c06f96fe07474 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ebac931796be61c10e1bf1ae8e17dd66.setIcon(icon_aea0b3ab23d22226b43c06f96fe07474);
        
    
        var popup_3a38412f2928986ed061cc1575f9f096 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_dc76ac64b31852ccecd1c7ac762e3598 = $(`&lt;div id=&quot;html_dc76ac64b31852ccecd1c7ac762e3598&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LANDRER &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 70000 €&lt;/div&gt;`)[0];
            popup_3a38412f2928986ed061cc1575f9f096.setContent(html_dc76ac64b31852ccecd1c7ac762e3598);
        

        marker_ebac931796be61c10e1bf1ae8e17dd66.bindPopup(popup_3a38412f2928986ed061cc1575f9f096)
        ;

        
    
    
            var marker_c85739c6fb42eacdb470cb7a98bc1cdf = L.marker(
                [48.034452, -4.643022],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_8c0a02b27daa0853053f45fd6b0204f0 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_c85739c6fb42eacdb470cb7a98bc1cdf.setIcon(icon_8c0a02b27daa0853053f45fd6b0204f0);
        
    
        var popup_cfcd32dfdaab584ddf756ee39d99245d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d1c1a46cbf5d860b6f8c2b732bedc82b = $(`&lt;div id=&quot;html_d1c1a46cbf5d860b6f8c2b732bedc82b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 890 DU LAVOIR &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 145000 €&lt;/div&gt;`)[0];
            popup_cfcd32dfdaab584ddf756ee39d99245d.setContent(html_d1c1a46cbf5d860b6f8c2b732bedc82b);
        

        marker_c85739c6fb42eacdb470cb7a98bc1cdf.bindPopup(popup_cfcd32dfdaab584ddf756ee39d99245d)
        ;

        
    
    
            var marker_b376a98070363f5f8054f4d5dd88d4e1 = L.marker(
                [48.034468, -4.642943],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_72cdf6d87e72b851bbc58fb5a9854497 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_b376a98070363f5f8054f4d5dd88d4e1.setIcon(icon_72cdf6d87e72b851bbc58fb5a9854497);
        
    
        var popup_5c544e7338451d7905d35b19aa088107 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d433a5f29ae079f9795300a95a0d131c = $(`&lt;div id=&quot;html_d433a5f29ae079f9795300a95a0d131c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LANDRER &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 185000 €&lt;/div&gt;`)[0];
            popup_5c544e7338451d7905d35b19aa088107.setContent(html_d433a5f29ae079f9795300a95a0d131c);
        

        marker_b376a98070363f5f8054f4d5dd88d4e1.bindPopup(popup_5c544e7338451d7905d35b19aa088107)
        ;

        
    
    
            var marker_c01a6468ff99040c39f2b7bb88445e8f = L.marker(
                [48.034629, -4.643036],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_983dc757fa4e3d7357254aaade9b8d0d = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_c01a6468ff99040c39f2b7bb88445e8f.setIcon(icon_983dc757fa4e3d7357254aaade9b8d0d);
        
    
        var popup_d57d4555296996c7b37f106ea1e4d5ef = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e814242f44e62f1a4185dcea12ddabe9 = $(`&lt;div id=&quot;html_e814242f44e62f1a4185dcea12ddabe9&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5244 DU LAVOIR &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 185000 €&lt;/div&gt;`)[0];
            popup_d57d4555296996c7b37f106ea1e4d5ef.setContent(html_e814242f44e62f1a4185dcea12ddabe9);
        

        marker_c01a6468ff99040c39f2b7bb88445e8f.bindPopup(popup_d57d4555296996c7b37f106ea1e4d5ef)
        ;

        
    
    
            var marker_083a78316b2f78a1ede5c516046ca42c = L.marker(
                [48.034359, -4.643113],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_b9ddfd26dbd990c22fb0860bcb93387f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_083a78316b2f78a1ede5c516046ca42c.setIcon(icon_b9ddfd26dbd990c22fb0860bcb93387f);
        
    
        var popup_c519d8259751718c9ee9051815a52dc1 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8b1286ffd5c7f3944183c12c3f9f6d02 = $(`&lt;div id=&quot;html_8b1286ffd5c7f3944183c12c3f9f6d02&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LANDRER &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 145000 €&lt;/div&gt;`)[0];
            popup_c519d8259751718c9ee9051815a52dc1.setContent(html_8b1286ffd5c7f3944183c12c3f9f6d02);
        

        marker_083a78316b2f78a1ede5c516046ca42c.bindPopup(popup_c519d8259751718c9ee9051815a52dc1)
        ;

        
    
    
            var marker_ff1370662797a818519356fe3b88e335 = L.marker(
                [48.034359, -4.643113],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_af671ca9f6da77d2e4c83da26ca522da = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ff1370662797a818519356fe3b88e335.setIcon(icon_af671ca9f6da77d2e4c83da26ca522da);
        
    
        var popup_758eb4388e9aff6924c70a78a7f311df = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_4418b1ab4bd46168bd4fcdfde2c60409 = $(`&lt;div id=&quot;html_4418b1ab4bd46168bd4fcdfde2c60409&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LANDRER &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 15000 €&lt;/div&gt;`)[0];
            popup_758eb4388e9aff6924c70a78a7f311df.setContent(html_4418b1ab4bd46168bd4fcdfde2c60409);
        

        marker_ff1370662797a818519356fe3b88e335.bindPopup(popup_758eb4388e9aff6924c70a78a7f311df)
        ;

        
    
    
            var marker_74abe9a9d5c628deb52f2d876e8df373 = L.marker(
                [48.034453, -4.64313],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_994a20890edba0c29bb739ccafcba44e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_74abe9a9d5c628deb52f2d876e8df373.setIcon(icon_994a20890edba0c29bb739ccafcba44e);
        
    
        var popup_5f9dd1b2cfbdf94b9df3b5e092bda41c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_217497740f8bf24e67857303ce880d05 = $(`&lt;div id=&quot;html_217497740f8bf24e67857303ce880d05&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LANDRER &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 145000 €&lt;/div&gt;`)[0];
            popup_5f9dd1b2cfbdf94b9df3b5e092bda41c.setContent(html_217497740f8bf24e67857303ce880d05);
        

        marker_74abe9a9d5c628deb52f2d876e8df373.bindPopup(popup_5f9dd1b2cfbdf94b9df3b5e092bda41c)
        ;

        
    
    
            var marker_ec39976c972d3a8cc652dc6166b58d3e = L.marker(
                [48.034679, -4.643321],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_8ca9fab0a62218886447cb9d24047cd9 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ec39976c972d3a8cc652dc6166b58d3e.setIcon(icon_8ca9fab0a62218886447cb9d24047cd9);
        
    
        var popup_43fd06f14548263f51c65a3b0cfd92a0 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_f983078052a6ed82b3bf48a8f7521dcd = $(`&lt;div id=&quot;html_f983078052a6ed82b3bf48a8f7521dcd&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LANDRER &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 15000 €&lt;/div&gt;`)[0];
            popup_43fd06f14548263f51c65a3b0cfd92a0.setContent(html_f983078052a6ed82b3bf48a8f7521dcd);
        

        marker_ec39976c972d3a8cc652dc6166b58d3e.bindPopup(popup_43fd06f14548263f51c65a3b0cfd92a0)
        ;

        
    
    
            var marker_47dfc965be098e705c0f7487ce7074b6 = L.marker(
                [48.03437, -4.64299],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_bdb783fee4c8a205f7a758320e7b9a88 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_47dfc965be098e705c0f7487ce7074b6.setIcon(icon_bdb783fee4c8a205f7a758320e7b9a88);
        
    
        var popup_ba53eab4d987a861860f2beb8f3402aa = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_b52da3f22348e62e6350410bff0b70e2 = $(`&lt;div id=&quot;html_b52da3f22348e62e6350410bff0b70e2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LANDRER &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 145000 €&lt;/div&gt;`)[0];
            popup_ba53eab4d987a861860f2beb8f3402aa.setContent(html_b52da3f22348e62e6350410bff0b70e2);
        

        marker_47dfc965be098e705c0f7487ce7074b6.bindPopup(popup_ba53eab4d987a861860f2beb8f3402aa)
        ;

        
    
    
            var marker_fa4b4eb0d831da97529e72b6baa48b94 = L.marker(
                [48.033664, -4.642346],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_f8f8ee786fab89a51c48a1b40a78cfd4 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_fa4b4eb0d831da97529e72b6baa48b94.setIcon(icon_f8f8ee786fab89a51c48a1b40a78cfd4);
        
    
        var popup_7d3502b81f1743b469ebaa03c1295f01 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_b24fd688fae84ce1e684f57cd95c3ec6 = $(`&lt;div id=&quot;html_b24fd688fae84ce1e684f57cd95c3ec6&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LANDRER &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 520 €&lt;/div&gt;`)[0];
            popup_7d3502b81f1743b469ebaa03c1295f01.setContent(html_b24fd688fae84ce1e684f57cd95c3ec6);
        

        marker_fa4b4eb0d831da97529e72b6baa48b94.bindPopup(popup_7d3502b81f1743b469ebaa03c1295f01)
        ;

        
    
    
            var marker_5c2244cf4cb1a1014db3141c096ed475 = L.marker(
                [48.030667, -4.635236],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_c983228ad66300375e471063b8a1ac0c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_5c2244cf4cb1a1014db3141c096ed475.setIcon(icon_c983228ad66300375e471063b8a1ac0c);
        
    
        var popup_30626af1dc78e4ea67dc8f32bdbf7c4e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2e483d1ac8caa41fda2a2f6ac086aedb = $(`&lt;div id=&quot;html_2e483d1ac8caa41fda2a2f6ac086aedb&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 852 DU YUN &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 90000 €&lt;/div&gt;`)[0];
            popup_30626af1dc78e4ea67dc8f32bdbf7c4e.setContent(html_2e483d1ac8caa41fda2a2f6ac086aedb);
        

        marker_5c2244cf4cb1a1014db3141c096ed475.bindPopup(popup_30626af1dc78e4ea67dc8f32bdbf7c4e)
        ;

        
    
    
            var marker_ac40c6160c6729a7b69b5e807eb03686 = L.marker(
                [48.030667, -4.635236],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_a0c0e815651de7daace6a7493e207378 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ac40c6160c6729a7b69b5e807eb03686.setIcon(icon_a0c0e815651de7daace6a7493e207378);
        
    
        var popup_d3c745e88822d6c9060f095bee8deaba = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_82f1f276ef4e87791e79039c7b8c609d = $(`&lt;div id=&quot;html_82f1f276ef4e87791e79039c7b8c609d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 852 DU YUN &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 90000 €&lt;/div&gt;`)[0];
            popup_d3c745e88822d6c9060f095bee8deaba.setContent(html_82f1f276ef4e87791e79039c7b8c609d);
        

        marker_ac40c6160c6729a7b69b5e807eb03686.bindPopup(popup_d3c745e88822d6c9060f095bee8deaba)
        ;

        
    
    
            var marker_8447fab927b1f1ea9cb714a79024fd4e = L.marker(
                [48.030674, -4.635427],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_9fdddb616cc4f0b281a18e9a2cbb8dd1 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_8447fab927b1f1ea9cb714a79024fd4e.setIcon(icon_9fdddb616cc4f0b281a18e9a2cbb8dd1);
        
    
        var popup_772c3c3a1f78285a425ade7bd7be2edd = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_29c552e2f66063918d5889dde2a078fe = $(`&lt;div id=&quot;html_29c552e2f66063918d5889dde2a078fe&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 183 DU YUN &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 150000 €&lt;/div&gt;`)[0];
            popup_772c3c3a1f78285a425ade7bd7be2edd.setContent(html_29c552e2f66063918d5889dde2a078fe);
        

        marker_8447fab927b1f1ea9cb714a79024fd4e.bindPopup(popup_772c3c3a1f78285a425ade7bd7be2edd)
        ;

        
    
    
            var marker_df3a4daa33f2e991cfa749628e6447bf = L.marker(
                [48.030889, -4.635429],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_a0674dba97b5e343e354c442d18a01cb = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_df3a4daa33f2e991cfa749628e6447bf.setIcon(icon_a0674dba97b5e343e354c442d18a01cb);
        
    
        var popup_97b2f85ef0027f1a7c5323572a16e76a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d7c7925e2366fe6bf992f478d7a58626 = $(`&lt;div id=&quot;html_d7c7925e2366fe6bf992f478d7a58626&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE LOCH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 150000 €&lt;/div&gt;`)[0];
            popup_97b2f85ef0027f1a7c5323572a16e76a.setContent(html_d7c7925e2366fe6bf992f478d7a58626);
        

        marker_df3a4daa33f2e991cfa749628e6447bf.bindPopup(popup_97b2f85ef0027f1a7c5323572a16e76a)
        ;

        
    
    
            var marker_c6242188ddab00037b46bfbfb3f11f3d = L.marker(
                [48.030399, -4.635129],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_dc64376ee7aeb7c253b1bedd635b4e16 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_c6242188ddab00037b46bfbfb3f11f3d.setIcon(icon_dc64376ee7aeb7c253b1bedd635b4e16);
        
    
        var popup_6146ce8f9bcbc8d7946f9c4aade5c953 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2fb9f0e46d3cc9a28ad3598a9c688f9a = $(`&lt;div id=&quot;html_2fb9f0e46d3cc9a28ad3598a9c688f9a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE LOCH &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 4500 €&lt;/div&gt;`)[0];
            popup_6146ce8f9bcbc8d7946f9c4aade5c953.setContent(html_2fb9f0e46d3cc9a28ad3598a9c688f9a);
        

        marker_c6242188ddab00037b46bfbfb3f11f3d.bindPopup(popup_6146ce8f9bcbc8d7946f9c4aade5c953)
        ;

        
    
    
            var marker_1dc4598a4d0df19091d86b0137cdfb32 = L.marker(
                [48.03029, -4.633439],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_6d20a5f3ee8dbbfde03c6c1de5f532a2 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_1dc4598a4d0df19091d86b0137cdfb32.setIcon(icon_6d20a5f3ee8dbbfde03c6c1de5f532a2);
        
    
        var popup_e032e780726858cfbe09d2f919eb6817 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e2e0af84d1a8d3d08f60b3b6503d8013 = $(`&lt;div id=&quot;html_e2e0af84d1a8d3d08f60b3b6503d8013&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE LOCH &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 160000 €&lt;/div&gt;`)[0];
            popup_e032e780726858cfbe09d2f919eb6817.setContent(html_e2e0af84d1a8d3d08f60b3b6503d8013);
        

        marker_1dc4598a4d0df19091d86b0137cdfb32.bindPopup(popup_e032e780726858cfbe09d2f919eb6817)
        ;

        
    
    
            var marker_7983a68a6e17886e01955373416ea40d = L.marker(
                [48.03029, -4.633439],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_6baa83c0d5721078f5dbd8556c420411 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_7983a68a6e17886e01955373416ea40d.setIcon(icon_6baa83c0d5721078f5dbd8556c420411);
        
    
        var popup_8d108d2895e4078fbfb67055c8090113 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_844fa8b16d039bab7a52788efa6b65ca = $(`&lt;div id=&quot;html_844fa8b16d039bab7a52788efa6b65ca&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE LOCH &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 12000 €&lt;/div&gt;`)[0];
            popup_8d108d2895e4078fbfb67055c8090113.setContent(html_844fa8b16d039bab7a52788efa6b65ca);
        

        marker_7983a68a6e17886e01955373416ea40d.bindPopup(popup_8d108d2895e4078fbfb67055c8090113)
        ;

        
    
    
            var marker_03b841adcb4bf341a735d83b77e4dfd6 = L.marker(
                [48.028923, -4.639614],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_56c62fbfbb8d2d517dc72c7e37558875 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_03b841adcb4bf341a735d83b77e4dfd6.setIcon(icon_56c62fbfbb8d2d517dc72c7e37558875);
        
    
        var popup_c864b12cc23cb2953d83f42c202e192d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_198ccf3c09a56ff6f63047f0cf0fd6db = $(`&lt;div id=&quot;html_198ccf3c09a56ff6f63047f0cf0fd6db&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  FEUNTEUN YEN &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 8000 €&lt;/div&gt;`)[0];
            popup_c864b12cc23cb2953d83f42c202e192d.setContent(html_198ccf3c09a56ff6f63047f0cf0fd6db);
        

        marker_03b841adcb4bf341a735d83b77e4dfd6.bindPopup(popup_c864b12cc23cb2953d83f42c202e192d)
        ;

        
    
    
            var marker_49c2c14f26704e7d2e478144d1d35bce = L.marker(
                [48.030106, -4.638071],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_fdad2e0e67dc708784a5bf9d909ff895 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_49c2c14f26704e7d2e478144d1d35bce.setIcon(icon_fdad2e0e67dc708784a5bf9d909ff895);
        
    
        var popup_3d044a53776847a77f85c9d5282d7e09 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7082bd957f4f60ce8a7f0753393338cc = $(`&lt;div id=&quot;html_7082bd957f4f60ce8a7f0753393338cc&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5157 LE LOCH &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 110000 €&lt;/div&gt;`)[0];
            popup_3d044a53776847a77f85c9d5282d7e09.setContent(html_7082bd957f4f60ce8a7f0753393338cc);
        

        marker_49c2c14f26704e7d2e478144d1d35bce.bindPopup(popup_3d044a53776847a77f85c9d5282d7e09)
        ;

        
    
    
            var marker_90291d263f54c309aa8e0026e53a7738 = L.marker(
                [48.030106, -4.638071],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_7dac781f9e87298f2f545ced318db8ae = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_90291d263f54c309aa8e0026e53a7738.setIcon(icon_7dac781f9e87298f2f545ced318db8ae);
        
    
        var popup_ae3f5fec059cd66b44590320dd2940b8 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8c5da2b77515df59e1e87d509150dd14 = $(`&lt;div id=&quot;html_8c5da2b77515df59e1e87d509150dd14&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5157 LE LOCH &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 110000 €&lt;/div&gt;`)[0];
            popup_ae3f5fec059cd66b44590320dd2940b8.setContent(html_8c5da2b77515df59e1e87d509150dd14);
        

        marker_90291d263f54c309aa8e0026e53a7738.bindPopup(popup_ae3f5fec059cd66b44590320dd2940b8)
        ;

        
    
    
            var marker_60f6c0f896b67bde6be66a91db7417d6 = L.marker(
                [48.031144, -4.639588],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_3e106875fb264cc23cd60b3d479b98e7 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_60f6c0f896b67bde6be66a91db7417d6.setIcon(icon_3e106875fb264cc23cd60b3d479b98e7);
        
    
        var popup_51aa4cad0ebf788c1f072bafa9901539 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_27329a15edb467d9fa00d0d77b9d0050 = $(`&lt;div id=&quot;html_27329a15edb467d9fa00d0d77b9d0050&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 848 DES STERNES &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 95000 €&lt;/div&gt;`)[0];
            popup_51aa4cad0ebf788c1f072bafa9901539.setContent(html_27329a15edb467d9fa00d0d77b9d0050);
        

        marker_60f6c0f896b67bde6be66a91db7417d6.bindPopup(popup_51aa4cad0ebf788c1f072bafa9901539)
        ;

        
    
    
            var marker_125bc0083897a9f490c0d58b026f0501 = L.marker(
                [48.030802, -4.637273],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_7aba82a51b133e82a8d32a831d77bd7b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_125bc0083897a9f490c0d58b026f0501.setIcon(icon_7aba82a51b133e82a8d32a831d77bd7b);
        
    
        var popup_d19f0b9637a3ad8a9d81b87783df8790 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7340c652ce2814cfe12300db5bb1077c = $(`&lt;div id=&quot;html_7340c652ce2814cfe12300db5bb1077c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5042 LE LOCH &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 104000 €&lt;/div&gt;`)[0];
            popup_d19f0b9637a3ad8a9d81b87783df8790.setContent(html_7340c652ce2814cfe12300db5bb1077c);
        

        marker_125bc0083897a9f490c0d58b026f0501.bindPopup(popup_d19f0b9637a3ad8a9d81b87783df8790)
        ;

        
    
    
            var marker_06ed01461558eeb8e4f645741fcade3d = L.marker(
                [48.030802, -4.637273],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_299941aaa48c196eec00c2230c71360d = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_06ed01461558eeb8e4f645741fcade3d.setIcon(icon_299941aaa48c196eec00c2230c71360d);
        
    
        var popup_50541d3054ed553cb5ef98bc5c390b03 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_330a4889b8e977ba93f6e523ac690678 = $(`&lt;div id=&quot;html_330a4889b8e977ba93f6e523ac690678&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5042 LE LOCH &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 104000 €&lt;/div&gt;`)[0];
            popup_50541d3054ed553cb5ef98bc5c390b03.setContent(html_330a4889b8e977ba93f6e523ac690678);
        

        marker_06ed01461558eeb8e4f645741fcade3d.bindPopup(popup_50541d3054ed553cb5ef98bc5c390b03)
        ;

        
    
    
            var marker_fb5156c6848f98815dc1969db5c87e6d = L.marker(
                [48.029826, -4.633884],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_c66300bf00ae39a41cc0d587f143d68c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_fb5156c6848f98815dc1969db5c87e6d.setIcon(icon_c66300bf00ae39a41cc0d587f143d68c);
        
    
        var popup_83cdd79eb852fee86348f1a35ad40c72 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_46a87157945485b452d1d21fcb5ec1c4 = $(`&lt;div id=&quot;html_46a87157945485b452d1d21fcb5ec1c4&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 829 LE LOCH &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 330000 €&lt;/div&gt;`)[0];
            popup_83cdd79eb852fee86348f1a35ad40c72.setContent(html_46a87157945485b452d1d21fcb5ec1c4);
        

        marker_fb5156c6848f98815dc1969db5c87e6d.bindPopup(popup_83cdd79eb852fee86348f1a35ad40c72)
        ;

        
    
    
            var marker_3fd7ec16202e5b08dd5845c1e52de573 = L.marker(
                [48.029826, -4.633884],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_eb85d1815b238947f8d7fe5674832b48 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_3fd7ec16202e5b08dd5845c1e52de573.setIcon(icon_eb85d1815b238947f8d7fe5674832b48);
        
    
        var popup_00f4f9ea753ed452c770841e891fc8b7 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_cd532366a91ebdca93c08e41ae5c105c = $(`&lt;div id=&quot;html_cd532366a91ebdca93c08e41ae5c105c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 829 LE LOCH &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 330000 €&lt;/div&gt;`)[0];
            popup_00f4f9ea753ed452c770841e891fc8b7.setContent(html_cd532366a91ebdca93c08e41ae5c105c);
        

        marker_3fd7ec16202e5b08dd5845c1e52de573.bindPopup(popup_00f4f9ea753ed452c770841e891fc8b7)
        ;

        
    
    
            var marker_59a4b368ba23056593b6c969d3b74766 = L.marker(
                [48.030076, -4.633865],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_bfc110c4170893ce517ecea1f5b49ad7 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_59a4b368ba23056593b6c969d3b74766.setIcon(icon_bfc110c4170893ce517ecea1f5b49ad7);
        
    
        var popup_3c72c4864fa3e4ce620d4078a642b2a5 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8334fbb64da43ec91ec51f0364e9f87e = $(`&lt;div id=&quot;html_8334fbb64da43ec91ec51f0364e9f87e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE LOCH &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 160000 €&lt;/div&gt;`)[0];
            popup_3c72c4864fa3e4ce620d4078a642b2a5.setContent(html_8334fbb64da43ec91ec51f0364e9f87e);
        

        marker_59a4b368ba23056593b6c969d3b74766.bindPopup(popup_3c72c4864fa3e4ce620d4078a642b2a5)
        ;

        
    
    
            var marker_864ea9432940c2819cbe1bffe252de17 = L.marker(
                [48.030076, -4.633865],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_e29360f640514bb2482d46e576ed30d4 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_864ea9432940c2819cbe1bffe252de17.setIcon(icon_e29360f640514bb2482d46e576ed30d4);
        
    
        var popup_e5c6d1a392b949ff3336fc029162200a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_585b816287a0b283d8d45226d41b693c = $(`&lt;div id=&quot;html_585b816287a0b283d8d45226d41b693c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE LOCH &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 145000 €&lt;/div&gt;`)[0];
            popup_e5c6d1a392b949ff3336fc029162200a.setContent(html_585b816287a0b283d8d45226d41b693c);
        

        marker_864ea9432940c2819cbe1bffe252de17.bindPopup(popup_e5c6d1a392b949ff3336fc029162200a)
        ;

        
    
    
            var marker_ccf41a6713326d0bd84e1f6e589090f4 = L.marker(
                [48.03015, -4.633985],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_2165d74acba8c8206f1b03699762f98d = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ccf41a6713326d0bd84e1f6e589090f4.setIcon(icon_2165d74acba8c8206f1b03699762f98d);
        
    
        var popup_af68929f333eb2943fc0344db37913c9 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_b6d04aa41767f6234f2231c259bfa472 = $(`&lt;div id=&quot;html_b6d04aa41767f6234f2231c259bfa472&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE LOCH &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 160000 €&lt;/div&gt;`)[0];
            popup_af68929f333eb2943fc0344db37913c9.setContent(html_b6d04aa41767f6234f2231c259bfa472);
        

        marker_ccf41a6713326d0bd84e1f6e589090f4.bindPopup(popup_af68929f333eb2943fc0344db37913c9)
        ;

        
    
    
            var marker_e6b159163f82b6fb23873c7f9db9e0cc = L.marker(
                [48.03015, -4.633985],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d98d306e16ed68f46d8b9f037b57da6e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_e6b159163f82b6fb23873c7f9db9e0cc.setIcon(icon_d98d306e16ed68f46d8b9f037b57da6e);
        
    
        var popup_bbbe8758ed457c35fce5531048749a7d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_48641294ec240f88e0a9d48a8913b7e3 = $(`&lt;div id=&quot;html_48641294ec240f88e0a9d48a8913b7e3&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE LOCH &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 145000 €&lt;/div&gt;`)[0];
            popup_bbbe8758ed457c35fce5531048749a7d.setContent(html_48641294ec240f88e0a9d48a8913b7e3);
        

        marker_e6b159163f82b6fb23873c7f9db9e0cc.bindPopup(popup_bbbe8758ed457c35fce5531048749a7d)
        ;

        
    
    
            var marker_9cfb3f86deaa138548efba5abe805571 = L.marker(
                [48.030128, -4.633784],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_532214521a648d359bb570c999889114 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_9cfb3f86deaa138548efba5abe805571.setIcon(icon_532214521a648d359bb570c999889114);
        
    
        var popup_ac2963c58b55fe6acf787bcb38cb525e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_43234ff1108aa7e63fdfc3766d627adc = $(`&lt;div id=&quot;html_43234ff1108aa7e63fdfc3766d627adc&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 830 DU YUN &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 160000 €&lt;/div&gt;`)[0];
            popup_ac2963c58b55fe6acf787bcb38cb525e.setContent(html_43234ff1108aa7e63fdfc3766d627adc);
        

        marker_9cfb3f86deaa138548efba5abe805571.bindPopup(popup_ac2963c58b55fe6acf787bcb38cb525e)
        ;

        
    
    
            var marker_033b43efb7bd9ef924ff3267eb397e0a = L.marker(
                [48.030128, -4.633784],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_9cbc725c3af11266296a806c65bdaa0e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_033b43efb7bd9ef924ff3267eb397e0a.setIcon(icon_9cbc725c3af11266296a806c65bdaa0e);
        
    
        var popup_4844ee2ad662e95e695c6e71f543a93f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_5b5946cab94436f7072507317838792f = $(`&lt;div id=&quot;html_5b5946cab94436f7072507317838792f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 830 DU YUN &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 145000 €&lt;/div&gt;`)[0];
            popup_4844ee2ad662e95e695c6e71f543a93f.setContent(html_5b5946cab94436f7072507317838792f);
        

        marker_033b43efb7bd9ef924ff3267eb397e0a.bindPopup(popup_4844ee2ad662e95e695c6e71f543a93f)
        ;

        
    
    
            var marker_deed7c38f9a53fcfaac4c6eaf185d681 = L.marker(
                [48.028267, -4.639354],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_4e462329eaabb3682ba624216afc97e1 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_deed7c38f9a53fcfaac4c6eaf185d681.setIcon(icon_4e462329eaabb3682ba624216afc97e1);
        
    
        var popup_4bf19132f4f2117bef87f504f8cdc5f5 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_b848553c996ba30189d098816785ef75 = $(`&lt;div id=&quot;html_b848553c996ba30189d098816785ef75&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  FEUNTEUN YEN &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 25000 €&lt;/div&gt;`)[0];
            popup_4bf19132f4f2117bef87f504f8cdc5f5.setContent(html_b848553c996ba30189d098816785ef75);
        

        marker_deed7c38f9a53fcfaac4c6eaf185d681.bindPopup(popup_4bf19132f4f2117bef87f504f8cdc5f5)
        ;

        
    
    
            var marker_c80939ab43ddb3bf1e62f5367684b90a = L.marker(
                [48.028834, -4.637905],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_6ebb40c1a14f9c206e124f6bbcff7287 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_c80939ab43ddb3bf1e62f5367684b90a.setIcon(icon_6ebb40c1a14f9c206e124f6bbcff7287);
        
    
        var popup_7604cde7e4d3ae07e3a75b08b80ce862 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_5975ade89f65677f796ef0179ed2c6cf = $(`&lt;div id=&quot;html_5975ade89f65677f796ef0179ed2c6cf&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 823 DU PETIT LOCH &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 130000 €&lt;/div&gt;`)[0];
            popup_7604cde7e4d3ae07e3a75b08b80ce862.setContent(html_5975ade89f65677f796ef0179ed2c6cf);
        

        marker_c80939ab43ddb3bf1e62f5367684b90a.bindPopup(popup_7604cde7e4d3ae07e3a75b08b80ce862)
        ;

        
    
    
            var marker_7b738f66f46984c5a5787ba9bc0935e7 = L.marker(
                [48.028834, -4.637905],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_07f720a67a191ba6548aa00c4d39083b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_7b738f66f46984c5a5787ba9bc0935e7.setIcon(icon_07f720a67a191ba6548aa00c4d39083b);
        
    
        var popup_2ae89e968ec21d51fb80a4aafc6ce08b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e001455fbc51056687e566a5437f7081 = $(`&lt;div id=&quot;html_e001455fbc51056687e566a5437f7081&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 823 DU PETIT LOCH &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 130000 €&lt;/div&gt;`)[0];
            popup_2ae89e968ec21d51fb80a4aafc6ce08b.setContent(html_e001455fbc51056687e566a5437f7081);
        

        marker_7b738f66f46984c5a5787ba9bc0935e7.bindPopup(popup_2ae89e968ec21d51fb80a4aafc6ce08b)
        ;

        
    
    
            var marker_a79f594c34b9962f9d2e390ab858e67e = L.marker(
                [48.030255, -4.633471],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_610615d589983e80a5a5f2cb08c263d1 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_a79f594c34b9962f9d2e390ab858e67e.setIcon(icon_610615d589983e80a5a5f2cb08c263d1);
        
    
        var popup_28ed1d5ec8b81431b6b1407446923cc5 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_6f44d6ac1fc054a41327813c6e6dbdb2 = $(`&lt;div id=&quot;html_6f44d6ac1fc054a41327813c6e6dbdb2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE LOCH &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 160000 €&lt;/div&gt;`)[0];
            popup_28ed1d5ec8b81431b6b1407446923cc5.setContent(html_6f44d6ac1fc054a41327813c6e6dbdb2);
        

        marker_a79f594c34b9962f9d2e390ab858e67e.bindPopup(popup_28ed1d5ec8b81431b6b1407446923cc5)
        ;

        
    
    
            var marker_8ed91548ca53c0f102062d8e5708aaa0 = L.marker(
                [48.030255, -4.633471],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_6e9f98d64beb18617f01a573e207f754 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_8ed91548ca53c0f102062d8e5708aaa0.setIcon(icon_6e9f98d64beb18617f01a573e207f754);
        
    
        var popup_6a1515c0333bb336e2007bf1959217e0 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ede7e6f3ac49ee35f57aca27772e70fc = $(`&lt;div id=&quot;html_ede7e6f3ac49ee35f57aca27772e70fc&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE LOCH &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 12000 €&lt;/div&gt;`)[0];
            popup_6a1515c0333bb336e2007bf1959217e0.setContent(html_ede7e6f3ac49ee35f57aca27772e70fc);
        

        marker_8ed91548ca53c0f102062d8e5708aaa0.bindPopup(popup_6a1515c0333bb336e2007bf1959217e0)
        ;

        
    
    
            var marker_a92b3378f7a6579d46fa92431fb77f2d = L.marker(
                [48.030041, -4.633801],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_fae2485a98bcff855250f15c55c6429b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_a92b3378f7a6579d46fa92431fb77f2d.setIcon(icon_fae2485a98bcff855250f15c55c6429b);
        
    
        var popup_f01468d62d7b24e98e4fd60bb24f7e9f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_3ddbb0c59899953e7edf1573ee3e7a78 = $(`&lt;div id=&quot;html_3ddbb0c59899953e7edf1573ee3e7a78&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE LOCH &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 330000 €&lt;/div&gt;`)[0];
            popup_f01468d62d7b24e98e4fd60bb24f7e9f.setContent(html_3ddbb0c59899953e7edf1573ee3e7a78);
        

        marker_a92b3378f7a6579d46fa92431fb77f2d.bindPopup(popup_f01468d62d7b24e98e4fd60bb24f7e9f)
        ;

        
    
    
            var marker_949b71b177ace0df38fbec8471ed30ee = L.marker(
                [48.029785, -4.634077],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_c00056ee36e2b204817c9ca9150657d3 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_949b71b177ace0df38fbec8471ed30ee.setIcon(icon_c00056ee36e2b204817c9ca9150657d3);
        
    
        var popup_598e87e8074840f24f2f95e87f39438f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9cc2eac98cb8f2cd21412452c05c2e30 = $(`&lt;div id=&quot;html_9cc2eac98cb8f2cd21412452c05c2e30&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE LOCH &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 330000 €&lt;/div&gt;`)[0];
            popup_598e87e8074840f24f2f95e87f39438f.setContent(html_9cc2eac98cb8f2cd21412452c05c2e30);
        

        marker_949b71b177ace0df38fbec8471ed30ee.bindPopup(popup_598e87e8074840f24f2f95e87f39438f)
        ;

        
    
    
            var marker_aed1bda60018240bce89d08cfaa0c772 = L.marker(
                [48.029924, -4.633868],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_9789ae2b7a364276c3457a0f587dec2f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_aed1bda60018240bce89d08cfaa0c772.setIcon(icon_9789ae2b7a364276c3457a0f587dec2f);
        
    
        var popup_0e7a031c403896aa6e4c098f0106fc6e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_5c611ae9a0b27c201da1a3616cde1b2b = $(`&lt;div id=&quot;html_5c611ae9a0b27c201da1a3616cde1b2b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5167 LE LOCH &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 330000 €&lt;/div&gt;`)[0];
            popup_0e7a031c403896aa6e4c098f0106fc6e.setContent(html_5c611ae9a0b27c201da1a3616cde1b2b);
        

        marker_aed1bda60018240bce89d08cfaa0c772.bindPopup(popup_0e7a031c403896aa6e4c098f0106fc6e)
        ;

        
    
    
            var marker_82c9b60098adc65a8f15e921e93c587c = L.marker(
                [48.030961, -4.637232],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_cdccbc0598acf04348f57fd325ac98a9 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_82c9b60098adc65a8f15e921e93c587c.setIcon(icon_cdccbc0598acf04348f57fd325ac98a9);
        
    
        var popup_652b7655f45e348dbd3a8d99172d4a20 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_863a2679c1e75d0e0cd56c72103ab453 = $(`&lt;div id=&quot;html_863a2679c1e75d0e0cd56c72103ab453&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE LOCH &lt;br&gt;Vente en 2019 &lt;br&gt;Prix 40000 €&lt;/div&gt;`)[0];
            popup_652b7655f45e348dbd3a8d99172d4a20.setContent(html_863a2679c1e75d0e0cd56c72103ab453);
        

        marker_82c9b60098adc65a8f15e921e93c587c.bindPopup(popup_652b7655f45e348dbd3a8d99172d4a20)
        ;

        
    
    
            var marker_fec20b10ce0e1af90c9b9c3a7f6ebb0c = L.marker(
                [48.03099, -4.636993],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_bee89e7cccf9f361ab193a49407b3898 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_fec20b10ce0e1af90c9b9c3a7f6ebb0c.setIcon(icon_bee89e7cccf9f361ab193a49407b3898);
        
    
        var popup_651b2bbc9732c2982df115cef6e88107 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_6a9de6b4eaf132d444aeeb175e6ca33c = $(`&lt;div id=&quot;html_6a9de6b4eaf132d444aeeb175e6ca33c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE LOCH &lt;br&gt;Vente en 2019 &lt;br&gt;Prix 40000 €&lt;/div&gt;`)[0];
            popup_651b2bbc9732c2982df115cef6e88107.setContent(html_6a9de6b4eaf132d444aeeb175e6ca33c);
        

        marker_fec20b10ce0e1af90c9b9c3a7f6ebb0c.bindPopup(popup_651b2bbc9732c2982df115cef6e88107)
        ;

        
    
    
            var marker_1c9d695718e3156489c7e0c5459efee0 = L.marker(
                [48.028939, -4.637948],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_5a026f3ae8f43496516e0d303633e001 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_1c9d695718e3156489c7e0c5459efee0.setIcon(icon_5a026f3ae8f43496516e0d303633e001);
        
    
        var popup_79b105505fb122a46bfe7cf133bdb05e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_0e9a740d481bcf6626c2d04ba46b34f7 = $(`&lt;div id=&quot;html_0e9a740d481bcf6626c2d04ba46b34f7&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  FEUNTEUN YEN &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 130000 €&lt;/div&gt;`)[0];
            popup_79b105505fb122a46bfe7cf133bdb05e.setContent(html_0e9a740d481bcf6626c2d04ba46b34f7);
        

        marker_1c9d695718e3156489c7e0c5459efee0.bindPopup(popup_79b105505fb122a46bfe7cf133bdb05e)
        ;

        
    
    
            var marker_099656de8577de4a380065617bdfa638 = L.marker(
                [48.028893, -4.637982],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_6791b75d05f6c296bf5a547b0fd27f38 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_099656de8577de4a380065617bdfa638.setIcon(icon_6791b75d05f6c296bf5a547b0fd27f38);
        
    
        var popup_f41fcc8fda2050af70103f0498d98b92 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_f35927bbb6362a75107a9c6818d40d92 = $(`&lt;div id=&quot;html_f35927bbb6362a75107a9c6818d40d92&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  FEUNTEUN YEN &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 130000 €&lt;/div&gt;`)[0];
            popup_f41fcc8fda2050af70103f0498d98b92.setContent(html_f35927bbb6362a75107a9c6818d40d92);
        

        marker_099656de8577de4a380065617bdfa638.bindPopup(popup_f41fcc8fda2050af70103f0498d98b92)
        ;

        
    
    
            var marker_310056f8401911ddcdd264d6eb7aaf6e = L.marker(
                [48.028893, -4.637982],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_de21ed25e602e4f28f057cf61f4c4de8 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_310056f8401911ddcdd264d6eb7aaf6e.setIcon(icon_de21ed25e602e4f28f057cf61f4c4de8);
        
    
        var popup_68e285d72f545ecea510b392d64f53d6 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_36a34d5a60a56d7a3fee0890c8a8e6e3 = $(`&lt;div id=&quot;html_36a34d5a60a56d7a3fee0890c8a8e6e3&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  FEUNTEUN YEN &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 130000 €&lt;/div&gt;`)[0];
            popup_68e285d72f545ecea510b392d64f53d6.setContent(html_36a34d5a60a56d7a3fee0890c8a8e6e3);
        

        marker_310056f8401911ddcdd264d6eb7aaf6e.bindPopup(popup_68e285d72f545ecea510b392d64f53d6)
        ;

        
    
    
            var marker_d7861a1d2efdba98af02d14f9c53e5c6 = L.marker(
                [48.031947, -4.638978],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_7e6f50158ea536310eec08d1bb4186d4 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_d7861a1d2efdba98af02d14f9c53e5c6.setIcon(icon_7e6f50158ea536310eec08d1bb4186d4);
        
    
        var popup_519232c8fcd9f2400276839359686b64 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_33932fda255d4a2f5198d376630e02f4 = $(`&lt;div id=&quot;html_33932fda255d4a2f5198d376630e02f4&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LANDRER &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 25000 €&lt;/div&gt;`)[0];
            popup_519232c8fcd9f2400276839359686b64.setContent(html_33932fda255d4a2f5198d376630e02f4);
        

        marker_d7861a1d2efdba98af02d14f9c53e5c6.bindPopup(popup_519232c8fcd9f2400276839359686b64)
        ;

        
    
    
            var marker_55bbd64533a1fc80ee6784840931eff1 = L.marker(
                [48.031284, -4.638403],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_6259e827f7faa25333545e32d6f32d2f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_55bbd64533a1fc80ee6784840931eff1.setIcon(icon_6259e827f7faa25333545e32d6f32d2f);
        
    
        var popup_de34a54cfb8a604527c214b4cbb14039 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2463fa3949c079791eb1da72e6b55781 = $(`&lt;div id=&quot;html_2463fa3949c079791eb1da72e6b55781&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE LOCH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 85000 €&lt;/div&gt;`)[0];
            popup_de34a54cfb8a604527c214b4cbb14039.setContent(html_2463fa3949c079791eb1da72e6b55781);
        

        marker_55bbd64533a1fc80ee6784840931eff1.bindPopup(popup_de34a54cfb8a604527c214b4cbb14039)
        ;

        
    
    
            var marker_a6fe567dfa97b0640f883571a1e02f86 = L.marker(
                [48.031255, -4.638835],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_165a39e6bbf734ee439d63f0a641ca97 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_a6fe567dfa97b0640f883571a1e02f86.setIcon(icon_165a39e6bbf734ee439d63f0a641ca97);
        
    
        var popup_0cf93a501ca50aed60f227407e1277fe = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a8111502bd87db6831b1aa48814ebad4 = $(`&lt;div id=&quot;html_a8111502bd87db6831b1aa48814ebad4&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5248 DU LOCH &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 95000 €&lt;/div&gt;`)[0];
            popup_0cf93a501ca50aed60f227407e1277fe.setContent(html_a8111502bd87db6831b1aa48814ebad4);
        

        marker_a6fe567dfa97b0640f883571a1e02f86.bindPopup(popup_0cf93a501ca50aed60f227407e1277fe)
        ;

        
    
    
            var marker_e78901aa364422536fe4ace7af147ccb = L.marker(
                [48.030932, -4.637457],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_de2e04dc5d32bf75673af59847a2ad86 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_e78901aa364422536fe4ace7af147ccb.setIcon(icon_de2e04dc5d32bf75673af59847a2ad86);
        
    
        var popup_080c5faa788c8b015793719b7d52bd6d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_15c97a045f2218bf7a5a753ed07513d4 = $(`&lt;div id=&quot;html_15c97a045f2218bf7a5a753ed07513d4&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE LOCH &lt;br&gt;Vente en 2019 &lt;br&gt;Prix 40000 €&lt;/div&gt;`)[0];
            popup_080c5faa788c8b015793719b7d52bd6d.setContent(html_15c97a045f2218bf7a5a753ed07513d4);
        

        marker_e78901aa364422536fe4ace7af147ccb.bindPopup(popup_080c5faa788c8b015793719b7d52bd6d)
        ;

        
    
    
            var marker_061944ed21acddd61551711230180467 = L.marker(
                [48.031303, -4.637572],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_32b5749aaf582e65cb227f14152bf826 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_061944ed21acddd61551711230180467.setIcon(icon_32b5749aaf582e65cb227f14152bf826);
        
    
        var popup_0b00079b4c9da84b82ca94beee372d3b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_cd381b07ede54c2319b2e9936975a971 = $(`&lt;div id=&quot;html_cd381b07ede54c2319b2e9936975a971&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 33 DU LOCH &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 135000 €&lt;/div&gt;`)[0];
            popup_0b00079b4c9da84b82ca94beee372d3b.setContent(html_cd381b07ede54c2319b2e9936975a971);
        

        marker_061944ed21acddd61551711230180467.bindPopup(popup_0b00079b4c9da84b82ca94beee372d3b)
        ;

        
    
    
            var marker_930fce8494d83b42b528330ab4eed622 = L.marker(
                [48.031569, -4.637401],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d5eade009d0d8790621e46964b5a6fb5 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_930fce8494d83b42b528330ab4eed622.setIcon(icon_d5eade009d0d8790621e46964b5a6fb5);
        
    
        var popup_381c32c57a2bd07ce2a131b9843b7cd5 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_4a30654106bd270ceb948ea62fa41662 = $(`&lt;div id=&quot;html_4a30654106bd270ceb948ea62fa41662&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE LOCH &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 22500 €&lt;/div&gt;`)[0];
            popup_381c32c57a2bd07ce2a131b9843b7cd5.setContent(html_4a30654106bd270ceb948ea62fa41662);
        

        marker_930fce8494d83b42b528330ab4eed622.bindPopup(popup_381c32c57a2bd07ce2a131b9843b7cd5)
        ;

        
    
    
            var marker_a8da773799d6df080ebb6022bc9f6b7c = L.marker(
                [48.031601, -4.637284],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_27e8be43cc27ff98ee1086b5c6a9394a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_a8da773799d6df080ebb6022bc9f6b7c.setIcon(icon_27e8be43cc27ff98ee1086b5c6a9394a);
        
    
        var popup_e2b7c6d9523ba3d2ed711cb622d41829 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c513d4739c056315fa732f18bb7ede03 = $(`&lt;div id=&quot;html_c513d4739c056315fa732f18bb7ede03&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE LOCH &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 22500 €&lt;/div&gt;`)[0];
            popup_e2b7c6d9523ba3d2ed711cb622d41829.setContent(html_c513d4739c056315fa732f18bb7ede03);
        

        marker_a8da773799d6df080ebb6022bc9f6b7c.bindPopup(popup_e2b7c6d9523ba3d2ed711cb622d41829)
        ;

        
    
    
            var marker_777b9515f85a9515ea942ebf062d304b = L.marker(
                [48.028933, -4.642586],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d37460d3ba9ebfe3ea9293f14fbf70c2 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_777b9515f85a9515ea942ebf062d304b.setIcon(icon_d37460d3ba9ebfe3ea9293f14fbf70c2);
        
    
        var popup_e9a65ed7ea60b6ff0b4ba10b2a5cd30f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_4c29394ba20b4c34f3224c1392e3fa1a = $(`&lt;div id=&quot;html_4c29394ba20b4c34f3224c1392e3fa1a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERINGAR &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 560 €&lt;/div&gt;`)[0];
            popup_e9a65ed7ea60b6ff0b4ba10b2a5cd30f.setContent(html_4c29394ba20b4c34f3224c1392e3fa1a);
        

        marker_777b9515f85a9515ea942ebf062d304b.bindPopup(popup_e9a65ed7ea60b6ff0b4ba10b2a5cd30f)
        ;

        
    
    
            var marker_95f341f0fec15ef6f1f1154b4c57bbef = L.marker(
                [48.030008, -4.646097],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_f234b07513c35f3c37f6af0f82612d43 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_95f341f0fec15ef6f1f1154b4c57bbef.setIcon(icon_f234b07513c35f3c37f6af0f82612d43);
        
    
        var popup_a11b7453bf3a543111aaf53db5f47165 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9fe4a57a6dabc2db4a729b399e5e6b83 = $(`&lt;div id=&quot;html_9fe4a57a6dabc2db4a729b399e5e6b83&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  TORAMUR &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 400 €&lt;/div&gt;`)[0];
            popup_a11b7453bf3a543111aaf53db5f47165.setContent(html_9fe4a57a6dabc2db4a729b399e5e6b83);
        

        marker_95f341f0fec15ef6f1f1154b4c57bbef.bindPopup(popup_a11b7453bf3a543111aaf53db5f47165)
        ;

        
    
    
            var marker_df738ad2623eed00a800023ce1bdd63e = L.marker(
                [48.030147, -4.645953],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_e528edd8b9ef2c7bffbcbce2eb43b247 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_df738ad2623eed00a800023ce1bdd63e.setIcon(icon_e528edd8b9ef2c7bffbcbce2eb43b247);
        
    
        var popup_7bb1e84bdc89029afbffc372db0ac6fa = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_6f6a91a78172531bb7f6a18f393a6245 = $(`&lt;div id=&quot;html_6f6a91a78172531bb7f6a18f393a6245&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  TORAMUR &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 400 €&lt;/div&gt;`)[0];
            popup_7bb1e84bdc89029afbffc372db0ac6fa.setContent(html_6f6a91a78172531bb7f6a18f393a6245);
        

        marker_df738ad2623eed00a800023ce1bdd63e.bindPopup(popup_7bb1e84bdc89029afbffc372db0ac6fa)
        ;

        
    
    
            var marker_adc6137f886ea24195aacebefb69afe8 = L.marker(
                [48.032362, -4.648255],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_6900f65c5bfd71e18b2e4eccef632a4c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_adc6137f886ea24195aacebefb69afe8.setIcon(icon_6900f65c5bfd71e18b2e4eccef632a4c);
        
    
        var popup_7ca7a05870c0dec31785f8bd139579f0 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1a36911f383f0ca2da61623b101e4724 = $(`&lt;div id=&quot;html_1a36911f383f0ca2da61623b101e4724&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERVEN VRAS &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 95000 €&lt;/div&gt;`)[0];
            popup_7ca7a05870c0dec31785f8bd139579f0.setContent(html_1a36911f383f0ca2da61623b101e4724);
        

        marker_adc6137f886ea24195aacebefb69afe8.bindPopup(popup_7ca7a05870c0dec31785f8bd139579f0)
        ;

        
    
    
            var marker_de6f9335547cd34ec761da990a510270 = L.marker(
                [48.032491, -4.648358],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_244f226210a62a5538a0be9bbd715a05 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_de6f9335547cd34ec761da990a510270.setIcon(icon_244f226210a62a5538a0be9bbd715a05);
        
    
        var popup_1b1d5c3fb761b1f00050c22b03577f73 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_64ad68dbfa531a22a6da709c45019078 = $(`&lt;div id=&quot;html_64ad68dbfa531a22a6da709c45019078&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 744 KERVEN VRAS &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 95000 €&lt;/div&gt;`)[0];
            popup_1b1d5c3fb761b1f00050c22b03577f73.setContent(html_64ad68dbfa531a22a6da709c45019078);
        

        marker_de6f9335547cd34ec761da990a510270.bindPopup(popup_1b1d5c3fb761b1f00050c22b03577f73)
        ;

        
    
    
            var marker_69605577d1ade63b40ce44e2805bfe04 = L.marker(
                [48.032491, -4.648358],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_709491e2885c9074f88bb62267106260 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_69605577d1ade63b40ce44e2805bfe04.setIcon(icon_709491e2885c9074f88bb62267106260);
        
    
        var popup_4705a08a0f1b9f934ee648f66ff1ba09 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9f809822cad615ca218bf059317c4d15 = $(`&lt;div id=&quot;html_9f809822cad615ca218bf059317c4d15&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 744 KERVEN VRAS &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 95000 €&lt;/div&gt;`)[0];
            popup_4705a08a0f1b9f934ee648f66ff1ba09.setContent(html_9f809822cad615ca218bf059317c4d15);
        

        marker_69605577d1ade63b40ce44e2805bfe04.bindPopup(popup_4705a08a0f1b9f934ee648f66ff1ba09)
        ;

        
    
    
            var marker_144ae7402572ab10f189b8657114c6b9 = L.marker(
                [48.031123, -4.645797],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_1058baa3a13b42e7213531b45fe97462 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_144ae7402572ab10f189b8657114c6b9.setIcon(icon_1058baa3a13b42e7213531b45fe97462);
        
    
        var popup_ccd89ba2ead7854fce78e81f2b79accd = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_39ed44c0d6d37d2d667e5e88e9de1ca6 = $(`&lt;div id=&quot;html_39ed44c0d6d37d2d667e5e88e9de1ca6&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERNEVEZ &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 135000 €&lt;/div&gt;`)[0];
            popup_ccd89ba2ead7854fce78e81f2b79accd.setContent(html_39ed44c0d6d37d2d667e5e88e9de1ca6);
        

        marker_144ae7402572ab10f189b8657114c6b9.bindPopup(popup_ccd89ba2ead7854fce78e81f2b79accd)
        ;

        
    
    
            var marker_e8b3fa2a7df9edb01e4b4e04ce351fef = L.marker(
                [48.031165, -4.645752],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_269a75380d3ca019031f115b10a41a38 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_e8b3fa2a7df9edb01e4b4e04ce351fef.setIcon(icon_269a75380d3ca019031f115b10a41a38);
        
    
        var popup_8f7ec10b0364f819ed51d91012c8c3f9 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8415ef8095c4caf429423c786e16b0f3 = $(`&lt;div id=&quot;html_8415ef8095c4caf429423c786e16b0f3&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERNEVEZ &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 135000 €&lt;/div&gt;`)[0];
            popup_8f7ec10b0364f819ed51d91012c8c3f9.setContent(html_8415ef8095c4caf429423c786e16b0f3);
        

        marker_e8b3fa2a7df9edb01e4b4e04ce351fef.bindPopup(popup_8f7ec10b0364f819ed51d91012c8c3f9)
        ;

        
    
    
            var marker_4b2b48b3fe4a2c67bb5c36d7b8faaf53 = L.marker(
                [48.030417, -4.644902],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_92a47019d23b1dd216961ee59ed0722e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_4b2b48b3fe4a2c67bb5c36d7b8faaf53.setIcon(icon_92a47019d23b1dd216961ee59ed0722e);
        
    
        var popup_d22eb556f7d1ef917a3ebb364374eef4 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_6ab8f7308966e0998a3f6957f4774bf8 = $(`&lt;div id=&quot;html_6ab8f7308966e0998a3f6957f4774bf8&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERNEVEZ &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 115000 €&lt;/div&gt;`)[0];
            popup_d22eb556f7d1ef917a3ebb364374eef4.setContent(html_6ab8f7308966e0998a3f6957f4774bf8);
        

        marker_4b2b48b3fe4a2c67bb5c36d7b8faaf53.bindPopup(popup_d22eb556f7d1ef917a3ebb364374eef4)
        ;

        
    
    
            var marker_73894a6fb30cb78d354de238a30bb008 = L.marker(
                [48.030485, -4.644543],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_7dbad1d4c50350bbd4d8e7c940cd8663 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_73894a6fb30cb78d354de238a30bb008.setIcon(icon_7dbad1d4c50350bbd4d8e7c940cd8663);
        
    
        var popup_30129d95588b60f01c80cd4de785525b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8d58fb60c41daa17a95d15b9ec94801a = $(`&lt;div id=&quot;html_8d58fb60c41daa17a95d15b9ec94801a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 767 KERNEVEZ &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 115000 €&lt;/div&gt;`)[0];
            popup_30129d95588b60f01c80cd4de785525b.setContent(html_8d58fb60c41daa17a95d15b9ec94801a);
        

        marker_73894a6fb30cb78d354de238a30bb008.bindPopup(popup_30129d95588b60f01c80cd4de785525b)
        ;

        
    
    
            var marker_82aa8a3e3ad41200f3892699ad1907e1 = L.marker(
                [48.02989, -4.644552],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_26d391acbbd0df362183b81b43fa569c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_82aa8a3e3ad41200f3892699ad1907e1.setIcon(icon_26d391acbbd0df362183b81b43fa569c);
        
    
        var popup_28fd43ddd86a20af89bcf4717e6ca060 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9ab787f07cc6e2e5e4fd8689d226f33c = $(`&lt;div id=&quot;html_9ab787f07cc6e2e5e4fd8689d226f33c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PEN A LEN &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 95000 €&lt;/div&gt;`)[0];
            popup_28fd43ddd86a20af89bcf4717e6ca060.setContent(html_9ab787f07cc6e2e5e4fd8689d226f33c);
        

        marker_82aa8a3e3ad41200f3892699ad1907e1.bindPopup(popup_28fd43ddd86a20af89bcf4717e6ca060)
        ;

        
    
    
            var marker_f70995ea466927fd357cccea6a3d1613 = L.marker(
                [48.029767, -4.644502],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_effe591d755484098c1d4f8297544815 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_f70995ea466927fd357cccea6a3d1613.setIcon(icon_effe591d755484098c1d4f8297544815);
        
    
        var popup_e255bab1f9685e25662513d9d305f218 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_835dca08475732231769991953ee1378 = $(`&lt;div id=&quot;html_835dca08475732231769991953ee1378&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  TORAMUR &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 4000 €&lt;/div&gt;`)[0];
            popup_e255bab1f9685e25662513d9d305f218.setContent(html_835dca08475732231769991953ee1378);
        

        marker_f70995ea466927fd357cccea6a3d1613.bindPopup(popup_e255bab1f9685e25662513d9d305f218)
        ;

        
    
    
            var marker_80c49093b3bf608022bc27a3039b43f4 = L.marker(
                [48.030563, -4.644659],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_6143ee71d18e7270d66a3455429b9482 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_80c49093b3bf608022bc27a3039b43f4.setIcon(icon_6143ee71d18e7270d66a3455429b9482);
        
    
        var popup_89845bc4c3f707b3b521b6086f050a65 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_883a226b76d6d6dd142ee0a9ddb31771 = $(`&lt;div id=&quot;html_883a226b76d6d6dd142ee0a9ddb31771&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERNEVEZ &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 115000 €&lt;/div&gt;`)[0];
            popup_89845bc4c3f707b3b521b6086f050a65.setContent(html_883a226b76d6d6dd142ee0a9ddb31771);
        

        marker_80c49093b3bf608022bc27a3039b43f4.bindPopup(popup_89845bc4c3f707b3b521b6086f050a65)
        ;

        
    
    
            var marker_4a8a484e06c8d09a22335711b878edc5 = L.marker(
                [48.031085, -4.645836],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_1abf3093fcb48e1f74776dd78b40470a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_4a8a484e06c8d09a22335711b878edc5.setIcon(icon_1abf3093fcb48e1f74776dd78b40470a);
        
    
        var popup_cd7f70faa4c1ea6b68124f8cba19bc2c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_68334b9f6c7575b01eb9f90d425e3e2f = $(`&lt;div id=&quot;html_68334b9f6c7575b01eb9f90d425e3e2f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERNEVEZ &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 135000 €&lt;/div&gt;`)[0];
            popup_cd7f70faa4c1ea6b68124f8cba19bc2c.setContent(html_68334b9f6c7575b01eb9f90d425e3e2f);
        

        marker_4a8a484e06c8d09a22335711b878edc5.bindPopup(popup_cd7f70faa4c1ea6b68124f8cba19bc2c)
        ;

        
    
    
            var marker_cb9508dbbb5c521398cafd4bfce23ba9 = L.marker(
                [48.029711, -4.644406],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_a77e97b988be9b9a0bb9be6dd907c79c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_cb9508dbbb5c521398cafd4bfce23ba9.setIcon(icon_a77e97b988be9b9a0bb9be6dd907c79c);
        
    
        var popup_c26004e87475ea7c7e57c020d48972d6 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2a517829b8c87b128e46524659e54e76 = $(`&lt;div id=&quot;html_2a517829b8c87b128e46524659e54e76&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5179 DES COURLIS &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 95000 €&lt;/div&gt;`)[0];
            popup_c26004e87475ea7c7e57c020d48972d6.setContent(html_2a517829b8c87b128e46524659e54e76);
        

        marker_cb9508dbbb5c521398cafd4bfce23ba9.bindPopup(popup_c26004e87475ea7c7e57c020d48972d6)
        ;

        
    
    
            var marker_bde0b79828cdcbc08d58487f3a433519 = L.marker(
                [48.02926, -4.644694],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_5680e95979d1e27f4b76d961461ea7e9 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_bde0b79828cdcbc08d58487f3a433519.setIcon(icon_5680e95979d1e27f4b76d961461ea7e9);
        
    
        var popup_ef3395e0202836abe9eeddd62c3c6063 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_28338e2f73912bc351114447fa7abca1 = $(`&lt;div id=&quot;html_28338e2f73912bc351114447fa7abca1&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 787 DES CANARIS &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 135000 €&lt;/div&gt;`)[0];
            popup_ef3395e0202836abe9eeddd62c3c6063.setContent(html_28338e2f73912bc351114447fa7abca1);
        

        marker_bde0b79828cdcbc08d58487f3a433519.bindPopup(popup_ef3395e0202836abe9eeddd62c3c6063)
        ;

        
    
    
            var marker_469476df6c4783cd1cc0be3ab5e960ed = L.marker(
                [48.029383, -4.644508],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_939f1c24fafc1ef2d87eabec63c50b41 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_469476df6c4783cd1cc0be3ab5e960ed.setIcon(icon_939f1c24fafc1ef2d87eabec63c50b41);
        
    
        var popup_0369dafa172e2a3449af690f5057d993 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8ec0ff1655da40a171c63b7e7de41e7f = $(`&lt;div id=&quot;html_8ec0ff1655da40a171c63b7e7de41e7f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  TORAMUR &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 100 €&lt;/div&gt;`)[0];
            popup_0369dafa172e2a3449af690f5057d993.setContent(html_8ec0ff1655da40a171c63b7e7de41e7f);
        

        marker_469476df6c4783cd1cc0be3ab5e960ed.bindPopup(popup_0369dafa172e2a3449af690f5057d993)
        ;

        
    
    
            var marker_3669891c5ccc99765d47f4b25223f27b = L.marker(
                [48.029287, -4.644565],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_bf5ebcd28bb266354d651f94f314c77d = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_3669891c5ccc99765d47f4b25223f27b.setIcon(icon_bf5ebcd28bb266354d651f94f314c77d);
        
    
        var popup_8d3b243e0600b3d27013a1cb7080f80b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a12fa5b8205196ba37f2b0464fc7083f = $(`&lt;div id=&quot;html_a12fa5b8205196ba37f2b0464fc7083f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  TORAMUR &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 135000 €&lt;/div&gt;`)[0];
            popup_8d3b243e0600b3d27013a1cb7080f80b.setContent(html_a12fa5b8205196ba37f2b0464fc7083f);
        

        marker_3669891c5ccc99765d47f4b25223f27b.bindPopup(popup_8d3b243e0600b3d27013a1cb7080f80b)
        ;

        
    
    
            var marker_70a9d83f38be2924f55bfe5e530f1cc8 = L.marker(
                [48.029233, -4.644453],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_fb5e0475886ee99349171d61e1a53b2e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_70a9d83f38be2924f55bfe5e530f1cc8.setIcon(icon_fb5e0475886ee99349171d61e1a53b2e);
        
    
        var popup_e5407fe4d57a439c736ee74038ac9eb5 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a12da84af8cd5346e8e1db2778c5088a = $(`&lt;div id=&quot;html_a12da84af8cd5346e8e1db2778c5088a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  TORAMUR &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 135000 €&lt;/div&gt;`)[0];
            popup_e5407fe4d57a439c736ee74038ac9eb5.setContent(html_a12da84af8cd5346e8e1db2778c5088a);
        

        marker_70a9d83f38be2924f55bfe5e530f1cc8.bindPopup(popup_e5407fe4d57a439c736ee74038ac9eb5)
        ;

        
    
    
            var marker_582ef4425d7194c28555e24a8a25131d = L.marker(
                [48.028687, -4.64324],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_c89174dc012b3f6bbb3107f661a5b0fe = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_582ef4425d7194c28555e24a8a25131d.setIcon(icon_c89174dc012b3f6bbb3107f661a5b0fe);
        
    
        var popup_6a2a6237e3c6c9ccc47750971da02618 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_4d510ffd9b5dad92f0739bc63ef49ffc = $(`&lt;div id=&quot;html_4d510ffd9b5dad92f0739bc63ef49ffc&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERINGAR &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 470 €&lt;/div&gt;`)[0];
            popup_6a2a6237e3c6c9ccc47750971da02618.setContent(html_4d510ffd9b5dad92f0739bc63ef49ffc);
        

        marker_582ef4425d7194c28555e24a8a25131d.bindPopup(popup_6a2a6237e3c6c9ccc47750971da02618)
        ;

        
    
    
            var marker_cb3de8988ad46146a2c3ab56ef4e3a1e = L.marker(
                [48.028761, -4.64309],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_3bd75a942210cac9708bdb4552c021b5 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_cb3de8988ad46146a2c3ab56ef4e3a1e.setIcon(icon_3bd75a942210cac9708bdb4552c021b5);
        
    
        var popup_3fc85bafd614f5c032ac22e4024784a8 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2917af001c52f248777b7a10c2d36c21 = $(`&lt;div id=&quot;html_2917af001c52f248777b7a10c2d36c21&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERINGAR &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 300 €&lt;/div&gt;`)[0];
            popup_3fc85bafd614f5c032ac22e4024784a8.setContent(html_2917af001c52f248777b7a10c2d36c21);
        

        marker_cb3de8988ad46146a2c3ab56ef4e3a1e.bindPopup(popup_3fc85bafd614f5c032ac22e4024784a8)
        ;

        
    
    
            var marker_cec808a250a10322660f5c600250eff1 = L.marker(
                [48.028075, -4.642873],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_c6cf8fa39e7a3fc8666684f0b1f7ecf4 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_cec808a250a10322660f5c600250eff1.setIcon(icon_c6cf8fa39e7a3fc8666684f0b1f7ecf4);
        
    
        var popup_78d2a946c654ad79cba64eb8a882c402 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c99c262646db9372efba6627a93a9370 = $(`&lt;div id=&quot;html_c99c262646db9372efba6627a93a9370&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERINGAR &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 252 €&lt;/div&gt;`)[0];
            popup_78d2a946c654ad79cba64eb8a882c402.setContent(html_c99c262646db9372efba6627a93a9370);
        

        marker_cec808a250a10322660f5c600250eff1.bindPopup(popup_78d2a946c654ad79cba64eb8a882c402)
        ;

        
    
    
            var marker_e696fe23e4834730cf1ad3fffcd28b73 = L.marker(
                [48.028192, -4.659539],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d4744886c497ab2b2b2bd01611de6be1 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_e696fe23e4834730cf1ad3fffcd28b73.setIcon(icon_d4744886c497ab2b2b2bd01611de6be1);
        
    
        var popup_c4cd2a89d7187f0c02ea65b6996f00c2 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ea8953b72597abdc9b48052ba7f8897f = $(`&lt;div id=&quot;html_ea8953b72597abdc9b48052ba7f8897f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 627 PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 80000 €&lt;/div&gt;`)[0];
            popup_c4cd2a89d7187f0c02ea65b6996f00c2.setContent(html_ea8953b72597abdc9b48052ba7f8897f);
        

        marker_e696fe23e4834730cf1ad3fffcd28b73.bindPopup(popup_c4cd2a89d7187f0c02ea65b6996f00c2)
        ;

        
    
    
            var marker_a0f61b50f0966f0371252318c5182fc1 = L.marker(
                [48.027647, -4.660189],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_dbacea0378bd561ca1f00fab6909eff8 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_a0f61b50f0966f0371252318c5182fc1.setIcon(icon_dbacea0378bd561ca1f00fab6909eff8);
        
    
        var popup_d729ec67aee7ce9f0a03049c4c55d134 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_29af69238a0f3974ae847aad27c6e838 = $(`&lt;div id=&quot;html_29af69238a0f3974ae847aad27c6e838&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 624 MAURICE BARLIER &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 132000 €&lt;/div&gt;`)[0];
            popup_d729ec67aee7ce9f0a03049c4c55d134.setContent(html_29af69238a0f3974ae847aad27c6e838);
        

        marker_a0f61b50f0966f0371252318c5182fc1.bindPopup(popup_d729ec67aee7ce9f0a03049c4c55d134)
        ;

        
    
    
            var marker_2dd606db00e5aa7a65faec20b145bf47 = L.marker(
                [48.02761, -4.660153],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_007623a97ead4ac86d5154bbc47007a6 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_2dd606db00e5aa7a65faec20b145bf47.setIcon(icon_007623a97ead4ac86d5154bbc47007a6);
        
    
        var popup_922fb27642853278b89a58a640cfc6d5 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_04f1494448e58ecd32c9991310b46bc8 = $(`&lt;div id=&quot;html_04f1494448e58ecd32c9991310b46bc8&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 132000 €&lt;/div&gt;`)[0];
            popup_922fb27642853278b89a58a640cfc6d5.setContent(html_04f1494448e58ecd32c9991310b46bc8);
        

        marker_2dd606db00e5aa7a65faec20b145bf47.bindPopup(popup_922fb27642853278b89a58a640cfc6d5)
        ;

        
    
    
            var marker_f84c92b32c15a6ac8c1f05f362abee00 = L.marker(
                [48.02761, -4.660153],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_bbad9e4a8b39293c28749f40a327fed6 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_f84c92b32c15a6ac8c1f05f362abee00.setIcon(icon_bbad9e4a8b39293c28749f40a327fed6);
        
    
        var popup_2e07de85434904b7115bf18df7f5be25 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_aaf0279cc9b7dc8c2cd187434d2e14d2 = $(`&lt;div id=&quot;html_aaf0279cc9b7dc8c2cd187434d2e14d2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 132000 €&lt;/div&gt;`)[0];
            popup_2e07de85434904b7115bf18df7f5be25.setContent(html_aaf0279cc9b7dc8c2cd187434d2e14d2);
        

        marker_f84c92b32c15a6ac8c1f05f362abee00.bindPopup(popup_2e07de85434904b7115bf18df7f5be25)
        ;

        
    
    
            var marker_99a0ba4cc565fffafab76f2131c5d064 = L.marker(
                [48.027649, -4.660502],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_3ee16db8286f6124e5c4c68d1eaa0c6a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_99a0ba4cc565fffafab76f2131c5d064.setIcon(icon_3ee16db8286f6124e5c4c68d1eaa0c6a);
        
    
        var popup_a6bd286a6cf43b83c26e7f82e3b1f8dd = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_206c88389c9fb86c32ee39ea5dd96852 = $(`&lt;div id=&quot;html_206c88389c9fb86c32ee39ea5dd96852&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 132000 €&lt;/div&gt;`)[0];
            popup_a6bd286a6cf43b83c26e7f82e3b1f8dd.setContent(html_206c88389c9fb86c32ee39ea5dd96852);
        

        marker_99a0ba4cc565fffafab76f2131c5d064.bindPopup(popup_a6bd286a6cf43b83c26e7f82e3b1f8dd)
        ;

        
    
    
            var marker_7c7b886250d8f054359d4cd00319685e = L.marker(
                [48.027566, -4.659833],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_e81b76dec358ad87a431e63d40df33bd = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_7c7b886250d8f054359d4cd00319685e.setIcon(icon_e81b76dec358ad87a431e63d40df33bd);
        
    
        var popup_07367a3d62f8926984da2a7c40bdddc5 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_f1e30a58e7d363b2ff7cd8edc11d7687 = $(`&lt;div id=&quot;html_f1e30a58e7d363b2ff7cd8edc11d7687&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 319714 €&lt;/div&gt;`)[0];
            popup_07367a3d62f8926984da2a7c40bdddc5.setContent(html_f1e30a58e7d363b2ff7cd8edc11d7687);
        

        marker_7c7b886250d8f054359d4cd00319685e.bindPopup(popup_07367a3d62f8926984da2a7c40bdddc5)
        ;

        
    
    
            var marker_e05aa517c315065913b386da460e48c6 = L.marker(
                [48.027423, -4.659046],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_907015d669a01345f46cc8a4e9d3ee7c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_e05aa517c315065913b386da460e48c6.setIcon(icon_907015d669a01345f46cc8a4e9d3ee7c);
        
    
        var popup_b2b94777e70de250cd6af7b34a353ec5 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_bd62cbee91b27b1bfdb49e9aa1ebe280 = $(`&lt;div id=&quot;html_bd62cbee91b27b1bfdb49e9aa1ebe280&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 20420 €&lt;/div&gt;`)[0];
            popup_b2b94777e70de250cd6af7b34a353ec5.setContent(html_bd62cbee91b27b1bfdb49e9aa1ebe280);
        

        marker_e05aa517c315065913b386da460e48c6.bindPopup(popup_b2b94777e70de250cd6af7b34a353ec5)
        ;

        
    
    
            var marker_2d2c048af733a405227005ae600d1c6e = L.marker(
                [48.027025, -4.659069],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_0aee5a67b330acee1efbd4cfc0a29057 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_2d2c048af733a405227005ae600d1c6e.setIcon(icon_0aee5a67b330acee1efbd4cfc0a29057);
        
    
        var popup_0e8f97138b2f9cbc69ab1fcfcb9b1f24 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_59f779325bbf07e6f9d65742e32215e9 = $(`&lt;div id=&quot;html_59f779325bbf07e6f9d65742e32215e9&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 20420 €&lt;/div&gt;`)[0];
            popup_0e8f97138b2f9cbc69ab1fcfcb9b1f24.setContent(html_59f779325bbf07e6f9d65742e32215e9);
        

        marker_2d2c048af733a405227005ae600d1c6e.bindPopup(popup_0e8f97138b2f9cbc69ab1fcfcb9b1f24)
        ;

        
    
    
            var marker_6162ab28dfc3c0347e24f72fc26ccccd = L.marker(
                [48.027795, -4.658928],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d8a9586eb931dd7587461387d3da48fb = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_6162ab28dfc3c0347e24f72fc26ccccd.setIcon(icon_d8a9586eb931dd7587461387d3da48fb);
        
    
        var popup_25c8bdaf35fb42b35ef5fa21fd749de3 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_965ea062cc17311c2ae69f7aa19c67f1 = $(`&lt;div id=&quot;html_965ea062cc17311c2ae69f7aa19c67f1&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 319714 €&lt;/div&gt;`)[0];
            popup_25c8bdaf35fb42b35ef5fa21fd749de3.setContent(html_965ea062cc17311c2ae69f7aa19c67f1);
        

        marker_6162ab28dfc3c0347e24f72fc26ccccd.bindPopup(popup_25c8bdaf35fb42b35ef5fa21fd749de3)
        ;

        
    
    
            var marker_8e00f88393f2bb584d04de5123c8f516 = L.marker(
                [48.027795, -4.658928],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_3c3213150e4d9691bbf7f96859b41ef3 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_8e00f88393f2bb584d04de5123c8f516.setIcon(icon_3c3213150e4d9691bbf7f96859b41ef3);
        
    
        var popup_3146d102bdc1e8167bebaacc44121a4a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8e9dc43cbb1a76400d9216cf41278b89 = $(`&lt;div id=&quot;html_8e9dc43cbb1a76400d9216cf41278b89&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 88236 €&lt;/div&gt;`)[0];
            popup_3146d102bdc1e8167bebaacc44121a4a.setContent(html_8e9dc43cbb1a76400d9216cf41278b89);
        

        marker_8e00f88393f2bb584d04de5123c8f516.bindPopup(popup_3146d102bdc1e8167bebaacc44121a4a)
        ;

        
    
    
            var marker_c77d9f93987b8bd9ce6f28f5e3ccd445 = L.marker(
                [48.027655, -4.658694],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_176cac0b0b80a80a6052524e3ccc4587 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_c77d9f93987b8bd9ce6f28f5e3ccd445.setIcon(icon_176cac0b0b80a80a6052524e3ccc4587);
        
    
        var popup_e7eed1821a3a257dcd2a49437728d3cd = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9038f912883f62c9ddc7ce883f84b168 = $(`&lt;div id=&quot;html_9038f912883f62c9ddc7ce883f84b168&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 70000 €&lt;/div&gt;`)[0];
            popup_e7eed1821a3a257dcd2a49437728d3cd.setContent(html_9038f912883f62c9ddc7ce883f84b168);
        

        marker_c77d9f93987b8bd9ce6f28f5e3ccd445.bindPopup(popup_e7eed1821a3a257dcd2a49437728d3cd)
        ;

        
    
    
            var marker_41bb863c7724c5a383cf9a7f6a18b0bd = L.marker(
                [48.02769, -4.658873],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d3c0dc1b87d2a56149f1122ac7bad778 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_41bb863c7724c5a383cf9a7f6a18b0bd.setIcon(icon_d3c0dc1b87d2a56149f1122ac7bad778);
        
    
        var popup_bc1fdd3343ad9054956523f493bf0876 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_33d2c1862fe9218bcc70cc77e670a6e6 = $(`&lt;div id=&quot;html_33d2c1862fe9218bcc70cc77e670a6e6&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 70000 €&lt;/div&gt;`)[0];
            popup_bc1fdd3343ad9054956523f493bf0876.setContent(html_33d2c1862fe9218bcc70cc77e670a6e6);
        

        marker_41bb863c7724c5a383cf9a7f6a18b0bd.bindPopup(popup_bc1fdd3343ad9054956523f493bf0876)
        ;

        
    
    
            var marker_495f8a1d816f560ac4c3cf033e78e253 = L.marker(
                [48.027744, -4.659922],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_048241813160d9111e92fb226cf4eb2a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_495f8a1d816f560ac4c3cf033e78e253.setIcon(icon_048241813160d9111e92fb226cf4eb2a);
        
    
        var popup_dae9723110a991eab8a874af26ea506e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ba356a4ec585a25de1af6f97fe196d2d = $(`&lt;div id=&quot;html_ba356a4ec585a25de1af6f97fe196d2d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 319714 €&lt;/div&gt;`)[0];
            popup_dae9723110a991eab8a874af26ea506e.setContent(html_ba356a4ec585a25de1af6f97fe196d2d);
        

        marker_495f8a1d816f560ac4c3cf033e78e253.bindPopup(popup_dae9723110a991eab8a874af26ea506e)
        ;

        
    
    
            var marker_6aa8ab8fed3099f92aec2a214171e4ae = L.marker(
                [48.027675, -4.65945],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_4014c34b2ceaba6211a133594baf6f0b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_6aa8ab8fed3099f92aec2a214171e4ae.setIcon(icon_4014c34b2ceaba6211a133594baf6f0b);
        
    
        var popup_e123163ac41bbaf1bafd2aa43adcee0e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2f50bce5f0f9e79827e25a50f9fda500 = $(`&lt;div id=&quot;html_2f50bce5f0f9e79827e25a50f9fda500&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 88236 €&lt;/div&gt;`)[0];
            popup_e123163ac41bbaf1bafd2aa43adcee0e.setContent(html_2f50bce5f0f9e79827e25a50f9fda500);
        

        marker_6aa8ab8fed3099f92aec2a214171e4ae.bindPopup(popup_e123163ac41bbaf1bafd2aa43adcee0e)
        ;

        
    
    
            var marker_48c6a195be97c82e947d0124166ad865 = L.marker(
                [48.027479, -4.659153],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_adf15dab4f4e27f309e2aea5f419602a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_48c6a195be97c82e947d0124166ad865.setIcon(icon_adf15dab4f4e27f309e2aea5f419602a);
        
    
        var popup_edbaa267265171173728445f41a84bfc = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_b535d920307180c1750f3e1661273f28 = $(`&lt;div id=&quot;html_b535d920307180c1750f3e1661273f28&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 20420 €&lt;/div&gt;`)[0];
            popup_edbaa267265171173728445f41a84bfc.setContent(html_b535d920307180c1750f3e1661273f28);
        

        marker_48c6a195be97c82e947d0124166ad865.bindPopup(popup_edbaa267265171173728445f41a84bfc)
        ;

        
    
    
            var marker_828cbe0d9ff8c07f25a804b85a8802d6 = L.marker(
                [48.027548, -4.659151],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_82f69747cf101013ecd96c35cc6429f5 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_828cbe0d9ff8c07f25a804b85a8802d6.setIcon(icon_82f69747cf101013ecd96c35cc6429f5);
        
    
        var popup_a3da9cba35ce19a8a703b6bce2b64c1c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_6825acc15b69a45c48d91108668fe6b4 = $(`&lt;div id=&quot;html_6825acc15b69a45c48d91108668fe6b4&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 20420 €&lt;/div&gt;`)[0];
            popup_a3da9cba35ce19a8a703b6bce2b64c1c.setContent(html_6825acc15b69a45c48d91108668fe6b4);
        

        marker_828cbe0d9ff8c07f25a804b85a8802d6.bindPopup(popup_a3da9cba35ce19a8a703b6bce2b64c1c)
        ;

        
    
    
            var marker_ac926dae3e44cd82aeaaf87c57eadd9e = L.marker(
                [48.027683, -4.659608],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_e5084b1034d0c40fef6e0b442e7150f9 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ac926dae3e44cd82aeaaf87c57eadd9e.setIcon(icon_e5084b1034d0c40fef6e0b442e7150f9);
        
    
        var popup_1ce9532b6225d1621ccac148672ad35e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_3c3a6d6009c1f38374011ff6ceac1dd2 = $(`&lt;div id=&quot;html_3c3a6d6009c1f38374011ff6ceac1dd2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 88236 €&lt;/div&gt;`)[0];
            popup_1ce9532b6225d1621ccac148672ad35e.setContent(html_3c3a6d6009c1f38374011ff6ceac1dd2);
        

        marker_ac926dae3e44cd82aeaaf87c57eadd9e.bindPopup(popup_1ce9532b6225d1621ccac148672ad35e)
        ;

        
    
    
            var marker_64f706b63e2614809ca925e376b528bc = L.marker(
                [48.029572, -4.658726],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_6a96b39495ea47ce74cdfc1ba5d3e898 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_64f706b63e2614809ca925e376b528bc.setIcon(icon_6a96b39495ea47ce74cdfc1ba5d3e898);
        
    
        var popup_2fb465bfdc6c0b7ff323596934b723d4 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e6935ea1f528198a7054daf736b8c990 = $(`&lt;div id=&quot;html_e6935ea1f528198a7054daf736b8c990&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 6750 €&lt;/div&gt;`)[0];
            popup_2fb465bfdc6c0b7ff323596934b723d4.setContent(html_e6935ea1f528198a7054daf736b8c990);
        

        marker_64f706b63e2614809ca925e376b528bc.bindPopup(popup_2fb465bfdc6c0b7ff323596934b723d4)
        ;

        
    
    
            var marker_3873b341dcdbf09f89da7ee062d6c916 = L.marker(
                [48.029572, -4.658726],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_f0f223e3ec67064d9bc21abb613244ed = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_3873b341dcdbf09f89da7ee062d6c916.setIcon(icon_f0f223e3ec67064d9bc21abb613244ed);
        
    
        var popup_7653d119eab68ef04d3041b7d3b54929 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_b42afa76d9a1d7e6a9d737fc10af520d = $(`&lt;div id=&quot;html_b42afa76d9a1d7e6a9d737fc10af520d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 6680 €&lt;/div&gt;`)[0];
            popup_7653d119eab68ef04d3041b7d3b54929.setContent(html_b42afa76d9a1d7e6a9d737fc10af520d);
        

        marker_3873b341dcdbf09f89da7ee062d6c916.bindPopup(popup_7653d119eab68ef04d3041b7d3b54929)
        ;

        
    
    
            var marker_2baa8348a12aa7923f4e6c3db2e1db54 = L.marker(
                [48.02952, -4.658273],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_af4b94d36a898adbedd9440d7a497f0d = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_2baa8348a12aa7923f4e6c3db2e1db54.setIcon(icon_af4b94d36a898adbedd9440d7a497f0d);
        
    
        var popup_9c9ddefb7265894244ace59129f94e1f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_305e8ce641e0d3e757ea7d8a24ec0bc7 = $(`&lt;div id=&quot;html_305e8ce641e0d3e757ea7d8a24ec0bc7&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 643 JOLIOT CURIE &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 100000 €&lt;/div&gt;`)[0];
            popup_9c9ddefb7265894244ace59129f94e1f.setContent(html_305e8ce641e0d3e757ea7d8a24ec0bc7);
        

        marker_2baa8348a12aa7923f4e6c3db2e1db54.bindPopup(popup_9c9ddefb7265894244ace59129f94e1f)
        ;

        
    
    
            var marker_a9973eec0b7a597d4ce2d1f4c0d51a0d = L.marker(
                [48.02942, -4.657944],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_88be67a807b8f99ad340e27bc9a76c65 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_a9973eec0b7a597d4ce2d1f4c0d51a0d.setIcon(icon_88be67a807b8f99ad340e27bc9a76c65);
        
    
        var popup_bfdff5dbf6141dd3771ce680415cd423 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_14df423a454a7c661738fdc9723aa613 = $(`&lt;div id=&quot;html_14df423a454a7c661738fdc9723aa613&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 642 JOLIOT CURIE &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 108000 €&lt;/div&gt;`)[0];
            popup_bfdff5dbf6141dd3771ce680415cd423.setContent(html_14df423a454a7c661738fdc9723aa613);
        

        marker_a9973eec0b7a597d4ce2d1f4c0d51a0d.bindPopup(popup_bfdff5dbf6141dd3771ce680415cd423)
        ;

        
    
    
            var marker_e1d9c4e8b2eb3e64a6e51b6b4f9fd319 = L.marker(
                [48.029433, -4.657617],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_753fd48a173c46055c5740737b8a9d97 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_e1d9c4e8b2eb3e64a6e51b6b4f9fd319.setIcon(icon_753fd48a173c46055c5740737b8a9d97);
        
    
        var popup_8721a0d8d31f0ce50d72df02e23be7a4 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7a00a5c34fe4bce54e01d1920868f085 = $(`&lt;div id=&quot;html_7a00a5c34fe4bce54e01d1920868f085&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 108000 €&lt;/div&gt;`)[0];
            popup_8721a0d8d31f0ce50d72df02e23be7a4.setContent(html_7a00a5c34fe4bce54e01d1920868f085);
        

        marker_e1d9c4e8b2eb3e64a6e51b6b4f9fd319.bindPopup(popup_8721a0d8d31f0ce50d72df02e23be7a4)
        ;

        
    
    
            var marker_35ea51806cba5307b403f0847068af27 = L.marker(
                [48.029721, -4.657327],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_34c7b142730f62af5f20fba7e5abc3a5 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_35ea51806cba5307b403f0847068af27.setIcon(icon_34c7b142730f62af5f20fba7e5abc3a5);
        
    
        var popup_4bc91abf582b4547421d8f96cf9f6414 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_91a0693133e3e524487c388992beeea4 = $(`&lt;div id=&quot;html_91a0693133e3e524487c388992beeea4&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 1500 €&lt;/div&gt;`)[0];
            popup_4bc91abf582b4547421d8f96cf9f6414.setContent(html_91a0693133e3e524487c388992beeea4);
        

        marker_35ea51806cba5307b403f0847068af27.bindPopup(popup_4bc91abf582b4547421d8f96cf9f6414)
        ;

        
    
    
            var marker_634d05a2b90d6ef60afd6206769905db = L.marker(
                [48.029753, -4.652942],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_173ce7c3afcf881189d01f71dd7df954 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_634d05a2b90d6ef60afd6206769905db.setIcon(icon_173ce7c3afcf881189d01f71dd7df954);
        
    
        var popup_45b9a7e15fe72440f21c3f7f07344981 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_80211d28e8a3c9b23096378c5034cacc = $(`&lt;div id=&quot;html_80211d28e8a3c9b23096378c5034cacc&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 698 KERGROAS &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 216400 €&lt;/div&gt;`)[0];
            popup_45b9a7e15fe72440f21c3f7f07344981.setContent(html_80211d28e8a3c9b23096378c5034cacc);
        

        marker_634d05a2b90d6ef60afd6206769905db.bindPopup(popup_45b9a7e15fe72440f21c3f7f07344981)
        ;

        
    
    
            var marker_34db0af5737d0e3895bfae30376d2a8e = L.marker(
                [48.029434, -4.652941],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_ab6ef449dac200c290148eba1bfe7dfa = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_34db0af5737d0e3895bfae30376d2a8e.setIcon(icon_ab6ef449dac200c290148eba1bfe7dfa);
        
    
        var popup_5649905584604e08cfcc5371618fd716 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d8aecdeaabeeb3c63be12fafbd3a5f2b = $(`&lt;div id=&quot;html_d8aecdeaabeeb3c63be12fafbd3a5f2b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGROAS &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 216400 €&lt;/div&gt;`)[0];
            popup_5649905584604e08cfcc5371618fd716.setContent(html_d8aecdeaabeeb3c63be12fafbd3a5f2b);
        

        marker_34db0af5737d0e3895bfae30376d2a8e.bindPopup(popup_5649905584604e08cfcc5371618fd716)
        ;

        
    
    
            var marker_85e7afba792ff51a2390c66f1ce4a51a = L.marker(
                [48.029533, -4.652801],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_7addf7f7edf391af6182793a319f1cd7 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_85e7afba792ff51a2390c66f1ce4a51a.setIcon(icon_7addf7f7edf391af6182793a319f1cd7);
        
    
        var popup_c749fcad48e0d83fbba387d68c33e226 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_327b1d76e7805c2b62c23a7d35de24dd = $(`&lt;div id=&quot;html_327b1d76e7805c2b62c23a7d35de24dd&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGROAS &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 216400 €&lt;/div&gt;`)[0];
            popup_c749fcad48e0d83fbba387d68c33e226.setContent(html_327b1d76e7805c2b62c23a7d35de24dd);
        

        marker_85e7afba792ff51a2390c66f1ce4a51a.bindPopup(popup_c749fcad48e0d83fbba387d68c33e226)
        ;

        
    
    
            var marker_bc8913b2594aa43e330e838ce4ffd482 = L.marker(
                [48.029117, -4.653558],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_f1ff5d5ecf2326830be6a541f6d26864 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_bc8913b2594aa43e330e838ce4ffd482.setIcon(icon_f1ff5d5ecf2326830be6a541f6d26864);
        
    
        var popup_f0643e29f694d901fdcebd10b64e4174 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_fdc682ad3033197ad7067b13a1062160 = $(`&lt;div id=&quot;html_fdc682ad3033197ad7067b13a1062160&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGROAS &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 665 €&lt;/div&gt;`)[0];
            popup_f0643e29f694d901fdcebd10b64e4174.setContent(html_fdc682ad3033197ad7067b13a1062160);
        

        marker_bc8913b2594aa43e330e838ce4ffd482.bindPopup(popup_f0643e29f694d901fdcebd10b64e4174)
        ;

        
    
    
            var marker_d923cadb6144b5d731f4234913523202 = L.marker(
                [48.028654, -4.65709],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_b001896f4527e133986d74e03042f124 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_d923cadb6144b5d731f4234913523202.setIcon(icon_b001896f4527e133986d74e03042f124);
        
    
        var popup_3da4f39b2db2d76b48bf80b7db49cce7 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7212e424312f79d8dd0a571bb4c584ab = $(`&lt;div id=&quot;html_7212e424312f79d8dd0a571bb4c584ab&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 20000 €&lt;/div&gt;`)[0];
            popup_3da4f39b2db2d76b48bf80b7db49cce7.setContent(html_7212e424312f79d8dd0a571bb4c584ab);
        

        marker_d923cadb6144b5d731f4234913523202.bindPopup(popup_3da4f39b2db2d76b48bf80b7db49cce7)
        ;

        
    
    
            var marker_6974b91647ee71f97017a7bcaaf5c989 = L.marker(
                [48.02875, -4.657401],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_67bfe19a28c9036b8fad2be5feb8bdbb = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_6974b91647ee71f97017a7bcaaf5c989.setIcon(icon_67bfe19a28c9036b8fad2be5feb8bdbb);
        
    
        var popup_63aaded65703a0c70b813733b5835b35 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d8d75f54776a222099b26230c1a0dfb3 = $(`&lt;div id=&quot;html_d8d75f54776a222099b26230c1a0dfb3&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 639 JOLIOT CURIE &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 20000 €&lt;/div&gt;`)[0];
            popup_63aaded65703a0c70b813733b5835b35.setContent(html_d8d75f54776a222099b26230c1a0dfb3);
        

        marker_6974b91647ee71f97017a7bcaaf5c989.bindPopup(popup_63aaded65703a0c70b813733b5835b35)
        ;

        
    
    
            var marker_30bfd064190d49cb3f6280bbcd925509 = L.marker(
                [48.028419, -4.658882],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_7d30fb705d400d8dbb7a2e896bf1e23f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_30bfd064190d49cb3f6280bbcd925509.setIcon(icon_7d30fb705d400d8dbb7a2e896bf1e23f);
        
    
        var popup_9b37af191c13400c6e1727638d662bd9 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_71689c81da18cc8f1744c512abaa838f = $(`&lt;div id=&quot;html_71689c81da18cc8f1744c512abaa838f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 659 LOUIS PASTEUR &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 110000 €&lt;/div&gt;`)[0];
            popup_9b37af191c13400c6e1727638d662bd9.setContent(html_71689c81da18cc8f1744c512abaa838f);
        

        marker_30bfd064190d49cb3f6280bbcd925509.bindPopup(popup_9b37af191c13400c6e1727638d662bd9)
        ;

        
    
    
            var marker_816f6aa8a8a08ab8a52ec7ab1838dbd1 = L.marker(
                [48.029315, -4.658641],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_725147240d84bf4ed1b6275b826c5088 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_816f6aa8a8a08ab8a52ec7ab1838dbd1.setIcon(icon_725147240d84bf4ed1b6275b826c5088);
        
    
        var popup_1e49a18b08d8a32cf052c8d50c870fba = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1ee7e445de833c71b6680105a0f94874 = $(`&lt;div id=&quot;html_1ee7e445de833c71b6680105a0f94874&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 649 LAENNEC &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 107000 €&lt;/div&gt;`)[0];
            popup_1e49a18b08d8a32cf052c8d50c870fba.setContent(html_1ee7e445de833c71b6680105a0f94874);
        

        marker_816f6aa8a8a08ab8a52ec7ab1838dbd1.bindPopup(popup_1e49a18b08d8a32cf052c8d50c870fba)
        ;

        
    
    
            var marker_e271ddff61af918a196ab8fa16ccacba = L.marker(
                [48.029245, -4.658772],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_46f293477930dbe5f70a621d7dd15744 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_e271ddff61af918a196ab8fa16ccacba.setIcon(icon_46f293477930dbe5f70a621d7dd15744);
        
    
        var popup_91b1571fcf8bd13e8e4035fd51a52f9f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1408f581524a4164d9e03d7bc2cbe726 = $(`&lt;div id=&quot;html_1408f581524a4164d9e03d7bc2cbe726&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 107000 €&lt;/div&gt;`)[0];
            popup_91b1571fcf8bd13e8e4035fd51a52f9f.setContent(html_1408f581524a4164d9e03d7bc2cbe726);
        

        marker_e271ddff61af918a196ab8fa16ccacba.bindPopup(popup_91b1571fcf8bd13e8e4035fd51a52f9f)
        ;

        
    
    
            var marker_74281f098fc753db3e0f961bd32672ee = L.marker(
                [48.029119, -4.658788],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d9f23aa968edcc6c67fb1fb6ad2c0205 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_74281f098fc753db3e0f961bd32672ee.setIcon(icon_d9f23aa968edcc6c67fb1fb6ad2c0205);
        
    
        var popup_6f48deec403ba4137e3354f924c2aa68 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_b08bca211f8a5b0871be647dd7c5598a = $(`&lt;div id=&quot;html_b08bca211f8a5b0871be647dd7c5598a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 651 LAENNEC &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 100000 €&lt;/div&gt;`)[0];
            popup_6f48deec403ba4137e3354f924c2aa68.setContent(html_b08bca211f8a5b0871be647dd7c5598a);
        

        marker_74281f098fc753db3e0f961bd32672ee.bindPopup(popup_6f48deec403ba4137e3354f924c2aa68)
        ;

        
    
    
            var marker_eb7fec3ac7723c5b172e8730d2c19905 = L.marker(
                [48.028909, -4.659106],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_81da10937e5ce840c02306a61d0edccb = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_eb7fec3ac7723c5b172e8730d2c19905.setIcon(icon_81da10937e5ce840c02306a61d0edccb);
        
    
        var popup_77bc13fbeec33b8310403d90d183ab4e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_158d80547989f45b4556288d0ab0ca9f = $(`&lt;div id=&quot;html_158d80547989f45b4556288d0ab0ca9f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 657 HONNORE D ESTIENNE D ORVES &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 106250 €&lt;/div&gt;`)[0];
            popup_77bc13fbeec33b8310403d90d183ab4e.setContent(html_158d80547989f45b4556288d0ab0ca9f);
        

        marker_eb7fec3ac7723c5b172e8730d2c19905.bindPopup(popup_77bc13fbeec33b8310403d90d183ab4e)
        ;

        
    
    
            var marker_bcdc2e4df2bc93f8f86cfdfa29d96c5f = L.marker(
                [48.029546, -4.658881],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_031f56447aa8ed1a0dc0d78972af4c6a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_bcdc2e4df2bc93f8f86cfdfa29d96c5f.setIcon(icon_031f56447aa8ed1a0dc0d78972af4c6a);
        
    
        var popup_eb8741b33be0349a19e722a5979d4d51 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_89319c3d4d79b34b27da2d3896498b54 = $(`&lt;div id=&quot;html_89319c3d4d79b34b27da2d3896498b54&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 6750 €&lt;/div&gt;`)[0];
            popup_eb8741b33be0349a19e722a5979d4d51.setContent(html_89319c3d4d79b34b27da2d3896498b54);
        

        marker_bcdc2e4df2bc93f8f86cfdfa29d96c5f.bindPopup(popup_eb8741b33be0349a19e722a5979d4d51)
        ;

        
    
    
            var marker_98951d16ff5c7c95eeecbb14842f243a = L.marker(
                [48.029546, -4.658881],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_879bb6d0c7156d63945a189715b8d6fd = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_98951d16ff5c7c95eeecbb14842f243a.setIcon(icon_879bb6d0c7156d63945a189715b8d6fd);
        
    
        var popup_2e7b7e88ac2108dee7c338c05033c4cb = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e08b51d66d3c3cdaaaf3206ff92ec76f = $(`&lt;div id=&quot;html_e08b51d66d3c3cdaaaf3206ff92ec76f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 6680 €&lt;/div&gt;`)[0];
            popup_2e7b7e88ac2108dee7c338c05033c4cb.setContent(html_e08b51d66d3c3cdaaaf3206ff92ec76f);
        

        marker_98951d16ff5c7c95eeecbb14842f243a.bindPopup(popup_2e7b7e88ac2108dee7c338c05033c4cb)
        ;

        
    
    
            var marker_f0bba33441ccddbfb2183f627a338e11 = L.marker(
                [48.029523, -4.658906],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_0f3a436cf6e312bef330fe21ff53e887 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_f0bba33441ccddbfb2183f627a338e11.setIcon(icon_0f3a436cf6e312bef330fe21ff53e887);
        
    
        var popup_31bcf56a2e917c07dfcb7bd5138183cb = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ff07e9556816f66e000b8b400477a165 = $(`&lt;div id=&quot;html_ff07e9556816f66e000b8b400477a165&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 6750 €&lt;/div&gt;`)[0];
            popup_31bcf56a2e917c07dfcb7bd5138183cb.setContent(html_ff07e9556816f66e000b8b400477a165);
        

        marker_f0bba33441ccddbfb2183f627a338e11.bindPopup(popup_31bcf56a2e917c07dfcb7bd5138183cb)
        ;

        
    
    
            var marker_48337bbcb40022dc2d199362c42ab79b = L.marker(
                [48.029481, -4.658808],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_016b3c9947c571a72002cb2adeaa7068 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_48337bbcb40022dc2d199362c42ab79b.setIcon(icon_016b3c9947c571a72002cb2adeaa7068);
        
    
        var popup_622d3baf5ed55385273339a31f0758f2 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9e8fb2b6610f8b3b52309c12254d2b5a = $(`&lt;div id=&quot;html_9e8fb2b6610f8b3b52309c12254d2b5a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 6750 €&lt;/div&gt;`)[0];
            popup_622d3baf5ed55385273339a31f0758f2.setContent(html_9e8fb2b6610f8b3b52309c12254d2b5a);
        

        marker_48337bbcb40022dc2d199362c42ab79b.bindPopup(popup_622d3baf5ed55385273339a31f0758f2)
        ;

        
    
    
            var marker_f4ad66273d9879762abf12a22673dc62 = L.marker(
                [48.029481, -4.658808],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_e67a2eb2eab980172859963e0c3b0e2f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_f4ad66273d9879762abf12a22673dc62.setIcon(icon_e67a2eb2eab980172859963e0c3b0e2f);
        
    
        var popup_2739c9ca884ceb79c079ca79d780eb4f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7054112b41049b3f148d9f1e88335e3c = $(`&lt;div id=&quot;html_7054112b41049b3f148d9f1e88335e3c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 6680 €&lt;/div&gt;`)[0];
            popup_2739c9ca884ceb79c079ca79d780eb4f.setContent(html_7054112b41049b3f148d9f1e88335e3c);
        

        marker_f4ad66273d9879762abf12a22673dc62.bindPopup(popup_2739c9ca884ceb79c079ca79d780eb4f)
        ;

        
    
    
            var marker_ee4c075af04897c8dcff0215bafa6dcc = L.marker(
                [48.029477, -4.658876],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_bbf105a1850c4e34d6b69cee7576aa31 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ee4c075af04897c8dcff0215bafa6dcc.setIcon(icon_bbf105a1850c4e34d6b69cee7576aa31);
        
    
        var popup_fb450c5a7a5952eaf48519e1f561ca7c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_de744fd6b427cd493d5ffc079f17dc84 = $(`&lt;div id=&quot;html_de744fd6b427cd493d5ffc079f17dc84&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 6750 €&lt;/div&gt;`)[0];
            popup_fb450c5a7a5952eaf48519e1f561ca7c.setContent(html_de744fd6b427cd493d5ffc079f17dc84);
        

        marker_ee4c075af04897c8dcff0215bafa6dcc.bindPopup(popup_fb450c5a7a5952eaf48519e1f561ca7c)
        ;

        
    
    
            var marker_f2f44d263ea993ae2d2fec5bdd53314a = L.marker(
                [48.032356, -4.652551],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_8e588e3e1a927cccb9a510a9fc3d0f7b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_f2f44d263ea993ae2d2fec5bdd53314a.setIcon(icon_8e588e3e1a927cccb9a510a9fc3d0f7b);
        
    
        var popup_93ef6dea723732ba6807d0ef347f38b0 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_5a855162aa061856880630b957fc754b = $(`&lt;div id=&quot;html_5a855162aa061856880630b957fc754b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERVEN VIAN &lt;br&gt;Vente en 2019 &lt;br&gt;Prix 1200 €&lt;/div&gt;`)[0];
            popup_93ef6dea723732ba6807d0ef347f38b0.setContent(html_5a855162aa061856880630b957fc754b);
        

        marker_f2f44d263ea993ae2d2fec5bdd53314a.bindPopup(popup_93ef6dea723732ba6807d0ef347f38b0)
        ;

        
    
    
            var marker_b55810615f83ea9871fe0f8b4b421f83 = L.marker(
                [48.032596, -4.652771],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_488bb22171a5be36d61ebc9c9a32f3a3 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_b55810615f83ea9871fe0f8b4b421f83.setIcon(icon_488bb22171a5be36d61ebc9c9a32f3a3);
        
    
        var popup_a5e82838bbde3c05d27831ae52d5797c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_bb60ac15f62eb5bdfb429746a839519a = $(`&lt;div id=&quot;html_bb60ac15f62eb5bdfb429746a839519a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 693 KERVEN VIAN &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 50000 €&lt;/div&gt;`)[0];
            popup_a5e82838bbde3c05d27831ae52d5797c.setContent(html_bb60ac15f62eb5bdfb429746a839519a);
        

        marker_b55810615f83ea9871fe0f8b4b421f83.bindPopup(popup_a5e82838bbde3c05d27831ae52d5797c)
        ;

        
    
    
            var marker_23becb8c8f2264640ff0806fc93dd66c = L.marker(
                [48.032113, -4.651856],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_50f57ea00d1dbb8a45e042d412295a66 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_23becb8c8f2264640ff0806fc93dd66c.setIcon(icon_50f57ea00d1dbb8a45e042d412295a66);
        
    
        var popup_a0a42545eaf658c1849be6d5f659066c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_0c01538e7d047f1cd9da9d9f1daa49c7 = $(`&lt;div id=&quot;html_0c01538e7d047f1cd9da9d9f1daa49c7&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 704 KERVEN VIAN &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 73000 €&lt;/div&gt;`)[0];
            popup_a0a42545eaf658c1849be6d5f659066c.setContent(html_0c01538e7d047f1cd9da9d9f1daa49c7);
        

        marker_23becb8c8f2264640ff0806fc93dd66c.bindPopup(popup_a0a42545eaf658c1849be6d5f659066c)
        ;

        
    
    
            var marker_6ca2fa91a6c63106b782a7a20768cb58 = L.marker(
                [48.032113, -4.651856],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_1cc08d6100c555e0f7190bc9d6668b66 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_6ca2fa91a6c63106b782a7a20768cb58.setIcon(icon_1cc08d6100c555e0f7190bc9d6668b66);
        
    
        var popup_cbf4788b8ae83ed09a0d1afb310d47a1 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_577b44a0839b8461ef647e06ca93377b = $(`&lt;div id=&quot;html_577b44a0839b8461ef647e06ca93377b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 704 KERVEN VIAN &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 73000 €&lt;/div&gt;`)[0];
            popup_cbf4788b8ae83ed09a0d1afb310d47a1.setContent(html_577b44a0839b8461ef647e06ca93377b);
        

        marker_6ca2fa91a6c63106b782a7a20768cb58.bindPopup(popup_cbf4788b8ae83ed09a0d1afb310d47a1)
        ;

        
    
    
            var marker_d8748b5161e5a4eed809cef53457ac4a = L.marker(
                [48.031947, -4.652685],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_5a1458da862e3247a144f78476bd726d = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_d8748b5161e5a4eed809cef53457ac4a.setIcon(icon_5a1458da862e3247a144f78476bd726d);
        
    
        var popup_7bcac31a13621796da3f37d54797546e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a09ac7f05613ee2067f2c5bd8664c077 = $(`&lt;div id=&quot;html_a09ac7f05613ee2067f2c5bd8664c077&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERVEN VIAN &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 50000 €&lt;/div&gt;`)[0];
            popup_7bcac31a13621796da3f37d54797546e.setContent(html_a09ac7f05613ee2067f2c5bd8664c077);
        

        marker_d8748b5161e5a4eed809cef53457ac4a.bindPopup(popup_7bcac31a13621796da3f37d54797546e)
        ;

        
    
    
            var marker_4e72be9b2ec40028cf5e9a9f48b3cada = L.marker(
                [48.0323, -4.65293],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_506ec3770e41a7f1baaadf5fa31deb44 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_4e72be9b2ec40028cf5e9a9f48b3cada.setIcon(icon_506ec3770e41a7f1baaadf5fa31deb44);
        
    
        var popup_011c50d579e168b1c2ad35b6303e10f8 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_14e4ca185e5a9ce751f62c955b126ea0 = $(`&lt;div id=&quot;html_14e4ca185e5a9ce751f62c955b126ea0&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERVEN VIAN &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 50000 €&lt;/div&gt;`)[0];
            popup_011c50d579e168b1c2ad35b6303e10f8.setContent(html_14e4ca185e5a9ce751f62c955b126ea0);
        

        marker_4e72be9b2ec40028cf5e9a9f48b3cada.bindPopup(popup_011c50d579e168b1c2ad35b6303e10f8)
        ;

        
    
    
            var marker_77cccb9fd2f423551e7b24ce8a770cdd = L.marker(
                [48.032208, -4.653457],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_760b7cc3f1550e25d60e69b5a5e59fb4 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_77cccb9fd2f423551e7b24ce8a770cdd.setIcon(icon_760b7cc3f1550e25d60e69b5a5e59fb4);
        
    
        var popup_2d5d57e5e5d7520ecd0ae717bc9da664 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_f63d58f59e7e98c5d8e8fbf1d3a7d1a4 = $(`&lt;div id=&quot;html_f63d58f59e7e98c5d8e8fbf1d3a7d1a4&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERVEN VIAN &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 50000 €&lt;/div&gt;`)[0];
            popup_2d5d57e5e5d7520ecd0ae717bc9da664.setContent(html_f63d58f59e7e98c5d8e8fbf1d3a7d1a4);
        

        marker_77cccb9fd2f423551e7b24ce8a770cdd.bindPopup(popup_2d5d57e5e5d7520ecd0ae717bc9da664)
        ;

        
    
    
            var marker_acf51810a1d03acc4a123f89d1cfe946 = L.marker(
                [48.032126, -4.666187],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_3d10b0aba50d47e7a27f222a9513ae1a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_acf51810a1d03acc4a123f89d1cfe946.setIcon(icon_3d10b0aba50d47e7a27f222a9513ae1a);
        
    
        var popup_bb9b1360c3b94b2cbc73b43360dea94a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a9da488acd34fcb9d4e10ea07a249566 = $(`&lt;div id=&quot;html_a9da488acd34fcb9d4e10ea07a249566&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  CUPLEIS &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 135000 €&lt;/div&gt;`)[0];
            popup_bb9b1360c3b94b2cbc73b43360dea94a.setContent(html_a9da488acd34fcb9d4e10ea07a249566);
        

        marker_acf51810a1d03acc4a123f89d1cfe946.bindPopup(popup_bb9b1360c3b94b2cbc73b43360dea94a)
        ;

        
    
    
            var marker_0bc3b2297949a9a1f71013fab0602dcc = L.marker(
                [48.032322, -4.666146],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_c85688b96a5506f0fb26f1dcb5a81e28 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_0bc3b2297949a9a1f71013fab0602dcc.setIcon(icon_c85688b96a5506f0fb26f1dcb5a81e28);
        
    
        var popup_ffb73dbab83fb05693afb0f0f30a5608 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_dc9a69307bec8b9a4c1c1c5a74dce776 = $(`&lt;div id=&quot;html_dc9a69307bec8b9a4c1c1c5a74dce776&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 357 LE DREFF &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 135000 €&lt;/div&gt;`)[0];
            popup_ffb73dbab83fb05693afb0f0f30a5608.setContent(html_dc9a69307bec8b9a4c1c1c5a74dce776);
        

        marker_0bc3b2297949a9a1f71013fab0602dcc.bindPopup(popup_ffb73dbab83fb05693afb0f0f30a5608)
        ;

        
    
    
            var marker_16bb423f1bd5040993608d835ecc24ec = L.marker(
                [48.032069, -4.666006],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_0f81911afa697e651e816876f9ef333c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_16bb423f1bd5040993608d835ecc24ec.setIcon(icon_0f81911afa697e651e816876f9ef333c);
        
    
        var popup_1f0df6743374ead0c0775b2fa79837c6 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_5d2167209417a81105d569caab87ba37 = $(`&lt;div id=&quot;html_5d2167209417a81105d569caab87ba37&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  CUPLEIS &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 135000 €&lt;/div&gt;`)[0];
            popup_1f0df6743374ead0c0775b2fa79837c6.setContent(html_5d2167209417a81105d569caab87ba37);
        

        marker_16bb423f1bd5040993608d835ecc24ec.bindPopup(popup_1f0df6743374ead0c0775b2fa79837c6)
        ;

        
    
    
            var marker_7cca8e7cb55087ee04fff39c010dabb9 = L.marker(
                [48.032103, -4.663845],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_73876fd51f01a0b6afd9a91977caf4dd = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_7cca8e7cb55087ee04fff39c010dabb9.setIcon(icon_73876fd51f01a0b6afd9a91977caf4dd);
        
    
        var popup_7dcbfcd85a7c9b0566fb8245f8b5427d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_cd46a2313365560b276d767fe578c68b = $(`&lt;div id=&quot;html_cd46a2313365560b276d767fe578c68b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 1 DU 19 MARS 1962 &lt;br&gt;Vente en 2019 &lt;br&gt;Prix 235000 €&lt;/div&gt;`)[0];
            popup_7dcbfcd85a7c9b0566fb8245f8b5427d.setContent(html_cd46a2313365560b276d767fe578c68b);
        

        marker_7cca8e7cb55087ee04fff39c010dabb9.bindPopup(popup_7dcbfcd85a7c9b0566fb8245f8b5427d)
        ;

        
    
    
            var marker_f297f181b47c338a38a8c76977664458 = L.marker(
                [48.032103, -4.663845],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_f123000ba560d15a209b7463740a3436 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_f297f181b47c338a38a8c76977664458.setIcon(icon_f123000ba560d15a209b7463740a3436);
        
    
        var popup_d2564f39b37c8f554b470f7f5ee264e3 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7c7b036356d8ee39c63a36c0e8c022a2 = $(`&lt;div id=&quot;html_7c7b036356d8ee39c63a36c0e8c022a2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 1 DU 19 MARS 1962 &lt;br&gt;Vente en 2019 &lt;br&gt;Prix 235000 €&lt;/div&gt;`)[0];
            popup_d2564f39b37c8f554b470f7f5ee264e3.setContent(html_7c7b036356d8ee39c63a36c0e8c022a2);
        

        marker_f297f181b47c338a38a8c76977664458.bindPopup(popup_d2564f39b37c8f554b470f7f5ee264e3)
        ;

        
    
    
            var marker_ad83cb59444ad2f9fdd3314b145c4896 = L.marker(
                [48.032342, -4.663088],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_508420c776eec8e9dda4c98865b22a33 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ad83cb59444ad2f9fdd3314b145c4896.setIcon(icon_508420c776eec8e9dda4c98865b22a33);
        
    
        var popup_c8c9185d79b09a73a0318725858e059b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_f03c9bd12a98e339b47ca7aefdd24897 = $(`&lt;div id=&quot;html_f03c9bd12a98e339b47ca7aefdd24897&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 2 JEAN JAURES &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 138000 €&lt;/div&gt;`)[0];
            popup_c8c9185d79b09a73a0318725858e059b.setContent(html_f03c9bd12a98e339b47ca7aefdd24897);
        

        marker_ad83cb59444ad2f9fdd3314b145c4896.bindPopup(popup_c8c9185d79b09a73a0318725858e059b)
        ;

        
    
    
            var marker_28fb34b3c25dd0a5b68f8161d0e7a702 = L.marker(
                [48.029727, -4.659546],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_1f9a4cc949dd4589d93627586b60bf58 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_28fb34b3c25dd0a5b68f8161d0e7a702.setIcon(icon_1f9a4cc949dd4589d93627586b60bf58);
        
    
        var popup_9fa52ee5072673f4afc8ec7dcafefe60 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_921d5b3eb1ef2fd2914424a3bb40de27 = $(`&lt;div id=&quot;html_921d5b3eb1ef2fd2914424a3bb40de27&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 590 GEORGES CLEMENCEAU &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 76500 €&lt;/div&gt;`)[0];
            popup_9fa52ee5072673f4afc8ec7dcafefe60.setContent(html_921d5b3eb1ef2fd2914424a3bb40de27);
        

        marker_28fb34b3c25dd0a5b68f8161d0e7a702.bindPopup(popup_9fa52ee5072673f4afc8ec7dcafefe60)
        ;

        
    
    
            var marker_afe062096474b5beaf51f8cbedd9afa7 = L.marker(
                [48.03013, -4.66045],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_ade54bf55a64de46da0251969e57d91e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_afe062096474b5beaf51f8cbedd9afa7.setIcon(icon_ade54bf55a64de46da0251969e57d91e);
        
    
        var popup_63fca0645172addd3636ab4a602f6a6c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_80eef3d88cd7d1de8a313540a50ffe9f = $(`&lt;div id=&quot;html_80eef3d88cd7d1de8a313540a50ffe9f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 135000 €&lt;/div&gt;`)[0];
            popup_63fca0645172addd3636ab4a602f6a6c.setContent(html_80eef3d88cd7d1de8a313540a50ffe9f);
        

        marker_afe062096474b5beaf51f8cbedd9afa7.bindPopup(popup_63fca0645172addd3636ab4a602f6a6c)
        ;

        
    
    
            var marker_2975b6fc0798b4d71b330dd014ff782d = L.marker(
                [48.029818, -4.660633],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_9ae0508dd66791852bbf7ea9c28760c5 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_2975b6fc0798b4d71b330dd014ff782d.setIcon(icon_9ae0508dd66791852bbf7ea9c28760c5);
        
    
        var popup_1e904342ea66fc28fc46b71d79a72fa3 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d07f4dc8ab8e51a82e783b5868e736f9 = $(`&lt;div id=&quot;html_d07f4dc8ab8e51a82e783b5868e736f9&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 135000 €&lt;/div&gt;`)[0];
            popup_1e904342ea66fc28fc46b71d79a72fa3.setContent(html_d07f4dc8ab8e51a82e783b5868e736f9);
        

        marker_2975b6fc0798b4d71b330dd014ff782d.bindPopup(popup_1e904342ea66fc28fc46b71d79a72fa3)
        ;

        
    
    
            var marker_ba3c71edf264b15c4dad5e25cce0c55a = L.marker(
                [48.030162, -4.66053],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_9a2b2935b4bc479a854a85095107b441 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ba3c71edf264b15c4dad5e25cce0c55a.setIcon(icon_9a2b2935b4bc479a854a85095107b441);
        
    
        var popup_db821558de93e686b759464670165c6b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_3a6e33451dec0f7c400a336b5e694cb5 = $(`&lt;div id=&quot;html_3a6e33451dec0f7c400a336b5e694cb5&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 581 PENNEACH &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 135000 €&lt;/div&gt;`)[0];
            popup_db821558de93e686b759464670165c6b.setContent(html_3a6e33451dec0f7c400a336b5e694cb5);
        

        marker_ba3c71edf264b15c4dad5e25cce0c55a.bindPopup(popup_db821558de93e686b759464670165c6b)
        ;

        
    
    
            var marker_f58de59393f9d5c10d1dd90c8f727825 = L.marker(
                [48.03093, -4.660721],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_c3b2955bf4911606091e489399d74d03 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_f58de59393f9d5c10d1dd90c8f727825.setIcon(icon_c3b2955bf4911606091e489399d74d03);
        
    
        var popup_3986415c285767d0350e115728fcdda6 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_5f1fa85576b5195e479ecee439f0c9e5 = $(`&lt;div id=&quot;html_5f1fa85576b5195e479ecee439f0c9e5&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGREIS &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 15000 €&lt;/div&gt;`)[0];
            popup_3986415c285767d0350e115728fcdda6.setContent(html_5f1fa85576b5195e479ecee439f0c9e5);
        

        marker_f58de59393f9d5c10d1dd90c8f727825.bindPopup(popup_3986415c285767d0350e115728fcdda6)
        ;

        
    
    
            var marker_1df5989d463d74b27e64d24a06ca76bd = L.marker(
                [48.03116, -4.6605],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_11f957e5f2fee66911213b7f0a2b001a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_1df5989d463d74b27e64d24a06ca76bd.setIcon(icon_11f957e5f2fee66911213b7f0a2b001a);
        
    
        var popup_d4c80a4f158bf9df09fa5f8bbf49a7c3 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c77c7ab131647dc2d77392c899af496a = $(`&lt;div id=&quot;html_c77c7ab131647dc2d77392c899af496a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 15000 €&lt;/div&gt;`)[0];
            popup_d4c80a4f158bf9df09fa5f8bbf49a7c3.setContent(html_c77c7ab131647dc2d77392c899af496a);
        

        marker_1df5989d463d74b27e64d24a06ca76bd.bindPopup(popup_d4c80a4f158bf9df09fa5f8bbf49a7c3)
        ;

        
    
    
            var marker_47b416990a9754bee47720f3daed27be = L.marker(
                [48.029724, -4.659167],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_6f1198785cb442db528404f70a4e846e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_47b416990a9754bee47720f3daed27be.setIcon(icon_6f1198785cb442db528404f70a4e846e);
        
    
        var popup_865ef6ea5dcc0ae22c2266b85882b03a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ee339f452486f4e385c020b632547efa = $(`&lt;div id=&quot;html_ee339f452486f4e385c020b632547efa&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 1442 €&lt;/div&gt;`)[0];
            popup_865ef6ea5dcc0ae22c2266b85882b03a.setContent(html_ee339f452486f4e385c020b632547efa);
        

        marker_47b416990a9754bee47720f3daed27be.bindPopup(popup_865ef6ea5dcc0ae22c2266b85882b03a)
        ;

        
    
    
            var marker_6da10c4c6da95c0aaea79cd3dd19725e = L.marker(
                [48.029486, -4.660628],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_61c132a118eed21227eec0e23d44b31d = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_6da10c4c6da95c0aaea79cd3dd19725e.setIcon(icon_61c132a118eed21227eec0e23d44b31d);
        
    
        var popup_3eeafdfac15044ca79465e4882225777 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9c6f5ea36e1761081fa29dc9586e5c8a = $(`&lt;div id=&quot;html_9c6f5ea36e1761081fa29dc9586e5c8a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 28990 €&lt;/div&gt;`)[0];
            popup_3eeafdfac15044ca79465e4882225777.setContent(html_9c6f5ea36e1761081fa29dc9586e5c8a);
        

        marker_6da10c4c6da95c0aaea79cd3dd19725e.bindPopup(popup_3eeafdfac15044ca79465e4882225777)
        ;

        
    
    
            var marker_e6c051ea682db92d4a89418d02c23b97 = L.marker(
                [48.029486, -4.660628],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_9e4e19f1eab2ec25dbada3d1c53d2c93 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_e6c051ea682db92d4a89418d02c23b97.setIcon(icon_9e4e19f1eab2ec25dbada3d1c53d2c93);
        
    
        var popup_3340d6c1e84320849ce5f37b190296e2 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_5314019768ac2da07b97c0ddb62f58ef = $(`&lt;div id=&quot;html_5314019768ac2da07b97c0ddb62f58ef&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 28990 €&lt;/div&gt;`)[0];
            popup_3340d6c1e84320849ce5f37b190296e2.setContent(html_5314019768ac2da07b97c0ddb62f58ef);
        

        marker_e6c051ea682db92d4a89418d02c23b97.bindPopup(popup_3340d6c1e84320849ce5f37b190296e2)
        ;

        
    
    
            var marker_039fe889b9bf732684955dbcb3c27f67 = L.marker(
                [48.029495, -4.660315],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_f92485579ecaf35747469b532957325a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_039fe889b9bf732684955dbcb3c27f67.setIcon(icon_f92485579ecaf35747469b532957325a);
        
    
        var popup_c71052fef472d1052d68568875735480 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_90cbe5bcef056def1aa125359e7b5b72 = $(`&lt;div id=&quot;html_90cbe5bcef056def1aa125359e7b5b72&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 600 YANN LUIS DOORNIK &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 28990 €&lt;/div&gt;`)[0];
            popup_c71052fef472d1052d68568875735480.setContent(html_90cbe5bcef056def1aa125359e7b5b72);
        

        marker_039fe889b9bf732684955dbcb3c27f67.bindPopup(popup_c71052fef472d1052d68568875735480)
        ;

        
    
    
            var marker_ae32ff6e86add68cc9d02bf7c9b30fd2 = L.marker(
                [48.0293, -4.659491],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_393bad9e63cfd87873faa9707e26f364 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ae32ff6e86add68cc9d02bf7c9b30fd2.setIcon(icon_393bad9e63cfd87873faa9707e26f364);
        
    
        var popup_2fe1cacad30cf471b846c824365be446 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_500d02ac93d4f6ee6733b656cfddd0fe = $(`&lt;div id=&quot;html_500d02ac93d4f6ee6733b656cfddd0fe&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 608 GEORGES CLEMENCEAU &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 55000 €&lt;/div&gt;`)[0];
            popup_2fe1cacad30cf471b846c824365be446.setContent(html_500d02ac93d4f6ee6733b656cfddd0fe);
        

        marker_ae32ff6e86add68cc9d02bf7c9b30fd2.bindPopup(popup_2fe1cacad30cf471b846c824365be446)
        ;

        
    
    
            var marker_ec5b034b10f2b4b64ef48ad404fd8c4e = L.marker(
                [48.028878, -4.659509],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_1fdcf84f15d2c2c3e35a5b809c75b581 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ec5b034b10f2b4b64ef48ad404fd8c4e.setIcon(icon_1fdcf84f15d2c2c3e35a5b809c75b581);
        
    
        var popup_04fc7a6fbb9569d8d08974614310a061 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7b5c920644d2e98180615f438a0d38fa = $(`&lt;div id=&quot;html_7b5c920644d2e98180615f438a0d38fa&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 77000 €&lt;/div&gt;`)[0];
            popup_04fc7a6fbb9569d8d08974614310a061.setContent(html_7b5c920644d2e98180615f438a0d38fa);
        

        marker_ec5b034b10f2b4b64ef48ad404fd8c4e.bindPopup(popup_04fc7a6fbb9569d8d08974614310a061)
        ;

        
    
    
            var marker_b263ac7c3e6606328d90851658154531 = L.marker(
                [48.029027, -4.659334],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_61f175ebe723cb9b65a9b45d3df23591 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_b263ac7c3e6606328d90851658154531.setIcon(icon_61f175ebe723cb9b65a9b45d3df23591);
        
    
        var popup_de7874e4612bfe9a43fb1367a3bd1345 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ec77cee0ae5d294415c39e3bcd779797 = $(`&lt;div id=&quot;html_ec77cee0ae5d294415c39e3bcd779797&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 610 HONNORE D ESTIENNE D ORVES &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 77000 €&lt;/div&gt;`)[0];
            popup_de7874e4612bfe9a43fb1367a3bd1345.setContent(html_ec77cee0ae5d294415c39e3bcd779797);
        

        marker_b263ac7c3e6606328d90851658154531.bindPopup(popup_de7874e4612bfe9a43fb1367a3bd1345)
        ;

        
    
    
            var marker_c368a10b513884a0f8b09c0f8039c3aa = L.marker(
                [48.028546, -4.659414],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_a7cd0c6698029dfe893743c6d27dac93 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_c368a10b513884a0f8b09c0f8039c3aa.setIcon(icon_a7cd0c6698029dfe893743c6d27dac93);
        
    
        var popup_5b8e366becf29d3d1019969dc65c7a16 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_f00c73929f37937f9689b462b6765fb0 = $(`&lt;div id=&quot;html_f00c73929f37937f9689b462b6765fb0&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 100000 €&lt;/div&gt;`)[0];
            popup_5b8e366becf29d3d1019969dc65c7a16.setContent(html_f00c73929f37937f9689b462b6765fb0);
        

        marker_c368a10b513884a0f8b09c0f8039c3aa.bindPopup(popup_5b8e366becf29d3d1019969dc65c7a16)
        ;

        
    
    
            var marker_7d5f738c1e738bacbb83952fcced4e19 = L.marker(
                [48.029293, -4.660225],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d14ae76a6639c1f4f1114148f78171e5 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_7d5f738c1e738bacbb83952fcced4e19.setIcon(icon_d14ae76a6639c1f4f1114148f78171e5);
        
    
        var popup_c09694159b3a0206e25a8c459f8300e8 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_db6edf816f821d5f458acdf5868997b2 = $(`&lt;div id=&quot;html_db6edf816f821d5f458acdf5868997b2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 602 YANN LUIS DOORNIK &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 20000 €&lt;/div&gt;`)[0];
            popup_c09694159b3a0206e25a8c459f8300e8.setContent(html_db6edf816f821d5f458acdf5868997b2);
        

        marker_7d5f738c1e738bacbb83952fcced4e19.bindPopup(popup_c09694159b3a0206e25a8c459f8300e8)
        ;

        
    
    
            var marker_829c010bf59fad32991c0cb367bc4f4f = L.marker(
                [48.029276, -4.660376],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_c697e79b530e3d34e4752fab1ce7e566 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_829c010bf59fad32991c0cb367bc4f4f.setIcon(icon_c697e79b530e3d34e4752fab1ce7e566);
        
    
        var popup_4017b9b3e79d3f28f7bb01989eee3ac9 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_56a0b225345dadfc10d5275dd931c75d = $(`&lt;div id=&quot;html_56a0b225345dadfc10d5275dd931c75d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 601 YANN LUIS DOORNIK &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 35000 €&lt;/div&gt;`)[0];
            popup_4017b9b3e79d3f28f7bb01989eee3ac9.setContent(html_56a0b225345dadfc10d5275dd931c75d);
        

        marker_829c010bf59fad32991c0cb367bc4f4f.bindPopup(popup_4017b9b3e79d3f28f7bb01989eee3ac9)
        ;

        
    
    
            var marker_91840bfb9cee006e76daad7b0a60b0af = L.marker(
                [48.029275, -4.66055],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_c11f7fe13ba1261f78d15626f5b0e95a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_91840bfb9cee006e76daad7b0a60b0af.setIcon(icon_c11f7fe13ba1261f78d15626f5b0e95a);
        
    
        var popup_30d9e5c11210f19f627af974cbab7897 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9dba0e79caffdb8ba3aced56f501d117 = $(`&lt;div id=&quot;html_9dba0e79caffdb8ba3aced56f501d117&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 200000 €&lt;/div&gt;`)[0];
            popup_30d9e5c11210f19f627af974cbab7897.setContent(html_9dba0e79caffdb8ba3aced56f501d117);
        

        marker_91840bfb9cee006e76daad7b0a60b0af.bindPopup(popup_30d9e5c11210f19f627af974cbab7897)
        ;

        
    
    
            var marker_60b943d1f925f7271a9d8438c8b0f9b7 = L.marker(
                [48.029015, -4.660849],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_a444974a3963372b6132018ca75ec39e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_60b943d1f925f7271a9d8438c8b0f9b7.setIcon(icon_a444974a3963372b6132018ca75ec39e);
        
    
        var popup_f3e626bcfee6bd4c4a0926a87ec350f3 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_0661875fb881d33183234570222ff2f7 = $(`&lt;div id=&quot;html_0661875fb881d33183234570222ff2f7&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 200000 €&lt;/div&gt;`)[0];
            popup_f3e626bcfee6bd4c4a0926a87ec350f3.setContent(html_0661875fb881d33183234570222ff2f7);
        

        marker_60b943d1f925f7271a9d8438c8b0f9b7.bindPopup(popup_f3e626bcfee6bd4c4a0926a87ec350f3)
        ;

        
    
    
            var marker_179e0a75fc750d6eac10db1876d5d758 = L.marker(
                [48.028032, -4.661616],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d62714dc52204d6287a9ddc0a92bfb83 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_179e0a75fc750d6eac10db1876d5d758.setIcon(icon_d62714dc52204d6287a9ddc0a92bfb83);
        
    
        var popup_6615fa1947b75ebf424163a590cff036 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_725ac0e74958f8711542df76f609e170 = $(`&lt;div id=&quot;html_725ac0e74958f8711542df76f609e170&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 617 PENNEACH &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 120000 €&lt;/div&gt;`)[0];
            popup_6615fa1947b75ebf424163a590cff036.setContent(html_725ac0e74958f8711542df76f609e170);
        

        marker_179e0a75fc750d6eac10db1876d5d758.bindPopup(popup_6615fa1947b75ebf424163a590cff036)
        ;

        
    
    
            var marker_acf508127921a6b2f2ddeea19e81f2ef = L.marker(
                [48.029302, -4.660764],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_92d50c03209e2cb09f756678368b3d0f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_acf508127921a6b2f2ddeea19e81f2ef.setIcon(icon_92d50c03209e2cb09f756678368b3d0f);
        
    
        var popup_ea53dfdcd11fbe10ad2712b143b45166 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_57dde0e4e4c80d331adb1fbbe384aad2 = $(`&lt;div id=&quot;html_57dde0e4e4c80d331adb1fbbe384aad2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 600 YANN LUIS DOORNIK &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 200000 €&lt;/div&gt;`)[0];
            popup_ea53dfdcd11fbe10ad2712b143b45166.setContent(html_57dde0e4e4c80d331adb1fbbe384aad2);
        

        marker_acf508127921a6b2f2ddeea19e81f2ef.bindPopup(popup_ea53dfdcd11fbe10ad2712b143b45166)
        ;

        
    
    
            var marker_8fd3a55c5335dd566335757ceab0fdc8 = L.marker(
                [48.029197, -4.660775],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_1e2e3b8eb142536ce2c9ac0658abca90 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_8fd3a55c5335dd566335757ceab0fdc8.setIcon(icon_1e2e3b8eb142536ce2c9ac0658abca90);
        
    
        var popup_aecf898a4187e6d3a9048d68419093d2 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_4caeb1295840f9571c69ee499f58a333 = $(`&lt;div id=&quot;html_4caeb1295840f9571c69ee499f58a333&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENNEACH &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 200000 €&lt;/div&gt;`)[0];
            popup_aecf898a4187e6d3a9048d68419093d2.setContent(html_4caeb1295840f9571c69ee499f58a333);
        

        marker_8fd3a55c5335dd566335757ceab0fdc8.bindPopup(popup_aecf898a4187e6d3a9048d68419093d2)
        ;

        
    
    
            var marker_e7c3d51b40b1a6d713a476cfa87803fe = L.marker(
                [48.037475, -4.671169],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_10151b3f870d764fd72fd17ec18e2eb3 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_e7c3d51b40b1a6d713a476cfa87803fe.setIcon(icon_10151b3f870d764fd72fd17ec18e2eb3);
        
    
        var popup_55d34a6e721ca89505fd5f2a39590080 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_edeeb5f6f6dc9925ab882c375e527626 = $(`&lt;div id=&quot;html_edeeb5f6f6dc9925ab882c375e527626&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERISBLEIS &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 2300 €&lt;/div&gt;`)[0];
            popup_55d34a6e721ca89505fd5f2a39590080.setContent(html_edeeb5f6f6dc9925ab882c375e527626);
        

        marker_e7c3d51b40b1a6d713a476cfa87803fe.bindPopup(popup_55d34a6e721ca89505fd5f2a39590080)
        ;

        
    
    
            var marker_5b97110b3790d6cd89c3695fb6449a5e = L.marker(
                [48.036994, -4.670194],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_4aaf21b5274c474a4a79d4aff23e90ad = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_5b97110b3790d6cd89c3695fb6449a5e.setIcon(icon_4aaf21b5274c474a4a79d4aff23e90ad);
        
    
        var popup_df1bbb0f66142f2b491ca8a96f502422 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_22832f2afa24acf3651c34663210c8a0 = $(`&lt;div id=&quot;html_22832f2afa24acf3651c34663210c8a0&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 9 BEL AIR &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 95000 €&lt;/div&gt;`)[0];
            popup_df1bbb0f66142f2b491ca8a96f502422.setContent(html_22832f2afa24acf3651c34663210c8a0);
        

        marker_5b97110b3790d6cd89c3695fb6449a5e.bindPopup(popup_df1bbb0f66142f2b491ca8a96f502422)
        ;

        
    
    
            var marker_5507f431cdc76e5adbc9c68f2a703efc = L.marker(
                [48.037585, -4.670302],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d999206145a9ca03030b30cd4d2e211a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_5507f431cdc76e5adbc9c68f2a703efc.setIcon(icon_d999206145a9ca03030b30cd4d2e211a);
        
    
        var popup_667539c3ce1cbae3d29a4387c59adf06 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d964395d14d9b33e89ca9f8c09e2ec97 = $(`&lt;div id=&quot;html_d964395d14d9b33e89ca9f8c09e2ec97&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 413 BIGORN &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 85000 €&lt;/div&gt;`)[0];
            popup_667539c3ce1cbae3d29a4387c59adf06.setContent(html_d964395d14d9b33e89ca9f8c09e2ec97);
        

        marker_5507f431cdc76e5adbc9c68f2a703efc.bindPopup(popup_667539c3ce1cbae3d29a4387c59adf06)
        ;

        
    
    
            var marker_288cfacb96327f121e3f88de0f52d4fd = L.marker(
                [48.035438, -4.666074],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_e01ccfce338aa7282be5e27b8a097c4d = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_288cfacb96327f121e3f88de0f52d4fd.setIcon(icon_e01ccfce338aa7282be5e27b8a097c4d);
        
    
        var popup_37f1172075a8188a93b519191c782cca = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_b99d19ecab5f4875ab27cb4431ca4877 = $(`&lt;div id=&quot;html_b99d19ecab5f4875ab27cb4431ca4877&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 328 LESTRIVIN &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 40000 €&lt;/div&gt;`)[0];
            popup_37f1172075a8188a93b519191c782cca.setContent(html_b99d19ecab5f4875ab27cb4431ca4877);
        

        marker_288cfacb96327f121e3f88de0f52d4fd.bindPopup(popup_37f1172075a8188a93b519191c782cca)
        ;

        
    
    
            var marker_d367df899d686787180c063c50cf4c44 = L.marker(
                [48.031937, -4.667835],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_487ac78e442b0386ed31fd10fd729ffd = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_d367df899d686787180c063c50cf4c44.setIcon(icon_487ac78e442b0386ed31fd10fd729ffd);
        
    
        var popup_a39e162d18bd7c56cb01d1be5aa34f32 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_89ee5abfc56cbd6f6645baa0979ffde5 = $(`&lt;div id=&quot;html_89ee5abfc56cbd6f6645baa0979ffde5&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE DREFF &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 1730 €&lt;/div&gt;`)[0];
            popup_a39e162d18bd7c56cb01d1be5aa34f32.setContent(html_89ee5abfc56cbd6f6645baa0979ffde5);
        

        marker_d367df899d686787180c063c50cf4c44.bindPopup(popup_a39e162d18bd7c56cb01d1be5aa34f32)
        ;

        
    
    
            var marker_1e702f932e94b5177353c03055033cbe = L.marker(
                [48.032216, -4.669539],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_c94c056d78df8184a413888d650a8fce = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_1e702f932e94b5177353c03055033cbe.setIcon(icon_c94c056d78df8184a413888d650a8fce);
        
    
        var popup_e673ce9d9fe768f20874be8ee7f7b64e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e37c9b3123870830aee2544a5ef7eaa1 = $(`&lt;div id=&quot;html_e37c9b3123870830aee2544a5ef7eaa1&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE DREFF &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 16864 €&lt;/div&gt;`)[0];
            popup_e673ce9d9fe768f20874be8ee7f7b64e.setContent(html_e37c9b3123870830aee2544a5ef7eaa1);
        

        marker_1e702f932e94b5177353c03055033cbe.bindPopup(popup_e673ce9d9fe768f20874be8ee7f7b64e)
        ;

        
    
    
            var marker_f4f41d50e963aeb5adc68537258b9a29 = L.marker(
                [48.032194, -4.668708],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_7a62602efe4af0fd004e5b90add6d4c7 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_f4f41d50e963aeb5adc68537258b9a29.setIcon(icon_7a62602efe4af0fd004e5b90add6d4c7);
        
    
        var popup_88239aaf033a1202b54c72be978d4c77 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e6579d7da546193c0bc525f308c6249c = $(`&lt;div id=&quot;html_e6579d7da546193c0bc525f308c6249c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE DREFF &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 48500 €&lt;/div&gt;`)[0];
            popup_88239aaf033a1202b54c72be978d4c77.setContent(html_e6579d7da546193c0bc525f308c6249c);
        

        marker_f4f41d50e963aeb5adc68537258b9a29.bindPopup(popup_88239aaf033a1202b54c72be978d4c77)
        ;

        
    
    
            var marker_6291c4cc38debab55ec0a5f43fd76b4d = L.marker(
                [48.032227, -4.669234],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_564d645000b92f1bc6acb612fccbab54 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_6291c4cc38debab55ec0a5f43fd76b4d.setIcon(icon_564d645000b92f1bc6acb612fccbab54);
        
    
        var popup_8893c914be16f9d280dc400d2f8be59f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8bbe7c572c969d8f147fcc93f0f641fa = $(`&lt;div id=&quot;html_8bbe7c572c969d8f147fcc93f0f641fa&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5063 LE DREFF &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 156500 €&lt;/div&gt;`)[0];
            popup_8893c914be16f9d280dc400d2f8be59f.setContent(html_8bbe7c572c969d8f147fcc93f0f641fa);
        

        marker_6291c4cc38debab55ec0a5f43fd76b4d.bindPopup(popup_8893c914be16f9d280dc400d2f8be59f)
        ;

        
    
    
            var marker_a7623dd3a36d74f63470393ae2e0e44d = L.marker(
                [48.032227, -4.669234],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_9484cdca9775efba70b7e232f48c406e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_a7623dd3a36d74f63470393ae2e0e44d.setIcon(icon_9484cdca9775efba70b7e232f48c406e);
        
    
        var popup_cad4a8b4b07e479d0f12b764c13aedf6 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7d8745581ea8b54c1a300534519c1579 = $(`&lt;div id=&quot;html_7d8745581ea8b54c1a300534519c1579&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5063 LE DREFF &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 156500 €&lt;/div&gt;`)[0];
            popup_cad4a8b4b07e479d0f12b764c13aedf6.setContent(html_7d8745581ea8b54c1a300534519c1579);
        

        marker_a7623dd3a36d74f63470393ae2e0e44d.bindPopup(popup_cad4a8b4b07e479d0f12b764c13aedf6)
        ;

        
    
    
            var marker_d1246ed4c0ed8b2b9b5d6577cf926ba8 = L.marker(
                [48.035868, -4.665483],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_56816273e29486939183d180876a7d10 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_d1246ed4c0ed8b2b9b5d6577cf926ba8.setIcon(icon_56816273e29486939183d180876a7d10);
        
    
        var popup_85c36049e611baa546954b36752f4485 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_0b0733d8abd1582f0c9ed1701511cecd = $(`&lt;div id=&quot;html_0b0733d8abd1582f0c9ed1701511cecd&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 324 LESTRIVIN &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 75000 €&lt;/div&gt;`)[0];
            popup_85c36049e611baa546954b36752f4485.setContent(html_0b0733d8abd1582f0c9ed1701511cecd);
        

        marker_d1246ed4c0ed8b2b9b5d6577cf926ba8.bindPopup(popup_85c36049e611baa546954b36752f4485)
        ;

        
    
    
            var marker_54a54789dadd1ce2961e89bd962dbdb9 = L.marker(
                [48.031773, -4.668096],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_8491923ed3c477dc9f9bc3144e28846f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_54a54789dadd1ce2961e89bd962dbdb9.setIcon(icon_8491923ed3c477dc9f9bc3144e28846f);
        
    
        var popup_15caed467456dd9f3bf5fc682f56a841 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_170b43e590f948f22783556678abae91 = $(`&lt;div id=&quot;html_170b43e590f948f22783556678abae91&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE DREFF &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 40000 €&lt;/div&gt;`)[0];
            popup_15caed467456dd9f3bf5fc682f56a841.setContent(html_170b43e590f948f22783556678abae91);
        

        marker_54a54789dadd1ce2961e89bd962dbdb9.bindPopup(popup_15caed467456dd9f3bf5fc682f56a841)
        ;

        
    
    
            var marker_e893f003645faecb15adb1728233353b = L.marker(
                [48.031754, -4.668504],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_ae1cc643a1982f60cbac3d0b73790f0a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_e893f003645faecb15adb1728233353b.setIcon(icon_ae1cc643a1982f60cbac3d0b73790f0a);
        
    
        var popup_5d42775cf3c0831fc8e1c044c0fe5875 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_226f543fca0a0bea4df62ed334e76fff = $(`&lt;div id=&quot;html_226f543fca0a0bea4df62ed334e76fff&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE DREFF &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 200 €&lt;/div&gt;`)[0];
            popup_5d42775cf3c0831fc8e1c044c0fe5875.setContent(html_226f543fca0a0bea4df62ed334e76fff);
        

        marker_e893f003645faecb15adb1728233353b.bindPopup(popup_5d42775cf3c0831fc8e1c044c0fe5875)
        ;

        
    
    
            var marker_4ab18822de267dc2313befacced211f0 = L.marker(
                [48.032476, -4.668501],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_a421a2495cacb17a510ffd532081c1a8 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_4ab18822de267dc2313befacced211f0.setIcon(icon_a421a2495cacb17a510ffd532081c1a8);
        
    
        var popup_ce375f871f12e9ac5ea0d26c043064d9 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_b51d62cf646b1a9bd3d98e836f13d1fb = $(`&lt;div id=&quot;html_b51d62cf646b1a9bd3d98e836f13d1fb&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE DREFF &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 55000 €&lt;/div&gt;`)[0];
            popup_ce375f871f12e9ac5ea0d26c043064d9.setContent(html_b51d62cf646b1a9bd3d98e836f13d1fb);
        

        marker_4ab18822de267dc2313befacced211f0.bindPopup(popup_ce375f871f12e9ac5ea0d26c043064d9)
        ;

        
    
    
            var marker_c0e74e70836a76252dce722d42e42cfe = L.marker(
                [48.032028, -4.668305],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_00d8489f3855465e18c7381b133fca5f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_c0e74e70836a76252dce722d42e42cfe.setIcon(icon_00d8489f3855465e18c7381b133fca5f);
        
    
        var popup_67bd3a62fc1066439c740fafb93abeaa = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_61155a40f1167a2fe8af7b0309b8814e = $(`&lt;div id=&quot;html_61155a40f1167a2fe8af7b0309b8814e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE DREFF &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 200 €&lt;/div&gt;`)[0];
            popup_67bd3a62fc1066439c740fafb93abeaa.setContent(html_61155a40f1167a2fe8af7b0309b8814e);
        

        marker_c0e74e70836a76252dce722d42e42cfe.bindPopup(popup_67bd3a62fc1066439c740fafb93abeaa)
        ;

        
    
    
            var marker_03eeb429e75bd2e9638d19d63d2397f5 = L.marker(
                [48.032104, -4.667031],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_6f7e8560a19976aec6cef87889c7f88d = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_03eeb429e75bd2e9638d19d63d2397f5.setIcon(icon_6f7e8560a19976aec6cef87889c7f88d);
        
    
        var popup_2ee25ce4f555fab557a5c4121bf6b63b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_07b725bc26baea29f72c47575dc75d6e = $(`&lt;div id=&quot;html_07b725bc26baea29f72c47575dc75d6e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE DREFF &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 1380 €&lt;/div&gt;`)[0];
            popup_2ee25ce4f555fab557a5c4121bf6b63b.setContent(html_07b725bc26baea29f72c47575dc75d6e);
        

        marker_03eeb429e75bd2e9638d19d63d2397f5.bindPopup(popup_2ee25ce4f555fab557a5c4121bf6b63b)
        ;

        
    
    
            var marker_cbf6d4cbf4f60754540ca02a45f8f17e = L.marker(
                [48.03204, -4.667037],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_74acfdbb78d75910b85d77147b8a353c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_cbf6d4cbf4f60754540ca02a45f8f17e.setIcon(icon_74acfdbb78d75910b85d77147b8a353c);
        
    
        var popup_504c02239a66d44a6feca1cb2d6cbc3d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1567f3e79d3ee44d17c24953eb32e243 = $(`&lt;div id=&quot;html_1567f3e79d3ee44d17c24953eb32e243&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE DREFF &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 1272 €&lt;/div&gt;`)[0];
            popup_504c02239a66d44a6feca1cb2d6cbc3d.setContent(html_1567f3e79d3ee44d17c24953eb32e243);
        

        marker_cbf6d4cbf4f60754540ca02a45f8f17e.bindPopup(popup_504c02239a66d44a6feca1cb2d6cbc3d)
        ;

        
    
    
            var marker_d0575d141f2d667407a85638187dac4e = L.marker(
                [48.032065, -4.66746],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_39df1e332fdc711816cb84b3620c93a6 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_d0575d141f2d667407a85638187dac4e.setIcon(icon_39df1e332fdc711816cb84b3620c93a6);
        
    
        var popup_feb27eb400656a9a19392658cd4b53ee = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_4c57a42e8546dd113daf59926bc8bbe6 = $(`&lt;div id=&quot;html_4c57a42e8546dd113daf59926bc8bbe6&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE DREFF &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 1554 €&lt;/div&gt;`)[0];
            popup_feb27eb400656a9a19392658cd4b53ee.setContent(html_4c57a42e8546dd113daf59926bc8bbe6);
        

        marker_d0575d141f2d667407a85638187dac4e.bindPopup(popup_feb27eb400656a9a19392658cd4b53ee)
        ;

        
    
    
            var marker_47beb41a3a5cacd75c640c1ff4ca0b5e = L.marker(
                [48.032029, -4.667945],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_a3e8c568bcd415663bef1b6c9b818a5b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_47beb41a3a5cacd75c640c1ff4ca0b5e.setIcon(icon_a3e8c568bcd415663bef1b6c9b818a5b);
        
    
        var popup_722cf43ef317ea1359900904cd9dab0f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_6a0696bd10fbf4b56aaab3aa53f1a3ad = $(`&lt;div id=&quot;html_6a0696bd10fbf4b56aaab3aa53f1a3ad&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE DREFF &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 912 €&lt;/div&gt;`)[0];
            popup_722cf43ef317ea1359900904cd9dab0f.setContent(html_6a0696bd10fbf4b56aaab3aa53f1a3ad);
        

        marker_47beb41a3a5cacd75c640c1ff4ca0b5e.bindPopup(popup_722cf43ef317ea1359900904cd9dab0f)
        ;

        
    
    
            var marker_77e97a320ffbe142f4f241752e3af207 = L.marker(
                [48.035466, -4.668009],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_7f53a33c525b7044906b471e1d87164c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_77e97a320ffbe142f4f241752e3af207.setIcon(icon_7f53a33c525b7044906b471e1d87164c);
        
    
        var popup_a9bfb87a20b509207e79b27be59cc56e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9305da5f667b0e79c987525f9770e461 = $(`&lt;div id=&quot;html_9305da5f667b0e79c987525f9770e461&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE BOURG &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 23940 €&lt;/div&gt;`)[0];
            popup_a9bfb87a20b509207e79b27be59cc56e.setContent(html_9305da5f667b0e79c987525f9770e461);
        

        marker_77e97a320ffbe142f4f241752e3af207.bindPopup(popup_a9bfb87a20b509207e79b27be59cc56e)
        ;

        
    
    
            var marker_ed035c41c3403757a4f7899ef9851d5f = L.marker(
                [48.035173, -4.667774],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_14a4761df05084b1daed592712dba763 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ed035c41c3403757a4f7899ef9851d5f.setIcon(icon_14a4761df05084b1daed592712dba763);
        
    
        var popup_2f58bc8ea6b52af3be6f39de98b86478 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_10ae806d37804df0e3c22706d4a749d8 = $(`&lt;div id=&quot;html_10ae806d37804df0e3c22706d4a749d8&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE BOURG &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 24500 €&lt;/div&gt;`)[0];
            popup_2f58bc8ea6b52af3be6f39de98b86478.setContent(html_10ae806d37804df0e3c22706d4a749d8);
        

        marker_ed035c41c3403757a4f7899ef9851d5f.bindPopup(popup_2f58bc8ea6b52af3be6f39de98b86478)
        ;

        
    
    
            var marker_9574e54d2463319f039090d3c2547d08 = L.marker(
                [48.035277, -4.666479],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_c10f173656c15ed20cc18b22f631a153 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_9574e54d2463319f039090d3c2547d08.setIcon(icon_c10f173656c15ed20cc18b22f631a153);
        
    
        var popup_5ce2a44f43982e184bcf33a7eda90232 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_0046ea0cf106b6be7302c86be8967cf8 = $(`&lt;div id=&quot;html_0046ea0cf106b6be7302c86be8967cf8&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE BOURG &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 1370 €&lt;/div&gt;`)[0];
            popup_5ce2a44f43982e184bcf33a7eda90232.setContent(html_0046ea0cf106b6be7302c86be8967cf8);
        

        marker_9574e54d2463319f039090d3c2547d08.bindPopup(popup_5ce2a44f43982e184bcf33a7eda90232)
        ;

        
    
    
            var marker_998bd8c96479df7fc06ee5a1ba19a429 = L.marker(
                [48.031809, -4.667808],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_2282b567ea8fb6798affb95d7ebb975c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_998bd8c96479df7fc06ee5a1ba19a429.setIcon(icon_2282b567ea8fb6798affb95d7ebb975c);
        
    
        var popup_380b7203225fb900eabc59e4d293a2a8 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c2924c5aaaec176bccf9d2fd49142006 = $(`&lt;div id=&quot;html_c2924c5aaaec176bccf9d2fd49142006&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 2 STANG AR GUER &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 6460 €&lt;/div&gt;`)[0];
            popup_380b7203225fb900eabc59e4d293a2a8.setContent(html_c2924c5aaaec176bccf9d2fd49142006);
        

        marker_998bd8c96479df7fc06ee5a1ba19a429.bindPopup(popup_380b7203225fb900eabc59e4d293a2a8)
        ;

        
    
    
            var marker_3a1ee8f5d9a10ed12ef1f37dbd48e62d = L.marker(
                [48.037175, -4.675032],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_edd68d60254d8e5cee92a1c099e74ca9 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_3a1ee8f5d9a10ed12ef1f37dbd48e62d.setIcon(icon_edd68d60254d8e5cee92a1c099e74ca9);
        
    
        var popup_0d29bbb9fe59951a80339955ffcebf8d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d86b859211ebf1218bb52a87b208548d = $(`&lt;div id=&quot;html_d86b859211ebf1218bb52a87b208548d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  ST YVES &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 82000 €&lt;/div&gt;`)[0];
            popup_0d29bbb9fe59951a80339955ffcebf8d.setContent(html_d86b859211ebf1218bb52a87b208548d);
        

        marker_3a1ee8f5d9a10ed12ef1f37dbd48e62d.bindPopup(popup_0d29bbb9fe59951a80339955ffcebf8d)
        ;

        
    
    
            var marker_7dfc2146e2cb3b99a894c5752807791d = L.marker(
                [48.037175, -4.675032],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_4161bde7acd035850cc9845d2091beb2 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_7dfc2146e2cb3b99a894c5752807791d.setIcon(icon_4161bde7acd035850cc9845d2091beb2);
        
    
        var popup_6a52f0da6955d6ea9d5b4d0c8b595e17 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d46fa7b9d3663b6bd2f605b92fd248fd = $(`&lt;div id=&quot;html_d46fa7b9d3663b6bd2f605b92fd248fd&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  ST YVES &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 82000 €&lt;/div&gt;`)[0];
            popup_6a52f0da6955d6ea9d5b4d0c8b595e17.setContent(html_d46fa7b9d3663b6bd2f605b92fd248fd);
        

        marker_7dfc2146e2cb3b99a894c5752807791d.bindPopup(popup_6a52f0da6955d6ea9d5b4d0c8b595e17)
        ;

        
    
    
            var marker_11d10b193beb78e508dc3ddacb51cbad = L.marker(
                [48.037391, -4.67533],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_1e3aa107269839edbd29e062349c4952 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_11d10b193beb78e508dc3ddacb51cbad.setIcon(icon_1e3aa107269839edbd29e062349c4952);
        
    
        var popup_c724a5341fa624e9d6b71635b1a41ab0 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_487ed5e0f5a4fd5a97ee674849650a37 = $(`&lt;div id=&quot;html_487ed5e0f5a4fd5a97ee674849650a37&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 419 ST YVES &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 82000 €&lt;/div&gt;`)[0];
            popup_c724a5341fa624e9d6b71635b1a41ab0.setContent(html_487ed5e0f5a4fd5a97ee674849650a37);
        

        marker_11d10b193beb78e508dc3ddacb51cbad.bindPopup(popup_c724a5341fa624e9d6b71635b1a41ab0)
        ;

        
    
    
            var marker_29deb9c34f90be40b41fcc2b8f1b1c8f = L.marker(
                [48.032151, -4.669829],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_607b8de898b23a8375eeda83151269d2 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_29deb9c34f90be40b41fcc2b8f1b1c8f.setIcon(icon_607b8de898b23a8375eeda83151269d2);
        
    
        var popup_8e14e5af546763fd3d94a16eec0b9832 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a1320774c16ffa65559968bf82c578b0 = $(`&lt;div id=&quot;html_a1320774c16ffa65559968bf82c578b0&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5043 LE DREFF &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 167500 €&lt;/div&gt;`)[0];
            popup_8e14e5af546763fd3d94a16eec0b9832.setContent(html_a1320774c16ffa65559968bf82c578b0);
        

        marker_29deb9c34f90be40b41fcc2b8f1b1c8f.bindPopup(popup_8e14e5af546763fd3d94a16eec0b9832)
        ;

        
    
    
            var marker_f2ebc7ab58dccc14fb2ad6e72b4504c9 = L.marker(
                [48.031881, -4.669537],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_29cfc3221a5ba8f54030cca42668783e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_f2ebc7ab58dccc14fb2ad6e72b4504c9.setIcon(icon_29cfc3221a5ba8f54030cca42668783e);
        
    
        var popup_b9f948ce4e1ed200871f4a89db890496 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1ee68be61b32cde123098d36cade1f48 = $(`&lt;div id=&quot;html_1ee68be61b32cde123098d36cade1f48&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE DREFF &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 167500 €&lt;/div&gt;`)[0];
            popup_b9f948ce4e1ed200871f4a89db890496.setContent(html_1ee68be61b32cde123098d36cade1f48);
        

        marker_f2ebc7ab58dccc14fb2ad6e72b4504c9.bindPopup(popup_b9f948ce4e1ed200871f4a89db890496)
        ;

        
    
    
            var marker_2f6b33fcf8bbabddb0fa52f5f4319fbe = L.marker(
                [48.031881, -4.669537],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_ce1690b592b9c2e75fe8391524b502ad = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_2f6b33fcf8bbabddb0fa52f5f4319fbe.setIcon(icon_ce1690b592b9c2e75fe8391524b502ad);
        
    
        var popup_9a314fb0ca49a782cfc7493539dc9929 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_bce5a11823e81f87f64c6dae11a48f78 = $(`&lt;div id=&quot;html_bce5a11823e81f87f64c6dae11a48f78&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LE DREFF &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 167500 €&lt;/div&gt;`)[0];
            popup_9a314fb0ca49a782cfc7493539dc9929.setContent(html_bce5a11823e81f87f64c6dae11a48f78);
        

        marker_2f6b33fcf8bbabddb0fa52f5f4319fbe.bindPopup(popup_9a314fb0ca49a782cfc7493539dc9929)
        ;

        
    
    
            var marker_1ae890b19614e68f60f60c4b849acae9 = L.marker(
                [48.033866, -4.677541],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_06b2dd01bffb9f60317aab4d2d646592 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_1ae890b19614e68f60f60c4b849acae9.setIcon(icon_06b2dd01bffb9f60317aab4d2d646592);
        
    
        var popup_410408631533cfa3a2f38289dc9a679f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_68b4f4c7485a7defaf91bcecd5c796f2 = $(`&lt;div id=&quot;html_68b4f4c7485a7defaf91bcecd5c796f2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERVERGAR &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_410408631533cfa3a2f38289dc9a679f.setContent(html_68b4f4c7485a7defaf91bcecd5c796f2);
        

        marker_1ae890b19614e68f60f60c4b849acae9.bindPopup(popup_410408631533cfa3a2f38289dc9a679f)
        ;

        
    
    
            var marker_17e72cde5e26e5527aa15b4f86253845 = L.marker(
                [48.035965, -4.680002],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_615648a5b7b4fa6e267a43bf9193c4bb = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_17e72cde5e26e5527aa15b4f86253845.setIcon(icon_615648a5b7b4fa6e267a43bf9193c4bb);
        
    
        var popup_9000b77a040e510e674365e1ceba9d8f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_6b35e26e20d2bc19ca1de647ad4baa17 = $(`&lt;div id=&quot;html_6b35e26e20d2bc19ca1de647ad4baa17&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  ST YVES &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_9000b77a040e510e674365e1ceba9d8f.setContent(html_6b35e26e20d2bc19ca1de647ad4baa17);
        

        marker_17e72cde5e26e5527aa15b4f86253845.bindPopup(popup_9000b77a040e510e674365e1ceba9d8f)
        ;

        
    
    
            var marker_4a3f05ab05000630cb5040ca47358d78 = L.marker(
                [48.037083, -4.675469],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_b04538969cfbb55dc045bbba48ff3f96 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_4a3f05ab05000630cb5040ca47358d78.setIcon(icon_b04538969cfbb55dc045bbba48ff3f96);
        
    
        var popup_abef20ef22bc3d6b6a1788a4ee8a740d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1f1ce9b5151affeed0c516103b872369 = $(`&lt;div id=&quot;html_1f1ce9b5151affeed0c516103b872369&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  ST YVES &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 4000 €&lt;/div&gt;`)[0];
            popup_abef20ef22bc3d6b6a1788a4ee8a740d.setContent(html_1f1ce9b5151affeed0c516103b872369);
        

        marker_4a3f05ab05000630cb5040ca47358d78.bindPopup(popup_abef20ef22bc3d6b6a1788a4ee8a740d)
        ;

        
    
    
            var marker_bf4a06730b99cd4bad2014ccb676ea3a = L.marker(
                [48.031265, -4.675454],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_fdf89326c6d29cc2d7529918afc278bd = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_bf4a06730b99cd4bad2014ccb676ea3a.setIcon(icon_fdf89326c6d29cc2d7529918afc278bd);
        
    
        var popup_52986716acd382304867352a68ffc005 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_631641f5506938633bc7d0bac9a1fee8 = $(`&lt;div id=&quot;html_631641f5506938633bc7d0bac9a1fee8&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  SAOUTENET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 120200 €&lt;/div&gt;`)[0];
            popup_52986716acd382304867352a68ffc005.setContent(html_631641f5506938633bc7d0bac9a1fee8);
        

        marker_bf4a06730b99cd4bad2014ccb676ea3a.bindPopup(popup_52986716acd382304867352a68ffc005)
        ;

        
    
    
            var marker_fbafb6eb8ad083dc7b8adc063b562193 = L.marker(
                [48.031266, -4.675849],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_b9f05e8ff5e4eab0427cb52decf60658 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_fbafb6eb8ad083dc7b8adc063b562193.setIcon(icon_b9f05e8ff5e4eab0427cb52decf60658);
        
    
        var popup_a0de16e74d6d85df24f2c83858ffd6c1 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e758f2b18657b8ff72f2c07df5f6a592 = $(`&lt;div id=&quot;html_e758f2b18657b8ff72f2c07df5f6a592&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 388 SAOUTENET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 120200 €&lt;/div&gt;`)[0];
            popup_a0de16e74d6d85df24f2c83858ffd6c1.setContent(html_e758f2b18657b8ff72f2c07df5f6a592);
        

        marker_fbafb6eb8ad083dc7b8adc063b562193.bindPopup(popup_a0de16e74d6d85df24f2c83858ffd6c1)
        ;

        
    
    
            var marker_a68f625fb50efc3dd93a91b0091e0f30 = L.marker(
                [48.039067, -4.686724],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_0cc3179a3b170f0cc118fffea452d2de = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_a68f625fb50efc3dd93a91b0091e0f30.setIcon(icon_0cc3179a3b170f0cc118fffea452d2de);
        
    
        var popup_a02efc110adb7bcdc9817d9e43cafa05 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_97fad5f1ce3f742d1c42b6402c2aa71d = $(`&lt;div id=&quot;html_97fad5f1ce3f742d1c42b6402c2aa71d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  TRIGUEN &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_a02efc110adb7bcdc9817d9e43cafa05.setContent(html_97fad5f1ce3f742d1c42b6402c2aa71d);
        

        marker_a68f625fb50efc3dd93a91b0091e0f30.bindPopup(popup_a02efc110adb7bcdc9817d9e43cafa05)
        ;

        
    
    
            var marker_bd660e1931f01b3d58a85a98d8ce4cef = L.marker(
                [48.039609, -4.686378],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d87141f4f36d60edaad38cc7cfc916d8 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_bd660e1931f01b3d58a85a98d8ce4cef.setIcon(icon_d87141f4f36d60edaad38cc7cfc916d8);
        
    
        var popup_5af1b6434be05a897f42e9b5aaed3868 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d51903f48cbf1c0420aa6b3ccaae7ae0 = $(`&lt;div id=&quot;html_d51903f48cbf1c0420aa6b3ccaae7ae0&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  TRIGUEN &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_5af1b6434be05a897f42e9b5aaed3868.setContent(html_d51903f48cbf1c0420aa6b3ccaae7ae0);
        

        marker_bd660e1931f01b3d58a85a98d8ce4cef.bindPopup(popup_5af1b6434be05a897f42e9b5aaed3868)
        ;

        
    
    
            var marker_d307045609e230ffae402f8aa6a26021 = L.marker(
                [48.039488, -4.687005],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_ad2ad78beb696ba2cc4b1a1faae385e4 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_d307045609e230ffae402f8aa6a26021.setIcon(icon_ad2ad78beb696ba2cc4b1a1faae385e4);
        
    
        var popup_874c7a54cdcf4f0462d0727c3f9cb5b2 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_eb1d159c6dc1efff5cc8a5659126b5af = $(`&lt;div id=&quot;html_eb1d159c6dc1efff5cc8a5659126b5af&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  TRIGUEN &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_874c7a54cdcf4f0462d0727c3f9cb5b2.setContent(html_eb1d159c6dc1efff5cc8a5659126b5af);
        

        marker_d307045609e230ffae402f8aa6a26021.bindPopup(popup_874c7a54cdcf4f0462d0727c3f9cb5b2)
        ;

        
    
    
            var marker_fa52b8ac222d98ae8c1d5e186089d0de = L.marker(
                [48.039714, -4.687761],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_52fa6b34db8009d41fa6f8baae8403d0 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_fa52b8ac222d98ae8c1d5e186089d0de.setIcon(icon_52fa6b34db8009d41fa6f8baae8403d0);
        
    
        var popup_fd4c6a1798ab232d19672b264f9ecd36 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_61ef3f60a0273cd923126e4338e450b2 = $(`&lt;div id=&quot;html_61ef3f60a0273cd923126e4338e450b2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  TRIGUEN &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 9500 €&lt;/div&gt;`)[0];
            popup_fd4c6a1798ab232d19672b264f9ecd36.setContent(html_61ef3f60a0273cd923126e4338e450b2);
        

        marker_fa52b8ac222d98ae8c1d5e186089d0de.bindPopup(popup_fd4c6a1798ab232d19672b264f9ecd36)
        ;

        
    
    
            var marker_89e733383d4b5966a63c1200fe1a85b4 = L.marker(
                [48.038991, -4.682838],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_1a53fe76c15d53a16b9e806820f4d9b6 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_89e733383d4b5966a63c1200fe1a85b4.setIcon(icon_1a53fe76c15d53a16b9e806820f4d9b6);
        
    
        var popup_e871e4446ba849f27606d26810fd9b0d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_3f4d767218991564aa019d8953d18d44 = $(`&lt;div id=&quot;html_3f4d767218991564aa019d8953d18d44&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 450 KERGUIDY HUELLA &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 140000 €&lt;/div&gt;`)[0];
            popup_e871e4446ba849f27606d26810fd9b0d.setContent(html_3f4d767218991564aa019d8953d18d44);
        

        marker_89e733383d4b5966a63c1200fe1a85b4.bindPopup(popup_e871e4446ba849f27606d26810fd9b0d)
        ;

        
    
    
            var marker_c71c4e13e424dcd04f779dc111099888 = L.marker(
                [48.038853, -4.68286],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_3fe97b51261dfcc7d2f46a910fd9d57b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_c71c4e13e424dcd04f779dc111099888.setIcon(icon_3fe97b51261dfcc7d2f46a910fd9d57b);
        
    
        var popup_b6ebb6783d828e17bb19fd6cb4de5aaa = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_eefb7c3e1d9facc2bc4e32193efad3f4 = $(`&lt;div id=&quot;html_eefb7c3e1d9facc2bc4e32193efad3f4&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGUIDY HUELLA &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 140000 €&lt;/div&gt;`)[0];
            popup_b6ebb6783d828e17bb19fd6cb4de5aaa.setContent(html_eefb7c3e1d9facc2bc4e32193efad3f4);
        

        marker_c71c4e13e424dcd04f779dc111099888.bindPopup(popup_b6ebb6783d828e17bb19fd6cb4de5aaa)
        ;

        
    
    
            var marker_25d1a100248884abca20056b1c23a123 = L.marker(
                [48.038866, -4.683235],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_89077b947403d3b0f20f05bd1909e016 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_25d1a100248884abca20056b1c23a123.setIcon(icon_89077b947403d3b0f20f05bd1909e016);
        
    
        var popup_32a65c1858340e6b5c8111f9d4cc0ce2 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_98378c3d8a6739cbc6d83656422cff56 = $(`&lt;div id=&quot;html_98378c3d8a6739cbc6d83656422cff56&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGUIDY HUELLA &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 1000 €&lt;/div&gt;`)[0];
            popup_32a65c1858340e6b5c8111f9d4cc0ce2.setContent(html_98378c3d8a6739cbc6d83656422cff56);
        

        marker_25d1a100248884abca20056b1c23a123.bindPopup(popup_32a65c1858340e6b5c8111f9d4cc0ce2)
        ;

        
    
    
            var marker_151c7726745d5e4319bb08c988c5e5cf = L.marker(
                [48.038967, -4.683676],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_26e09920b209e341bea37413c6bd8e08 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_151c7726745d5e4319bb08c988c5e5cf.setIcon(icon_26e09920b209e341bea37413c6bd8e08);
        
    
        var popup_b77bc07203322216e717fd28f0868d80 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_021199a53aa6848efedb2e8caba912f8 = $(`&lt;div id=&quot;html_021199a53aa6848efedb2e8caba912f8&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGUIDY HUELLA &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 1000 €&lt;/div&gt;`)[0];
            popup_b77bc07203322216e717fd28f0868d80.setContent(html_021199a53aa6848efedb2e8caba912f8);
        

        marker_151c7726745d5e4319bb08c988c5e5cf.bindPopup(popup_b77bc07203322216e717fd28f0868d80)
        ;

        
    
    
            var marker_5fe2a65d559f019d185deaaf2d53b2c2 = L.marker(
                [48.03855, -4.682722],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_8bf483c63f04d4a694006c1f094c6e23 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_5fe2a65d559f019d185deaaf2d53b2c2.setIcon(icon_8bf483c63f04d4a694006c1f094c6e23);
        
    
        var popup_2f24b161dc7e022b2b5b32744c09497e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7f86ad2b849991cf642f88c717e7188a = $(`&lt;div id=&quot;html_7f86ad2b849991cf642f88c717e7188a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGUIDY HUELLA &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 50000 €&lt;/div&gt;`)[0];
            popup_2f24b161dc7e022b2b5b32744c09497e.setContent(html_7f86ad2b849991cf642f88c717e7188a);
        

        marker_5fe2a65d559f019d185deaaf2d53b2c2.bindPopup(popup_2f24b161dc7e022b2b5b32744c09497e)
        ;

        
    
    
            var marker_809639a8f9fe8ac8fba13f9eb29b513b = L.marker(
                [48.038341, -4.682722],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_6656780019d194678bdd95e09da5ba32 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_809639a8f9fe8ac8fba13f9eb29b513b.setIcon(icon_6656780019d194678bdd95e09da5ba32);
        
    
        var popup_0803774e376a013de5392e03a5d43d2a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_6d1acbc9943e2b3fe664696a548ebfd7 = $(`&lt;div id=&quot;html_6d1acbc9943e2b3fe664696a548ebfd7&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 79 KERGUIDY HUELLA &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 50000 €&lt;/div&gt;`)[0];
            popup_0803774e376a013de5392e03a5d43d2a.setContent(html_6d1acbc9943e2b3fe664696a548ebfd7);
        

        marker_809639a8f9fe8ac8fba13f9eb29b513b.bindPopup(popup_0803774e376a013de5392e03a5d43d2a)
        ;

        
    
    
            var marker_208667255e3e32bb6c1ce521640a1850 = L.marker(
                [48.038341, -4.682722],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_b4fae39271b445723e837984b086f8c8 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_208667255e3e32bb6c1ce521640a1850.setIcon(icon_b4fae39271b445723e837984b086f8c8);
        
    
        var popup_53dea8cb831bf014db5d61bf8df1cfc6 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_57d807b3ba2e8d39d066540bab5e9368 = $(`&lt;div id=&quot;html_57d807b3ba2e8d39d066540bab5e9368&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 79 KERGUIDY HUELLA &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 50000 €&lt;/div&gt;`)[0];
            popup_53dea8cb831bf014db5d61bf8df1cfc6.setContent(html_57d807b3ba2e8d39d066540bab5e9368);
        

        marker_208667255e3e32bb6c1ce521640a1850.bindPopup(popup_53dea8cb831bf014db5d61bf8df1cfc6)
        ;

        
    
    
            var marker_6a20ab695092f97f52d2b880e63e0186 = L.marker(
                [48.038181, -4.68265],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_3427bc3b5165c11b3c1bd2317cecb9da = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_6a20ab695092f97f52d2b880e63e0186.setIcon(icon_3427bc3b5165c11b3c1bd2317cecb9da);
        
    
        var popup_98aa948f6a3f0ee6a70335d7741ac818 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1424b76e381e00133650a840c9f5ed78 = $(`&lt;div id=&quot;html_1424b76e381e00133650a840c9f5ed78&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGUIDY HUELLA &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 50000 €&lt;/div&gt;`)[0];
            popup_98aa948f6a3f0ee6a70335d7741ac818.setContent(html_1424b76e381e00133650a840c9f5ed78);
        

        marker_6a20ab695092f97f52d2b880e63e0186.bindPopup(popup_98aa948f6a3f0ee6a70335d7741ac818)
        ;

        
    
    
            var marker_044f06dd459acbfa88de654851b40706 = L.marker(
                [48.038468, -4.682588],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_2d25f1306c8094092ee587ddc09b5df4 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_044f06dd459acbfa88de654851b40706.setIcon(icon_2d25f1306c8094092ee587ddc09b5df4);
        
    
        var popup_652f24f787fee850ce140a5b06cc9576 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_b0712564d662f107c44bceabee8d0f3b = $(`&lt;div id=&quot;html_b0712564d662f107c44bceabee8d0f3b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGUIDY HUELLA &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 50000 €&lt;/div&gt;`)[0];
            popup_652f24f787fee850ce140a5b06cc9576.setContent(html_b0712564d662f107c44bceabee8d0f3b);
        

        marker_044f06dd459acbfa88de654851b40706.bindPopup(popup_652f24f787fee850ce140a5b06cc9576)
        ;

        
    
    
            var marker_b432b35d39fa2d0a4424abea32133215 = L.marker(
                [48.038016, -4.679714],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_a1f4830146af3ec991cec2ce5902fe2f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_b432b35d39fa2d0a4424abea32133215.setIcon(icon_a1f4830146af3ec991cec2ce5902fe2f);
        
    
        var popup_30dca13297c19c19b2d6c7f87e20e177 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_30d668d92967f8f3b2de5d86d7b9e6fb = $(`&lt;div id=&quot;html_30d668d92967f8f3b2de5d86d7b9e6fb&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 443 ST YVES &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 30000 €&lt;/div&gt;`)[0];
            popup_30dca13297c19c19b2d6c7f87e20e177.setContent(html_30d668d92967f8f3b2de5d86d7b9e6fb);
        

        marker_b432b35d39fa2d0a4424abea32133215.bindPopup(popup_30dca13297c19c19b2d6c7f87e20e177)
        ;

        
    
    
            var marker_be2b0a046b01eb652c13c9e87cdff004 = L.marker(
                [48.036314, -4.6811],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_0a250a10f6368c77bb74bfba17cd4d82 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_be2b0a046b01eb652c13c9e87cdff004.setIcon(icon_0a250a10f6368c77bb74bfba17cd4d82);
        
    
        var popup_625a7ecb05ac0f1f870e2cc4ef82eca1 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_f100ee45dcf0aa960bc327ae9a5d8609 = $(`&lt;div id=&quot;html_f100ee45dcf0aa960bc327ae9a5d8609&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGUIDY IZELLA &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_625a7ecb05ac0f1f870e2cc4ef82eca1.setContent(html_f100ee45dcf0aa960bc327ae9a5d8609);
        

        marker_be2b0a046b01eb652c13c9e87cdff004.bindPopup(popup_625a7ecb05ac0f1f870e2cc4ef82eca1)
        ;

        
    
    
            var marker_4c868f47f43ac04b8f67dd0c3f11cba8 = L.marker(
                [48.036969, -4.68162],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_02688749c0a31c92dd06f72f2d7b4102 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_4c868f47f43ac04b8f67dd0c3f11cba8.setIcon(icon_02688749c0a31c92dd06f72f2d7b4102);
        
    
        var popup_cf3255059ba5d2e00c43bdf4c6c9a592 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_79523178a16a03800a01e9b3df7b1702 = $(`&lt;div id=&quot;html_79523178a16a03800a01e9b3df7b1702&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 427 KERGUIDY IZELLA &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 65000 €&lt;/div&gt;`)[0];
            popup_cf3255059ba5d2e00c43bdf4c6c9a592.setContent(html_79523178a16a03800a01e9b3df7b1702);
        

        marker_4c868f47f43ac04b8f67dd0c3f11cba8.bindPopup(popup_cf3255059ba5d2e00c43bdf4c6c9a592)
        ;

        
    
    
            var marker_a229091ff5c126aa5a985b34a9e01b4e = L.marker(
                [48.040493, -4.685761],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_0e9b216b46ef566166d41d271f691518 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_a229091ff5c126aa5a985b34a9e01b4e.setIcon(icon_0e9b216b46ef566166d41d271f691518);
        
    
        var popup_cb54c37761ce05716f6d6b68a39c62f0 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_3fdbb71c4e132da8c6e987b942b80dc6 = $(`&lt;div id=&quot;html_3fdbb71c4e132da8c6e987b942b80dc6&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  TRIGUEN &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 300 €&lt;/div&gt;`)[0];
            popup_cb54c37761ce05716f6d6b68a39c62f0.setContent(html_3fdbb71c4e132da8c6e987b942b80dc6);
        

        marker_a229091ff5c126aa5a985b34a9e01b4e.bindPopup(popup_cb54c37761ce05716f6d6b68a39c62f0)
        ;

        
    
    
            var marker_35c2aad14aae70c195bc1c7bfc3a041f = L.marker(
                [48.037078, -4.681764],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_0feb848c446f96bdc03a93c43a158879 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_35c2aad14aae70c195bc1c7bfc3a041f.setIcon(icon_0feb848c446f96bdc03a93c43a158879);
        
    
        var popup_20db64797ec86c88235c7079d06d59fa = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7fcb76c133cc2a32a802514f7ecc861b = $(`&lt;div id=&quot;html_7fcb76c133cc2a32a802514f7ecc861b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGUIDY IZELLA &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 65000 €&lt;/div&gt;`)[0];
            popup_20db64797ec86c88235c7079d06d59fa.setContent(html_7fcb76c133cc2a32a802514f7ecc861b);
        

        marker_35c2aad14aae70c195bc1c7bfc3a041f.bindPopup(popup_20db64797ec86c88235c7079d06d59fa)
        ;

        
    
    
            var marker_50583aa660acd846574fa4a6950dbb60 = L.marker(
                [48.037095, -4.681785],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_181fcda2ad3c2b1e10b4edd40c78c301 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_50583aa660acd846574fa4a6950dbb60.setIcon(icon_181fcda2ad3c2b1e10b4edd40c78c301);
        
    
        var popup_8821672a6f1d290679504d937aaa7ee9 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a9f4a43c59f560bbea2b9791b4bda1f6 = $(`&lt;div id=&quot;html_a9f4a43c59f560bbea2b9791b4bda1f6&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGUIDY IZELLA &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 65000 €&lt;/div&gt;`)[0];
            popup_8821672a6f1d290679504d937aaa7ee9.setContent(html_a9f4a43c59f560bbea2b9791b4bda1f6);
        

        marker_50583aa660acd846574fa4a6950dbb60.bindPopup(popup_8821672a6f1d290679504d937aaa7ee9)
        ;

        
    
    
            var marker_2e5d20868b7d63e57c3665da8667c540 = L.marker(
                [48.037774, -4.690038],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_3d140ce878a658dfe9ba9aef2b691ec8 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_2e5d20868b7d63e57c3665da8667c540.setIcon(icon_3d140ce878a658dfe9ba9aef2b691ec8);
        
    
        var popup_cf5a37ffd49c34b83c862ee22126301f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7c5a4e69c5bc5a4afbb468f47409273b = $(`&lt;div id=&quot;html_7c5a4e69c5bc5a4afbb468f47409273b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_cf5a37ffd49c34b83c862ee22126301f.setContent(html_7c5a4e69c5bc5a4afbb468f47409273b);
        

        marker_2e5d20868b7d63e57c3665da8667c540.bindPopup(popup_cf5a37ffd49c34b83c862ee22126301f)
        ;

        
    
    
            var marker_bff57adee164961600ed1d09e1dd8c75 = L.marker(
                [48.036453, -4.688123],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_6b3b323c6828ce9c9a3a51a41c443796 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_bff57adee164961600ed1d09e1dd8c75.setIcon(icon_6b3b323c6828ce9c9a3a51a41c443796);
        
    
        var popup_4505d3b281dfb0c18646ac70c75582e8 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_4bbd56fb7a084cbec25625266aadecb6 = $(`&lt;div id=&quot;html_4bbd56fb7a084cbec25625266aadecb6&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 441 KERGOUNEAU &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 78000 €&lt;/div&gt;`)[0];
            popup_4505d3b281dfb0c18646ac70c75582e8.setContent(html_4bbd56fb7a084cbec25625266aadecb6);
        

        marker_bff57adee164961600ed1d09e1dd8c75.bindPopup(popup_4505d3b281dfb0c18646ac70c75582e8)
        ;

        
    
    
            var marker_e6d2a049ca6dc4d2c690701f9bc3dbd9 = L.marker(
                [48.03416, -4.686732],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_04efa99764f399f09e7c8d2c70d808c0 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_e6d2a049ca6dc4d2c690701f9bc3dbd9.setIcon(icon_04efa99764f399f09e7c8d2c70d808c0);
        
    
        var popup_1127e853c66d24c741e1583813780931 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7d6ab714295ab3014823c3f1f61377dd = $(`&lt;div id=&quot;html_7d6ab714295ab3014823c3f1f61377dd&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGOUNEAU &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 2000 €&lt;/div&gt;`)[0];
            popup_1127e853c66d24c741e1583813780931.setContent(html_7d6ab714295ab3014823c3f1f61377dd);
        

        marker_e6d2a049ca6dc4d2c690701f9bc3dbd9.bindPopup(popup_1127e853c66d24c741e1583813780931)
        ;

        
    
    
            var marker_03807eb0660aac14225202d6550f7db3 = L.marker(
                [48.035102, -4.691314],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_54202b632fd3cd44a656a5c5bee9984e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_03807eb0660aac14225202d6550f7db3.setIcon(icon_54202b632fd3cd44a656a5c5bee9984e);
        
    
        var popup_d9507e7055b90bc319d40e7a4b9e130e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_51f5210de4727d06f2f0173831df973b = $(`&lt;div id=&quot;html_51f5210de4727d06f2f0173831df973b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_d9507e7055b90bc319d40e7a4b9e130e.setContent(html_51f5210de4727d06f2f0173831df973b);
        

        marker_03807eb0660aac14225202d6550f7db3.bindPopup(popup_d9507e7055b90bc319d40e7a4b9e130e)
        ;

        
    
    
            var marker_2fbb221288e90f51e6c4c9e727557940 = L.marker(
                [48.035065, -4.692017],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_1fd70b9c9352043888af1081f71840c7 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_2fbb221288e90f51e6c4c9e727557940.setIcon(icon_1fd70b9c9352043888af1081f71840c7);
        
    
        var popup_7a8584734e2d96ec3ced941a268d750c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_5b97ca10bf66286062f0bde2fb93a05b = $(`&lt;div id=&quot;html_5b97ca10bf66286062f0bde2fb93a05b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_7a8584734e2d96ec3ced941a268d750c.setContent(html_5b97ca10bf66286062f0bde2fb93a05b);
        

        marker_2fbb221288e90f51e6c4c9e727557940.bindPopup(popup_7a8584734e2d96ec3ced941a268d750c)
        ;

        
    
    
            var marker_e1705227e75ba9622645bac769cd5c67 = L.marker(
                [48.035476, -4.691752],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_3e34663da67a82323ab5ad07a9b34ce2 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_e1705227e75ba9622645bac769cd5c67.setIcon(icon_3e34663da67a82323ab5ad07a9b34ce2);
        
    
        var popup_9e0e5d3c39033b4efbab4cf9d0f387e8 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a3d9634eef51eff1a501525b2a662007 = $(`&lt;div id=&quot;html_a3d9634eef51eff1a501525b2a662007&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_9e0e5d3c39033b4efbab4cf9d0f387e8.setContent(html_a3d9634eef51eff1a501525b2a662007);
        

        marker_e1705227e75ba9622645bac769cd5c67.bindPopup(popup_9e0e5d3c39033b4efbab4cf9d0f387e8)
        ;

        
    
    
            var marker_6cd654694428cbb25058ae520821fbeb = L.marker(
                [48.036437, -4.691571],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_f47c7549cc4c2b51c1ff25b2e312471f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_6cd654694428cbb25058ae520821fbeb.setIcon(icon_f47c7549cc4c2b51c1ff25b2e312471f);
        
    
        var popup_b26179939949805abbd34c7a9268aead = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a4044d7e7225cf7275ab012182709a12 = $(`&lt;div id=&quot;html_a4044d7e7225cf7275ab012182709a12&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 7 KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 220000 €&lt;/div&gt;`)[0];
            popup_b26179939949805abbd34c7a9268aead.setContent(html_a4044d7e7225cf7275ab012182709a12);
        

        marker_6cd654694428cbb25058ae520821fbeb.bindPopup(popup_b26179939949805abbd34c7a9268aead)
        ;

        
    
    
            var marker_08e69273ba198fe085141483a81d3b1e = L.marker(
                [48.036606, -4.691669],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_28bdddef98ada2f52b7df116390bf0b5 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_08e69273ba198fe085141483a81d3b1e.setIcon(icon_28bdddef98ada2f52b7df116390bf0b5);
        
    
        var popup_a3accb5c5820b76506da4b9d12a50952 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8d8359e5c72a5d662eaa9c2695abcb0d = $(`&lt;div id=&quot;html_8d8359e5c72a5d662eaa9c2695abcb0d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 220000 €&lt;/div&gt;`)[0];
            popup_a3accb5c5820b76506da4b9d12a50952.setContent(html_8d8359e5c72a5d662eaa9c2695abcb0d);
        

        marker_08e69273ba198fe085141483a81d3b1e.bindPopup(popup_a3accb5c5820b76506da4b9d12a50952)
        ;

        
    
    
            var marker_e33fc80424aa92703db2960e39e90d64 = L.marker(
                [48.035953, -4.692281],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_b8460eeee8307754064d023e6e862a2e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_e33fc80424aa92703db2960e39e90d64.setIcon(icon_b8460eeee8307754064d023e6e862a2e);
        
    
        var popup_e86c16e25134b492208c947d744dcf95 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_cb998c285e4c1cd8523fc5ad8c40da44 = $(`&lt;div id=&quot;html_cb998c285e4c1cd8523fc5ad8c40da44&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_e86c16e25134b492208c947d744dcf95.setContent(html_cb998c285e4c1cd8523fc5ad8c40da44);
        

        marker_e33fc80424aa92703db2960e39e90d64.bindPopup(popup_e86c16e25134b492208c947d744dcf95)
        ;

        
    
    
            var marker_9160b58bdf2c7579d4a76943a7a06bf1 = L.marker(
                [48.036274, -4.692947],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_a199e9e58c9caad4e636b4ff8b61769d = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_9160b58bdf2c7579d4a76943a7a06bf1.setIcon(icon_a199e9e58c9caad4e636b4ff8b61769d);
        
    
        var popup_8069d06483d3a61afb2cbd7a6a2e8f63 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2a417ea3f3a1f766ad21bdcce24680af = $(`&lt;div id=&quot;html_2a417ea3f3a1f766ad21bdcce24680af&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_8069d06483d3a61afb2cbd7a6a2e8f63.setContent(html_2a417ea3f3a1f766ad21bdcce24680af);
        

        marker_9160b58bdf2c7579d4a76943a7a06bf1.bindPopup(popup_8069d06483d3a61afb2cbd7a6a2e8f63)
        ;

        
    
    
            var marker_505885a078ff6e58f24d498101a07ba7 = L.marker(
                [48.035786, -4.692659],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_e2dc254e3f492c1f6d5f1b149a423d47 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_505885a078ff6e58f24d498101a07ba7.setIcon(icon_e2dc254e3f492c1f6d5f1b149a423d47);
        
    
        var popup_f64d1d73c38002ab9186303cee1943aa = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_73bac4048c05f11f497a0bdd9c868934 = $(`&lt;div id=&quot;html_73bac4048c05f11f497a0bdd9c868934&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_f64d1d73c38002ab9186303cee1943aa.setContent(html_73bac4048c05f11f497a0bdd9c868934);
        

        marker_505885a078ff6e58f24d498101a07ba7.bindPopup(popup_f64d1d73c38002ab9186303cee1943aa)
        ;

        
    
    
            var marker_120672a805bef0058f8fac52191c59aa = L.marker(
                [48.039565, -4.695594],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d89e6574649b97e17a178539f03ff2ad = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_120672a805bef0058f8fac52191c59aa.setIcon(icon_d89e6574649b97e17a178539f03ff2ad);
        
    
        var popup_304876d86a33637f7f6156268faa2772 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8cb350fe84b6be00e57d4fa20875c936 = $(`&lt;div id=&quot;html_8cb350fe84b6be00e57d4fa20875c936&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 532 KERVEUR &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 110000 €&lt;/div&gt;`)[0];
            popup_304876d86a33637f7f6156268faa2772.setContent(html_8cb350fe84b6be00e57d4fa20875c936);
        

        marker_120672a805bef0058f8fac52191c59aa.bindPopup(popup_304876d86a33637f7f6156268faa2772)
        ;

        
    
    
            var marker_dffa6472cddba1d2eda25b42b483d421 = L.marker(
                [48.039468, -4.69537],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_7bb38e643eda1bcc5fb724902dc35fd5 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_dffa6472cddba1d2eda25b42b483d421.setIcon(icon_7bb38e643eda1bcc5fb724902dc35fd5);
        
    
        var popup_7f9f608e1708eab1adf7c9bba4b5b495 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_6e6bc118b6d3a4ee66028ddd0fbd0a5d = $(`&lt;div id=&quot;html_6e6bc118b6d3a4ee66028ddd0fbd0a5d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 533 KERVEUR &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 110000 €&lt;/div&gt;`)[0];
            popup_7f9f608e1708eab1adf7c9bba4b5b495.setContent(html_6e6bc118b6d3a4ee66028ddd0fbd0a5d);
        

        marker_dffa6472cddba1d2eda25b42b483d421.bindPopup(popup_7f9f608e1708eab1adf7c9bba4b5b495)
        ;

        
    
    
            var marker_62c861f4b1cf74362fe0988c08e8697e = L.marker(
                [48.038843, -4.692848],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_c55950727e977c9587206a473af821fc = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_62c861f4b1cf74362fe0988c08e8697e.setIcon(icon_c55950727e977c9587206a473af821fc);
        
    
        var popup_2e777a1349dcdbc166a3cf4dfb82d47f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c5a6e97d3a0817ed552e8393d5817206 = $(`&lt;div id=&quot;html_c5a6e97d3a0817ed552e8393d5817206&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 5165 KERVEUR &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 126954 €&lt;/div&gt;`)[0];
            popup_2e777a1349dcdbc166a3cf4dfb82d47f.setContent(html_c5a6e97d3a0817ed552e8393d5817206);
        

        marker_62c861f4b1cf74362fe0988c08e8697e.bindPopup(popup_2e777a1349dcdbc166a3cf4dfb82d47f)
        ;

        
    
    
            var marker_141787d36125eb7ad6462db28027e80d = L.marker(
                [48.03887, -4.693093],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_c53e0ccc3caec975df011a568f0962aa = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_141787d36125eb7ad6462db28027e80d.setIcon(icon_c53e0ccc3caec975df011a568f0962aa);
        
    
        var popup_3f15d0b2f0082b037a4373125a27359e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_cb27e24f927a710e712dd3f027b013f2 = $(`&lt;div id=&quot;html_cb27e24f927a710e712dd3f027b013f2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERVEUR &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 126954 €&lt;/div&gt;`)[0];
            popup_3f15d0b2f0082b037a4373125a27359e.setContent(html_cb27e24f927a710e712dd3f027b013f2);
        

        marker_141787d36125eb7ad6462db28027e80d.bindPopup(popup_3f15d0b2f0082b037a4373125a27359e)
        ;

        
    
    
            var marker_6c9e19ea19ad924e55cb132b1c44767f = L.marker(
                [48.038956, -4.693006],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_e1b8d9bd2f3390ac7cc1a782cbe4c37e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_6c9e19ea19ad924e55cb132b1c44767f.setIcon(icon_e1b8d9bd2f3390ac7cc1a782cbe4c37e);
        
    
        var popup_1a213aedfe5deee2aed33c087cc655a6 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c342623929979d876a0a2b15a866ee66 = $(`&lt;div id=&quot;html_c342623929979d876a0a2b15a866ee66&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERVEUR &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 126954 €&lt;/div&gt;`)[0];
            popup_1a213aedfe5deee2aed33c087cc655a6.setContent(html_c342623929979d876a0a2b15a866ee66);
        

        marker_6c9e19ea19ad924e55cb132b1c44767f.bindPopup(popup_1a213aedfe5deee2aed33c087cc655a6)
        ;

        
    
    
            var marker_3fb3f2548f0ec8b9efa4e1f5e92c0555 = L.marker(
                [48.039019, -4.693033],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_ad44e576768c9ac18da730d37408cf8f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_3fb3f2548f0ec8b9efa4e1f5e92c0555.setIcon(icon_ad44e576768c9ac18da730d37408cf8f);
        
    
        var popup_ac34acee54f151cb16618b6df4325495 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8dec8c79e3384638d1675328a73e6a58 = $(`&lt;div id=&quot;html_8dec8c79e3384638d1675328a73e6a58&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERVEUR &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 126954 €&lt;/div&gt;`)[0];
            popup_ac34acee54f151cb16618b6df4325495.setContent(html_8dec8c79e3384638d1675328a73e6a58);
        

        marker_3fb3f2548f0ec8b9efa4e1f5e92c0555.bindPopup(popup_ac34acee54f151cb16618b6df4325495)
        ;

        
    
    
            var marker_d6206dbaa13c150243da436dddf79b7e = L.marker(
                [48.039019, -4.693033],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_a6f54c911cecfa6bbec9a20d2cfd5ee6 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_d6206dbaa13c150243da436dddf79b7e.setIcon(icon_a6f54c911cecfa6bbec9a20d2cfd5ee6);
        
    
        var popup_f92733a361cdd990477713a020ac62e0 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e4446cb6ca30f110b9fff5606f05d57a = $(`&lt;div id=&quot;html_e4446cb6ca30f110b9fff5606f05d57a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERVEUR &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 126954 €&lt;/div&gt;`)[0];
            popup_f92733a361cdd990477713a020ac62e0.setContent(html_e4446cb6ca30f110b9fff5606f05d57a);
        

        marker_d6206dbaa13c150243da436dddf79b7e.bindPopup(popup_f92733a361cdd990477713a020ac62e0)
        ;

        
    
    
            var marker_254c3d6b8476330b997eb68c9e0e6737 = L.marker(
                [48.039075, -4.693155],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_df23f28ce6a77f854f4b2ea9ea662cea = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_254c3d6b8476330b997eb68c9e0e6737.setIcon(icon_df23f28ce6a77f854f4b2ea9ea662cea);
        
    
        var popup_f51309e50c1108f3dd8e259a4bb1d673 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_b0f039fdba4952bbcae3d630ae4b0f48 = $(`&lt;div id=&quot;html_b0f039fdba4952bbcae3d630ae4b0f48&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERVEUR &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 126954 €&lt;/div&gt;`)[0];
            popup_f51309e50c1108f3dd8e259a4bb1d673.setContent(html_b0f039fdba4952bbcae3d630ae4b0f48);
        

        marker_254c3d6b8476330b997eb68c9e0e6737.bindPopup(popup_f51309e50c1108f3dd8e259a4bb1d673)
        ;

        
    
    
            var marker_c3342fcc8e7f33432356a666869bb665 = L.marker(
                [48.039002, -4.691981],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_56b37e69a67e92c5807f825a74eabaa6 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_c3342fcc8e7f33432356a666869bb665.setIcon(icon_56b37e69a67e92c5807f825a74eabaa6);
        
    
        var popup_ec94ffd99f04a5fb463b1dc6924a8eaa = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_911b0b7da715cbd0cfb9ba89e12ec23f = $(`&lt;div id=&quot;html_911b0b7da715cbd0cfb9ba89e12ec23f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGADALEN &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 126954 €&lt;/div&gt;`)[0];
            popup_ec94ffd99f04a5fb463b1dc6924a8eaa.setContent(html_911b0b7da715cbd0cfb9ba89e12ec23f);
        

        marker_c3342fcc8e7f33432356a666869bb665.bindPopup(popup_ec94ffd99f04a5fb463b1dc6924a8eaa)
        ;

        
    
    
            var marker_b586e9fa61360293ff6f811a366117fc = L.marker(
                [48.039252, -4.693005],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_f81edae09785387bfb865ac168ac00f7 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_b586e9fa61360293ff6f811a366117fc.setIcon(icon_f81edae09785387bfb865ac168ac00f7);
        
    
        var popup_447064ee4442da05ad4b4493466bcb3c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_6a9dbb65c8f2fcc8d45ead72f47e1b4c = $(`&lt;div id=&quot;html_6a9dbb65c8f2fcc8d45ead72f47e1b4c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERVEUR &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 126954 €&lt;/div&gt;`)[0];
            popup_447064ee4442da05ad4b4493466bcb3c.setContent(html_6a9dbb65c8f2fcc8d45ead72f47e1b4c);
        

        marker_b586e9fa61360293ff6f811a366117fc.bindPopup(popup_447064ee4442da05ad4b4493466bcb3c)
        ;

        
    
    
            var marker_a672bd0901e407b26cafd186bf3e19c6 = L.marker(
                [48.039059, -4.692348],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_8e249ec59ff330759416800d031cc702 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_a672bd0901e407b26cafd186bf3e19c6.setIcon(icon_8e249ec59ff330759416800d031cc702);
        
    
        var popup_3e0c9c2cb70ee1956798a1f8f9da949b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_5457cf4b2673d71a7aa5ace4069c8b60 = $(`&lt;div id=&quot;html_5457cf4b2673d71a7aa5ace4069c8b60&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGADALEN &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 126954 €&lt;/div&gt;`)[0];
            popup_3e0c9c2cb70ee1956798a1f8f9da949b.setContent(html_5457cf4b2673d71a7aa5ace4069c8b60);
        

        marker_a672bd0901e407b26cafd186bf3e19c6.bindPopup(popup_3e0c9c2cb70ee1956798a1f8f9da949b)
        ;

        
    
    
            var marker_a28d63488a19554b50ad89467cd97aa6 = L.marker(
                [48.039002, -4.692107],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_1de6b393dac8a1ecdee4066d7b18c417 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_a28d63488a19554b50ad89467cd97aa6.setIcon(icon_1de6b393dac8a1ecdee4066d7b18c417);
        
    
        var popup_8fd36cf4cd435d6568aee3fb7a4fdfd1 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_48d960fd732c30129aaeef31ddae5800 = $(`&lt;div id=&quot;html_48d960fd732c30129aaeef31ddae5800&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGADALEN &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 126954 €&lt;/div&gt;`)[0];
            popup_8fd36cf4cd435d6568aee3fb7a4fdfd1.setContent(html_48d960fd732c30129aaeef31ddae5800);
        

        marker_a28d63488a19554b50ad89467cd97aa6.bindPopup(popup_8fd36cf4cd435d6568aee3fb7a4fdfd1)
        ;

        
    
    
            var marker_15646db216330d66cba2fd639c2b8a95 = L.marker(
                [48.039295, -4.692184],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_1d9cc55d11999f7ea9e946e201b63bab = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_15646db216330d66cba2fd639c2b8a95.setIcon(icon_1d9cc55d11999f7ea9e946e201b63bab);
        
    
        var popup_68ad63bd487f6e19f4292effd36a62b3 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_643cf02b6c493dddeef0f9f0f396209b = $(`&lt;div id=&quot;html_643cf02b6c493dddeef0f9f0f396209b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGADALEN &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 126954 €&lt;/div&gt;`)[0];
            popup_68ad63bd487f6e19f4292effd36a62b3.setContent(html_643cf02b6c493dddeef0f9f0f396209b);
        

        marker_15646db216330d66cba2fd639c2b8a95.bindPopup(popup_68ad63bd487f6e19f4292effd36a62b3)
        ;

        
    
    
            var marker_ad6eba0ab40788f57c80a1c42914a495 = L.marker(
                [48.039396, -4.695612],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_314596599b1bba3adc6ce06c89440384 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ad6eba0ab40788f57c80a1c42914a495.setIcon(icon_314596599b1bba3adc6ce06c89440384);
        
    
        var popup_0f7c19a453def21607f5dfeaea173693 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_15d379b8b6127dd47b8530e669f4c488 = $(`&lt;div id=&quot;html_15d379b8b6127dd47b8530e669f4c488&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERVEUR &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 110000 €&lt;/div&gt;`)[0];
            popup_0f7c19a453def21607f5dfeaea173693.setContent(html_15d379b8b6127dd47b8530e669f4c488);
        

        marker_ad6eba0ab40788f57c80a1c42914a495.bindPopup(popup_0f7c19a453def21607f5dfeaea173693)
        ;

        
    
    
            var marker_87084b7754e4b6474ebfd470ca3e7927 = L.marker(
                [48.039341, -4.695469],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_bbd9bfb823c4c93be0d739fadb6870b9 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_87084b7754e4b6474ebfd470ca3e7927.setIcon(icon_bbd9bfb823c4c93be0d739fadb6870b9);
        
    
        var popup_e90d9cf27d3c8b9c54dd52b524f01060 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_f82352a1f990f3439a9c63b67f6605c5 = $(`&lt;div id=&quot;html_f82352a1f990f3439a9c63b67f6605c5&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERVEUR &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 110000 €&lt;/div&gt;`)[0];
            popup_e90d9cf27d3c8b9c54dd52b524f01060.setContent(html_f82352a1f990f3439a9c63b67f6605c5);
        

        marker_87084b7754e4b6474ebfd470ca3e7927.bindPopup(popup_e90d9cf27d3c8b9c54dd52b524f01060)
        ;

        
    
    
            var marker_4385fb13bd75931bb3645dd62b75e12e = L.marker(
                [48.039154, -4.696306],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_3f2ede96d9610d05cece0377e9232617 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_4385fb13bd75931bb3645dd62b75e12e.setIcon(icon_3f2ede96d9610d05cece0377e9232617);
        
    
        var popup_98957480469b59d79e3d871c75afa9bd = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_795d70c6dc4510e6ba6016120a42d1c4 = $(`&lt;div id=&quot;html_795d70c6dc4510e6ba6016120a42d1c4&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 529 KERVEUR &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 79000 €&lt;/div&gt;`)[0];
            popup_98957480469b59d79e3d871c75afa9bd.setContent(html_795d70c6dc4510e6ba6016120a42d1c4);
        

        marker_4385fb13bd75931bb3645dd62b75e12e.bindPopup(popup_98957480469b59d79e3d871c75afa9bd)
        ;

        
    
    
            var marker_19e38d439df984ae390de38287a00ae6 = L.marker(
                [48.039104, -4.6964],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_993fdbe92b3352086214596babd270d4 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_19e38d439df984ae390de38287a00ae6.setIcon(icon_993fdbe92b3352086214596babd270d4);
        
    
        var popup_f9057396b0592c58627957f2149c402c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_cf19de9e64c96b36345f6fea8c9f09e9 = $(`&lt;div id=&quot;html_cf19de9e64c96b36345f6fea8c9f09e9&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERVEUR &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 79000 €&lt;/div&gt;`)[0];
            popup_f9057396b0592c58627957f2149c402c.setContent(html_cf19de9e64c96b36345f6fea8c9f09e9);
        

        marker_19e38d439df984ae390de38287a00ae6.bindPopup(popup_f9057396b0592c58627957f2149c402c)
        ;

        
    
    
            var marker_69655a4bae55d05386a61f0bf8d08b7b = L.marker(
                [48.036976, -4.690694],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_eb438022aad64d54b9c20c8dc1608a69 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_69655a4bae55d05386a61f0bf8d08b7b.setIcon(icon_eb438022aad64d54b9c20c8dc1608a69);
        
    
        var popup_a3dab6708873034e14ff5b03d6ea77ea = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_735ba2a0d5b7a7913abb5f7f765afb28 = $(`&lt;div id=&quot;html_735ba2a0d5b7a7913abb5f7f765afb28&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_a3dab6708873034e14ff5b03d6ea77ea.setContent(html_735ba2a0d5b7a7913abb5f7f765afb28);
        

        marker_69655a4bae55d05386a61f0bf8d08b7b.bindPopup(popup_a3dab6708873034e14ff5b03d6ea77ea)
        ;

        
    
    
            var marker_caf7d38c4ce051f7d660d858f9871973 = L.marker(
                [48.036808, -4.690624],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d2ca7b7ae00c25568ce058b4f61282d9 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_caf7d38c4ce051f7d660d858f9871973.setIcon(icon_d2ca7b7ae00c25568ce058b4f61282d9);
        
    
        var popup_21573e1d2df478074331486f45e13fc6 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c77d89a1de976aeb289cfe9394d0dcb5 = $(`&lt;div id=&quot;html_c77d89a1de976aeb289cfe9394d0dcb5&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_21573e1d2df478074331486f45e13fc6.setContent(html_c77d89a1de976aeb289cfe9394d0dcb5);
        

        marker_caf7d38c4ce051f7d660d858f9871973.bindPopup(popup_21573e1d2df478074331486f45e13fc6)
        ;

        
    
    
            var marker_f0c39a646e71d016a97b3b574db2ba45 = L.marker(
                [48.036033, -4.693366],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_9af8a8a95ddb4a3102fdad9abf6f6f03 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_f0c39a646e71d016a97b3b574db2ba45.setIcon(icon_9af8a8a95ddb4a3102fdad9abf6f6f03);
        
    
        var popup_320917ebdfd6609392490b495dc2ccd2 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_269bbd3d6563db387bcc70b047118d13 = $(`&lt;div id=&quot;html_269bbd3d6563db387bcc70b047118d13&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_320917ebdfd6609392490b495dc2ccd2.setContent(html_269bbd3d6563db387bcc70b047118d13);
        

        marker_f0c39a646e71d016a97b3b574db2ba45.bindPopup(popup_320917ebdfd6609392490b495dc2ccd2)
        ;

        
    
    
            var marker_e680bcabb9354e67e2728166d3175b5d = L.marker(
                [48.036084, -4.693148],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_3080edf86b319cc20fff25117a5b2de4 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_e680bcabb9354e67e2728166d3175b5d.setIcon(icon_3080edf86b319cc20fff25117a5b2de4);
        
    
        var popup_75e71b4efdba49658d41891561a599bb = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9366d57dede2ab7b290f89e0acff9c60 = $(`&lt;div id=&quot;html_9366d57dede2ab7b290f89e0acff9c60&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 469 KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_75e71b4efdba49658d41891561a599bb.setContent(html_9366d57dede2ab7b290f89e0acff9c60);
        

        marker_e680bcabb9354e67e2728166d3175b5d.bindPopup(popup_75e71b4efdba49658d41891561a599bb)
        ;

        
    
    
            var marker_f0b1aa6fcc3b8c26587092785cc1a347 = L.marker(
                [48.039218, -4.696355],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_9460361e9f9ec687a8e5dc718a7eecb7 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_f0b1aa6fcc3b8c26587092785cc1a347.setIcon(icon_9460361e9f9ec687a8e5dc718a7eecb7);
        
    
        var popup_4d30a5eb4006ed2f9a0e396769e43cf2 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d9c8f129e57c6b32e05a1715d6a60124 = $(`&lt;div id=&quot;html_d9c8f129e57c6b32e05a1715d6a60124&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERVEUR &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 3130 €&lt;/div&gt;`)[0];
            popup_4d30a5eb4006ed2f9a0e396769e43cf2.setContent(html_d9c8f129e57c6b32e05a1715d6a60124);
        

        marker_f0b1aa6fcc3b8c26587092785cc1a347.bindPopup(popup_4d30a5eb4006ed2f9a0e396769e43cf2)
        ;

        
    
    
            var marker_1c7e9c0796c00888876881abe2dd3fce = L.marker(
                [48.039218, -4.696355],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_0b2832b59e59b836515b347390f6353e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_1c7e9c0796c00888876881abe2dd3fce.setIcon(icon_0b2832b59e59b836515b347390f6353e);
        
    
        var popup_af18a133ccf64df9294dc87969578955 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_fab0e37b39f1ae37a7bcc328f9ad071e = $(`&lt;div id=&quot;html_fab0e37b39f1ae37a7bcc328f9ad071e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERVEUR &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 3130 €&lt;/div&gt;`)[0];
            popup_af18a133ccf64df9294dc87969578955.setContent(html_fab0e37b39f1ae37a7bcc328f9ad071e);
        

        marker_1c7e9c0796c00888876881abe2dd3fce.bindPopup(popup_af18a133ccf64df9294dc87969578955)
        ;

        
    
    
            var marker_fad9388d8350d287917fa0fa6a0384ef = L.marker(
                [48.039218, -4.696355],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_612f999e3f72a1f1e3b309da8d5ee1ac = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_fad9388d8350d287917fa0fa6a0384ef.setIcon(icon_612f999e3f72a1f1e3b309da8d5ee1ac);
        
    
        var popup_b422d26d64dfca7d9b9772e46e5df707 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_66ab08d3a37bfb1b7161d1dce4aece90 = $(`&lt;div id=&quot;html_66ab08d3a37bfb1b7161d1dce4aece90&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERVEUR &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 79000 €&lt;/div&gt;`)[0];
            popup_b422d26d64dfca7d9b9772e46e5df707.setContent(html_66ab08d3a37bfb1b7161d1dce4aece90);
        

        marker_fad9388d8350d287917fa0fa6a0384ef.bindPopup(popup_b422d26d64dfca7d9b9772e46e5df707)
        ;

        
    
    
            var marker_6e11227ee67f8c4594d7d48d13e30238 = L.marker(
                [48.039218, -4.696355],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_16662b7584a71ee6a57a73846f27d290 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_6e11227ee67f8c4594d7d48d13e30238.setIcon(icon_16662b7584a71ee6a57a73846f27d290);
        
    
        var popup_a453c21decc0f31bef18226eb9abdbaf = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e3ce79c138eed143ea15deccff1c43a2 = $(`&lt;div id=&quot;html_e3ce79c138eed143ea15deccff1c43a2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERVEUR &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 79000 €&lt;/div&gt;`)[0];
            popup_a453c21decc0f31bef18226eb9abdbaf.setContent(html_e3ce79c138eed143ea15deccff1c43a2);
        

        marker_6e11227ee67f8c4594d7d48d13e30238.bindPopup(popup_a453c21decc0f31bef18226eb9abdbaf)
        ;

        
    
    
            var marker_af19f9254e3eeb5e160b693255b2f4e0 = L.marker(
                [48.036276, -4.688193],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_33444cb093e9063482d0512b51958807 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_af19f9254e3eeb5e160b693255b2f4e0.setIcon(icon_33444cb093e9063482d0512b51958807);
        
    
        var popup_10e056e23a2e81eaa3a8051d7cbc0a8f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_f53d0d820565757bd530eaecbff0f1ea = $(`&lt;div id=&quot;html_f53d0d820565757bd530eaecbff0f1ea&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERGOUNEAU &lt;br&gt;Vente en 2016 &lt;br&gt;Prix 78000 €&lt;/div&gt;`)[0];
            popup_10e056e23a2e81eaa3a8051d7cbc0a8f.setContent(html_f53d0d820565757bd530eaecbff0f1ea);
        

        marker_af19f9254e3eeb5e160b693255b2f4e0.bindPopup(popup_10e056e23a2e81eaa3a8051d7cbc0a8f)
        ;

        
    
    
            var marker_d1e1b0b9023db6e54e63ed96e2b2bb75 = L.marker(
                [48.039613, -4.702379],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_a7ef9c6ee9f30202fcd6663295aea9d8 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_d1e1b0b9023db6e54e63ed96e2b2bb75.setIcon(icon_a7ef9c6ee9f30202fcd6663295aea9d8);
        
    
        var popup_eff2e973832fff72a43e4333c25b87ad = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_f8190981c75455a42c4ec28cc2df6938 = $(`&lt;div id=&quot;html_f8190981c75455a42c4ec28cc2df6938&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 518 DES LANGOUSTIERS &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 85000 €&lt;/div&gt;`)[0];
            popup_eff2e973832fff72a43e4333c25b87ad.setContent(html_f8190981c75455a42c4ec28cc2df6938);
        

        marker_d1e1b0b9023db6e54e63ed96e2b2bb75.bindPopup(popup_eff2e973832fff72a43e4333c25b87ad)
        ;

        
    
    
            var marker_367a87691f7df16b5cc8862f62a7fda4 = L.marker(
                [48.039673, -4.702259],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_1c9bdb7776ade98011e131ee25c10308 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_367a87691f7df16b5cc8862f62a7fda4.setIcon(icon_1c9bdb7776ade98011e131ee25c10308);
        
    
        var popup_7c2a903bb10dea0c4c557689f1306901 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e690b015cf571bae650b0153ca7132f3 = $(`&lt;div id=&quot;html_e690b015cf571bae650b0153ca7132f3&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESCOFF &lt;br&gt;Vente en 2019 &lt;br&gt;Prix 63000 €&lt;/div&gt;`)[0];
            popup_7c2a903bb10dea0c4c557689f1306901.setContent(html_e690b015cf571bae650b0153ca7132f3);
        

        marker_367a87691f7df16b5cc8862f62a7fda4.bindPopup(popup_7c2a903bb10dea0c4c557689f1306901)
        ;

        
    
    
            var marker_62b8257d424e0e8de562ab1d1682b07a = L.marker(
                [48.039692, -4.70207],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_0baa169b260d4e6efba9b707f78a7741 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_62b8257d424e0e8de562ab1d1682b07a.setIcon(icon_0baa169b260d4e6efba9b707f78a7741);
        
    
        var popup_2c5c90370a13906f9b03f5f122d6bb82 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_f606a315ce515505534df2ce6d2c7254 = $(`&lt;div id=&quot;html_f606a315ce515505534df2ce6d2c7254&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 519 DES LANGOUSTIERS &lt;br&gt;Vente en 2019 &lt;br&gt;Prix 63000 €&lt;/div&gt;`)[0];
            popup_2c5c90370a13906f9b03f5f122d6bb82.setContent(html_f606a315ce515505534df2ce6d2c7254);
        

        marker_62b8257d424e0e8de562ab1d1682b07a.bindPopup(popup_2c5c90370a13906f9b03f5f122d6bb82)
        ;

        
    
    
            var marker_862ee9631a6082c1abfc79b97193a8b3 = L.marker(
                [48.039564, -4.699931],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_1d5dd63bfa39f5f7958a579fc47ed025 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_862ee9631a6082c1abfc79b97193a8b3.setIcon(icon_1d5dd63bfa39f5f7958a579fc47ed025);
        
    
        var popup_57fb50d6e683e0804def3482bdedea6a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_841e6501e3447fde8f51082589a2a5f7 = $(`&lt;div id=&quot;html_841e6501e3447fde8f51082589a2a5f7&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHERNEAU &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 67000 €&lt;/div&gt;`)[0];
            popup_57fb50d6e683e0804def3482bdedea6a.setContent(html_841e6501e3447fde8f51082589a2a5f7);
        

        marker_862ee9631a6082c1abfc79b97193a8b3.bindPopup(popup_57fb50d6e683e0804def3482bdedea6a)
        ;

        
    
    
            var marker_75ee29dcc868b115220e09e72e5a3398 = L.marker(
                [48.03942, -4.699823],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_6d9aac159a6f2cd45d8b8f1862aade23 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_75ee29dcc868b115220e09e72e5a3398.setIcon(icon_6d9aac159a6f2cd45d8b8f1862aade23);
        
    
        var popup_1360f653c43527b45aafd6ab51fb9309 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_0e2091b53336e2a8bbb0f1ad77f09497 = $(`&lt;div id=&quot;html_0e2091b53336e2a8bbb0f1ad77f09497&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 522 KERHERNEAU &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 67000 €&lt;/div&gt;`)[0];
            popup_1360f653c43527b45aafd6ab51fb9309.setContent(html_0e2091b53336e2a8bbb0f1ad77f09497);
        

        marker_75ee29dcc868b115220e09e72e5a3398.bindPopup(popup_1360f653c43527b45aafd6ab51fb9309)
        ;

        
    
    
            var marker_5c13ac5327875ee5853b00c9a162e10f = L.marker(
                [48.038956, -4.700808],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_0e90e9a6710431d58a52bfb9b21f5d07 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_5c13ac5327875ee5853b00c9a162e10f.setIcon(icon_0e90e9a6710431d58a52bfb9b21f5d07);
        
    
        var popup_990b4eaad7e3d0f97a950478e8d3090f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_280d9c615effd1bdfc3748dc544f8fd2 = $(`&lt;div id=&quot;html_280d9c615effd1bdfc3748dc544f8fd2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 512 KERHERNEAU &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 90000 €&lt;/div&gt;`)[0];
            popup_990b4eaad7e3d0f97a950478e8d3090f.setContent(html_280d9c615effd1bdfc3748dc544f8fd2);
        

        marker_5c13ac5327875ee5853b00c9a162e10f.bindPopup(popup_990b4eaad7e3d0f97a950478e8d3090f)
        ;

        
    
    
            var marker_ce1aaa87c6aae3df9d25aedce2d0ae4f = L.marker(
                [48.036296, -4.697725],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_0bd798c1cbe52966bd268f8f3d5d8b0a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ce1aaa87c6aae3df9d25aedce2d0ae4f.setIcon(icon_0bd798c1cbe52966bd268f8f3d5d8b0a);
        
    
        var popup_989b95f38b7d7bf2f6604b28a8439c86 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_fd52935d0414517fe093bb5dc1f33d80 = $(`&lt;div id=&quot;html_fd52935d0414517fe093bb5dc1f33d80&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_989b95f38b7d7bf2f6604b28a8439c86.setContent(html_fd52935d0414517fe093bb5dc1f33d80);
        

        marker_ce1aaa87c6aae3df9d25aedce2d0ae4f.bindPopup(popup_989b95f38b7d7bf2f6604b28a8439c86)
        ;

        
    
    
            var marker_e4cc869859ca75daeaa8117bf831a896 = L.marker(
                [48.036447, -4.697202],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_945a1def0eb3440f2fde0561c79a839c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_e4cc869859ca75daeaa8117bf831a896.setIcon(icon_945a1def0eb3440f2fde0561c79a839c);
        
    
        var popup_a9bab85ee43ff5541eaf95cf7a8bbae4 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9f6ca4f7533329c265aa235fb82aa5a7 = $(`&lt;div id=&quot;html_9f6ca4f7533329c265aa235fb82aa5a7&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_a9bab85ee43ff5541eaf95cf7a8bbae4.setContent(html_9f6ca4f7533329c265aa235fb82aa5a7);
        

        marker_e4cc869859ca75daeaa8117bf831a896.bindPopup(popup_a9bab85ee43ff5541eaf95cf7a8bbae4)
        ;

        
    
    
            var marker_41b3f8a7eba2d84f8344da6600f2cf01 = L.marker(
                [48.035864, -4.697461],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_68235bb7d2ccf1e31acfb7326fe7665c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_41b3f8a7eba2d84f8344da6600f2cf01.setIcon(icon_68235bb7d2ccf1e31acfb7326fe7665c);
        
    
        var popup_c49fb0a96933c634a52abf6ec71a561a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_002ad5c2e4acf05d47c2006d253decae = $(`&lt;div id=&quot;html_002ad5c2e4acf05d47c2006d253decae&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_c49fb0a96933c634a52abf6ec71a561a.setContent(html_002ad5c2e4acf05d47c2006d253decae);
        

        marker_41b3f8a7eba2d84f8344da6600f2cf01.bindPopup(popup_c49fb0a96933c634a52abf6ec71a561a)
        ;

        
    
    
            var marker_0273889a240703c6b4d03880492e28f4 = L.marker(
                [48.035463, -4.696018],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_e1232bfadb9457784ab61e7d5db735c5 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_0273889a240703c6b4d03880492e28f4.setIcon(icon_e1232bfadb9457784ab61e7d5db735c5);
        
    
        var popup_b3eb61c3f6f88f0ee75a8b4ac9080f86 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_6655881dfa224fdd21c0988b98f020b3 = $(`&lt;div id=&quot;html_6655881dfa224fdd21c0988b98f020b3&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 2000 €&lt;/div&gt;`)[0];
            popup_b3eb61c3f6f88f0ee75a8b4ac9080f86.setContent(html_6655881dfa224fdd21c0988b98f020b3);
        

        marker_0273889a240703c6b4d03880492e28f4.bindPopup(popup_b3eb61c3f6f88f0ee75a8b4ac9080f86)
        ;

        
    
    
            var marker_6b7555e88bf59cc9daf226c53e96e8c9 = L.marker(
                [48.035472, -4.695434],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_3765a3f4e5a7138721b44b4ea291431e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_6b7555e88bf59cc9daf226c53e96e8c9.setIcon(icon_3765a3f4e5a7138721b44b4ea291431e);
        
    
        var popup_c513299b652ca353e7c3869571c70095 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7740a105d2edb6e9add7b37452407957 = $(`&lt;div id=&quot;html_7740a105d2edb6e9add7b37452407957&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 2000 €&lt;/div&gt;`)[0];
            popup_c513299b652ca353e7c3869571c70095.setContent(html_7740a105d2edb6e9add7b37452407957);
        

        marker_6b7555e88bf59cc9daf226c53e96e8c9.bindPopup(popup_c513299b652ca353e7c3869571c70095)
        ;

        
    
    
            var marker_ac93568f10add66215ecc72cb58b4eed = L.marker(
                [48.034764, -4.695967],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_98e74eb9e981c377ab5a62938aa9a357 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_ac93568f10add66215ecc72cb58b4eed.setIcon(icon_98e74eb9e981c377ab5a62938aa9a357);
        
    
        var popup_b2ac63416065e963b9a608db909a0b46 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_3f609d4e02e7f4e2bb6fdcba3e30b9a3 = $(`&lt;div id=&quot;html_3f609d4e02e7f4e2bb6fdcba3e30b9a3&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_b2ac63416065e963b9a608db909a0b46.setContent(html_3f609d4e02e7f4e2bb6fdcba3e30b9a3);
        

        marker_ac93568f10add66215ecc72cb58b4eed.bindPopup(popup_b2ac63416065e963b9a608db909a0b46)
        ;

        
    
    
            var marker_0bfb19bee9457e0b5e5f87493cad6643 = L.marker(
                [48.035936, -4.698135],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_ba5a005fcd83a38bc0b5426eef2439e3 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_0bfb19bee9457e0b5e5f87493cad6643.setIcon(icon_ba5a005fcd83a38bc0b5426eef2439e3);
        
    
        var popup_393de595cc8b230d84ca4620cd312264 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c4cb2cd884f800ad8c637e9896f1ae1f = $(`&lt;div id=&quot;html_c4cb2cd884f800ad8c637e9896f1ae1f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERLEDEC &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_393de595cc8b230d84ca4620cd312264.setContent(html_c4cb2cd884f800ad8c637e9896f1ae1f);
        

        marker_0bfb19bee9457e0b5e5f87493cad6643.bindPopup(popup_393de595cc8b230d84ca4620cd312264)
        ;

        
    
    
            var marker_54371da2a9e21eeb448ddbbbdec94c78 = L.marker(
                [48.037184, -4.700004],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_57dbaedf700a99289155ebb1c7a6839f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_54371da2a9e21eeb448ddbbbdec94c78.setIcon(icon_57dbaedf700a99289155ebb1c7a6839f);
        
    
        var popup_fc00cc172d78e5263d8a3d7d9170cac2 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_41ee7ed05c89e8b62a5bd753b2a8f8f6 = $(`&lt;div id=&quot;html_41ee7ed05c89e8b62a5bd753b2a8f8f6&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 501 KERLEDEC &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 105000 €&lt;/div&gt;`)[0];
            popup_fc00cc172d78e5263d8a3d7d9170cac2.setContent(html_41ee7ed05c89e8b62a5bd753b2a8f8f6);
        

        marker_54371da2a9e21eeb448ddbbbdec94c78.bindPopup(popup_fc00cc172d78e5263d8a3d7d9170cac2)
        ;

        
    
    
            var marker_45a23080c7707bba73a5fa66af7549c8 = L.marker(
                [48.0353, -4.695154],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_5613f6bbf96b8d00aa0096e31e9b859a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_45a23080c7707bba73a5fa66af7549c8.setIcon(icon_5613f6bbf96b8d00aa0096e31e9b859a);
        
    
        var popup_ca9e57fa4086e3aff38c7af71a210000 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c66eaa96f562046c487471986c991bcb = $(`&lt;div id=&quot;html_c66eaa96f562046c487471986c991bcb&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 2000 €&lt;/div&gt;`)[0];
            popup_ca9e57fa4086e3aff38c7af71a210000.setContent(html_c66eaa96f562046c487471986c991bcb);
        

        marker_45a23080c7707bba73a5fa66af7549c8.bindPopup(popup_ca9e57fa4086e3aff38c7af71a210000)
        ;

        
    
    
            var marker_98117c61f0a6090932e99a7147b907b9 = L.marker(
                [48.033405, -4.697879],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_db7304a652e0f7249eb219b2e2285b94 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_98117c61f0a6090932e99a7147b907b9.setIcon(icon_db7304a652e0f7249eb219b2e2285b94);
        
    
        var popup_686e427e1b4ded3f73c5555546082c08 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_cfbb951b0be7e86919eb2e2622111dca = $(`&lt;div id=&quot;html_cfbb951b0be7e86919eb2e2622111dca&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENDREFF &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 1000 €&lt;/div&gt;`)[0];
            popup_686e427e1b4ded3f73c5555546082c08.setContent(html_cfbb951b0be7e86919eb2e2622111dca);
        

        marker_98117c61f0a6090932e99a7147b907b9.bindPopup(popup_686e427e1b4ded3f73c5555546082c08)
        ;

        
    
    
            var marker_62e7f35b0d416ab9004b18ea15a86cbf = L.marker(
                [48.034132, -4.697513],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_769c639add683fb31eece9e3eac99fea = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_62e7f35b0d416ab9004b18ea15a86cbf.setIcon(icon_769c639add683fb31eece9e3eac99fea);
        
    
        var popup_1712948f8c67e9352c3a7141fbcd5f5f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_418f445eb9577969e31391c8363a47c9 = $(`&lt;div id=&quot;html_418f445eb9577969e31391c8363a47c9&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENDREFF &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 2600 €&lt;/div&gt;`)[0];
            popup_1712948f8c67e9352c3a7141fbcd5f5f.setContent(html_418f445eb9577969e31391c8363a47c9);
        

        marker_62e7f35b0d416ab9004b18ea15a86cbf.bindPopup(popup_1712948f8c67e9352c3a7141fbcd5f5f)
        ;

        
    
    
            var marker_06d099b5c61694f5a0b34a5d020da510 = L.marker(
                [48.034179, -4.69737],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_230fea9c45e565f63e66df6f6fd8a670 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_06d099b5c61694f5a0b34a5d020da510.setIcon(icon_230fea9c45e565f63e66df6f6fd8a670);
        
    
        var popup_fc7692fb42957166f06c17d9f64904fb = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ec20b1184c6f146afd136a22b77bf32c = $(`&lt;div id=&quot;html_ec20b1184c6f146afd136a22b77bf32c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENDREFF &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 2600 €&lt;/div&gt;`)[0];
            popup_fc7692fb42957166f06c17d9f64904fb.setContent(html_ec20b1184c6f146afd136a22b77bf32c);
        

        marker_06d099b5c61694f5a0b34a5d020da510.bindPopup(popup_fc7692fb42957166f06c17d9f64904fb)
        ;

        
    
    
            var marker_a67f26af3ab85e4b8947e190a2a1579b = L.marker(
                [48.034256, -4.697217],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_fae587b94e70c1f6be3e88028fd93873 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_a67f26af3ab85e4b8947e190a2a1579b.setIcon(icon_fae587b94e70c1f6be3e88028fd93873);
        
    
        var popup_05f325d7594a5c4afb15509ee170cf1c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_aafa40dacae87dbbda96b40d50839e9f = $(`&lt;div id=&quot;html_aafa40dacae87dbbda96b40d50839e9f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENDREFF &lt;br&gt;Vente en 2017 &lt;br&gt;Prix 2600 €&lt;/div&gt;`)[0];
            popup_05f325d7594a5c4afb15509ee170cf1c.setContent(html_aafa40dacae87dbbda96b40d50839e9f);
        

        marker_a67f26af3ab85e4b8947e190a2a1579b.bindPopup(popup_05f325d7594a5c4afb15509ee170cf1c)
        ;

        
    
    
            var marker_933eba0e6b7c9d21af6322710e997126 = L.marker(
                [48.033896, -4.696278],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_e59b8f259eed493f5bc71f805acce3f2 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_933eba0e6b7c9d21af6322710e997126.setIcon(icon_e59b8f259eed493f5bc71f805acce3f2);
        
    
        var popup_56dac8217e9a627b38e43925dda53360 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7f28df0b09ab15df989ef8780c9f52e1 = $(`&lt;div id=&quot;html_7f28df0b09ab15df989ef8780c9f52e1&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENDREFF &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_56dac8217e9a627b38e43925dda53360.setContent(html_7f28df0b09ab15df989ef8780c9f52e1);
        

        marker_933eba0e6b7c9d21af6322710e997126.bindPopup(popup_56dac8217e9a627b38e43925dda53360)
        ;

        
    
    
            var marker_0afbc3727abe6860de5222a6db117530 = L.marker(
                [48.033771, -4.696386],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d81a98aaeaa4f7669a87055aea25abc8 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_0afbc3727abe6860de5222a6db117530.setIcon(icon_d81a98aaeaa4f7669a87055aea25abc8);
        
    
        var popup_e3ced8747144d8641a4760c09e79b1c6 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_173ee2df84b6ee31dcab245eb34c5e75 = $(`&lt;div id=&quot;html_173ee2df84b6ee31dcab245eb34c5e75&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENDREFF &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_e3ced8747144d8641a4760c09e79b1c6.setContent(html_173ee2df84b6ee31dcab245eb34c5e75);
        

        marker_0afbc3727abe6860de5222a6db117530.bindPopup(popup_e3ced8747144d8641a4760c09e79b1c6)
        ;

        
    
    
            var marker_2241f06ec692abda9b4afe8137980929 = L.marker(
                [48.033917, -4.695076],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_71cd8e01cc0880669914b09984e259e8 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_2241f06ec692abda9b4afe8137980929.setIcon(icon_71cd8e01cc0880669914b09984e259e8);
        
    
        var popup_3e4caddcf550dd2cc48797cdefaf2e55 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_afe9cca101a6eff468459f4b3053c511 = $(`&lt;div id=&quot;html_afe9cca101a6eff468459f4b3053c511&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENDREFF &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_3e4caddcf550dd2cc48797cdefaf2e55.setContent(html_afe9cca101a6eff468459f4b3053c511);
        

        marker_2241f06ec692abda9b4afe8137980929.bindPopup(popup_3e4caddcf550dd2cc48797cdefaf2e55)
        ;

        
    
    
            var marker_54aad5d20615fd33312e0c64daab9b85 = L.marker(
                [48.034252, -4.69472],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d3cb2734bf0ef8a55e54ad2b3e490e54 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_54aad5d20615fd33312e0c64daab9b85.setIcon(icon_d3cb2734bf0ef8a55e54ad2b3e490e54);
        
    
        var popup_186f727562a2f9a703263d12bf2ae0ab = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_3031c73bd43347a7975752cec35c1bbd = $(`&lt;div id=&quot;html_3031c73bd43347a7975752cec35c1bbd&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_186f727562a2f9a703263d12bf2ae0ab.setContent(html_3031c73bd43347a7975752cec35c1bbd);
        

        marker_54aad5d20615fd33312e0c64daab9b85.bindPopup(popup_186f727562a2f9a703263d12bf2ae0ab)
        ;

        
    
    
            var marker_3d0c7174edfcc1c55df34be43b292257 = L.marker(
                [48.034656, -4.694467],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_649f7841db1a7319b7ed2fc48a799118 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_3d0c7174edfcc1c55df34be43b292257.setIcon(icon_649f7841db1a7319b7ed2fc48a799118);
        
    
        var popup_0b949b839bbbdcb02ce615c6d05c0b51 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_85ea24c98a3a975c62768f4435dacebf = $(`&lt;div id=&quot;html_85ea24c98a3a975c62768f4435dacebf&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_0b949b839bbbdcb02ce615c6d05c0b51.setContent(html_85ea24c98a3a975c62768f4435dacebf);
        

        marker_3d0c7174edfcc1c55df34be43b292257.bindPopup(popup_0b949b839bbbdcb02ce615c6d05c0b51)
        ;

        
    
    
            var marker_55f82de4a6c00ef7cea560f677443331 = L.marker(
                [48.034764, -4.693713],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_142a5f6639a347083d8f6a7db408b733 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_55f82de4a6c00ef7cea560f677443331.setIcon(icon_142a5f6639a347083d8f6a7db408b733);
        
    
        var popup_ca54e703b39042835aab03c95b283fc6 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_210147cf07f6f851ef0b2274a5ad5be8 = $(`&lt;div id=&quot;html_210147cf07f6f851ef0b2274a5ad5be8&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_ca54e703b39042835aab03c95b283fc6.setContent(html_210147cf07f6f851ef0b2274a5ad5be8);
        

        marker_55f82de4a6c00ef7cea560f677443331.bindPopup(popup_ca54e703b39042835aab03c95b283fc6)
        ;

        
    
    
            var marker_a2aee6fd028a6ed697291878a309cba7 = L.marker(
                [48.035019, -4.692941],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_f880fc9d2d388f2a2772c52695efb127 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_a2aee6fd028a6ed697291878a309cba7.setIcon(icon_f880fc9d2d388f2a2772c52695efb127);
        
    
        var popup_a0ec5ee37a330f2ef812808c9ac3f84e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a4838ada72553f0ed9b6fd5c67c4e53d = $(`&lt;div id=&quot;html_a4838ada72553f0ed9b6fd5c67c4e53d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_a0ec5ee37a330f2ef812808c9ac3f84e.setContent(html_a4838ada72553f0ed9b6fd5c67c4e53d);
        

        marker_a2aee6fd028a6ed697291878a309cba7.bindPopup(popup_a0ec5ee37a330f2ef812808c9ac3f84e)
        ;

        
    
    
            var marker_7620b48af6123ed4fb8f41b0a0e6dc6f = L.marker(
                [48.033803, -4.692637],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_4974162909347455ad663dd69062edd6 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_7620b48af6123ed4fb8f41b0a0e6dc6f.setIcon(icon_4974162909347455ad663dd69062edd6);
        
    
        var popup_e3e69a7d2912220c5fa0dcf184fd85f5 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1d84786dc7db449df10ee053e28e66e2 = $(`&lt;div id=&quot;html_1d84786dc7db449df10ee053e28e66e2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_e3e69a7d2912220c5fa0dcf184fd85f5.setContent(html_1d84786dc7db449df10ee053e28e66e2);
        

        marker_7620b48af6123ed4fb8f41b0a0e6dc6f.bindPopup(popup_e3e69a7d2912220c5fa0dcf184fd85f5)
        ;

        
    
    
            var marker_a87f50a6c66214cc8cf17c9c6a1ab847 = L.marker(
                [48.034254, -4.692985],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_7fa8ac86983db06229dd971a9b67168e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_a87f50a6c66214cc8cf17c9c6a1ab847.setIcon(icon_7fa8ac86983db06229dd971a9b67168e);
        
    
        var popup_429924b567addd04320a23429aa8977e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1ad125a7599a97b666c85ff33cfa1c57 = $(`&lt;div id=&quot;html_1ad125a7599a97b666c85ff33cfa1c57&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_429924b567addd04320a23429aa8977e.setContent(html_1ad125a7599a97b666c85ff33cfa1c57);
        

        marker_a87f50a6c66214cc8cf17c9c6a1ab847.bindPopup(popup_429924b567addd04320a23429aa8977e)
        ;

        
    
    
            var marker_715c79240558e21a3723d2b401612203 = L.marker(
                [48.033044, -4.694456],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_04892d7dd1384807593a3e7286705510 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_715c79240558e21a3723d2b401612203.setIcon(icon_04892d7dd1384807593a3e7286705510);
        
    
        var popup_88c2282baeedfaa2a9e7797909fdf964 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a55137af6b7d6bc4772f64f883cf1ad7 = $(`&lt;div id=&quot;html_a55137af6b7d6bc4772f64f883cf1ad7&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_88c2282baeedfaa2a9e7797909fdf964.setContent(html_a55137af6b7d6bc4772f64f883cf1ad7);
        

        marker_715c79240558e21a3723d2b401612203.bindPopup(popup_88c2282baeedfaa2a9e7797909fdf964)
        ;

        
    
    
            var marker_e1a74ac2cae2d06cf0126bf4035cdf9b = L.marker(
                [48.032164, -4.695861],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d5aebb44a6d146206a77a9c82f5906da = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_e1a74ac2cae2d06cf0126bf4035cdf9b.setIcon(icon_d5aebb44a6d146206a77a9c82f5906da);
        
    
        var popup_49e71e157f90800ff888fbaa273df65e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7d64f7f01a26e5e4037d490e51e08106 = $(`&lt;div id=&quot;html_7d64f7f01a26e5e4037d490e51e08106&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENDREFF &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_49e71e157f90800ff888fbaa273df65e.setContent(html_7d64f7f01a26e5e4037d490e51e08106);
        

        marker_e1a74ac2cae2d06cf0126bf4035cdf9b.bindPopup(popup_49e71e157f90800ff888fbaa273df65e)
        ;

        
    
    
            var marker_5d4b4e36a5a0a5596989a60d73862df1 = L.marker(
                [48.032199, -4.695948],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_6492719905aabe08de76b4284844bf43 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_5d4b4e36a5a0a5596989a60d73862df1.setIcon(icon_6492719905aabe08de76b4284844bf43);
        
    
        var popup_35461c68c4c1626aeb3ff918de13359d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2c89cd39be8f6079479b6ac82ba3616b = $(`&lt;div id=&quot;html_2c89cd39be8f6079479b6ac82ba3616b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENDREFF &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_35461c68c4c1626aeb3ff918de13359d.setContent(html_2c89cd39be8f6079479b6ac82ba3616b);
        

        marker_5d4b4e36a5a0a5596989a60d73862df1.bindPopup(popup_35461c68c4c1626aeb3ff918de13359d)
        ;

        
    
    
            var marker_f294c6836c0ded733b95b4618cdad6f7 = L.marker(
                [48.032363, -4.695963],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_d58d2b57c1aa0b2c2e9e54945a8a1e71 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_f294c6836c0ded733b95b4618cdad6f7.setIcon(icon_d58d2b57c1aa0b2c2e9e54945a8a1e71);
        
    
        var popup_2310f754f05bdbeb19f7e95fc0ab57eb = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_cc8b598f154a61aaecbdeb710cec14e6 = $(`&lt;div id=&quot;html_cc8b598f154a61aaecbdeb710cec14e6&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENDREFF &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_2310f754f05bdbeb19f7e95fc0ab57eb.setContent(html_cc8b598f154a61aaecbdeb710cec14e6);
        

        marker_f294c6836c0ded733b95b4618cdad6f7.bindPopup(popup_2310f754f05bdbeb19f7e95fc0ab57eb)
        ;

        
    
    
            var marker_78ad0db9e74a8f18ccd22525e75b6892 = L.marker(
                [48.032829, -4.695875],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_e7ad6ea85443a79db1a457534072f6f3 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_78ad0db9e74a8f18ccd22525e75b6892.setIcon(icon_e7ad6ea85443a79db1a457534072f6f3);
        
    
        var popup_704abafcd9c16f2b4b429290db5c1d20 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_de07ae405a4d3ead69f71148c37391c3 = $(`&lt;div id=&quot;html_de07ae405a4d3ead69f71148c37391c3&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENDREFF &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_704abafcd9c16f2b4b429290db5c1d20.setContent(html_de07ae405a4d3ead69f71148c37391c3);
        

        marker_78ad0db9e74a8f18ccd22525e75b6892.bindPopup(popup_704abafcd9c16f2b4b429290db5c1d20)
        ;

        
    
    
            var marker_cc6c7e083f7663724f4dec42b059575a = L.marker(
                [48.032868, -4.698845],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_694da4abc3fefab526d4cab3d40671a9 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_cc6c7e083f7663724f4dec42b059575a.setIcon(icon_694da4abc3fefab526d4cab3d40671a9);
        
    
        var popup_76da6f798679e7191f0e1f6e9704e1c3 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_49509d1faa863c1c009dbaeee0081dd4 = $(`&lt;div id=&quot;html_49509d1faa863c1c009dbaeee0081dd4&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENDREFF &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_76da6f798679e7191f0e1f6e9704e1c3.setContent(html_49509d1faa863c1c009dbaeee0081dd4);
        

        marker_cc6c7e083f7663724f4dec42b059575a.bindPopup(popup_76da6f798679e7191f0e1f6e9704e1c3)
        ;

        
    
    
            var marker_b4fb65d1cdf3e8470b0320511f9dda1c = L.marker(
                [48.034176, -4.692413],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_c54e63389f9ab7c0fccba754a0cb0ede = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_b4fb65d1cdf3e8470b0320511f9dda1c.setIcon(icon_c54e63389f9ab7c0fccba754a0cb0ede);
        
    
        var popup_eeb8436777d7f8cc6f74b9b16cbf6c1f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_def2d1e1137e741c61c7e6277d7e3223 = $(`&lt;div id=&quot;html_def2d1e1137e741c61c7e6277d7e3223&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_eeb8436777d7f8cc6f74b9b16cbf6c1f.setContent(html_def2d1e1137e741c61c7e6277d7e3223);
        

        marker_b4fb65d1cdf3e8470b0320511f9dda1c.bindPopup(popup_eeb8436777d7f8cc6f74b9b16cbf6c1f)
        ;

        
    
    
            var marker_37e8824b398c6834a2f381f812c56e19 = L.marker(
                [48.031321, -4.699822],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_bdab70f44518366e424d121501617b88 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_37e8824b398c6834a2f381f812c56e19.setIcon(icon_bdab70f44518366e424d121501617b88);
        
    
        var popup_cb1c4c26172c5fa82a74c3b4f6f92131 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_f29e03967ff8d72efad27ab7bba59d4b = $(`&lt;div id=&quot;html_f29e03967ff8d72efad27ab7bba59d4b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENDREFF &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_cb1c4c26172c5fa82a74c3b4f6f92131.setContent(html_f29e03967ff8d72efad27ab7bba59d4b);
        

        marker_37e8824b398c6834a2f381f812c56e19.bindPopup(popup_cb1c4c26172c5fa82a74c3b4f6f92131)
        ;

        
    
    
            var marker_c4c590be158e73797afe61680d6a6f4f = L.marker(
                [48.033613, -4.691981],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_8da96765e6725935a32fa3247ae67440 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_c4c590be158e73797afe61680d6a6f4f.setIcon(icon_8da96765e6725935a32fa3247ae67440);
        
    
        var popup_98f82348b1f07e24d0378340ee751a83 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_4184db1b34b09ddde056fb874cf59f89 = $(`&lt;div id=&quot;html_4184db1b34b09ddde056fb874cf59f89&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  KERHURET &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_98f82348b1f07e24d0378340ee751a83.setContent(html_4184db1b34b09ddde056fb874cf59f89);
        

        marker_c4c590be158e73797afe61680d6a6f4f.bindPopup(popup_98f82348b1f07e24d0378340ee751a83)
        ;

        
    
    
            var marker_d9c998e3e7b9d9be1973329d1dce514b = L.marker(
                [48.031735, -4.694329],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_1f14c015c5dda8cf1a9030a7cca7f326 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_d9c998e3e7b9d9be1973329d1dce514b.setIcon(icon_1f14c015c5dda8cf1a9030a7cca7f326);
        
    
        var popup_0589e43ed826bbd0e9ff1e3c2c759241 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e80afc9b39f2b2c4b8fd4e7b75d14908 = $(`&lt;div id=&quot;html_e80afc9b39f2b2c4b8fd4e7b75d14908&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENDREFF &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_0589e43ed826bbd0e9ff1e3c2c759241.setContent(html_e80afc9b39f2b2c4b8fd4e7b75d14908);
        

        marker_d9c998e3e7b9d9be1973329d1dce514b.bindPopup(popup_0589e43ed826bbd0e9ff1e3c2c759241)
        ;

        
    
    
            var marker_39be154f82601d3bd1cf95fc4ba98c09 = L.marker(
                [48.032211, -4.693393],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_ff2ea4ac75e5d01b2daee4b3756c9886 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_39be154f82601d3bd1cf95fc4ba98c09.setIcon(icon_ff2ea4ac75e5d01b2daee4b3756c9886);
        
    
        var popup_9dae71924d48af5917332e4106966621 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_83e35837734dcb14b6fada12636a5911 = $(`&lt;div id=&quot;html_83e35837734dcb14b6fada12636a5911&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENDREFF &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_9dae71924d48af5917332e4106966621.setContent(html_83e35837734dcb14b6fada12636a5911);
        

        marker_39be154f82601d3bd1cf95fc4ba98c09.bindPopup(popup_9dae71924d48af5917332e4106966621)
        ;

        
    
    
            var marker_90e51ac8ef6ae682f71563f7275563a8 = L.marker(
                [48.032453, -4.693736],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_7f9ed2da8758c7ca2597a96146e8965c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;red&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_90e51ac8ef6ae682f71563f7275563a8.setIcon(icon_7f9ed2da8758c7ca2597a96146e8965c);
        
    
        var popup_5a0e172b564c72550bc1f946995ac9f1 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e4a1e2024e98af265003cc91c71542e4 = $(`&lt;div id=&quot;html_e4a1e2024e98af265003cc91c71542e4&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  PENDREFF &lt;br&gt;Vente en 2018 &lt;br&gt;Prix 270000 €&lt;/div&gt;`)[0];
            popup_5a0e172b564c72550bc1f946995ac9f1.setContent(html_e4a1e2024e98af265003cc91c71542e4);
        

        marker_90e51ac8ef6ae682f71563f7275563a8.bindPopup(popup_5a0e172b564c72550bc1f946995ac9f1)
        ;

        
    
    
            var marker_9db8ba4f7d38c3db75f7b4efecb9bc79 = L.marker(
                [48.034415, -4.705258],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_9ecdf49fece60383893355e07d6b44c1 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_9db8ba4f7d38c3db75f7b4efecb9bc79.setIcon(icon_9ecdf49fece60383893355e07d6b44c1);
        
    
        var popup_51f24ce61a6d96c680864ca62a67eeb6 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_3ec4e8ac947c1933417d5c019083ca73 = $(`&lt;div id=&quot;html_3ec4e8ac947c1933417d5c019083ca73&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESCOFF &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 897 €&lt;/div&gt;`)[0];
            popup_51f24ce61a6d96c680864ca62a67eeb6.setContent(html_3ec4e8ac947c1933417d5c019083ca73);
        

        marker_9db8ba4f7d38c3db75f7b4efecb9bc79.bindPopup(popup_51f24ce61a6d96c680864ca62a67eeb6)
        ;

        
    
    
            var marker_36fa0a485fa367d97ee7a1642ce33c64 = L.marker(
                [48.037084, -4.712427],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_2c57e00fcbd207c1fbefe49c85eaadc2 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_36fa0a485fa367d97ee7a1642ce33c64.setIcon(icon_2c57e00fcbd207c1fbefe49c85eaadc2);
        
    
        var popup_e7fbf65d7a7afe37483f9c5a71317d30 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7320cc4d6aec30f1c39710e9db581978 = $(`&lt;div id=&quot;html_7320cc4d6aec30f1c39710e9db581978&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESCOFF &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 161500 €&lt;/div&gt;`)[0];
            popup_e7fbf65d7a7afe37483f9c5a71317d30.setContent(html_7320cc4d6aec30f1c39710e9db581978);
        

        marker_36fa0a485fa367d97ee7a1642ce33c64.bindPopup(popup_e7fbf65d7a7afe37483f9c5a71317d30)
        ;

        
    
    
            var marker_21e020e4db756ac056a670d5e9723860 = L.marker(
                [48.037312, -4.712316],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_15a004faf239af4be45bf30d49061fff = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;home&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_21e020e4db756ac056a670d5e9723860.setIcon(icon_15a004faf239af4be45bf30d49061fff);
        
    
        var popup_c42ef1fdaf1b81bf8b8cfbe496c8a3fb = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_6d0ca7c5a80aef6c01abcd3a829930ed = $(`&lt;div id=&quot;html_6d0ca7c5a80aef6c01abcd3a829930ed&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 290 LESCOFF &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 161500 €&lt;/div&gt;`)[0];
            popup_c42ef1fdaf1b81bf8b8cfbe496c8a3fb.setContent(html_6d0ca7c5a80aef6c01abcd3a829930ed);
        

        marker_21e020e4db756ac056a670d5e9723860.bindPopup(popup_c42ef1fdaf1b81bf8b8cfbe496c8a3fb)
        ;

        
    
    
            var marker_7130c505eec31e7dede3e03dfa8b99c0 = L.marker(
                [48.037312, -4.712316],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_507385587d162784411989939a04f0f2 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_7130c505eec31e7dede3e03dfa8b99c0.setIcon(icon_507385587d162784411989939a04f0f2);
        
    
        var popup_9ccba982629380451354b85f2de4bdeb = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_47cc4873c2ac7083d9df5ef0d49cf335 = $(`&lt;div id=&quot;html_47cc4873c2ac7083d9df5ef0d49cf335&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse: 290 LESCOFF &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 161500 €&lt;/div&gt;`)[0];
            popup_9ccba982629380451354b85f2de4bdeb.setContent(html_47cc4873c2ac7083d9df5ef0d49cf335);
        

        marker_7130c505eec31e7dede3e03dfa8b99c0.bindPopup(popup_9ccba982629380451354b85f2de4bdeb)
        ;

        
    
    
            var marker_2f9dc483b2de0a137c0b66d2735ffed2 = L.marker(
                [48.037271, -4.711856],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_80fa5fa5a09bf632e022e2a89bb115d3 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_2f9dc483b2de0a137c0b66d2735ffed2.setIcon(icon_80fa5fa5a09bf632e022e2a89bb115d3);
        
    
        var popup_cbf0c2a8dbccb1dba356a23ec676e21c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c7fe51c37b3645dbae67f25bac0a07fc = $(`&lt;div id=&quot;html_c7fe51c37b3645dbae67f25bac0a07fc&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  LESCOFF &lt;br&gt;Vente en 2015 &lt;br&gt;Prix 161500 €&lt;/div&gt;`)[0];
            popup_cbf0c2a8dbccb1dba356a23ec676e21c.setContent(html_c7fe51c37b3645dbae67f25bac0a07fc);
        

        marker_2f9dc483b2de0a137c0b66d2735ffed2.bindPopup(popup_cbf0c2a8dbccb1dba356a23ec676e21c)
        ;

        
    
    
            var marker_7d147a0ebf540535c5c300314d795254 = L.marker(
                [48.033956, -4.716009],
                {}
            ).addTo(map_115b72cdcb5fe41fbc0524ad7e0caf27);
        
    
            var icon_237166f8a9c6b72f3be97ae0a26158af = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;lightblue&quot;, &quot;prefix&quot;: &quot;glyphicon&quot;}
            );
            marker_7d147a0ebf540535c5c300314d795254.setIcon(icon_237166f8a9c6b72f3be97ae0a26158af);
        
    
        var popup_1e16d5b5541b8b7815a681631666470b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_bde870d6f2c33dd11961e0ac9d71c4ec = $(`&lt;div id=&quot;html_bde870d6f2c33dd11961e0ac9d71c4ec&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Adresse:  BESTREE &lt;br&gt;Vente en 2014 &lt;br&gt;Prix 897 €&lt;/div&gt;`)[0];
            popup_1e16d5b5541b8b7815a681631666470b.setContent(html_bde870d6f2c33dd11961e0ac9d71c4ec);
        

        marker_7d147a0ebf540535c5c300314d795254.bindPopup(popup_1e16d5b5541b8b7815a681631666470b)
        ;

        
    
    
            map_115b72cdcb5fe41fbc0524ad7e0caf27.fitBounds(
                [[48.027025, -4.717967], [48.043125, -4.633439]],
                {}
            );
        
&lt;/script&gt;" style="position:absolute;width:100%;height:100%;left:0;top:0;border:none !important;" allowfullscreen webkitallowfullscreen mozallowfullscreen></iframe></div></div>

{{< /rawhtml >}}

# Géocoder des données grâce aux API officielles

Jusqu'à présent, nous avons travaillés sur des données où la dimension
géographique était déjà présente ou relativement facile à intégrer.

Ce cas idéal ne se rencontre pas nécessairement dans la pratique.
On dispose parfois de localisations plus ou moins précises et plus ou
moins bien formattées pour déterminer la localisation de certains
lieux.

Depuis quelques années, un service officiel de géocodage a été mis en place.
Celui-ci est gratuit et permet de manière efficace de coder des adresses
à partir d'une API. Cette API, connue sous le nom de la Base d'Adresses Nationale
(BAN) a bénéficié de la mise en commun de données de plusieurs
acteurs (collectivités locales, Poste) et de compétences d'acteurs
comme Etalab. La documentation de celle-ci est disponible à l'adresse
https://api.gouv.fr/les-api/base-adresse-nationale

Pour illustrer la manière de géocoder des données avec `Python`, nous
allons partir de la base
[des résultats des auto-écoles à l'examen du permis sur l'année 2018](https://www.data.gouv.fr/fr/datasets/taux-de-reussite-auto-ecole-par-auto-ecole-en-2018/).

Ces données nécessitent un petit peu de travail pour être propres à une
analyse statistique. Après avoir renommé les colonnes, nous n'allons conserver que
les informations relatives au permis B (permis voiture classique) et
les auto-écoles ayant présenté au moins 20 personnes à l'examen.

``` python
import pandas as pd
import xlrd
import geopandas as gpd

df = pd.read_excel("https://www.data.gouv.fr/fr/datasets/r/d4b6b072-8a7d-4e04-a029-8cdbdbaf36a5", header = [0,1])

index_0 = ["" if df.columns[i][0].startswith("Unnamed") else df.columns[i][0] for i in range(len(df.columns))]
index_1 = [df.columns[i][1] for i in range(len(df.columns))]
keep_index = [True if el in ('', "B") else False for el in index_0] 

cols = [index_0[i] + " " + index_1[i].replace("+", "_") for i in range(len(df.columns))]
df.columns = cols
df = df.loc[:, keep_index]
df.columns = df.columns.str.replace("(^ |°)", "", regex = True).str.replace(" ", "_")
df = df.dropna(subset = ['B_NB'])
df = df.loc[~df["B_NB"].astype(str).str.contains("(\%|\.)"),:]

df['B_NB'] = df['B_NB'].astype(int)
df['B_TR'] = df['B_TR'].str.replace(",", ".").str.replace("%","").astype(float)

df = df.loc[df["B_NB"]>20]
```

    /tmp/ipykernel_32964/1059845781.py:16: UserWarning:

    This pattern is interpreted as a regular expression, and has match groups. To actually get the groups, use str.extract.

Sur cet échantillon, le taux de réussite moyen était, en 2018, de 58.02%

Nos informations géographiques prennent la forme suivante:

``` python
df.loc[:,['Adresse','CP','Ville']].head(5)
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Adresse</th>
      <th>CP</th>
      <th>Ville</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>56 RUE CHARLES ROBIN</td>
      <td>01000</td>
      <td>BOURG EN BRESSE</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7, avenue Revermont</td>
      <td>01250</td>
      <td>Ceyzeriat</td>
    </tr>
    <tr>
      <th>3</th>
      <td>72 PLACE DE LA MAIRIE</td>
      <td>01000</td>
      <td>SAINT-DENIS LES BOURG</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6 RUE DU LYCEE</td>
      <td>01000</td>
      <td>BOURG EN BRESSE</td>
    </tr>
    <tr>
      <th>5</th>
      <td>9 place Edgard Quinet</td>
      <td>01000</td>
      <td>BOURG EN BRESSE</td>
    </tr>
  </tbody>
</table>
</div>

Autrement dit, nous disposons d'une adresse, d'un code postal et d'un nom
de ville. Ces informations peuvent servir à faire une recherche
sur la localisation d'une auto-école.

## Utiliser l'API BAN

La [documentation officielle de l'API](https://adresse.data.gouv.fr/api-doc/adresse)
propose un certain nombre d'exemples de manière de géolocaliser des données.
Dans notre situation, deux points d'entrée paraissent intéressants:

-   L'API `/search/` qui représente un point d'entrée avec des URL de la forme
    https://api-adresse.data.gouv.fr/search/?q=\<adresse\>&postcode=\<codepostal\>&limit=1
-   L'API `/search/csv` qui prend un CSV en entrée et retourne ce même CSV avec
    les observations géocodées. La requête prend la forme suivante, en apparence
    moins simple à mettre en oeuvre :
    `curl -X POST -F data=@search.csv -F columns=adresse -F columns=postcode https://api-adresse.data.gouv.fr/search/csv/`

La tentation serait forte d'utiliser la première méthode avec une boucle sur les
lignes de notre DataFrame pour géocoder l'ensemble de notre jeu de données.
Cela serait néanmoins une mauvaise idée car les communications entre notre
session Python et les serveurs de l'API seraient beaucoup trop nombreuses
pour offrir des performances satisfaisantes.

Pour vous en convaincre, vous pouvez exécuter le code suivant sur un petit
échantillon de données (par exemple 100 comme ici) et remarquer que le temps
d'exécution est assez important

``` python
import time

dfgeoloc = df.loc[:, ['Adresse','CP','Ville']].apply(lambda s: s.str.lower().str.replace(","," "))
dfgeoloc['url'] = (dfgeoloc['Adresse'] + "+" + dfgeoloc['Ville'].str.replace("-",'+')).str.replace(" ","+")
dfgeoloc['url'] = 'https://api-adresse.data.gouv.fr/search/?q=' + dfgeoloc['url'] + "&postcode=" + df['CP'] + "&limit=1"
dfgeoloc = dfgeoloc.dropna()

start_time = time.time()

def get_geoloc(i):
    print(i)
    return gpd.GeoDataFrame.from_features(requests.get(dfgeoloc['url'].iloc[i]).json()['features'])

local = [get_geoloc(i) for i in range(len(dfgeoloc.head(10)))]
print("--- %s seconds ---" % (time.time() - start_time))
```

Comme l'indique la documentation, si on désire industrialiser notre processus
de géocodage, on va privilégier l'API CSV.

Pour obtenir une requête CURL cohérente avec le format désiré par l'API
on va à nouveau utiliser `requests` mais cette fois avec des paramètres
supplémentaires:

-   `data` va nous permettre de passer des paramètres à CURL (équivalents aux `-F`
    de la requête CURL):
    -   `columns`: Les colonnes utilisées pour localiser une donnée. En l'occurrence,
        on utilise l'adresse et la ville (car les codes postaux n'étant pas uniques,
        un même nom de voirie peut se trouver dans plusieurs villes partageant le même
        code postal)
    -   `postcode`: Le code postal de la ville. Idéalement nous aurions utilisé
        le code Insee mais nous ne l'avons pas dans nos données.
    -   `result_columns`: on restreint les données échangées avec l'API aux
        colonnes qui nous intéressent. Cela permet d'accélérer les processus (on
        échange moins de données) et de réduire l'impact carbone de notre activité
        (moins de transferts = moins d'énergie dépensée). En l'occurrence, on ne ressort
        que les données géolocalisées et un score de confiance en la géolocalisation.
-   `files`: permet d'envoyer un fichier via CURL

Les données sont récupérées avec `request.post`. Comme il s'agit d'une
chaîne de caractère, nous pouvons directement la lire avec `pandas` en
utilisant `io.StringIO` pour éviter d'écrire des données intermédiaires.

Le nombre d'échos semblant être limité, je propose de procéder par morceaux
(ici je découpe mon jeu de données en 5 morceaux).

``` python
import requests
import io   
import numpy as np
import time

params = {
    'columns': ['Adresse', 'Ville'],
    'postcode': 'CP',
    'result_columns': ['result_score', 'latitude', 'longitude'],
}

df[['Adresse','CP','Ville']] = df.loc[:, ['Adresse','CP','Ville']].apply(lambda s: s.str.lower().str.replace(","," "))

def geoloc_chunk(x):
    dfgeoloc = x.loc[:, ['Adresse','CP','Ville']]
    dfgeoloc.to_csv("datageocodage.csv", index=False)
    response = requests.post('https://api-adresse.data.gouv.fr/search/csv/', data=params, files={'data': ('datageocodage.csv', open('datageocodage.csv', 'rb'))})
    geoloc = pd.read_csv(io.StringIO(response.text), dtype = {'CP': 'str'})
    return geoloc
    
start_time = time.time()
geodata = [geoloc_chunk(dd) for dd in np.array_split(df, 10)]
print("--- %s seconds ---" % (time.time() - start_time))
```

    --- 68.69667387008667 seconds ---

Cette méthode est beaucoup plus rapide et permet ainsi, une fois retourné à nos
données initiales, d'avoir un jeu de données géolocalisé

``` python
geodata = pd.concat(geodata, ignore_index = True)
df_xy = df.merge(geodata, on = ['Adresse','CP','Ville'])
df_xy = df_xy.dropna(subset = ['latitude','longitude'])
df_xy['text'] = df_xy['Raison_Sociale'] + '<br>' + df_xy['Adresse'] + '<br>' + df_xy['Ville'] + '<br>Nombre de candidats:' + df_xy['B_NB'].astype(str)

df_xy.filter(['Raison_Sociale','Adresse','CP','Ville','latitude','longitude'], axis = "columns").sample(10)
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Raison_Sociale</th>
      <th>Adresse</th>
      <th>CP</th>
      <th>Ville</th>
      <th>latitude</th>
      <th>longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>7475</th>
      <td>NANGIS PERMIS</td>
      <td>5 rue général leclerc</td>
      <td>77370</td>
      <td>nangis</td>
      <td>48.556315</td>
      <td>3.013009</td>
    </tr>
    <tr>
      <th>2697</th>
      <td>ESPACE CONDUITE CHINON 37</td>
      <td>62 rue descartes</td>
      <td>37500</td>
      <td>chinon</td>
      <td>47.163149</td>
      <td>0.248649</td>
    </tr>
    <tr>
      <th>1502</th>
      <td>AUTO-ECOLE C PERMIS St POL</td>
      <td>20 route de plouénan</td>
      <td>29250</td>
      <td>saint-pol-de-leon</td>
      <td>48.677480</td>
      <td>-3.989139</td>
    </tr>
    <tr>
      <th>9113</th>
      <td>ZZ-URBAN PERMIS</td>
      <td>20 route du pave blanc</td>
      <td>92140</td>
      <td>clamart</td>
      <td>48.781804</td>
      <td>2.238769</td>
    </tr>
    <tr>
      <th>8153</th>
      <td>Athena conduite</td>
      <td>11 rue d'entraigues</td>
      <td>83170</td>
      <td>brignoles</td>
      <td>43.405622</td>
      <td>6.060863</td>
    </tr>
    <tr>
      <th>6606</th>
      <td>CFCV Vibraye</td>
      <td>34 rue xavier boutet</td>
      <td>72320</td>
      <td>vibraye</td>
      <td>48.059877</td>
      <td>0.733962</td>
    </tr>
    <tr>
      <th>5975</th>
      <td>HAAS</td>
      <td>1 avenue du dr houillon</td>
      <td>67600</td>
      <td>selestat</td>
      <td>48.260926</td>
      <td>7.458351</td>
    </tr>
    <tr>
      <th>3400</th>
      <td>CHARRIER / GRAND LIEU CONDUITE</td>
      <td>8 rue felix platel</td>
      <td>44310</td>
      <td>saint philbert de gd lieu</td>
      <td>47.037184</td>
      <td>-1.643277</td>
    </tr>
    <tr>
      <th>3549</th>
      <td>Camille Conduite</td>
      <td>18 place du martroi</td>
      <td>45190</td>
      <td>beaugency</td>
      <td>47.777274</td>
      <td>1.630156</td>
    </tr>
    <tr>
      <th>1410</th>
      <td>PLEIN SUD CONDUITE</td>
      <td>3 bis bld de l'europe</td>
      <td>28500</td>
      <td>vernouillet</td>
      <td>48.719353</td>
      <td>1.369368</td>
    </tr>
  </tbody>
</table>
</div>

Il ne reste plus qu'à utiliser `geopandas`
et nous serons en mesure de faire une carte des localisations des auto-écoles :

``` python
import geopandas as gpd
dfgeo = gpd.GeoDataFrame(df_xy, geometry=gpd.points_from_xy(df_xy.longitude, df_xy.latitude))
```

Nous allons représenter les stations dans l'Essonne avec un zoom initialement
sur les villes de Massy et Palaiseau. Le code est le suivant:

``` python
import folium

# Représenter toutes les autoécoles de l'Essonne
df_91 = df_xy.loc[df_xy["Dept"] == "091"]

# Centrer la vue initiale sur Massy-Palaiseau
df_pal = df_xy.loc[df_xy['Ville'].isin(["massy", "palaiseau"])]
center = df_pal[['latitude', 'longitude']].mean().values.tolist()
sw = df_pal[['latitude', 'longitude']].min().values.tolist()
ne = df_pal[['latitude', 'longitude']].max().values.tolist()

m = folium.Map(location = center, tiles='Stamen Toner')

# I can add marker one by one on the map
for i in range(0,len(df_91)):
    folium.Marker([df_91.iloc[i]['latitude'], df_91.iloc[i]['longitude']],
                  popup=df_91.iloc[i]['text'],
                  icon=folium.Icon(icon='car', prefix='fa')).add_to(m)

m.fit_bounds([sw, ne])
```

Ce qui permet d'obtenir la carte:

{{< rawhtml >}}

<div style="width:100%;"><div style="position:relative;width:100%;height:0;padding-bottom:60%;"><span style="color:#565656">Make this Notebook Trusted to load map: File -> Trust Notebook</span><iframe srcdoc="&lt;!DOCTYPE html&gt;
&lt;head&gt;    
    &lt;meta http-equiv=&quot;content-type&quot; content=&quot;text/html; charset=UTF-8&quot; /&gt;
    
        &lt;script&gt;
            L_NO_TOUCH = false;
            L_DISABLE_3D = false;
        &lt;/script&gt;
    
    &lt;style&gt;html, body {width: 100%;height: 100%;margin: 0;padding: 0;}&lt;/style&gt;
    &lt;style&gt;#map {position:absolute;top:0;bottom:0;right:0;left:0;}&lt;/style&gt;
    &lt;script src=&quot;https://cdn.jsdelivr.net/npm/leaflet@1.6.0/dist/leaflet.js&quot;&gt;&lt;/script&gt;
    &lt;script src=&quot;https://code.jquery.com/jquery-1.12.4.min.js&quot;&gt;&lt;/script&gt;
    &lt;script src=&quot;https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/js/bootstrap.min.js&quot;&gt;&lt;/script&gt;
    &lt;script src=&quot;https://cdnjs.cloudflare.com/ajax/libs/Leaflet.awesome-markers/2.0.2/leaflet.awesome-markers.js&quot;&gt;&lt;/script&gt;
    &lt;link rel=&quot;stylesheet&quot; href=&quot;https://cdn.jsdelivr.net/npm/leaflet@1.6.0/dist/leaflet.css&quot;/&gt;
    &lt;link rel=&quot;stylesheet&quot; href=&quot;https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css&quot;/&gt;
    &lt;link rel=&quot;stylesheet&quot; href=&quot;https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css&quot;/&gt;
    &lt;link rel=&quot;stylesheet&quot; href=&quot;https://maxcdn.bootstrapcdn.com/font-awesome/4.6.3/css/font-awesome.min.css&quot;/&gt;
    &lt;link rel=&quot;stylesheet&quot; href=&quot;https://cdnjs.cloudflare.com/ajax/libs/Leaflet.awesome-markers/2.0.2/leaflet.awesome-markers.css&quot;/&gt;
    &lt;link rel=&quot;stylesheet&quot; href=&quot;https://cdn.jsdelivr.net/gh/python-visualization/folium/folium/templates/leaflet.awesome.rotate.min.css&quot;/&gt;
    
            &lt;meta name=&quot;viewport&quot; content=&quot;width=device-width,
                initial-scale=1.0, maximum-scale=1.0, user-scalable=no&quot; /&gt;
            &lt;style&gt;
                #map_e702c6a9dd177ded27b22e0aa262378e {
                    position: relative;
                    width: 100.0%;
                    height: 100.0%;
                    left: 0.0%;
                    top: 0.0%;
                }
            &lt;/style&gt;
        
&lt;/head&gt;
&lt;body&gt;    
    
            &lt;div class=&quot;folium-map&quot; id=&quot;map_e702c6a9dd177ded27b22e0aa262378e&quot; &gt;&lt;/div&gt;
        
&lt;/body&gt;
&lt;script&gt;    
    
            var map_e702c6a9dd177ded27b22e0aa262378e = L.map(
                &quot;map_e702c6a9dd177ded27b22e0aa262378e&quot;,
                {
                    center: [48.719988769230774, 2.255833230769231],
                    crs: L.CRS.EPSG3857,
                    zoom: 10,
                    zoomControl: true,
                    preferCanvas: false,
                }
            );

            

        
    
            var tile_layer_d4c6724801c005d3aed44ee01690460b = L.tileLayer(
                &quot;https://stamen-tiles-{s}.a.ssl.fastly.net/toner/{z}/{x}/{y}.png&quot;,
                {&quot;attribution&quot;: &quot;Map tiles by \u003ca href=\&quot;http://stamen.com\&quot;\u003eStamen Design\u003c/a\u003e, under \u003ca href=\&quot;http://creativecommons.org/licenses/by/3.0\&quot;\u003eCC BY 3.0\u003c/a\u003e. Data by \u0026copy; \u003ca href=\&quot;http://openstreetmap.org\&quot;\u003eOpenStreetMap\u003c/a\u003e, under \u003ca href=\&quot;http://www.openstreetmap.org/copyright\&quot;\u003eODbL\u003c/a\u003e.&quot;, &quot;detectRetina&quot;: false, &quot;maxNativeZoom&quot;: 18, &quot;maxZoom&quot;: 18, &quot;minZoom&quot;: 0, &quot;noWrap&quot;: false, &quot;opacity&quot;: 1, &quot;subdomains&quot;: &quot;abc&quot;, &quot;tms&quot;: false}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var marker_3169902c3e360803b53f11beb2711dc1 = L.marker(
                [48.588546, 2.452578],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_0b993e508ced990aa65bb8d48166c291 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_3169902c3e360803b53f11beb2711dc1.setIcon(icon_0b993e508ced990aa65bb8d48166c291);
        
    
        var popup_4e185dd61fcdd2de40d78688ed635366 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_15863ead607bdfb3c5de9265913dfef6 = $(`&lt;div id=&quot;html_15863ead607bdfb3c5de9265913dfef6&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;GENERALISTE&lt;br&gt;route de lisses&lt;br&gt;villabe&lt;br&gt;Nombre de candidats:46&lt;/div&gt;`)[0];
            popup_4e185dd61fcdd2de40d78688ed635366.setContent(html_15863ead607bdfb3c5de9265913dfef6);
        

        marker_3169902c3e360803b53f11beb2711dc1.bindPopup(popup_4e185dd61fcdd2de40d78688ed635366)
        ;

        
    
    
            var marker_2686db3194b01eb0d4dce9e2ef053660 = L.marker(
                [48.697171, 2.522375],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_6da2cb0869a7468a6ec3b77d5d4913a6 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_2686db3194b01eb0d4dce9e2ef053660.setIcon(icon_6da2cb0869a7468a6ec3b77d5d4913a6);
        
    
        var popup_db3c6be8442fd94b2b9bb8463168f348 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d24ece70f7e40be6b73d07349b541d36 = $(`&lt;div id=&quot;html_d24ece70f7e40be6b73d07349b541d36&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;AS CONDUITE&lt;br&gt;5  villa hector berlioz&lt;br&gt;epinay sous senart&lt;br&gt;Nombre de candidats:131&lt;/div&gt;`)[0];
            popup_db3c6be8442fd94b2b9bb8463168f348.setContent(html_d24ece70f7e40be6b73d07349b541d36);
        

        marker_2686db3194b01eb0d4dce9e2ef053660.bindPopup(popup_db3c6be8442fd94b2b9bb8463168f348)
        ;

        
    
    
            var marker_49d0749887a558cbba8a07c20915d071 = L.marker(
                [48.71605, 2.246954],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_510a9a116f5e343f1a369e8f10da128b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_49d0749887a558cbba8a07c20915d071.setIcon(icon_510a9a116f5e343f1a369e8f10da128b);
        
    
        var popup_26a5415728efb8c935c4eda464614030 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_cae990cc5fdaef56407afde8b1c7959a = $(`&lt;div id=&quot;html_cae990cc5fdaef56407afde8b1c7959a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;OBJECTIF CONDUITE&lt;br&gt;57 bis rue de paris&lt;br&gt;palaiseau&lt;br&gt;Nombre de candidats:130&lt;/div&gt;`)[0];
            popup_26a5415728efb8c935c4eda464614030.setContent(html_cae990cc5fdaef56407afde8b1c7959a);
        

        marker_49d0749887a558cbba8a07c20915d071.bindPopup(popup_26a5415728efb8c935c4eda464614030)
        ;

        
    
    
            var marker_ccee9269013afd1103d59bc1dc536829 = L.marker(
                [48.400441, 2.469892],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_b7aae7e1cf66ae5488c89c7bade6c521 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_ccee9269013afd1103d59bc1dc536829.setIcon(icon_b7aae7e1cf66ae5488c89c7bade6c521);
        
    
        var popup_f3504ec1f398f9d3502112ab1b10300a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d79bc0380515ae52eda5d00ac48fa045 = $(`&lt;div id=&quot;html_d79bc0380515ae52eda5d00ac48fa045&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ECOLE DE CONDUITE HARTMANN&lt;br&gt;8 boulevard du marechal joffre&lt;br&gt;milly la foret&lt;br&gt;Nombre de candidats:28&lt;/div&gt;`)[0];
            popup_f3504ec1f398f9d3502112ab1b10300a.setContent(html_d79bc0380515ae52eda5d00ac48fa045);
        

        marker_ccee9269013afd1103d59bc1dc536829.bindPopup(popup_f3504ec1f398f9d3502112ab1b10300a)
        ;

        
    
    
            var marker_b67b25f9249009206eba8f51691313cc = L.marker(
                [48.653289, 2.315548],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_a554a0d1551b7ced7ef6615d3d57aff0 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_b67b25f9249009206eba8f51691313cc.setIcon(icon_a554a0d1551b7ced7ef6615d3d57aff0);
        
    
        var popup_439bb9d99c20b4b07bf614623dfd9c56 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2128235a1ede9679c8b9fe84c13c1126 = $(`&lt;div id=&quot;html_2128235a1ede9679c8b9fe84c13c1126&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;BONNE CONDUITE&lt;br&gt;6 rue antoine rocca&lt;br&gt;sainte genevieve des bois&lt;br&gt;Nombre de candidats:184&lt;/div&gt;`)[0];
            popup_439bb9d99c20b4b07bf614623dfd9c56.setContent(html_2128235a1ede9679c8b9fe84c13c1126);
        

        marker_b67b25f9249009206eba8f51691313cc.bindPopup(popup_439bb9d99c20b4b07bf614623dfd9c56)
        ;

        
    
    
            var marker_4933cf34df2589f4407d61c3dc3525cf = L.marker(
                [48.618335, 2.393758],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_6dfab424e94c67be4ed234d51effea06 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_4933cf34df2589f4407d61c3dc3525cf.setIcon(icon_6dfab424e94c67be4ed234d51effea06);
        
    
        var popup_8cf4cc474fe9c6ca42cc2b91dfcc7d24 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_57e92824a71e90fd788fed3c4b35a574 = $(`&lt;div id=&quot;html_57e92824a71e90fd788fed3c4b35a574&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CANAL&lt;br&gt;31 rue du pont amar&lt;br&gt;courcouronnes&lt;br&gt;Nombre de candidats:154&lt;/div&gt;`)[0];
            popup_8cf4cc474fe9c6ca42cc2b91dfcc7d24.setContent(html_57e92824a71e90fd788fed3c4b35a574);
        

        marker_4933cf34df2589f4407d61c3dc3525cf.bindPopup(popup_8cf4cc474fe9c6ca42cc2b91dfcc7d24)
        ;

        
    
    
            var marker_1fd75a6001c70fccd63645dfb901c2f9 = L.marker(
                [48.677388, 2.356115],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_b1eb01fc1ddb25511e12d52c5bd6aa2d = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_1fd75a6001c70fccd63645dfb901c2f9.setIcon(icon_b1eb01fc1ddb25511e12d52c5bd6aa2d);
        
    
        var popup_2505b4cea702e7fdff01a37162383c09 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_336e271d82ddba78d490f381aac04c35 = $(`&lt;div id=&quot;html_336e271d82ddba78d490f381aac04c35&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CLUB CONDUITE&lt;br&gt;1 rue de chateaubriand&lt;br&gt;savigny sur orge&lt;br&gt;Nombre de candidats:165&lt;/div&gt;`)[0];
            popup_2505b4cea702e7fdff01a37162383c09.setContent(html_336e271d82ddba78d490f381aac04c35);
        

        marker_1fd75a6001c70fccd63645dfb901c2f9.bindPopup(popup_2505b4cea702e7fdff01a37162383c09)
        ;

        
    
    
            var marker_432c27dc521b56de98c286dca07231ad = L.marker(
                [48.64628, 2.355058],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_50d9a6054818430c2a5cdbc212e97061 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_432c27dc521b56de98c286dca07231ad.setIcon(icon_50d9a6054818430c2a5cdbc212e97061);
        
    
        var popup_77c347a2684e67072cd3f2a8e0cc703c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2370fb1cbf2253314f082afc95c2b00d = $(`&lt;div id=&quot;html_2370fb1cbf2253314f082afc95c2b00d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;EXPRESS AUTO ECOLE&lt;br&gt;43 boulevard de la gribelette&lt;br&gt;morsang sur orge&lt;br&gt;Nombre de candidats:115&lt;/div&gt;`)[0];
            popup_77c347a2684e67072cd3f2a8e0cc703c.setContent(html_2370fb1cbf2253314f082afc95c2b00d);
        

        marker_432c27dc521b56de98c286dca07231ad.bindPopup(popup_77c347a2684e67072cd3f2a8e0cc703c)
        ;

        
    
    
            var marker_30852528d667fca39df659bf5ce54f22 = L.marker(
                [48.676632, 2.388355],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_7edc028b344c9c81dcf2c155074cd978 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_30852528d667fca39df659bf5ce54f22.setIcon(icon_7edc028b344c9c81dcf2c155074cd978);
        
    
        var popup_b8825febdfd13c22ae1a9d9aa56ac69b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_57e98b27c216658e7d494f76d72050fb = $(`&lt;div id=&quot;html_57e98b27c216658e7d494f76d72050fb&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;S.J.T.&lt;br&gt;12 rue de ris&lt;br&gt;viry chatillon&lt;br&gt;Nombre de candidats:30&lt;/div&gt;`)[0];
            popup_b8825febdfd13c22ae1a9d9aa56ac69b.setContent(html_57e98b27c216658e7d494f76d72050fb);
        

        marker_30852528d667fca39df659bf5ce54f22.bindPopup(popup_b8825febdfd13c22ae1a9d9aa56ac69b)
        ;

        
    
    
            var marker_5683d9a3193dbd2c569a04f8df0e3a2e = L.marker(
                [48.588004, 2.248526],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_6a9627061e42faf00abaf934d42464f3 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_5683d9a3193dbd2c569a04f8df0e3a2e.setIcon(icon_6a9627061e42faf00abaf934d42464f3);
        
    
        var popup_15d52820822ec43eaae39d07c1312c6d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d2a909acb5c63302c08cafaf5a6cea96 = $(`&lt;div id=&quot;html_d2a909acb5c63302c08cafaf5a6cea96&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;GUY&lt;br&gt;4 rue pasteur&lt;br&gt;arpajon&lt;br&gt;Nombre de candidats:88&lt;/div&gt;`)[0];
            popup_15d52820822ec43eaae39d07c1312c6d.setContent(html_d2a909acb5c63302c08cafaf5a6cea96);
        

        marker_5683d9a3193dbd2c569a04f8df0e3a2e.bindPopup(popup_15d52820822ec43eaae39d07c1312c6d)
        ;

        
    
    
            var marker_f01f93d3571767df8e52f6f8023e55d1 = L.marker(
                [48.621723, 2.441047],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_165e6bdb26059f4ea2de3aaaedcf68ad = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_f01f93d3571767df8e52f6f8023e55d1.setIcon(icon_165e6bdb26059f4ea2de3aaaedcf68ad);
        
    
        var popup_e7c099e530e37708d7dc6e5f2650db33 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9e4168570ad60009b26aa016ef39e610 = $(`&lt;div id=&quot;html_9e4168570ad60009b26aa016ef39e610&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DRIVE SCHOOL&lt;br&gt;9 place de la commune&lt;br&gt;evry&lt;br&gt;Nombre de candidats:134&lt;/div&gt;`)[0];
            popup_e7c099e530e37708d7dc6e5f2650db33.setContent(html_9e4168570ad60009b26aa016ef39e610);
        

        marker_f01f93d3571767df8e52f6f8023e55d1.bindPopup(popup_e7c099e530e37708d7dc6e5f2650db33)
        ;

        
    
    
            var marker_f5675a51e90503db1afdae129ba0c41f = L.marker(
                [48.714733, 2.24724],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_0d7839e6280c15236c51604775106793 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_f5675a51e90503db1afdae129ba0c41f.setIcon(icon_0d7839e6280c15236c51604775106793);
        
    
        var popup_206c6484be0873dd18468baba65bd1bf = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_93e03e4df0138411b6bc74f7a621f694 = $(`&lt;div id=&quot;html_93e03e4df0138411b6bc74f7a621f694&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CONDUITE SURE&lt;br&gt;7 bis rue d auvergne&lt;br&gt;palaiseau&lt;br&gt;Nombre de candidats:462&lt;/div&gt;`)[0];
            popup_206c6484be0873dd18468baba65bd1bf.setContent(html_93e03e4df0138411b6bc74f7a621f694);
        

        marker_f5675a51e90503db1afdae129ba0c41f.bindPopup(popup_206c6484be0873dd18468baba65bd1bf)
        ;

        
    
    
            var marker_b7a266123dfca07f79dcf50b80477dd3 = L.marker(
                [48.598572, 2.492607],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_fa4af35e53e807be7c402e1b82666332 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_b7a266123dfca07f79dcf50b80477dd3.setIcon(icon_fa4af35e53e807be7c402e1b82666332);
        
    
        var popup_305112f46da467e1594e956c1bd2214b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_b2350e48855f94c168458cfc531cdd1c = $(`&lt;div id=&quot;html_b2350e48855f94c168458cfc531cdd1c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;UNIVERS PERMIS&lt;br&gt;52 54 grande rue charles de gaulle&lt;br&gt;saintry sur seine&lt;br&gt;Nombre de candidats:26&lt;/div&gt;`)[0];
            popup_305112f46da467e1594e956c1bd2214b.setContent(html_b2350e48855f94c168458cfc531cdd1c);
        

        marker_b7a266123dfca07f79dcf50b80477dd3.bindPopup(popup_305112f46da467e1594e956c1bd2214b)
        ;

        
    
    
            var marker_2ccd524ef6a8a36e65dbd24d04c8b98d = L.marker(
                [48.71752, 2.247603],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_9d8b2983c076e18bd8df77dde5f696a5 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_2ccd524ef6a8a36e65dbd24d04c8b98d.setIcon(icon_9d8b2983c076e18bd8df77dde5f696a5);
        
    
        var popup_a20dff5a0bdd0a8e053cb7c4a1d328fb = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_f78e4a6d9d7f0a3abf41cacfe9e77231 = $(`&lt;div id=&quot;html_f78e4a6d9d7f0a3abf41cacfe9e77231&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;FLASH&lt;br&gt;5 rue de la gare&lt;br&gt;palaiseau&lt;br&gt;Nombre de candidats:338&lt;/div&gt;`)[0];
            popup_a20dff5a0bdd0a8e053cb7c4a1d328fb.setContent(html_f78e4a6d9d7f0a3abf41cacfe9e77231);
        

        marker_2ccd524ef6a8a36e65dbd24d04c8b98d.bindPopup(popup_a20dff5a0bdd0a8e053cb7c4a1d328fb)
        ;

        
    
    
            var marker_403c542b6579dcfc450dd20185f8ea2f = L.marker(
                [48.632897, 2.442926],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_32882dfda92290fd1de1938b50bb78f4 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_403c542b6579dcfc450dd20185f8ea2f.setIcon(icon_32882dfda92290fd1de1938b50bb78f4);
        
    
        var popup_aea40da79e3a9a1f8aeaf97bc9dead17 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9be4e3cf910be91b1b8eb52717bfd079 = $(`&lt;div id=&quot;html_9be4e3cf910be91b1b8eb52717bfd079&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;AGUADO&lt;br&gt;2 rue auguste renoir&lt;br&gt;evry&lt;br&gt;Nombre de candidats:208&lt;/div&gt;`)[0];
            popup_aea40da79e3a9a1f8aeaf97bc9dead17.setContent(html_9be4e3cf910be91b1b8eb52717bfd079);
        

        marker_403c542b6579dcfc450dd20185f8ea2f.bindPopup(popup_aea40da79e3a9a1f8aeaf97bc9dead17)
        ;

        
    
    
            var marker_aa69fc1b3e5239d056bd8650a6541278 = L.marker(
                [48.623076, 2.429552],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_261c028d3c50e5572069815702c825ad = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_aa69fc1b3e5239d056bd8650a6541278.setIcon(icon_261c028d3c50e5572069815702c825ad);
        
    
        var popup_714c765e440788ca068a150d1122c73b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9e7bd64d2db800933cafc5d478001d42 = $(`&lt;div id=&quot;html_9e7bd64d2db800933cafc5d478001d42&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CATHEDRALE&lt;br&gt;13 cours monseigneur romero&lt;br&gt;evry&lt;br&gt;Nombre de candidats:256&lt;/div&gt;`)[0];
            popup_714c765e440788ca068a150d1122c73b.setContent(html_9e7bd64d2db800933cafc5d478001d42);
        

        marker_aa69fc1b3e5239d056bd8650a6541278.bindPopup(popup_714c765e440788ca068a150d1122c73b)
        ;

        
    
    
            var marker_a2bacc1d2c887893d8309d0058e48d14 = L.marker(
                [48.642355, 2.430613],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_6043d3fb12f87cff41c278cb62adc7d1 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_a2bacc1d2c887893d8309d0058e48d14.setIcon(icon_6043d3fb12f87cff41c278cb62adc7d1);
        
    
        var popup_cd837395941e21194be68a0fbb733391 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_555dc4a991b871672cc8ced1e89d76d8 = $(`&lt;div id=&quot;html_555dc4a991b871672cc8ced1e89d76d8&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CER CHAMPS ELYSEES&lt;br&gt;cc des champs elysees           14 place troisdorf&lt;br&gt;evry&lt;br&gt;Nombre de candidats:201&lt;/div&gt;`)[0];
            popup_cd837395941e21194be68a0fbb733391.setContent(html_555dc4a991b871672cc8ced1e89d76d8);
        

        marker_a2bacc1d2c887893d8309d0058e48d14.bindPopup(popup_cd837395941e21194be68a0fbb733391)
        ;

        
    
    
            var marker_618f0ba6d0e94218cdbab73ccce7166d = L.marker(
                [48.622599, 2.450813],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_2c55899c7d72dd5a7fc72f4ab4c5f075 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_618f0ba6d0e94218cdbab73ccce7166d.setIcon(icon_2c55899c7d72dd5a7fc72f4ab4c5f075);
        
    
        var popup_d2c9e00701c6b507c9043acc25bf14c3 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_819847b41a9d897d6c9b1ea7e5fbaebf = $(`&lt;div id=&quot;html_819847b41a9d897d6c9b1ea7e5fbaebf&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CER CLAREVA EVRY&lt;br&gt;1 place du 19 mars 1962&lt;br&gt;evry&lt;br&gt;Nombre de candidats:171&lt;/div&gt;`)[0];
            popup_d2c9e00701c6b507c9043acc25bf14c3.setContent(html_819847b41a9d897d6c9b1ea7e5fbaebf);
        

        marker_618f0ba6d0e94218cdbab73ccce7166d.bindPopup(popup_d2c9e00701c6b507c9043acc25bf14c3)
        ;

        
    
    
            var marker_5a2aa5b905c6ad95fdae4250988ac791 = L.marker(
                [48.626966, 2.430378],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_cbc89f1087369dfc9241e16110680b6c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_5a2aa5b905c6ad95fdae4250988ac791.setIcon(icon_cbc89f1087369dfc9241e16110680b6c);
        
    
        var popup_b39028f7658d811bce2385aeee19e57b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_55c13fce3f7a194908fd322aa5fcc0a5 = $(`&lt;div id=&quot;html_55c13fce3f7a194908fd322aa5fcc0a5&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ECF AGORA&lt;br&gt;24 cours blaise pascal&lt;br&gt;evry&lt;br&gt;Nombre de candidats:445&lt;/div&gt;`)[0];
            popup_b39028f7658d811bce2385aeee19e57b.setContent(html_55c13fce3f7a194908fd322aa5fcc0a5);
        

        marker_5a2aa5b905c6ad95fdae4250988ac791.bindPopup(popup_b39028f7658d811bce2385aeee19e57b)
        ;

        
    
    
            var marker_fecbc0ed5189eb2d531febd6d87f4562 = L.marker(
                [48.628788, 2.437711],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_39c973dff2adf91d016c7fafcc21567b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_fecbc0ed5189eb2d531febd6d87f4562.setIcon(icon_39c973dff2adf91d016c7fafcc21567b);
        
    
        var popup_fb35453f064e43f79a1b2c874c07b8ba = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d73ad46c87555e155ac7039a14a5d97d = $(`&lt;div id=&quot;html_d73ad46c87555e155ac7039a14a5d97d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;INDIVIDUELS PREF&lt;br&gt;prefecture de l essonne&lt;br&gt;evry&lt;br&gt;Nombre de candidats:269&lt;/div&gt;`)[0];
            popup_fb35453f064e43f79a1b2c874c07b8ba.setContent(html_d73ad46c87555e155ac7039a14a5d97d);
        

        marker_fecbc0ed5189eb2d531febd6d87f4562.bindPopup(popup_fb35453f064e43f79a1b2c874c07b8ba)
        ;

        
    
    
            var marker_8d5ea1e7fb136479c00bab9414065742 = L.marker(
                [48.624739, 2.425478],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_39c5d5c27ee522d253fe51ae0120a4b8 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_8d5ea1e7fb136479c00bab9414065742.setIcon(icon_39c5d5c27ee522d253fe51ae0120a4b8);
        
    
        var popup_14516d5d6cc44878016bc288c5026708 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_41d520f8a24c6922261e6490f449c6e8 = $(`&lt;div id=&quot;html_41d520f8a24c6922261e6490f449c6e8&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;INRI&#x27;S EVRY&lt;br&gt;25 boulevard francois mitterrand&lt;br&gt;evry&lt;br&gt;Nombre de candidats:177&lt;/div&gt;`)[0];
            popup_14516d5d6cc44878016bc288c5026708.setContent(html_41d520f8a24c6922261e6490f449c6e8);
        

        marker_8d5ea1e7fb136479c00bab9414065742.bindPopup(popup_14516d5d6cc44878016bc288c5026708)
        ;

        
    
    
            var marker_496ec2f28d0f8da22249592eda076730 = L.marker(
                [48.627059, 2.43094],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_53e1990a08501cfc704c742ce992cdc9 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_496ec2f28d0f8da22249592eda076730.setIcon(icon_53e1990a08501cfc704c742ce992cdc9);
        
    
        var popup_4a54cf4d336101288ee6c31f55e3b9c2 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_0f6de5bf64896296d17dd01bd132adab = $(`&lt;div id=&quot;html_0f6de5bf64896296d17dd01bd132adab&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;SESAM CONDUITE&lt;br&gt;15 traversée galilée&lt;br&gt;evry&lt;br&gt;Nombre de candidats:316&lt;/div&gt;`)[0];
            popup_4a54cf4d336101288ee6c31f55e3b9c2.setContent(html_0f6de5bf64896296d17dd01bd132adab);
        

        marker_496ec2f28d0f8da22249592eda076730.bindPopup(popup_4a54cf4d336101288ee6c31f55e3b9c2)
        ;

        
    
    
            var marker_c409705853a7a78bf358b9aad9ffd95f = L.marker(
                [48.615159, 2.381436],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_0c49ddc45b965d21cc2f12bcd1d95c0c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_c409705853a7a78bf358b9aad9ffd95f.setIcon(icon_0c49ddc45b965d21cc2f12bcd1d95c0c);
        
    
        var popup_ef92933e6fbf3ebcb3bc22b41f642786 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a91be7dd0612630d3fc55a8cd6c326c6 = $(`&lt;div id=&quot;html_a91be7dd0612630d3fc55a8cd6c326c6&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CER START UP&lt;br&gt;18 bis rue charles de gaulle&lt;br&gt;bondoufle&lt;br&gt;Nombre de candidats:203&lt;/div&gt;`)[0];
            popup_ef92933e6fbf3ebcb3bc22b41f642786.setContent(html_a91be7dd0612630d3fc55a8cd6c326c6);
        

        marker_c409705853a7a78bf358b9aad9ffd95f.bindPopup(popup_ef92933e6fbf3ebcb3bc22b41f642786)
        ;

        
    
    
            var marker_0e193c90d1c2d6f614b87518a808b725 = L.marker(
                [48.633602, 2.440035],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_dc9dd49f9db79ee6184f77c9e1610ba8 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_0e193c90d1c2d6f614b87518a808b725.setIcon(icon_dc9dd49f9db79ee6184f77c9e1610ba8);
        
    
        var popup_2866f1628978e910ed8c95a5f2e6b117 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_81ec44aaa656d8c08b2a4e405bb8a225 = $(`&lt;div id=&quot;html_81ec44aaa656d8c08b2a4e405bb8a225&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;GREEN CONDUITE COURCOURONNES&lt;br&gt;6  allée de l&#x27;orme à martin&lt;br&gt;courcouronnes&lt;br&gt;Nombre de candidats:86&lt;/div&gt;`)[0];
            popup_2866f1628978e910ed8c95a5f2e6b117.setContent(html_81ec44aaa656d8c08b2a4e405bb8a225);
        

        marker_0e193c90d1c2d6f614b87518a808b725.bindPopup(popup_2866f1628978e910ed8c95a5f2e6b117)
        ;

        
    
    
            var marker_9da83bc959af37732fcbfa5a955e53f3 = L.marker(
                [48.626627, 2.423945],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_6b95bfbc0dbfe4fe1b761ac433e64d30 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_9da83bc959af37732fcbfa5a955e53f3.setIcon(icon_6b95bfbc0dbfe4fe1b761ac433e64d30);
        
    
        var popup_ad6b6c74fc98fcf921998f8404a28636 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_39dffce0b5031dcbae5c3dc28d0df4f6 = $(`&lt;div id=&quot;html_39dffce0b5031dcbae5c3dc28d0df4f6&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;SABFA CONDUITE&lt;br&gt;128 allée des champs élysées&lt;br&gt;courcouronnes&lt;br&gt;Nombre de candidats:81&lt;/div&gt;`)[0];
            popup_ad6b6c74fc98fcf921998f8404a28636.setContent(html_39dffce0b5031dcbae5c3dc28d0df4f6);
        

        marker_9da83bc959af37732fcbfa5a955e53f3.bindPopup(popup_ad6b6c74fc98fcf921998f8404a28636)
        ;

        
    
    
            var marker_ceb4ef696db4045605bfa6146b3750c2 = L.marker(
                [48.611549, 2.461763],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_4d8ecb98cec2815dbb469d6bb203cdc4 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_ceb4ef696db4045605bfa6146b3750c2.setIcon(icon_4d8ecb98cec2815dbb469d6bb203cdc4);
        
    
        var popup_5e21c8997e476885520eb5beb347f3bc = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_5a70693a53b10e4d84027e1d28999b98 = $(`&lt;div id=&quot;html_5a70693a53b10e4d84027e1d28999b98&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ABC MG&lt;br&gt;106 boulevard jean jaures&lt;br&gt;corbeil essonnes&lt;br&gt;Nombre de candidats:405&lt;/div&gt;`)[0];
            popup_5e21c8997e476885520eb5beb347f3bc.setContent(html_5a70693a53b10e4d84027e1d28999b98);
        

        marker_ceb4ef696db4045605bfa6146b3750c2.bindPopup(popup_5e21c8997e476885520eb5beb347f3bc)
        ;

        
    
    
            var marker_0fc259e6070f70affa30c9c688566724 = L.marker(
                [48.607224, 2.483705],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_3d46c8adf4011bcebe8a4a2b1b08a375 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_0fc259e6070f70affa30c9c688566724.setIcon(icon_3d46c8adf4011bcebe8a4a2b1b08a375);
        
    
        var popup_0d81d27a999b1f1e3179731a22cb97bc = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_15cd4335eb7754f9643c02d16bd236b9 = $(`&lt;div id=&quot;html_15cd4335eb7754f9643c02d16bd236b9&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;AUTO ECOLE DU STADE&lt;br&gt;98 rue saint spire&lt;br&gt;corbeil essonnes&lt;br&gt;Nombre de candidats:37&lt;/div&gt;`)[0];
            popup_0d81d27a999b1f1e3179731a22cb97bc.setContent(html_15cd4335eb7754f9643c02d16bd236b9);
        

        marker_0fc259e6070f70affa30c9c688566724.bindPopup(popup_0d81d27a999b1f1e3179731a22cb97bc)
        ;

        
    
    
            var marker_5a1d7e2734bcdeac2821142f722b0885 = L.marker(
                [48.607224, 2.483705],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_6074172347b912ca6606a1d7f900a8dc = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_5a1d7e2734bcdeac2821142f722b0885.setIcon(icon_6074172347b912ca6606a1d7f900a8dc);
        
    
        var popup_16d4ddaf5977558813f28a1f53812ab8 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_49819ee581a61e022df09af0b2534148 = $(`&lt;div id=&quot;html_49819ee581a61e022df09af0b2534148&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;AUTO ECOLE DU STADE&lt;br&gt;98 rue saint spire&lt;br&gt;corbeil essonnes&lt;br&gt;Nombre de candidats:37&lt;/div&gt;`)[0];
            popup_16d4ddaf5977558813f28a1f53812ab8.setContent(html_49819ee581a61e022df09af0b2534148);
        

        marker_5a1d7e2734bcdeac2821142f722b0885.bindPopup(popup_16d4ddaf5977558813f28a1f53812ab8)
        ;

        
    
    
            var marker_302f421d569e2a7c42c67eebe20f9a75 = L.marker(
                [48.607224, 2.483705],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_6555c6930b5cd4c3b24fa3d253ceda40 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_302f421d569e2a7c42c67eebe20f9a75.setIcon(icon_6555c6930b5cd4c3b24fa3d253ceda40);
        
    
        var popup_415d60a9516fd82517c93c5e4334c109 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_22ca2bd522a10484a8bc34f230c68049 = $(`&lt;div id=&quot;html_22ca2bd522a10484a8bc34f230c68049&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DU STADE MC&lt;br&gt;98 rue saint spire&lt;br&gt;corbeil essonnes&lt;br&gt;Nombre de candidats:218&lt;/div&gt;`)[0];
            popup_415d60a9516fd82517c93c5e4334c109.setContent(html_22ca2bd522a10484a8bc34f230c68049);
        

        marker_302f421d569e2a7c42c67eebe20f9a75.bindPopup(popup_415d60a9516fd82517c93c5e4334c109)
        ;

        
    
    
            var marker_70795801794af3e930d650d567753702 = L.marker(
                [48.607224, 2.483705],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_602b6cd49c5df65b55919e80415cb598 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_70795801794af3e930d650d567753702.setIcon(icon_602b6cd49c5df65b55919e80415cb598);
        
    
        var popup_6727dfe56f72410a6982c52dc32dd5fc = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_4c63e1fc772e1a28874aab783f925a11 = $(`&lt;div id=&quot;html_4c63e1fc772e1a28874aab783f925a11&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DU STADE MC&lt;br&gt;98 rue saint spire&lt;br&gt;corbeil essonnes&lt;br&gt;Nombre de candidats:218&lt;/div&gt;`)[0];
            popup_6727dfe56f72410a6982c52dc32dd5fc.setContent(html_4c63e1fc772e1a28874aab783f925a11);
        

        marker_70795801794af3e930d650d567753702.bindPopup(popup_6727dfe56f72410a6982c52dc32dd5fc)
        ;

        
    
    
            var marker_431a127b1737f8cad8967a43c85e304a = L.marker(
                [48.614308, 2.485885],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_cdf562d21db215754d4f2a6185f7b943 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_431a127b1737f8cad8967a43c85e304a.setIcon(icon_cdf562d21db215754d4f2a6185f7b943);
        
    
        var popup_690ef1690874591bd4d88c1818429154 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_0719a630ad9bf4a315d793b0e7aca857 = $(`&lt;div id=&quot;html_0719a630ad9bf4a315d793b0e7aca857&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;AUTO ECOLE GS2&lt;br&gt;1 place saint leonard&lt;br&gt;corbeil essonnes&lt;br&gt;Nombre de candidats:160&lt;/div&gt;`)[0];
            popup_690ef1690874591bd4d88c1818429154.setContent(html_0719a630ad9bf4a315d793b0e7aca857);
        

        marker_431a127b1737f8cad8967a43c85e304a.bindPopup(popup_690ef1690874591bd4d88c1818429154)
        ;

        
    
    
            var marker_24af2eac3f8edf1d40f2b996fb3d3f4a = L.marker(
                [48.60387, 2.468207],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_bfeabb76168c617ff79f31099bc9e3f2 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_24af2eac3f8edf1d40f2b996fb3d3f4a.setIcon(icon_bfeabb76168c617ff79f31099bc9e3f2);
        
    
        var popup_6507a7dedeee0486567f42b45b25ad6d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_87748fd30232eec3407774011f1c1fb9 = $(`&lt;div id=&quot;html_87748fd30232eec3407774011f1c1fb9&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CER CLAREVA N7&lt;br&gt;23 rue de paris&lt;br&gt;corbeil essonnes&lt;br&gt;Nombre de candidats:93&lt;/div&gt;`)[0];
            popup_6507a7dedeee0486567f42b45b25ad6d.setContent(html_87748fd30232eec3407774011f1c1fb9);
        

        marker_24af2eac3f8edf1d40f2b996fb3d3f4a.bindPopup(popup_6507a7dedeee0486567f42b45b25ad6d)
        ;

        
    
    
            var marker_af4d7de771a008e272a12e88221b47de = L.marker(
                [48.613775, 2.485656],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_4b8dbccc9e4f8e67908e6177a5082abb = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_af4d7de771a008e272a12e88221b47de.setIcon(icon_4b8dbccc9e4f8e67908e6177a5082abb);
        
    
        var popup_53e1f99a37fb3361582eff03216b5480 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_03fb446a8d8667f7be77c8c7f68b4b35 = $(`&lt;div id=&quot;html_03fb446a8d8667f7be77c8c7f68b4b35&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CLAREVA&lt;br&gt;5 rue de la percherie&lt;br&gt;corbeil essonnes&lt;br&gt;Nombre de candidats:255&lt;/div&gt;`)[0];
            popup_53e1f99a37fb3361582eff03216b5480.setContent(html_03fb446a8d8667f7be77c8c7f68b4b35);
        

        marker_af4d7de771a008e272a12e88221b47de.bindPopup(popup_53e1f99a37fb3361582eff03216b5480)
        ;

        
    
    
            var marker_7c75ca8a25a6a60e47bdd39b91d28f35 = L.marker(
                [48.611887, 2.474488],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_47b280d314cf4e1444e1f0b28d0c72a6 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_7c75ca8a25a6a60e47bdd39b91d28f35.setIcon(icon_47b280d314cf4e1444e1f0b28d0c72a6);
        
    
        var popup_8c8cdb678f334c84d8dda3fbfa53c80b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2e0935910850d99f000172bcae5486a5 = $(`&lt;div id=&quot;html_2e0935910850d99f000172bcae5486a5&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CORBEIL&lt;br&gt;29 rue du general leclerc&lt;br&gt;corbeil essonnes&lt;br&gt;Nombre de candidats:121&lt;/div&gt;`)[0];
            popup_8c8cdb678f334c84d8dda3fbfa53c80b.setContent(html_2e0935910850d99f000172bcae5486a5);
        

        marker_7c75ca8a25a6a60e47bdd39b91d28f35.bindPopup(popup_8c8cdb678f334c84d8dda3fbfa53c80b)
        ;

        
    
    
            var marker_4ee1bcd1647a3ebd966abd65abba8386 = L.marker(
                [48.596741, 2.478434],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_48227f7cf10fe9c8a5080ed665df3481 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_4ee1bcd1647a3ebd966abd65abba8386.setIcon(icon_48227f7cf10fe9c8a5080ed665df3481);
        
    
        var popup_121b08efda80ed645305371c277857ff = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_3774cf2b9dff4f4d150af6ff3d48587a = $(`&lt;div id=&quot;html_3774cf2b9dff4f4d150af6ff3d48587a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DE LA PLACE AUTO ECOLE&lt;br&gt;16  place des victoires&lt;br&gt;corbeil essonnes&lt;br&gt;Nombre de candidats:71&lt;/div&gt;`)[0];
            popup_121b08efda80ed645305371c277857ff.setContent(html_3774cf2b9dff4f4d150af6ff3d48587a);
        

        marker_4ee1bcd1647a3ebd966abd65abba8386.bindPopup(popup_121b08efda80ed645305371c277857ff)
        ;

        
    
    
            var marker_3cbfd862cfad9bb25e211bfbaa08d7ae = L.marker(
                [48.605725, 2.467335],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_3c8ac11d40153e0d24a10879ea91f847 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_3cbfd862cfad9bb25e211bfbaa08d7ae.setIcon(icon_3c8ac11d40153e0d24a10879ea91f847);
        
    
        var popup_31fe6f2f07d401768caaae18f123fa2f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9040010ebf1ff1b3943bcfa2f6e27f04 = $(`&lt;div id=&quot;html_9040010ebf1ff1b3943bcfa2f6e27f04&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ESPACE SECURITE&lt;br&gt;60 rue du marechal de lattre de tassigny&lt;br&gt;corbeil essonnes&lt;br&gt;Nombre de candidats:130&lt;/div&gt;`)[0];
            popup_31fe6f2f07d401768caaae18f123fa2f.setContent(html_9040010ebf1ff1b3943bcfa2f6e27f04);
        

        marker_3cbfd862cfad9bb25e211bfbaa08d7ae.bindPopup(popup_31fe6f2f07d401768caaae18f123fa2f)
        ;

        
    
    
            var marker_800f403045ca43e22d2a41019b81e993 = L.marker(
                [48.607224, 2.483705],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_435f0cf2836d90cf3f7c1957b25d1a77 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_800f403045ca43e22d2a41019b81e993.setIcon(icon_435f0cf2836d90cf3f7c1957b25d1a77);
        
    
        var popup_526c0b13c37b76d36d6e8445ded6c8fe = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_dc020f979777c48a3e48863650b3f1d3 = $(`&lt;div id=&quot;html_dc020f979777c48a3e48863650b3f1d3&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;GMC CORBEIL&lt;br&gt;98 rue saint spire&lt;br&gt;corbeil essonne&lt;br&gt;Nombre de candidats:65&lt;/div&gt;`)[0];
            popup_526c0b13c37b76d36d6e8445ded6c8fe.setContent(html_dc020f979777c48a3e48863650b3f1d3);
        

        marker_800f403045ca43e22d2a41019b81e993.bindPopup(popup_526c0b13c37b76d36d6e8445ded6c8fe)
        ;

        
    
    
            var marker_cc5915d545f9450b6b7bcf8d8ca32dea = L.marker(
                [48.585973, 2.472127],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_d30e589c4847adb9d3bf6386c6164a58 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_cc5915d545f9450b6b7bcf8d8ca32dea.setIcon(icon_d30e589c4847adb9d3bf6386c6164a58);
        
    
        var popup_6839aff9cbd231a23e58bcd45c13cc61 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_3d535e9b6f11c41fcb45b5ec6484c588 = $(`&lt;div id=&quot;html_3d535e9b6f11c41fcb45b5ec6484c588&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;KS AUTO ECOLE&lt;br&gt;5 rue jules alexandre geoffroy&lt;br&gt;corbeil essonnes&lt;br&gt;Nombre de candidats:37&lt;/div&gt;`)[0];
            popup_6839aff9cbd231a23e58bcd45c13cc61.setContent(html_3d535e9b6f11c41fcb45b5ec6484c588);
        

        marker_cc5915d545f9450b6b7bcf8d8ca32dea.bindPopup(popup_6839aff9cbd231a23e58bcd45c13cc61)
        ;

        
    
    
            var marker_eb2f61e535cd714eac4d5c82496b7fec = L.marker(
                [48.596813, 2.466427],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_aef463281aa21cae41aefdf251157411 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_eb2f61e535cd714eac4d5c82496b7fec.setIcon(icon_aef463281aa21cae41aefdf251157411);
        
    
        var popup_8676bc3017879db5e808a539b0ccb020 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_4f12bb041c128ca04929ceb0e3c85014 = $(`&lt;div id=&quot;html_4f12bb041c128ca04929ceb0e3c85014&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MC CORBEIL&lt;br&gt;47 rue de la papeterie&lt;br&gt;corbeil essonnes&lt;br&gt;Nombre de candidats:59&lt;/div&gt;`)[0];
            popup_8676bc3017879db5e808a539b0ccb020.setContent(html_4f12bb041c128ca04929ceb0e3c85014);
        

        marker_eb2f61e535cd714eac4d5c82496b7fec.bindPopup(popup_8676bc3017879db5e808a539b0ccb020)
        ;

        
    
    
            var marker_9900faac63d07f835aed61f36b198e5a = L.marker(
                [48.58828, 2.456344],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_99b259bf333e1b1e07f0c32019f7e754 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_9900faac63d07f835aed61f36b198e5a.setIcon(icon_99b259bf333e1b1e07f0c32019f7e754);
        
    
        var popup_8cab14b4cc601a424706d0f426cdd034 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_fda78a4e5adf1bddefb51545240c5de4 = $(`&lt;div id=&quot;html_fda78a4e5adf1bddefb51545240c5de4&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;VILLABE&lt;br&gt;5 place roland vincent&lt;br&gt;villabe&lt;br&gt;Nombre de candidats:195&lt;/div&gt;`)[0];
            popup_8cab14b4cc601a424706d0f426cdd034.setContent(html_fda78a4e5adf1bddefb51545240c5de4);
        

        marker_9900faac63d07f835aed61f36b198e5a.bindPopup(popup_8cab14b4cc601a424706d0f426cdd034)
        ;

        
    
    
            var marker_c66a1dbb160b544be010f7e163d03867 = L.marker(
                [48.717797, 2.240353],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_db01fed80531b5f5ffb4a734dcd8513b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_c66a1dbb160b544be010f7e163d03867.setIcon(icon_db01fed80531b5f5ffb4a734dcd8513b);
        
    
        var popup_7611d1f53c89ababee293ad4a22c1ea0 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_beeea88f3530a0a2c14da0bfc697bb40 = $(`&lt;div id=&quot;html_beeea88f3530a0a2c14da0bfc697bb40&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;3C AUTO ECOLE&lt;br&gt;84-86 rue louise bruneau&lt;br&gt;palaiseau&lt;br&gt;Nombre de candidats:148&lt;/div&gt;`)[0];
            popup_7611d1f53c89ababee293ad4a22c1ea0.setContent(html_beeea88f3530a0a2c14da0bfc697bb40);
        

        marker_c66a1dbb160b544be010f7e163d03867.bindPopup(popup_7611d1f53c89ababee293ad4a22c1ea0)
        ;

        
    
    
            var marker_cb9c6abb65e417fef7a5c1ab5c96f890 = L.marker(
                [48.711726, 2.244015],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_f0ad1d339ce550c96812ceacc5ffa91f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_cb9c6abb65e417fef7a5c1ab5c96f890.setIcon(icon_f0ad1d339ce550c96812ceacc5ffa91f);
        
    
        var popup_5bcde0e00f7c6cf392cd59394b9ec6a1 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_b702f75e32e3a3cc0a9a68a2fc5a2205 = $(`&lt;div id=&quot;html_b702f75e32e3a3cc0a9a68a2fc5a2205&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;INRI&#x27;S PALAISEAU&lt;br&gt;13 rue du docteur morere&lt;br&gt;palaiseau&lt;br&gt;Nombre de candidats:99&lt;/div&gt;`)[0];
            popup_5bcde0e00f7c6cf392cd59394b9ec6a1.setContent(html_b702f75e32e3a3cc0a9a68a2fc5a2205);
        

        marker_cb9c6abb65e417fef7a5c1ab5c96f890.bindPopup(popup_5bcde0e00f7c6cf392cd59394b9ec6a1)
        ;

        
    
    
            var marker_aa006a605140e81cb6da9d67925136c3 = L.marker(
                [48.713811, 2.25819],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_d3553dc4f0f088d8ee5e50835014f998 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_aa006a605140e81cb6da9d67925136c3.setIcon(icon_d3553dc4f0f088d8ee5e50835014f998);
        
    
        var popup_586a0c8b3c5332fe8d0ef3978c384b7d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7bf43e10785772009acb564ba4a50a8b = $(`&lt;div id=&quot;html_7bf43e10785772009acb564ba4a50a8b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MC VINAY&lt;br&gt;1c ave du 1 mai&lt;br&gt;palaiseau&lt;br&gt;Nombre de candidats:86&lt;/div&gt;`)[0];
            popup_586a0c8b3c5332fe8d0ef3978c384b7d.setContent(html_7bf43e10785772009acb564ba4a50a8b);
        

        marker_aa006a605140e81cb6da9d67925136c3.bindPopup(popup_586a0c8b3c5332fe8d0ef3978c384b7d)
        ;

        
    
    
            var marker_f17f4e3004e4797e5ba5e3c203a34327 = L.marker(
                [48.707787, 2.240003],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_e2b8b16589f74345094b1504c7787771 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_f17f4e3004e4797e5ba5e3c203a34327.setIcon(icon_e2b8b16589f74345094b1504c7787771);
        
    
        var popup_bb277c42ff8d4c7b56156501641720ea = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9b2afcdc8e30dadf77412339fffd083c = $(`&lt;div id=&quot;html_9b2afcdc8e30dadf77412339fffd083c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;RUE DE PARIS&lt;br&gt;251 rue de paris&lt;br&gt;palaiseau&lt;br&gt;Nombre de candidats:182&lt;/div&gt;`)[0];
            popup_bb277c42ff8d4c7b56156501641720ea.setContent(html_9b2afcdc8e30dadf77412339fffd083c);
        

        marker_f17f4e3004e4797e5ba5e3c203a34327.bindPopup(popup_bb277c42ff8d4c7b56156501641720ea)
        ;

        
    
    
            var marker_96e8111947187fc6245e512530a5f537 = L.marker(
                [48.64893, 2.410102],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_1027ac5e713d9414eb85d687b4734572 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_96e8111947187fc6245e512530a5f537.setIcon(icon_1027ac5e713d9414eb85d687b4734572);
        
    
        var popup_0e52308b3101ae25de1ca11371653459 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c8eb7a50aa663e6d349618b81f85e4bf = $(`&lt;div id=&quot;html_c8eb7a50aa663e6d349618b81f85e4bf&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;AUTO ECOLE GEORGE SAND&lt;br&gt;28 avenue george sand&lt;br&gt;ris orangis&lt;br&gt;Nombre de candidats:167&lt;/div&gt;`)[0];
            popup_0e52308b3101ae25de1ca11371653459.setContent(html_c8eb7a50aa663e6d349618b81f85e4bf);
        

        marker_96e8111947187fc6245e512530a5f537.bindPopup(popup_0e52308b3101ae25de1ca11371653459)
        ;

        
    
    
            var marker_826fe63341ffe494b68ab1c674243f2d = L.marker(
                [48.649212, 2.408361],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_f1c2c18078c778eadf3a08f3b7349902 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_826fe63341ffe494b68ab1c674243f2d.setIcon(icon_f1c2c18078c778eadf3a08f3b7349902);
        
    
        var popup_13b5e1dae63e843bbc5ff4b88cad0aad = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_397b7ed9178006a35b73680b4c6c4873 = $(`&lt;div id=&quot;html_397b7ed9178006a35b73680b4c6c4873&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CER DU MOULIN A VENT&lt;br&gt;14 place du moulin a vent&lt;br&gt;ris orangis&lt;br&gt;Nombre de candidats:125&lt;/div&gt;`)[0];
            popup_13b5e1dae63e843bbc5ff4b88cad0aad.setContent(html_397b7ed9178006a35b73680b4c6c4873);
        

        marker_826fe63341ffe494b68ab1c674243f2d.bindPopup(popup_13b5e1dae63e843bbc5ff4b88cad0aad)
        ;

        
    
    
            var marker_5db94068a6bfdd9544480fd8b08aef82 = L.marker(
                [48.652114, 2.398761],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_040e45f90a4abaf58951e6f3fafa360b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_5db94068a6bfdd9544480fd8b08aef82.setIcon(icon_040e45f90a4abaf58951e6f3fafa360b);
        
    
        var popup_b7adfdee4bc6fde3a89a59cb1f7abba7 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d8df65b51d9ca31856f86e26ff49c8c2 = $(`&lt;div id=&quot;html_d8df65b51d9ca31856f86e26ff49c8c2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;LES IRIS&lt;br&gt;85 bis route de grigny&lt;br&gt;ris-orangis&lt;br&gt;Nombre de candidats:30&lt;/div&gt;`)[0];
            popup_b7adfdee4bc6fde3a89a59cb1f7abba7.setContent(html_d8df65b51d9ca31856f86e26ff49c8c2);
        

        marker_5db94068a6bfdd9544480fd8b08aef82.bindPopup(popup_b7adfdee4bc6fde3a89a59cb1f7abba7)
        ;

        
    
    
            var marker_36f2697b958aa40c50431b1835ea683f = L.marker(
                [48.652114, 2.398761],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_d1c88f9c3719eacea438f9736a1d554f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_36f2697b958aa40c50431b1835ea683f.setIcon(icon_d1c88f9c3719eacea438f9736a1d554f);
        
    
        var popup_e82ed874bd35450374d6940fd19a895c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ae88b7931e5142be46c60f24241c580c = $(`&lt;div id=&quot;html_ae88b7931e5142be46c60f24241c580c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;LES IRIS&lt;br&gt;85 bis route de grigny&lt;br&gt;ris orangis&lt;br&gt;Nombre de candidats:91&lt;/div&gt;`)[0];
            popup_e82ed874bd35450374d6940fd19a895c.setContent(html_ae88b7931e5142be46c60f24241c580c);
        

        marker_36f2697b958aa40c50431b1835ea683f.bindPopup(popup_e82ed874bd35450374d6940fd19a895c)
        ;

        
    
    
            var marker_67998e540a3b07c2b5b3a70b08531370 = L.marker(
                [48.6519, 2.399947],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_f9af1e818198bb82da19e0ead61fa2fd = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_67998e540a3b07c2b5b3a70b08531370.setIcon(icon_f9af1e818198bb82da19e0ead61fa2fd);
        
    
        var popup_091c4bae924c8e84482a53b1ddf57669 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_67ffade2c1a6ef9fd49ba9273bff3397 = $(`&lt;div id=&quot;html_67ffade2c1a6ef9fd49ba9273bff3397&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;REFLEXE RIS&lt;br&gt;79 rue de grigny&lt;br&gt;ris orangis&lt;br&gt;Nombre de candidats:54&lt;/div&gt;`)[0];
            popup_091c4bae924c8e84482a53b1ddf57669.setContent(html_67ffade2c1a6ef9fd49ba9273bff3397);
        

        marker_67998e540a3b07c2b5b3a70b08531370.bindPopup(popup_091c4bae924c8e84482a53b1ddf57669)
        ;

        
    
    
            var marker_d982303cb056bc7994fb733c3db052e7 = L.marker(
                [48.6519, 2.399947],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_21fb460ee624357b695d2faa1afe629d = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_d982303cb056bc7994fb733c3db052e7.setIcon(icon_21fb460ee624357b695d2faa1afe629d);
        
    
        var popup_2166321d6ea0185059125dcf628f618d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_94449a87fbe96e1f0b6ef06fa233bfdb = $(`&lt;div id=&quot;html_94449a87fbe96e1f0b6ef06fa233bfdb&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;REFLEXE RIS&lt;br&gt;79 route de grigny&lt;br&gt;ris orangis&lt;br&gt;Nombre de candidats:67&lt;/div&gt;`)[0];
            popup_2166321d6ea0185059125dcf628f618d.setContent(html_94449a87fbe96e1f0b6ef06fa233bfdb);
        

        marker_d982303cb056bc7994fb733c3db052e7.bindPopup(popup_2166321d6ea0185059125dcf628f618d)
        ;

        
    
    
            var marker_a901a4b1eac669062560105bc1175e07 = L.marker(
                [48.648799, 2.408386],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_fd0248c8e81a5d89e328fd1a5422c67e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_a901a4b1eac669062560105bc1175e07.setIcon(icon_fd0248c8e81a5d89e328fd1a5422c67e);
        
    
        var popup_c78427235a87fc7a639e969f49950aab = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e34c4b21d4bf6dd178aec20ab5db6be8 = $(`&lt;div id=&quot;html_e34c4b21d4bf6dd178aec20ab5db6be8&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;RIS ORANGIS CONDUITE CEDREY&lt;br&gt;71 rue pierre brossolette&lt;br&gt;ris orangis&lt;br&gt;Nombre de candidats:38&lt;/div&gt;`)[0];
            popup_c78427235a87fc7a639e969f49950aab.setContent(html_e34c4b21d4bf6dd178aec20ab5db6be8);
        

        marker_a901a4b1eac669062560105bc1175e07.bindPopup(popup_c78427235a87fc7a639e969f49950aab)
        ;

        
    
    
            var marker_110d7a0ce9030ee0cd667cc867a170fe = L.marker(
                [48.648799, 2.408386],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_c493dfab2121f90771383cf0c62d1fa3 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_110d7a0ce9030ee0cd667cc867a170fe.setIcon(icon_c493dfab2121f90771383cf0c62d1fa3);
        
    
        var popup_74f41624aac2b0a565d734a6ef6639cc = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_048ccb7d2b7bfc6f67997838e4c98671 = $(`&lt;div id=&quot;html_048ccb7d2b7bfc6f67997838e4c98671&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;RIS ORANGIS CONDUITE CEDREY&lt;br&gt;71 rue pierre brossolette&lt;br&gt;ris orangis&lt;br&gt;Nombre de candidats:38&lt;/div&gt;`)[0];
            popup_74f41624aac2b0a565d734a6ef6639cc.setContent(html_048ccb7d2b7bfc6f67997838e4c98671);
        

        marker_110d7a0ce9030ee0cd667cc867a170fe.bindPopup(popup_74f41624aac2b0a565d734a6ef6639cc)
        ;

        
    
    
            var marker_377ea02dadb8a19a3556edee383a4a69 = L.marker(
                [48.648799, 2.408386],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_b779f81d5fc492f51b73b2b2594376ba = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_377ea02dadb8a19a3556edee383a4a69.setIcon(icon_b779f81d5fc492f51b73b2b2594376ba);
        
    
        var popup_4e60f9e8e96a3605a9146f851798f3e1 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_98a5abbad14094df68736dfbeee8896f = $(`&lt;div id=&quot;html_98a5abbad14094df68736dfbeee8896f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;RIS ORANGIS CONDUITE CEDREY&lt;br&gt;71 rue pierre brossolette&lt;br&gt;ris orangis&lt;br&gt;Nombre de candidats:65&lt;/div&gt;`)[0];
            popup_4e60f9e8e96a3605a9146f851798f3e1.setContent(html_98a5abbad14094df68736dfbeee8896f);
        

        marker_377ea02dadb8a19a3556edee383a4a69.bindPopup(popup_4e60f9e8e96a3605a9146f851798f3e1)
        ;

        
    
    
            var marker_88e0b703c950aaf59c75613a42985914 = L.marker(
                [48.648799, 2.408386],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_778f259a0b5121cfdab42596c9daf6fa = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_88e0b703c950aaf59c75613a42985914.setIcon(icon_778f259a0b5121cfdab42596c9daf6fa);
        
    
        var popup_ad896238aa81d372026beb49516fffd1 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_76410be9d627c7e854041c2b5718b02d = $(`&lt;div id=&quot;html_76410be9d627c7e854041c2b5718b02d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;RIS ORANGIS CONDUITE CEDREY&lt;br&gt;71 rue pierre brossolette&lt;br&gt;ris orangis&lt;br&gt;Nombre de candidats:65&lt;/div&gt;`)[0];
            popup_ad896238aa81d372026beb49516fffd1.setContent(html_76410be9d627c7e854041c2b5718b02d);
        

        marker_88e0b703c950aaf59c75613a42985914.bindPopup(popup_ad896238aa81d372026beb49516fffd1)
        ;

        
    
    
            var marker_aebb29b97e521cd069239b70fff66cd2 = L.marker(
                [48.658641, 2.412706],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_1105251839e23e1be9b14c28adacde63 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_aebb29b97e521cd069239b70fff66cd2.setIcon(icon_1105251839e23e1be9b14c28adacde63);
        
    
        var popup_9209bd37eb60389ef87a464a6731e200 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d4d9cd512b9c966219197c71b6acce78 = $(`&lt;div id=&quot;html_d4d9cd512b9c966219197c71b6acce78&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;VAL DE RIS&lt;br&gt;15bis rue edmond nonte&lt;br&gt;ris orangis&lt;br&gt;Nombre de candidats:137&lt;/div&gt;`)[0];
            popup_9209bd37eb60389ef87a464a6731e200.setContent(html_d4d9cd512b9c966219197c71b6acce78);
        

        marker_aebb29b97e521cd069239b70fff66cd2.bindPopup(popup_9209bd37eb60389ef87a464a6731e200)
        ;

        
    
    
            var marker_fe817f3fdbc7607d4669ded76a6bad06 = L.marker(
                [48.43363, 2.155981],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_545d8c3f1a88dde10621cbaca3072c3d = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_fe817f3fdbc7607d4669ded76a6bad06.setIcon(icon_545d8c3f1a88dde10621cbaca3072c3d);
        
    
        var popup_a06414ef95870a91395d215165eaac68 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ff75f048e060d2f9700669300e5b3b6a = $(`&lt;div id=&quot;html_ff75f048e060d2f9700669300e5b3b6a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;AED AUTO ECOLE&lt;br&gt;63 rue saint jacques&lt;br&gt;etampes&lt;br&gt;Nombre de candidats:158&lt;/div&gt;`)[0];
            popup_a06414ef95870a91395d215165eaac68.setContent(html_ff75f048e060d2f9700669300e5b3b6a);
        

        marker_fe817f3fdbc7607d4669ded76a6bad06.bindPopup(popup_a06414ef95870a91395d215165eaac68)
        ;

        
    
    
            var marker_3cbc294a4b6bd880fdffb8e3e944b194 = L.marker(
                [48.431869, 2.156248],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_46cf6fc0e8c021005e74f48deae85391 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_3cbc294a4b6bd880fdffb8e3e944b194.setIcon(icon_46cf6fc0e8c021005e74f48deae85391);
        
    
        var popup_6e33f0ff62daeb120bd785e358baa435 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_189f91fb205f2890bc195e8697416f29 = $(`&lt;div id=&quot;html_189f91fb205f2890bc195e8697416f29&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ANTHONY auto ecole&lt;br&gt;56 rue paul  doumer&lt;br&gt;etampes&lt;br&gt;Nombre de candidats:82&lt;/div&gt;`)[0];
            popup_6e33f0ff62daeb120bd785e358baa435.setContent(html_189f91fb205f2890bc195e8697416f29);
        

        marker_3cbc294a4b6bd880fdffb8e3e944b194.bindPopup(popup_6e33f0ff62daeb120bd785e358baa435)
        ;

        
    
    
            var marker_7f40ffbc41e15353f3bd7f679d4a346c = L.marker(
                [48.436844, 2.164301],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_ed3916e82c6ae0a389a8e5cb3c7546f3 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_7f40ffbc41e15353f3bd7f679d4a346c.setIcon(icon_ed3916e82c6ae0a389a8e5cb3c7546f3);
        
    
        var popup_3e2a0d53b47814699750509280cfc69c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d17a03e7c7aabba00a1c8161ee68422c = $(`&lt;div id=&quot;html_d17a03e7c7aabba00a1c8161ee68422c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DU PORT&lt;br&gt;5 rue des archers&lt;br&gt;etampes&lt;br&gt;Nombre de candidats:211&lt;/div&gt;`)[0];
            popup_3e2a0d53b47814699750509280cfc69c.setContent(html_d17a03e7c7aabba00a1c8161ee68422c);
        

        marker_7f40ffbc41e15353f3bd7f679d4a346c.bindPopup(popup_3e2a0d53b47814699750509280cfc69c)
        ;

        
    
    
            var marker_26b5ab29007ce20b0c84d1fe4bfd1723 = L.marker(
                [48.436327, 2.158636],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_12eb4709e562399d8a6aa35bf676b398 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_26b5ab29007ce20b0c84d1fe4bfd1723.setIcon(icon_12eb4709e562399d8a6aa35bf676b398);
        
    
        var popup_fe6af427c17e2a35b5d45d805ad70fea = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ed2872e6c3a5655104451a32edce99c3 = $(`&lt;div id=&quot;html_ed2872e6c3a5655104451a32edce99c3&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;E.C.E EVASION&lt;br&gt;1 bd henri iv&lt;br&gt;etampes&lt;br&gt;Nombre de candidats:144&lt;/div&gt;`)[0];
            popup_fe6af427c17e2a35b5d45d805ad70fea.setContent(html_ed2872e6c3a5655104451a32edce99c3);
        

        marker_26b5ab29007ce20b0c84d1fe4bfd1723.bindPopup(popup_fe6af427c17e2a35b5d45d805ad70fea)
        ;

        
    
    
            var marker_fc13e8b71b90a32d5cceeac1dcbbe961 = L.marker(
                [48.428999, 2.146614],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_0d1fda5900e02a697cf0791b06a7ba7c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_fc13e8b71b90a32d5cceeac1dcbbe961.setIcon(icon_0d1fda5900e02a697cf0791b06a7ba7c);
        
    
        var popup_f33aef36043230356157c5cb2b4ed4c3 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_649418ab36a5887bc7ec0e3c885b7433 = $(`&lt;div id=&quot;html_649418ab36a5887bc7ec0e3c885b7433&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;GARE SAINT MARTIN AUTO ECOLE&lt;br&gt;16 rue saint martin&lt;br&gt;etampes&lt;br&gt;Nombre de candidats:64&lt;/div&gt;`)[0];
            popup_f33aef36043230356157c5cb2b4ed4c3.setContent(html_649418ab36a5887bc7ec0e3c885b7433);
        

        marker_fc13e8b71b90a32d5cceeac1dcbbe961.bindPopup(popup_f33aef36043230356157c5cb2b4ed4c3)
        ;

        
    
    
            var marker_3997590b8b4913ab40fcac3b742dce54 = L.marker(
                [48.432733, 2.154262],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_70d3ad48b53c8d589a849d17cc120339 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_3997590b8b4913ab40fcac3b742dce54.setIcon(icon_70d3ad48b53c8d589a849d17cc120339);
        
    
        var popup_73366d181d3812698fa8c4c7c813be52 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_bc9cf3e61237ab0d98f581c43369400b = $(`&lt;div id=&quot;html_bc9cf3e61237ab0d98f581c43369400b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;OBJECTIF STAR PILOTE&lt;br&gt;101  rue saint jacques&lt;br&gt;etampes&lt;br&gt;Nombre de candidats:109&lt;/div&gt;`)[0];
            popup_73366d181d3812698fa8c4c7c813be52.setContent(html_bc9cf3e61237ab0d98f581c43369400b);
        

        marker_3997590b8b4913ab40fcac3b742dce54.bindPopup(popup_73366d181d3812698fa8c4c7c813be52)
        ;

        
    
    
            var marker_e0f086722a564a906eb91e6e36e6f730 = L.marker(
                [48.433038, 2.154667],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_ac3d62b67f1048359151bc933d2f5ee2 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_e0f086722a564a906eb91e6e36e6f730.setIcon(icon_ac3d62b67f1048359151bc933d2f5ee2);
        
    
        var popup_4c7510211f66db9e66ee0fb7f498bbc6 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_09d1e8338bd524096d8a6f62930e7669 = $(`&lt;div id=&quot;html_09d1e8338bd524096d8a6f62930e7669&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ZENA CONDUITE&lt;br&gt;118 rue saint jacques&lt;br&gt;etampes&lt;br&gt;Nombre de candidats:36&lt;/div&gt;`)[0];
            popup_4c7510211f66db9e66ee0fb7f498bbc6.setContent(html_09d1e8338bd524096d8a6f62930e7669);
        

        marker_e0f086722a564a906eb91e6e36e6f730.bindPopup(popup_4c7510211f66db9e66ee0fb7f498bbc6)
        ;

        
    
    
            var marker_708013f0503718f65b7a73687510e49c = L.marker(
                [48.693012, 2.292512],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_73a31241ea6f56598322c5c75b550fcd = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_708013f0503718f65b7a73687510e49c.setIcon(icon_73a31241ea6f56598322c5c75b550fcd);
        
    
        var popup_ddb75d3a25eb72135adc6cc403b04cce = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_819170269cd965034a6532784ab95435 = $(`&lt;div id=&quot;html_819170269cd965034a6532784ab95435&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;137&lt;br&gt;137 rue du president francois mitterand&lt;br&gt;longjumeau&lt;br&gt;Nombre de candidats:451&lt;/div&gt;`)[0];
            popup_ddb75d3a25eb72135adc6cc403b04cce.setContent(html_819170269cd965034a6532784ab95435);
        

        marker_708013f0503718f65b7a73687510e49c.bindPopup(popup_ddb75d3a25eb72135adc6cc403b04cce)
        ;

        
    
    
            var marker_8db1684a051c4c050d5807c3d7fbaa99 = L.marker(
                [48.695158, 2.298565],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_6a50dca49ef19136656f790fd58dc906 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_8db1684a051c4c050d5807c3d7fbaa99.setIcon(icon_6a50dca49ef19136656f790fd58dc906);
        
    
        var popup_e8ae57c0b4cf2ff54084f07b377bc3e8 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8e5e4fa4bd12bbf8c699b01c9756109e = $(`&lt;div id=&quot;html_8e5e4fa4bd12bbf8c699b01c9756109e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CER LONGJUMEAU CONDUITE&lt;br&gt;18  avenue general de gaulle&lt;br&gt;longjumeau&lt;br&gt;Nombre de candidats:282&lt;/div&gt;`)[0];
            popup_e8ae57c0b4cf2ff54084f07b377bc3e8.setContent(html_8e5e4fa4bd12bbf8c699b01c9756109e);
        

        marker_8db1684a051c4c050d5807c3d7fbaa99.bindPopup(popup_e8ae57c0b4cf2ff54084f07b377bc3e8)
        ;

        
    
    
            var marker_509806bbb33bd7864ba96c2e058257cf = L.marker(
                [48.661582, 2.36376],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_64c70b52b2e616bdeb1fcf2a279ab442 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_509806bbb33bd7864ba96c2e058257cf.setIcon(icon_64c70b52b2e616bdeb1fcf2a279ab442);
        
    
        var popup_3274ef4081053e64594d84f5186ccae3 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a5301f2526b738afb3f6ea8b146d2d7c = $(`&lt;div id=&quot;html_a5301f2526b738afb3f6ea8b146d2d7c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ABC VIRY&lt;br&gt;60 avenue du commandant barre&lt;br&gt;viry-chatillon&lt;br&gt;Nombre de candidats:358&lt;/div&gt;`)[0];
            popup_3274ef4081053e64594d84f5186ccae3.setContent(html_a5301f2526b738afb3f6ea8b146d2d7c);
        

        marker_509806bbb33bd7864ba96c2e058257cf.bindPopup(popup_3274ef4081053e64594d84f5186ccae3)
        ;

        
    
    
            var marker_9fd064539e4d647eb75c351b159ee173 = L.marker(
                [48.675887, 2.368652],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_17e7fe1dd915e64e92fc63d90a8937aa = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_9fd064539e4d647eb75c351b159ee173.setIcon(icon_17e7fe1dd915e64e92fc63d90a8937aa);
        
    
        var popup_3c674c52fbae3c2786954bfb736d2f7a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a97b22c7ce12fa52aad90f4f5b954af9 = $(`&lt;div id=&quot;html_a97b22c7ce12fa52aad90f4f5b954af9&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ADOLPHE&lt;br&gt;160 avenue gabriel peri&lt;br&gt;viry chatillon&lt;br&gt;Nombre de candidats:330&lt;/div&gt;`)[0];
            popup_3c674c52fbae3c2786954bfb736d2f7a.setContent(html_a97b22c7ce12fa52aad90f4f5b954af9);
        

        marker_9fd064539e4d647eb75c351b159ee173.bindPopup(popup_3c674c52fbae3c2786954bfb736d2f7a)
        ;

        
    
    
            var marker_094b89c36510c079cf3090272c9a4428 = L.marker(
                [48.648107, 2.365923],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_16ab4c7e3d63315d6fd3dc14dcdb6393 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_094b89c36510c079cf3090272c9a4428.setIcon(icon_16ab4c7e3d63315d6fd3dc14dcdb6393);
        
    
        var popup_6bb623bf39474d51205de48aecadad07 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_006009e3173f2affe88aea36b81d43e5 = $(`&lt;div id=&quot;html_006009e3173f2affe88aea36b81d43e5&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CER VIRY&lt;br&gt;107 109 bd de la gribelette&lt;br&gt;viry chatillon&lt;br&gt;Nombre de candidats:102&lt;/div&gt;`)[0];
            popup_6bb623bf39474d51205de48aecadad07.setContent(html_006009e3173f2affe88aea36b81d43e5);
        

        marker_094b89c36510c079cf3090272c9a4428.bindPopup(popup_6bb623bf39474d51205de48aecadad07)
        ;

        
    
    
            var marker_2517b5121345c465baaa09f22570973f = L.marker(
                [48.675156, 2.386103],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_374576a3cdc1333703e9268959b539a0 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_2517b5121345c465baaa09f22570973f.setIcon(icon_374576a3cdc1333703e9268959b539a0);
        
    
        var popup_b6d7827a92b181833b125e244c34407b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_756837a9ce05656d45b6f4aeeb76519f = $(`&lt;div id=&quot;html_756837a9ce05656d45b6f4aeeb76519f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;INRI&#x27;S GARE DE VIRY&lt;br&gt;39/43 avenue general de gaulle&lt;br&gt;viry chatillon&lt;br&gt;Nombre de candidats:149&lt;/div&gt;`)[0];
            popup_b6d7827a92b181833b125e244c34407b.setContent(html_756837a9ce05656d45b6f4aeeb76519f);
        

        marker_2517b5121345c465baaa09f22570973f.bindPopup(popup_b6d7827a92b181833b125e244c34407b)
        ;

        
    
    
            var marker_1b96d38d8323365676cbc1ce8e27b1f4 = L.marker(
                [48.67472, 2.38701],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_deca4e9710880b7d884dce2ecedc6506 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_1b96d38d8323365676cbc1ce8e27b1f4.setIcon(icon_deca4e9710880b7d884dce2ecedc6506);
        
    
        var popup_ab95e4dd0f95daea1b9e877276a58c7b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c8f75ad34f1e31601e729217dd8619fc = $(`&lt;div id=&quot;html_c8f75ad34f1e31601e729217dd8619fc&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;VIRY FORMATION&lt;br&gt;56 av du general de gaulle&lt;br&gt;viry chatillon&lt;br&gt;Nombre de candidats:52&lt;/div&gt;`)[0];
            popup_ab95e4dd0f95daea1b9e877276a58c7b.setContent(html_c8f75ad34f1e31601e729217dd8619fc);
        

        marker_1b96d38d8323365676cbc1ce8e27b1f4.bindPopup(popup_ab95e4dd0f95daea1b9e877276a58c7b)
        ;

        
    
    
            var marker_cf208a171cb9f60a4dcd15ee22a15bf6 = L.marker(
                [48.673256, 2.375937],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_09195bb7396412d84590a7d2eb1cd5fb = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_cf208a171cb9f60a4dcd15ee22a15bf6.setIcon(icon_09195bb7396412d84590a7d2eb1cd5fb);
        
    
        var popup_bea440720998c2597c8997b1281b98ff = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_586c7e9277c775d57e9c128ec6a07222 = $(`&lt;div id=&quot;html_586c7e9277c775d57e9c128ec6a07222&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;VIRY TREMPLIN&lt;br&gt;10 place des martyrs&lt;br&gt;viry chatillon&lt;br&gt;Nombre de candidats:49&lt;/div&gt;`)[0];
            popup_bea440720998c2597c8997b1281b98ff.setContent(html_586c7e9277c775d57e9c128ec6a07222);
        

        marker_cf208a171cb9f60a4dcd15ee22a15bf6.bindPopup(popup_bea440720998c2597c8997b1281b98ff)
        ;

        
    
    
            var marker_548c79d40df10c50cc16bba7cfc35885 = L.marker(
                [48.69898, 2.137461],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_4ecb5c3aa2902320d201a1fe96bf5ddf = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_548c79d40df10c50cc16bba7cfc35885.setIcon(icon_4ecb5c3aa2902320d201a1fe96bf5ddf);
        
    
        var popup_262dd8676e0f03dc22a83eaa4032266e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_38aa6c4ed39d5dcd4873f25282c102b2 = $(`&lt;div id=&quot;html_38aa6c4ed39d5dcd4873f25282c102b2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;GIF LA VALLEE -  LL CONDUITE&lt;br&gt;7-9  rue raoul dautry&lt;br&gt;gif sur yvette&lt;br&gt;Nombre de candidats:146&lt;/div&gt;`)[0];
            popup_262dd8676e0f03dc22a83eaa4032266e.setContent(html_38aa6c4ed39d5dcd4873f25282c102b2);
        

        marker_548c79d40df10c50cc16bba7cfc35885.bindPopup(popup_262dd8676e0f03dc22a83eaa4032266e)
        ;

        
    
    
            var marker_2aab70a7fa8ca43068487131984b6bd6 = L.marker(
                [48.688086, 2.115665],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_ae0bfa5989d5fd6d4cc66bc9535c3938 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_2aab70a7fa8ca43068487131984b6bd6.setIcon(icon_ae0bfa5989d5fd6d4cc66bc9535c3938);
        
    
        var popup_a5b003e55c89bde4c833ace7013e52a8 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2231ffeca870a30916ebc7e1a8e90074 = $(`&lt;div id=&quot;html_2231ffeca870a30916ebc7e1a8e90074&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;LL CONDUITE&lt;br&gt;1 place du marche neuf chevry 2&lt;br&gt;gif sur yvette&lt;br&gt;Nombre de candidats:236&lt;/div&gt;`)[0];
            popup_a5b003e55c89bde4c833ace7013e52a8.setContent(html_2231ffeca870a30916ebc7e1a8e90074);
        

        marker_2aab70a7fa8ca43068487131984b6bd6.bindPopup(popup_a5b003e55c89bde4c833ace7013e52a8)
        ;

        
    
    
            var marker_271bda9bd2feea54872b0ecb669d7eb9 = L.marker(
                [48.712348, 2.401416],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_90d5faad0a374012fa9d368842558eab = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_271bda9bd2feea54872b0ecb669d7eb9.setIcon(icon_90d5faad0a374012fa9d368842558eab);
        
    
        var popup_65bbf4c6b475c542b14c8f74cdb73704 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_42b45b97a7cbf36f9fbf3e6940cd923b = $(`&lt;div id=&quot;html_42b45b97a7cbf36f9fbf3e6940cd923b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ATHIS TREMPLIN AUTO ECOLE&lt;br&gt;5a rue de la montagne mons&lt;br&gt;athis mons&lt;br&gt;Nombre de candidats:102&lt;/div&gt;`)[0];
            popup_65bbf4c6b475c542b14c8f74cdb73704.setContent(html_42b45b97a7cbf36f9fbf3e6940cd923b);
        

        marker_271bda9bd2feea54872b0ecb669d7eb9.bindPopup(popup_65bbf4c6b475c542b14c8f74cdb73704)
        ;

        
    
    
            var marker_20688747f9bfc7ea0dba5d01f26a4c43 = L.marker(
                [48.698926, 2.371746],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_9f85f23bd02ac91f1301aa014d81bbdc = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_20688747f9bfc7ea0dba5d01f26a4c43.setIcon(icon_9f85f23bd02ac91f1301aa014d81bbdc);
        
    
        var popup_f8f4e99fd66f6d813f1610cb4ac3b699 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_640a8a9197e8625867effc9b2c742256 = $(`&lt;div id=&quot;html_640a8a9197e8625867effc9b2c742256&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CER ATHIS&lt;br&gt;11  rue francois mitterand&lt;br&gt;athis mons&lt;br&gt;Nombre de candidats:51&lt;/div&gt;`)[0];
            popup_f8f4e99fd66f6d813f1610cb4ac3b699.setContent(html_640a8a9197e8625867effc9b2c742256);
        

        marker_20688747f9bfc7ea0dba5d01f26a4c43.bindPopup(popup_f8f4e99fd66f6d813f1610cb4ac3b699)
        ;

        
    
    
            var marker_5d8175b0028e5e6c6c16ee647acb7214 = L.marker(
                [48.698926, 2.371746],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_26fe0685ac65bebe44d4e20bfb54653d = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_5d8175b0028e5e6c6c16ee647acb7214.setIcon(icon_26fe0685ac65bebe44d4e20bfb54653d);
        
    
        var popup_a45ed0831f911e2a4903216b885478a9 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_646e301379e4ae94ea802bd1275d1b65 = $(`&lt;div id=&quot;html_646e301379e4ae94ea802bd1275d1b65&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CER ATHIS&lt;br&gt;11 rue francois mitterand&lt;br&gt;athis mons&lt;br&gt;Nombre de candidats:46&lt;/div&gt;`)[0];
            popup_a45ed0831f911e2a4903216b885478a9.setContent(html_646e301379e4ae94ea802bd1275d1b65);
        

        marker_5d8175b0028e5e6c6c16ee647acb7214.bindPopup(popup_a45ed0831f911e2a4903216b885478a9)
        ;

        
    
    
            var marker_71406a86d9daf7dde6b69071b4e4edf1 = L.marker(
                [48.70516, 2.391903],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_cc2f20e14365fd77ea0e97758bb7c0be = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_71406a86d9daf7dde6b69071b4e4edf1.setIcon(icon_cc2f20e14365fd77ea0e97758bb7c0be);
        
    
        var popup_6a70748a78845f5ba4c883de505788b0 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2d3fa29d8040795262d49158dcd25f44 = $(`&lt;div id=&quot;html_2d3fa29d8040795262d49158dcd25f44&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CER ATHIS FORMATION&lt;br&gt;155 avenue du 18 avril&lt;br&gt;athis mons&lt;br&gt;Nombre de candidats:83&lt;/div&gt;`)[0];
            popup_6a70748a78845f5ba4c883de505788b0.setContent(html_2d3fa29d8040795262d49158dcd25f44);
        

        marker_71406a86d9daf7dde6b69071b4e4edf1.bindPopup(popup_6a70748a78845f5ba4c883de505788b0)
        ;

        
    
    
            var marker_7ec02168158be6cf00d90709a3cabaf7 = L.marker(
                [48.700653, 2.357122],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_a40e668b3e10ae9d28d1753b5a31986d = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_7ec02168158be6cf00d90709a3cabaf7.setIcon(icon_a40e668b3e10ae9d28d1753b5a31986d);
        
    
        var popup_8af04a7c91501f9c6e2742a5f8e3744b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c2321f454e20c332364b2879799f95e0 = $(`&lt;div id=&quot;html_c2321f454e20c332364b2879799f95e0&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DE LA PYRAMIDE AUTO ECOLE&lt;br&gt;88  rue de la voie verte&lt;br&gt;athis mons&lt;br&gt;Nombre de candidats:149&lt;/div&gt;`)[0];
            popup_8af04a7c91501f9c6e2742a5f8e3744b.setContent(html_c2321f454e20c332364b2879799f95e0);
        

        marker_7ec02168158be6cf00d90709a3cabaf7.bindPopup(popup_8af04a7c91501f9c6e2742a5f8e3744b)
        ;

        
    
    
            var marker_4d6c2150e10b04ffed04a452c810cc4a = L.marker(
                [48.708186, 2.388788],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_4e35439308317a78cc25a9984315addb = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_4d6c2150e10b04ffed04a452c810cc4a.setIcon(icon_4e35439308317a78cc25a9984315addb);
        
    
        var popup_b7f790d3ce0587106ebbe18fcc02b25b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c2e093d1c1d9baf8bd7b92ef9792f7b5 = $(`&lt;div id=&quot;html_c2e093d1c1d9baf8bd7b92ef9792f7b5&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ESR ATHIS&lt;br&gt;11 rue paul vaillant couturier&lt;br&gt;athis mons&lt;br&gt;Nombre de candidats:42&lt;/div&gt;`)[0];
            popup_b7f790d3ce0587106ebbe18fcc02b25b.setContent(html_c2e093d1c1d9baf8bd7b92ef9792f7b5);
        

        marker_4d6c2150e10b04ffed04a452c810cc4a.bindPopup(popup_b7f790d3ce0587106ebbe18fcc02b25b)
        ;

        
    
    
            var marker_9038ba0d4493085c6ce8a242f06b964e = L.marker(
                [48.703939, 2.371519],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_02c10d8725e4e80a3933b039c58b8583 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_9038ba0d4493085c6ce8a242f06b964e.setIcon(icon_02c10d8725e4e80a3933b039c58b8583);
        
    
        var popup_6fe392a6f7c113f9cd1f5fe625e0c5d5 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_cd043834bdba06947e5e99728883623e = $(`&lt;div id=&quot;html_cd043834bdba06947e5e99728883623e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;INRIS ATHIS MONS CONDUITE&lt;br&gt;75 avenue francois mitterand&lt;br&gt;athis mons&lt;br&gt;Nombre de candidats:104&lt;/div&gt;`)[0];
            popup_6fe392a6f7c113f9cd1f5fe625e0c5d5.setContent(html_cd043834bdba06947e5e99728883623e);
        

        marker_9038ba0d4493085c6ce8a242f06b964e.bindPopup(popup_6fe392a6f7c113f9cd1f5fe625e0c5d5)
        ;

        
    
    
            var marker_a5bab8f584344a802067ab8598f7f4cd = L.marker(
                [48.681142, 2.409145],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_21f6b48348bf5e8720d6c1a4bfa72806 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_a5bab8f584344a802067ab8598f7f4cd.setIcon(icon_21f6b48348bf5e8720d6c1a4bfa72806);
        
    
        var popup_c0baeee8b58c05e9556e282e6f1abf23 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_0ccb21733b8cfe07bd95adec6aacf148 = $(`&lt;div id=&quot;html_0ccb21733b8cfe07bd95adec6aacf148&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;AUTO ECOLE LEFEVRE&lt;br&gt;130 boulevard henri barbusse&lt;br&gt;draveil&lt;br&gt;Nombre de candidats:27&lt;/div&gt;`)[0];
            popup_c0baeee8b58c05e9556e282e6f1abf23.setContent(html_0ccb21733b8cfe07bd95adec6aacf148);
        

        marker_a5bab8f584344a802067ab8598f7f4cd.bindPopup(popup_c0baeee8b58c05e9556e282e6f1abf23)
        ;

        
    
    
            var marker_d1ce5c0cdb87183500a096b2e9689d13 = L.marker(
                [48.682943, 2.408266],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_21349948fb0b2f8d5d77681fe03864b9 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_d1ce5c0cdb87183500a096b2e9689d13.setIcon(icon_21349948fb0b2f8d5d77681fe03864b9);
        
    
        var popup_21b9ecb9a6babae0e23c100b09f24d70 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c7d09e933bd15148720e87bdfa0e9f02 = $(`&lt;div id=&quot;html_c7d09e933bd15148720e87bdfa0e9f02&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DRAVEIL AUTO ECOLE&lt;br&gt;170 avenue henri barbusse&lt;br&gt;draveil&lt;br&gt;Nombre de candidats:136&lt;/div&gt;`)[0];
            popup_21b9ecb9a6babae0e23c100b09f24d70.setContent(html_c7d09e933bd15148720e87bdfa0e9f02);
        

        marker_d1ce5c0cdb87183500a096b2e9689d13.bindPopup(popup_21b9ecb9a6babae0e23c100b09f24d70)
        ;

        
    
    
            var marker_99e53b948dfeff955ca792b88f65c2c4 = L.marker(
                [48.68089, 2.410059],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_1095cf0ab969eb2cc570a36ab1bf8254 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_99e53b948dfeff955ca792b88f65c2c4.setIcon(icon_1095cf0ab969eb2cc570a36ab1bf8254);
        
    
        var popup_f9bf62958c8c7f3ce50832d2f449847d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_eb9d88e75ba628d18f2fa210f5d37fc0 = $(`&lt;div id=&quot;html_eb9d88e75ba628d18f2fa210f5d37fc0&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DRAVEIL AUTO ECOLE&lt;br&gt;170boulevard henri barbusse&lt;br&gt;draveil&lt;br&gt;Nombre de candidats:49&lt;/div&gt;`)[0];
            popup_f9bf62958c8c7f3ce50832d2f449847d.setContent(html_eb9d88e75ba628d18f2fa210f5d37fc0);
        

        marker_99e53b948dfeff955ca792b88f65c2c4.bindPopup(popup_f9bf62958c8c7f3ce50832d2f449847d)
        ;

        
    
    
            var marker_90c0dfab74e741b3989b9ab2cca39462 = L.marker(
                [48.686472, 2.411134],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_8f0d6b43e046c5947fc2db25d164584c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_90c0dfab74e741b3989b9ab2cca39462.setIcon(icon_8f0d6b43e046c5947fc2db25d164584c);
        
    
        var popup_9eb65438a956c747fbfe48fb6519b0a1 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_5fbe2ab90a34ce13e14b775ab2cdb69e = $(`&lt;div id=&quot;html_5fbe2ab90a34ce13e14b775ab2cdb69e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DRAVEIL TREMPLIN&lt;br&gt;7 rue jean moulin&lt;br&gt;draveil&lt;br&gt;Nombre de candidats:56&lt;/div&gt;`)[0];
            popup_9eb65438a956c747fbfe48fb6519b0a1.setContent(html_5fbe2ab90a34ce13e14b775ab2cdb69e);
        

        marker_90c0dfab74e741b3989b9ab2cca39462.bindPopup(popup_9eb65438a956c747fbfe48fb6519b0a1)
        ;

        
    
    
            var marker_804bf7a3ff98a288f1c574aafea14e52 = L.marker(
                [48.686472, 2.411134],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_b7538b25d792074104bb235473fa09e5 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_804bf7a3ff98a288f1c574aafea14e52.setIcon(icon_b7538b25d792074104bb235473fa09e5);
        
    
        var popup_314f8e1009577f99e87434a3ceac99a1 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2f7bb56613feedf388859ec65b95ff7f = $(`&lt;div id=&quot;html_2f7bb56613feedf388859ec65b95ff7f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DRAVEIL TREMPLIN&lt;br&gt;7 rue jean moulin&lt;br&gt;draveil&lt;br&gt;Nombre de candidats:56&lt;/div&gt;`)[0];
            popup_314f8e1009577f99e87434a3ceac99a1.setContent(html_2f7bb56613feedf388859ec65b95ff7f);
        

        marker_804bf7a3ff98a288f1c574aafea14e52.bindPopup(popup_314f8e1009577f99e87434a3ceac99a1)
        ;

        
    
    
            var marker_80fb1f364efd915511671570b0724bc1 = L.marker(
                [48.686472, 2.411134],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_12c05c7173287dd2a812b2cd4f7ceefb = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_80fb1f364efd915511671570b0724bc1.setIcon(icon_12c05c7173287dd2a812b2cd4f7ceefb);
        
    
        var popup_3c2d9f78e70546dadc1587c1c0887fd9 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_4b1f9641b6b2df84c7875df65ee38960 = $(`&lt;div id=&quot;html_4b1f9641b6b2df84c7875df65ee38960&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;TREMPLIN DRAVEIL&lt;br&gt;7 rue jean moulin&lt;br&gt;draveil&lt;br&gt;Nombre de candidats:21&lt;/div&gt;`)[0];
            popup_3c2d9f78e70546dadc1587c1c0887fd9.setContent(html_4b1f9641b6b2df84c7875df65ee38960);
        

        marker_80fb1f364efd915511671570b0724bc1.bindPopup(popup_3c2d9f78e70546dadc1587c1c0887fd9)
        ;

        
    
    
            var marker_0d8849045f3dc996e4e526597fcc9782 = L.marker(
                [48.686472, 2.411134],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_93863ad0f6c6b7c87a6ee3e95acd708b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_0d8849045f3dc996e4e526597fcc9782.setIcon(icon_93863ad0f6c6b7c87a6ee3e95acd708b);
        
    
        var popup_69669054daab66878f4cc806f72b82f3 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_660a48ed04660190445b6f2fba59cea1 = $(`&lt;div id=&quot;html_660a48ed04660190445b6f2fba59cea1&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;TREMPLIN DRAVEIL&lt;br&gt;7 rue jean moulin&lt;br&gt;draveil&lt;br&gt;Nombre de candidats:21&lt;/div&gt;`)[0];
            popup_69669054daab66878f4cc806f72b82f3.setContent(html_660a48ed04660190445b6f2fba59cea1);
        

        marker_0d8849045f3dc996e4e526597fcc9782.bindPopup(popup_69669054daab66878f4cc806f72b82f3)
        ;

        
    
    
            var marker_577e6b2124f4cda225417b496377e119 = L.marker(
                [48.686458, 2.415581],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_b9ab4e891d0cf3d209cfa8074b19c461 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_577e6b2124f4cda225417b496377e119.setIcon(icon_b9ab4e891d0cf3d209cfa8074b19c461);
        
    
        var popup_d93702b6447b1863edb615c0a1929b46 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_fedcc5670edac4c3ae5c304a39a75a7f = $(`&lt;div id=&quot;html_fedcc5670edac4c3ae5c304a39a75a7f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;FC SABRINA&lt;br&gt;32 rue de nainville&lt;br&gt;draveil&lt;br&gt;Nombre de candidats:321&lt;/div&gt;`)[0];
            popup_d93702b6447b1863edb615c0a1929b46.setContent(html_fedcc5670edac4c3ae5c304a39a75a7f);
        

        marker_577e6b2124f4cda225417b496377e119.bindPopup(popup_d93702b6447b1863edb615c0a1929b46)
        ;

        
    
    
            var marker_88ba6c3b1da470a56638d2cc737aec81 = L.marker(
                [48.681142, 2.409145],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_f48ab215b8a821a6d811eff9c962bb4e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_88ba6c3b1da470a56638d2cc737aec81.setIcon(icon_f48ab215b8a821a6d811eff9c962bb4e);
        
    
        var popup_6ea7cd576afd861f39aa5229c5ed9372 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7361d192e9d030a959176523848d5b31 = $(`&lt;div id=&quot;html_7361d192e9d030a959176523848d5b31&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;LEFEVRE&lt;br&gt;130 bld h barbusse&lt;br&gt;draveil&lt;br&gt;Nombre de candidats:86&lt;/div&gt;`)[0];
            popup_6ea7cd576afd861f39aa5229c5ed9372.setContent(html_7361d192e9d030a959176523848d5b31);
        

        marker_88ba6c3b1da470a56638d2cc737aec81.bindPopup(popup_6ea7cd576afd861f39aa5229c5ed9372)
        ;

        
    
    
            var marker_27ba89857f811074483233100b3cc9a3 = L.marker(
                [48.608957, 2.312579],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_5522426f86ca0a62050998731e4e85f1 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_27ba89857f811074483233100b3cc9a3.setIcon(icon_5522426f86ca0a62050998731e4e85f1);
        
    
        var popup_cb6564dc12e3eaf525bc29bda661d997 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_fa424b43cbdc894190928fbe4a7be84e = $(`&lt;div id=&quot;html_fa424b43cbdc894190928fbe4a7be84e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;BRETIGNY TREMPLIN&lt;br&gt;1 rue henri douard&lt;br&gt;bretigny sur orge&lt;br&gt;Nombre de candidats:91&lt;/div&gt;`)[0];
            popup_cb6564dc12e3eaf525bc29bda661d997.setContent(html_fa424b43cbdc894190928fbe4a7be84e);
        

        marker_27ba89857f811074483233100b3cc9a3.bindPopup(popup_cb6564dc12e3eaf525bc29bda661d997)
        ;

        
    
    
            var marker_3bfafc5fc6960405bbd2213c6bb33d5c = L.marker(
                [48.606068, 2.302472],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_da5997083d27b83cd2f8b1d6428b7e40 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_3bfafc5fc6960405bbd2213c6bb33d5c.setIcon(icon_da5997083d27b83cd2f8b1d6428b7e40);
        
    
        var popup_c2fde5a8c5a69b5f2502ad5134249feb = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a640249dd0ee0b690732beb3d6a4dee3 = $(`&lt;div id=&quot;html_a640249dd0ee0b690732beb3d6a4dee3&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ECF BRETIGNY GARE&lt;br&gt;1 rue alfred leblanc&lt;br&gt;bretigny&lt;br&gt;Nombre de candidats:323&lt;/div&gt;`)[0];
            popup_c2fde5a8c5a69b5f2502ad5134249feb.setContent(html_a640249dd0ee0b690732beb3d6a4dee3);
        

        marker_3bfafc5fc6960405bbd2213c6bb33d5c.bindPopup(popup_c2fde5a8c5a69b5f2502ad5134249feb)
        ;

        
    
    
            var marker_55e420e861cd860dadd4d9d4a47abd26 = L.marker(
                [48.609105, 2.305028],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_dcafabe9e975e614283c54b902b69437 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_55e420e861cd860dadd4d9d4a47abd26.setIcon(icon_dcafabe9e975e614283c54b902b69437);
        
    
        var popup_4562bb3a7dd26d8ba5846225e2035851 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_12428760b76598382e904c80ed6f58e2 = $(`&lt;div id=&quot;html_12428760b76598382e904c80ed6f58e2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;GREEN CONDUITE&lt;br&gt;6 rue de la paix&lt;br&gt;bretigny sur orge&lt;br&gt;Nombre de candidats:97&lt;/div&gt;`)[0];
            popup_4562bb3a7dd26d8ba5846225e2035851.setContent(html_12428760b76598382e904c80ed6f58e2);
        

        marker_55e420e861cd860dadd4d9d4a47abd26.bindPopup(popup_4562bb3a7dd26d8ba5846225e2035851)
        ;

        
    
    
            var marker_e80b96c19a190fd6060226b5e3a7808c = L.marker(
                [48.607321, 2.30379],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_e9c317086202524cc0576d79cbf8004a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_e80b96c19a190fd6060226b5e3a7808c.setIcon(icon_e9c317086202524cc0576d79cbf8004a);
        
    
        var popup_aab92177cd51bccd6fbe7035c5b804b0 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e9406aa1ca2c43b04fd8ebce34a57537 = $(`&lt;div id=&quot;html_e9406aa1ca2c43b04fd8ebce34a57537&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MC BRETIGNY&lt;br&gt;18 rue d estienne d orves&lt;br&gt;bretigny sur orge&lt;br&gt;Nombre de candidats:288&lt;/div&gt;`)[0];
            popup_aab92177cd51bccd6fbe7035c5b804b0.setContent(html_e9406aa1ca2c43b04fd8ebce34a57537);
        

        marker_e80b96c19a190fd6060226b5e3a7808c.bindPopup(popup_aab92177cd51bccd6fbe7035c5b804b0)
        ;

        
    
    
            var marker_07edd3f32a76d80e2f6d398aef0c3f2f = L.marker(
                [48.706374, 2.455781],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_4ddfea0907a9b3c7ea7c8fdef45d28a1 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_07edd3f32a76d80e2f6d398aef0c3f2f.setIcon(icon_4ddfea0907a9b3c7ea7c8fdef45d28a1);
        
    
        var popup_c73965eff4f9b3f2857300134adcc40d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_049b8e459f36d26ccd7b8e68ef2dd656 = $(`&lt;div id=&quot;html_049b8e459f36d26ccd7b8e68ef2dd656&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;AMG MONTGERON&lt;br&gt;58 avenue de la republique&lt;br&gt;montgeron&lt;br&gt;Nombre de candidats:122&lt;/div&gt;`)[0];
            popup_c73965eff4f9b3f2857300134adcc40d.setContent(html_049b8e459f36d26ccd7b8e68ef2dd656);
        

        marker_07edd3f32a76d80e2f6d398aef0c3f2f.bindPopup(popup_c73965eff4f9b3f2857300134adcc40d)
        ;

        
    
    
            var marker_d2b20b363aa0977925abae9318b04573 = L.marker(
                [48.71567, 2.443257],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_56d8a859eca9fe2c5fd8efc55efb4bba = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_d2b20b363aa0977925abae9318b04573.setIcon(icon_56d8a859eca9fe2c5fd8efc55efb4bba);
        
    
        var popup_5222ac3671adf8eb6e7bfa21b80e5c65 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_29c8add168c5d24a1958f9003a536582 = $(`&lt;div id=&quot;html_29c8add168c5d24a1958f9003a536582&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CER PRO CONDUITE Montgeron&lt;br&gt;8 route de corbeil&lt;br&gt;montgeron&lt;br&gt;Nombre de candidats:104&lt;/div&gt;`)[0];
            popup_5222ac3671adf8eb6e7bfa21b80e5c65.setContent(html_29c8add168c5d24a1958f9003a536582);
        

        marker_d2b20b363aa0977925abae9318b04573.bindPopup(popup_5222ac3671adf8eb6e7bfa21b80e5c65)
        ;

        
    
    
            var marker_50bad9bd432432f1d718ddcc791cd473 = L.marker(
                [48.704759, 2.460538],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_418a1c734151596bb2b8a039a2597596 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_50bad9bd432432f1d718ddcc791cd473.setIcon(icon_418a1c734151596bb2b8a039a2597596);
        
    
        var popup_951a859d699f72a2d290b104387583b4 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9f83694e94c2618d10db6ed828ca85ad = $(`&lt;div id=&quot;html_9f83694e94c2618d10db6ed828ca85ad&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DANY&lt;br&gt;95 avenue de la republique&lt;br&gt;montgeron&lt;br&gt;Nombre de candidats:111&lt;/div&gt;`)[0];
            popup_951a859d699f72a2d290b104387583b4.setContent(html_9f83694e94c2618d10db6ed828ca85ad);
        

        marker_50bad9bd432432f1d718ddcc791cd473.bindPopup(popup_951a859d699f72a2d290b104387583b4)
        ;

        
    
    
            var marker_183e1765a985a50bb9f14047eb031c79 = L.marker(
                [48.708042, 2.461764],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_ed986962a145d8ee7cbfc6ce8a458a1a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_183e1765a985a50bb9f14047eb031c79.setIcon(icon_ed986962a145d8ee7cbfc6ce8a458a1a);
        
    
        var popup_97af07e9e401507224c6d581c1ebb4ee = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e217ae65d5d5f2dde75ce173fdb925d1 = $(`&lt;div id=&quot;html_e217ae65d5d5f2dde75ce173fdb925d1&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;GO PERMIS&lt;br&gt;52 ter rue du docteur leon deglaire&lt;br&gt;montgeron&lt;br&gt;Nombre de candidats:159&lt;/div&gt;`)[0];
            popup_97af07e9e401507224c6d581c1ebb4ee.setContent(html_e217ae65d5d5f2dde75ce173fdb925d1);
        

        marker_183e1765a985a50bb9f14047eb031c79.bindPopup(popup_97af07e9e401507224c6d581c1ebb4ee)
        ;

        
    
    
            var marker_ee8dfd4cac9c3539c5c500796ae9ab1f = L.marker(
                [48.707946, 2.453813],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_da66f80f460eb0855088d3cd8b0c29ae = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_ee8dfd4cac9c3539c5c500796ae9ab1f.setIcon(icon_da66f80f460eb0855088d3cd8b0c29ae);
        
    
        var popup_e30139f3e0525be573d5e60067622ec0 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_07f8d6558487bae59c919562d3c018b9 = $(`&lt;div id=&quot;html_07f8d6558487bae59c919562d3c018b9&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;INRI&#x27;S MONTGERON&lt;br&gt;33 avenue de la republique&lt;br&gt;montgeron&lt;br&gt;Nombre de candidats:159&lt;/div&gt;`)[0];
            popup_e30139f3e0525be573d5e60067622ec0.setContent(html_07f8d6558487bae59c919562d3c018b9);
        

        marker_ee8dfd4cac9c3539c5c500796ae9ab1f.bindPopup(popup_e30139f3e0525be573d5e60067622ec0)
        ;

        
    
    
            var marker_7859668d99401b34b5f342595e8ee789 = L.marker(
                [48.707946, 2.453813],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_cd6b6568b6fadade770a3798e7880f6b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_7859668d99401b34b5f342595e8ee789.setIcon(icon_cd6b6568b6fadade770a3798e7880f6b);
        
    
        var popup_32ae9317822712c8efe9dce6f9abb30a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_67827cd941fb68e483f26df72bddf54a = $(`&lt;div id=&quot;html_67827cd941fb68e483f26df72bddf54a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;INRI&#x27;S MONTGERON&lt;br&gt;33 avenue de la republique&lt;br&gt;montgeron&lt;br&gt;Nombre de candidats:159&lt;/div&gt;`)[0];
            popup_32ae9317822712c8efe9dce6f9abb30a.setContent(html_67827cd941fb68e483f26df72bddf54a);
        

        marker_7859668d99401b34b5f342595e8ee789.bindPopup(popup_32ae9317822712c8efe9dce6f9abb30a)
        ;

        
    
    
            var marker_7cb8aca03c81c7dd81330b5ab15323de = L.marker(
                [48.707946, 2.453813],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_229207c3881c4d9ecca2f4db64e714ca = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_7cb8aca03c81c7dd81330b5ab15323de.setIcon(icon_229207c3881c4d9ecca2f4db64e714ca);
        
    
        var popup_e162a5c64378aa6c37ca609ac14efba0 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_87b19181f345ab8b433294412f52c300 = $(`&lt;div id=&quot;html_87b19181f345ab8b433294412f52c300&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;INRIS MONTGERON&lt;br&gt;33 avenue de la republique&lt;br&gt;montgeron&lt;br&gt;Nombre de candidats:34&lt;/div&gt;`)[0];
            popup_e162a5c64378aa6c37ca609ac14efba0.setContent(html_87b19181f345ab8b433294412f52c300);
        

        marker_7cb8aca03c81c7dd81330b5ab15323de.bindPopup(popup_e162a5c64378aa6c37ca609ac14efba0)
        ;

        
    
    
            var marker_5514610b7211cc10a62ea5217df2b860 = L.marker(
                [48.707946, 2.453813],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_0389e664b68209da97d7a8d27a205569 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_5514610b7211cc10a62ea5217df2b860.setIcon(icon_0389e664b68209da97d7a8d27a205569);
        
    
        var popup_8f7c514db0540d164bc3f6e727cb25e7 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1dc86e06560944ce647b90bff7e6480d = $(`&lt;div id=&quot;html_1dc86e06560944ce647b90bff7e6480d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;INRIS MONTGERON&lt;br&gt;33 avenue de la republique&lt;br&gt;montgeron&lt;br&gt;Nombre de candidats:34&lt;/div&gt;`)[0];
            popup_8f7c514db0540d164bc3f6e727cb25e7.setContent(html_1dc86e06560944ce647b90bff7e6480d);
        

        marker_5514610b7211cc10a62ea5217df2b860.bindPopup(popup_8f7c514db0540d164bc3f6e727cb25e7)
        ;

        
    
    
            var marker_89cd52747f2d4b880140c180c02ee3d3 = L.marker(
                [48.699717, 2.46863],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_c7183cd539b6521c04f905ed2f80dd93 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_89cd52747f2d4b880140c180c02ee3d3.setIcon(icon_c7183cd539b6521c04f905ed2f80dd93);
        
    
        var popup_0aa38788a4fc9abecba870c26f5fa1ea = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a837724b965fb746b341349bcebb7d6f = $(`&lt;div id=&quot;html_a837724b965fb746b341349bcebb7d6f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ROUTE 91&lt;br&gt;135 av de la republique&lt;br&gt;montgeron&lt;br&gt;Nombre de candidats:102&lt;/div&gt;`)[0];
            popup_0aa38788a4fc9abecba870c26f5fa1ea.setContent(html_a837724b965fb746b341349bcebb7d6f);
        

        marker_89cd52747f2d4b880140c180c02ee3d3.bindPopup(popup_0aa38788a4fc9abecba870c26f5fa1ea)
        ;

        
    
    
            var marker_8dc3e5f518b1409ae873c174fd065831 = L.marker(
                [48.701299, 2.466167],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_3ebba22e67417679408d99672faac46c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_8dc3e5f518b1409ae873c174fd065831.setIcon(icon_3ebba22e67417679408d99672faac46c);
        
    
        var popup_d18ec95e397b64b5447b7749b87b31b5 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d45d30333b60857586ba4848d00380b2 = $(`&lt;div id=&quot;html_d45d30333b60857586ba4848d00380b2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;START AUTO MOTO ECOLE&lt;br&gt;2  rue du général lelong&lt;br&gt;montgeron&lt;br&gt;Nombre de candidats:45&lt;/div&gt;`)[0];
            popup_d18ec95e397b64b5447b7749b87b31b5.setContent(html_d45d30333b60857586ba4848d00380b2);
        

        marker_8dc3e5f518b1409ae873c174fd065831.bindPopup(popup_d18ec95e397b64b5447b7749b87b31b5)
        ;

        
    
    
            var marker_b9edadd4a93ddebe9f45fa22de571753 = L.marker(
                [48.63506, 2.320784],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_375686b7faf399548f6f2ae4b91d404c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_b9edadd4a93ddebe9f45fa22de571753.setIcon(icon_375686b7faf399548f6f2ae4b91d404c);
        
    
        var popup_c3f3039721de67c38616dcd2370ae8d7 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e86d217dd92ea9ceb16b964159d8e342 = $(`&lt;div id=&quot;html_e86d217dd92ea9ceb16b964159d8e342&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CONDUIRE C EST PERMIS&lt;br&gt;19 bis rue st saens&lt;br&gt;st michel sur orge&lt;br&gt;Nombre de candidats:54&lt;/div&gt;`)[0];
            popup_c3f3039721de67c38616dcd2370ae8d7.setContent(html_e86d217dd92ea9ceb16b964159d8e342);
        

        marker_b9edadd4a93ddebe9f45fa22de571753.bindPopup(popup_c3f3039721de67c38616dcd2370ae8d7)
        ;

        
    
    
            var marker_3835594b2e6e21ab5247832e5ddd145f = L.marker(
                [48.636346, 2.321267],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_315ecfecfaee16f8d3201a908d56aca8 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_3835594b2e6e21ab5247832e5ddd145f.setIcon(icon_315ecfecfaee16f8d3201a908d56aca8);
        
    
        var popup_bc4e33b88c23de10490d587fcfdbff56 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_30561fa3da7d9705b70caf8511998cae = $(`&lt;div id=&quot;html_30561fa3da7d9705b70caf8511998cae&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;EBR&lt;br&gt;38 rue berlioz&lt;br&gt;st michel sur orge&lt;br&gt;Nombre de candidats:149&lt;/div&gt;`)[0];
            popup_bc4e33b88c23de10490d587fcfdbff56.setContent(html_30561fa3da7d9705b70caf8511998cae);
        

        marker_3835594b2e6e21ab5247832e5ddd145f.bindPopup(popup_bc4e33b88c23de10490d587fcfdbff56)
        ;

        
    
    
            var marker_6069099d44deddcb09f29bb44b439cfb = L.marker(
                [48.636124, 2.305515],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_38ec1d09f806b69897491138161a8406 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_6069099d44deddcb09f29bb44b439cfb.setIcon(icon_38ec1d09f806b69897491138161a8406);
        
    
        var popup_93b235a7922d0c588e83b53190e35769 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_feea09ae7fcc72dd955fa0eef936c211 = $(`&lt;div id=&quot;html_feea09ae7fcc72dd955fa0eef936c211&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;EDUCAT ROUTE&lt;br&gt;11 mail de l europe&lt;br&gt;saint michel sur orge&lt;br&gt;Nombre de candidats:171&lt;/div&gt;`)[0];
            popup_93b235a7922d0c588e83b53190e35769.setContent(html_feea09ae7fcc72dd955fa0eef936c211);
        

        marker_6069099d44deddcb09f29bb44b439cfb.bindPopup(popup_93b235a7922d0c588e83b53190e35769)
        ;

        
    
    
            var marker_80ae75385d93f2018e07e8daefea70a9 = L.marker(
                [48.635472, 2.304795],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_ece7d4e4ddce123778cc711e78924fc4 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_80ae75385d93f2018e07e8daefea70a9.setIcon(icon_ece7d4e4ddce123778cc711e78924fc4);
        
    
        var popup_58f4c43f8337b4526cf384725bd87dfc = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a3de65f3d3ae7c445eac5276305c7532 = $(`&lt;div id=&quot;html_a3de65f3d3ae7c445eac5276305c7532&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;LE FLAMBOYANT&lt;br&gt;67 rue de montlhery&lt;br&gt;saint michel sur orge&lt;br&gt;Nombre de candidats:45&lt;/div&gt;`)[0];
            popup_58f4c43f8337b4526cf384725bd87dfc.setContent(html_a3de65f3d3ae7c445eac5276305c7532);
        

        marker_80ae75385d93f2018e07e8daefea70a9.bindPopup(popup_58f4c43f8337b4526cf384725bd87dfc)
        ;

        
    
    
            var marker_ede4e9aec520f3fd777a132d165c81b7 = L.marker(
                [48.620372, 2.492423],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_1351bb207d0335ea2fc7a6b0db1fbc50 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_ede4e9aec520f3fd777a132d165c81b7.setIcon(icon_1351bb207d0335ea2fc7a6b0db1fbc50);
        
    
        var popup_4155a6ae1f86621b7e655b350d5e97f6 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_0df0edfca5c98709ce415f09d6998825 = $(`&lt;div id=&quot;html_0df0edfca5c98709ce415f09d6998825&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;A3 CONDUITE&lt;br&gt;4  place de l &#x27;europe&lt;br&gt;saint germain les corbeil&lt;br&gt;Nombre de candidats:37&lt;/div&gt;`)[0];
            popup_4155a6ae1f86621b7e655b350d5e97f6.setContent(html_0df0edfca5c98709ce415f09d6998825);
        

        marker_ede4e9aec520f3fd777a132d165c81b7.bindPopup(popup_4155a6ae1f86621b7e655b350d5e97f6)
        ;

        
    
    
            var marker_80e0089e6f23cfe4db70978259c03987 = L.marker(
                [48.619858, 2.493637],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_7ecab0fd120d4982703a9c486d8c3be6 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_80e0089e6f23cfe4db70978259c03987.setIcon(icon_7ecab0fd120d4982703a9c486d8c3be6);
        
    
        var popup_20c8fc96bab85fa90288dbe4db8d23be = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d294adda5b979b571b1feaf681c938db = $(`&lt;div id=&quot;html_d294adda5b979b571b1feaf681c938db&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CER SAINT GERMAIN LES CORBEIL&lt;br&gt;1 allee du val fleury&lt;br&gt;saint germain les corbeil&lt;br&gt;Nombre de candidats:225&lt;/div&gt;`)[0];
            popup_20c8fc96bab85fa90288dbe4db8d23be.setContent(html_d294adda5b979b571b1feaf681c938db);
        

        marker_80e0089e6f23cfe4db70978259c03987.bindPopup(popup_20c8fc96bab85fa90288dbe4db8d23be)
        ;

        
    
    
            var marker_4c9333cc806c5bbc3d7d746e50d0d73b = L.marker(
                [48.636973, 2.512383],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_62658849bf1de2d23bf40d872020055c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_4c9333cc806c5bbc3d7d746e50d0d73b.setIcon(icon_62658849bf1de2d23bf40d872020055c);
        
    
        var popup_b9fb762513a5f4a4822b8653e7b4b269 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_dc360ab5d2ac16f5d7e256c6a7385bb9 = $(`&lt;div id=&quot;html_dc360ab5d2ac16f5d7e256c6a7385bb9&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;RODOLPHE&lt;br&gt;1 rue du commandant lissac&lt;br&gt;tigery&lt;br&gt;Nombre de candidats:52&lt;/div&gt;`)[0];
            popup_b9fb762513a5f4a4822b8653e7b4b269.setContent(html_dc360ab5d2ac16f5d7e256c6a7385bb9);
        

        marker_4c9333cc806c5bbc3d7d746e50d0d73b.bindPopup(popup_b9fb762513a5f4a4822b8653e7b4b269)
        ;

        
    
    
            var marker_87be80599a2c0f4ecab6f3432000b56c = L.marker(
                [48.686663, 2.378295],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_7f6909ad4d726f6964ccf8b1eabc3f60 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_87be80599a2c0f4ecab6f3432000b56c.setIcon(icon_7f6909ad4d726f6964ccf8b1eabc3f60);
        
    
        var popup_cd0a0709f3e202c144f7564862742b9a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_77cf5e502cf8eef1c2ef43cde78838bf = $(`&lt;div id=&quot;html_77cf5e502cf8eef1c2ef43cde78838bf&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;AMG CONDUITE&lt;br&gt;34 rue pasteur&lt;br&gt;juvisy&lt;br&gt;Nombre de candidats:153&lt;/div&gt;`)[0];
            popup_cd0a0709f3e202c144f7564862742b9a.setContent(html_77cf5e502cf8eef1c2ef43cde78838bf);
        

        marker_87be80599a2c0f4ecab6f3432000b56c.bindPopup(popup_cd0a0709f3e202c144f7564862742b9a)
        ;

        
    
    
            var marker_25f8fd2a43db681980b38d07e2b2d428 = L.marker(
                [48.690145, 2.377198],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_3c7dd80dfceb00966186d74be621ed14 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_25f8fd2a43db681980b38d07e2b2d428.setIcon(icon_3c7dd80dfceb00966186d74be621ed14);
        
    
        var popup_c1ddfe4e69097fff3188edc3d757f143 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_967141a4a0ce7b4b949b91d43e223de2 = $(`&lt;div id=&quot;html_967141a4a0ce7b4b949b91d43e223de2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DU MARCHE&lt;br&gt;5 rue paul marais&lt;br&gt;juvisy sur orge&lt;br&gt;Nombre de candidats:43&lt;/div&gt;`)[0];
            popup_c1ddfe4e69097fff3188edc3d757f143.setContent(html_967141a4a0ce7b4b949b91d43e223de2);
        

        marker_25f8fd2a43db681980b38d07e2b2d428.bindPopup(popup_c1ddfe4e69097fff3188edc3d757f143)
        ;

        
    
    
            var marker_470230cb05f2d9e81b9a2c5adaa75c73 = L.marker(
                [48.684491, 2.375547],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_e4cad2989dadb7c556f6dc7af3175165 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_470230cb05f2d9e81b9a2c5adaa75c73.setIcon(icon_e4cad2989dadb7c556f6dc7af3175165);
        
    
        var popup_28eb9fc3470f29d6a7afbc90625ae05d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_5c3b75a856b2143568e74ea4b9ddfeee = $(`&lt;div id=&quot;html_5c3b75a856b2143568e74ea4b9ddfeee&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ESR JUVISY&lt;br&gt;6 avenue de la cour de france&lt;br&gt;juvisy / orge&lt;br&gt;Nombre de candidats:108&lt;/div&gt;`)[0];
            popup_28eb9fc3470f29d6a7afbc90625ae05d.setContent(html_5c3b75a856b2143568e74ea4b9ddfeee);
        

        marker_470230cb05f2d9e81b9a2c5adaa75c73.bindPopup(popup_28eb9fc3470f29d6a7afbc90625ae05d)
        ;

        
    
    
            var marker_58cbab12fd0ace6c50d3b02351f3502f = L.marker(
                [48.688352, 2.381731],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_95e2487063e544a4d08c5b8c98fb4462 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_58cbab12fd0ace6c50d3b02351f3502f.setIcon(icon_95e2487063e544a4d08c5b8c98fb4462);
        
    
        var popup_4f55d04684c948d456e0c1912547f217 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2e8425fa5fb5577a296b6ed42fbed3a9 = $(`&lt;div id=&quot;html_2e8425fa5fb5577a296b6ed42fbed3a9&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;JUVISY CONDUITE&lt;br&gt;19  rue pierre semard&lt;br&gt;juvisy sur orge&lt;br&gt;Nombre de candidats:30&lt;/div&gt;`)[0];
            popup_4f55d04684c948d456e0c1912547f217.setContent(html_2e8425fa5fb5577a296b6ed42fbed3a9);
        

        marker_58cbab12fd0ace6c50d3b02351f3502f.bindPopup(popup_4f55d04684c948d456e0c1912547f217)
        ;

        
    
    
            var marker_320a6556dec18cb8453fd0276eb838c3 = L.marker(
                [48.690856, 2.378005],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_7539abb9ae21da0f716a07d0572741c9 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_320a6556dec18cb8453fd0276eb838c3.setIcon(icon_7539abb9ae21da0f716a07d0572741c9);
        
    
        var popup_b329a9afa803273022d92085d6bf7da2 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d03fe31920b17898e86ea12a4cb45e0c = $(`&lt;div id=&quot;html_d03fe31920b17898e86ea12a4cb45e0c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;JUVISY TREMPLIN&lt;br&gt;38 rue victor hugo&lt;br&gt;juvisy-sur-orge&lt;br&gt;Nombre de candidats:184&lt;/div&gt;`)[0];
            popup_b329a9afa803273022d92085d6bf7da2.setContent(html_d03fe31920b17898e86ea12a4cb45e0c);
        

        marker_320a6556dec18cb8453fd0276eb838c3.bindPopup(popup_b329a9afa803273022d92085d6bf7da2)
        ;

        
    
    
            var marker_aeefc7eeed64486821cbba0ed95d1a81 = L.marker(
                [48.691081, 2.379364],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_fe61b1214485230dbe4428426bf48fe7 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_aeefc7eeed64486821cbba0ed95d1a81.setIcon(icon_fe61b1214485230dbe4428426bf48fe7);
        
    
        var popup_32354ff8eefb19c70efef00dc29d4b6e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d1bad36fa304264cbfd3bbe4a4d527f9 = $(`&lt;div id=&quot;html_d1bad36fa304264cbfd3bbe4a4d527f9&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ROMEO AUTO ECOLE&lt;br&gt;13 avenue d&#x27;estienne d&#x27;orves&lt;br&gt;juvisy&lt;br&gt;Nombre de candidats:157&lt;/div&gt;`)[0];
            popup_32354ff8eefb19c70efef00dc29d4b6e.setContent(html_d1bad36fa304264cbfd3bbe4a4d527f9);
        

        marker_aeefc7eeed64486821cbba0ed95d1a81.bindPopup(popup_32354ff8eefb19c70efef00dc29d4b6e)
        ;

        
    
    
            var marker_2b91280d409f42962e8d6ce57031c6bf = L.marker(
                [48.687505, 2.38453],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_052f397c0e4f566696c882b63e2f7f4b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_2b91280d409f42962e8d6ce57031c6bf.setIcon(icon_052f397c0e4f566696c882b63e2f7f4b);
        
    
        var popup_58d2b17d8ed393ffb063e1ae89671003 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_6d06f3919f363331cd5f6fe80fb18940 = $(`&lt;div id=&quot;html_6d06f3919f363331cd5f6fe80fb18940&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;SABRINA JUVISY&lt;br&gt;30 rue montessuy&lt;br&gt;juvisy / orge&lt;br&gt;Nombre de candidats:243&lt;/div&gt;`)[0];
            popup_58d2b17d8ed393ffb063e1ae89671003.setContent(html_6d06f3919f363331cd5f6fe80fb18940);
        

        marker_2b91280d409f42962e8d6ce57031c6bf.bindPopup(popup_58d2b17d8ed393ffb063e1ae89671003)
        ;

        
    
    
            var marker_ab009bff2074d5bb1b536d8df223a042 = L.marker(
                [48.70449, 2.436046],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_d798298b238230905fc1517fd9c528d7 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_ab009bff2074d5bb1b536d8df223a042.setIcon(icon_d798298b238230905fc1517fd9c528d7);
        
    
        var popup_b8baed95cddc3d1b7f7e3a55dc1301b3 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1e07626ff10ce94b57e16fa06bc239ff = $(`&lt;div id=&quot;html_1e07626ff10ce94b57e16fa06bc239ff&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;AVM CONDUITE&lt;br&gt;212 rue henri barbusse&lt;br&gt;vigneux sur seine&lt;br&gt;Nombre de candidats:231&lt;/div&gt;`)[0];
            popup_b8baed95cddc3d1b7f7e3a55dc1301b3.setContent(html_1e07626ff10ce94b57e16fa06bc239ff);
        

        marker_ab009bff2074d5bb1b536d8df223a042.bindPopup(popup_b8baed95cddc3d1b7f7e3a55dc1301b3)
        ;

        
    
    
            var marker_ba3ebb095b89d30991ede9806cc2d426 = L.marker(
                [48.707778, 2.413924],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_3bb929b0354c4a8ad8bd3ffbfeb24200 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_ba3ebb095b89d30991ede9806cc2d426.setIcon(icon_3bb929b0354c4a8ad8bd3ffbfeb24200);
        
    
        var popup_512e901f2c013aa80347d3cc0e99c61d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_3a68190b3dce38161f7ba416df9d4f34 = $(`&lt;div id=&quot;html_3a68190b3dce38161f7ba416df9d4f34&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DE LA GARE VIGNEUX&lt;br&gt;2 place du president robert lakota&lt;br&gt;vigneux sur seine&lt;br&gt;Nombre de candidats:130&lt;/div&gt;`)[0];
            popup_512e901f2c013aa80347d3cc0e99c61d.setContent(html_3a68190b3dce38161f7ba416df9d4f34);
        

        marker_ba3ebb095b89d30991ede9806cc2d426.bindPopup(popup_512e901f2c013aa80347d3cc0e99c61d)
        ;

        
    
    
            var marker_571f3fb497cad7524e2f4142bc43193c = L.marker(
                [48.708944, 2.431987],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_394f9b9e9ed09691510c74760a9f75ce = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_571f3fb497cad7524e2f4142bc43193c.setIcon(icon_394f9b9e9ed09691510c74760a9f75ce);
        
    
        var popup_bb5718b88d5aaae75239296529c55a28 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_cf8a98a789dd1abba16a2c43b131a0ee = $(`&lt;div id=&quot;html_cf8a98a789dd1abba16a2c43b131a0ee&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ECF PRO CONDUITE&lt;br&gt;5 place max dormoy&lt;br&gt;vigneux sur seine&lt;br&gt;Nombre de candidats:130&lt;/div&gt;`)[0];
            popup_bb5718b88d5aaae75239296529c55a28.setContent(html_cf8a98a789dd1abba16a2c43b131a0ee);
        

        marker_571f3fb497cad7524e2f4142bc43193c.bindPopup(popup_bb5718b88d5aaae75239296529c55a28)
        ;

        
    
    
            var marker_c0be26a1831b3d712e18ff01f873c254 = L.marker(
                [48.697674, 2.431193],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_74722ca6d23865e494917f782e04f9f4 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_c0be26a1831b3d712e18ff01f873c254.setIcon(icon_74722ca6d23865e494917f782e04f9f4);
        
    
        var popup_b025596f738b9f9db15c4df4707bd6c7 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_70eab4a28679163c000b5e83dd6b006f = $(`&lt;div id=&quot;html_70eab4a28679163c000b5e83dd6b006f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;VIGNEUX.NET AUTO ECOLE&lt;br&gt;79  rue gabriel peri&lt;br&gt;vigneux sur seine&lt;br&gt;Nombre de candidats:142&lt;/div&gt;`)[0];
            popup_b025596f738b9f9db15c4df4707bd6c7.setContent(html_70eab4a28679163c000b5e83dd6b006f);
        

        marker_c0be26a1831b3d712e18ff01f873c254.bindPopup(popup_b025596f738b9f9db15c4df4707bd6c7)
        ;

        
    
    
            var marker_9a11ed1af9a398381b784e03e2cf6489 = L.marker(
                [48.614759, 2.506969],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_2064f43125cd1838415d37d034f2e516 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_9a11ed1af9a398381b784e03e2cf6489.setIcon(icon_2064f43125cd1838415d37d034f2e516);
        
    
        var popup_7372e353d8c50f94c51ec89f62ef0956 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_62dc82ca99f0791afd5012f7c64eae51 = $(`&lt;div id=&quot;html_62dc82ca99f0791afd5012f7c64eae51&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ST PIERRE CONDUITE&lt;br&gt;12  rue du commerce&lt;br&gt;saint pierre du perray&lt;br&gt;Nombre de candidats:111&lt;/div&gt;`)[0];
            popup_7372e353d8c50f94c51ec89f62ef0956.setContent(html_62dc82ca99f0791afd5012f7c64eae51);
        

        marker_9a11ed1af9a398381b784e03e2cf6489.bindPopup(popup_7372e353d8c50f94c51ec89f62ef0956)
        ;

        
    
    
            var marker_ff8f6ea3b734e0bf19e22cd3dff13089 = L.marker(
                [48.587253, 2.247824],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_807511251af47fa0b5e2e1d0574e9188 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_ff8f6ea3b734e0bf19e22cd3dff13089.setIcon(icon_807511251af47fa0b5e2e1d0574e9188);
        
    
        var popup_5d2293a7b17537236239f09090ef27e9 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_0218dd1b8c90443497458435aa9972a3 = $(`&lt;div id=&quot;html_0218dd1b8c90443497458435aa9972a3&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ARPAJON AUTO ECOLE&lt;br&gt;9 rue abel cornaton&lt;br&gt;arpajon&lt;br&gt;Nombre de candidats:282&lt;/div&gt;`)[0];
            popup_5d2293a7b17537236239f09090ef27e9.setContent(html_0218dd1b8c90443497458435aa9972a3);
        

        marker_ff8f6ea3b734e0bf19e22cd3dff13089.bindPopup(popup_5d2293a7b17537236239f09090ef27e9)
        ;

        
    
    
            var marker_f9272522e48c6713655f40e093a8f45e = L.marker(
                [48.586476, 2.24338],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_2e6fe3b8b0721a1ca515678ffa90a1ae = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_f9272522e48c6713655f40e093a8f45e.setIcon(icon_2e6fe3b8b0721a1ca515678ffa90a1ae);
        
    
        var popup_b7a942a0e01de6b60860e60bceec375c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_281058440f813cda67de2d6853279ebb = $(`&lt;div id=&quot;html_281058440f813cda67de2d6853279ebb&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DE LA GARE ARPAJON&lt;br&gt;21 av aristide briand&lt;br&gt;arpajon&lt;br&gt;Nombre de candidats:126&lt;/div&gt;`)[0];
            popup_b7a942a0e01de6b60860e60bceec375c.setContent(html_281058440f813cda67de2d6853279ebb);
        

        marker_f9272522e48c6713655f40e093a8f45e.bindPopup(popup_b7a942a0e01de6b60860e60bceec375c)
        ;

        
    
    
            var marker_2f7036df818aeefcabf345169c8ae292 = L.marker(
                [48.596161, 2.246298],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_974d09e5d05aa44c57f4cc09338650ce = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_2f7036df818aeefcabf345169c8ae292.setIcon(icon_974d09e5d05aa44c57f4cc09338650ce);
        
    
        var popup_14aeb728a6e86eed23edb9fcba6c0e57 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_156652caccf39a80ed21a0a7a2c87116 = $(`&lt;div id=&quot;html_156652caccf39a80ed21a0a7a2c87116&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ECF CAMPUS 91&lt;br&gt;19 avenue de la division leclerc&lt;br&gt;arpajon&lt;br&gt;Nombre de candidats:100&lt;/div&gt;`)[0];
            popup_14aeb728a6e86eed23edb9fcba6c0e57.setContent(html_156652caccf39a80ed21a0a7a2c87116);
        

        marker_2f7036df818aeefcabf345169c8ae292.bindPopup(popup_14aeb728a6e86eed23edb9fcba6c0e57)
        ;

        
    
    
            var marker_5be2f6e09993edf88d3719c5ff779a9c = L.marker(
                [48.588249, 2.250753],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_cdf75e4f87fe5e09b63524f1d52a9baa = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_5be2f6e09993edf88d3719c5ff779a9c.setIcon(icon_cdf75e4f87fe5e09b63524f1d52a9baa);
        
    
        var popup_637731db0a5d87c7969a4396d64951eb = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1b8c66fa034ca3f00e1b0c726f17de1d = $(`&lt;div id=&quot;html_1b8c66fa034ca3f00e1b0c726f17de1d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MC ARPAJON AUTO ECOLE&lt;br&gt;1  rue gambetta&lt;br&gt;arpajon&lt;br&gt;Nombre de candidats:59&lt;/div&gt;`)[0];
            popup_637731db0a5d87c7969a4396d64951eb.setContent(html_1b8c66fa034ca3f00e1b0c726f17de1d);
        

        marker_5be2f6e09993edf88d3719c5ff779a9c.bindPopup(popup_637731db0a5d87c7969a4396d64951eb)
        ;

        
    
    
            var marker_20c8f612dcd52c755ade34fd4a33fc56 = L.marker(
                [48.590891, 2.247956],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_f81a4e08eb72f2d08d3f8f0f41d7525e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_20c8f612dcd52c755ade34fd4a33fc56.setIcon(icon_f81a4e08eb72f2d08d3f8f0f41d7525e);
        
    
        var popup_291b1b8eb8a991a810299f86bf6fdb5f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_258812a147f85b8b03605291fa75fd98 = $(`&lt;div id=&quot;html_258812a147f85b8b03605291fa75fd98&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;PERMIS ZEN AUTO ECOLE&lt;br&gt;56 grande rue&lt;br&gt;arpajon&lt;br&gt;Nombre de candidats:79&lt;/div&gt;`)[0];
            popup_291b1b8eb8a991a810299f86bf6fdb5f.setContent(html_258812a147f85b8b03605291fa75fd98);
        

        marker_20c8f612dcd52c755ade34fd4a33fc56.bindPopup(popup_291b1b8eb8a991a810299f86bf6fdb5f)
        ;

        
    
    
            var marker_48ebe39337a76115c0815382aa6f88cc = L.marker(
                [48.588543, 2.249026],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_f035aaa4d54ca9c9f7035a76d04e8bb1 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_48ebe39337a76115c0815382aa6f88cc.setIcon(icon_f035aaa4d54ca9c9f7035a76d04e8bb1);
        
    
        var popup_cfeb61ad170e25154c0df1c9aaea0f94 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_0530fb23f28f014d2e5f69cd5534820a = $(`&lt;div id=&quot;html_0530fb23f28f014d2e5f69cd5534820a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;RASPAIL&lt;br&gt;6 rue raspail&lt;br&gt;arpajon&lt;br&gt;Nombre de candidats:246&lt;/div&gt;`)[0];
            popup_cfeb61ad170e25154c0df1c9aaea0f94.setContent(html_0530fb23f28f014d2e5f69cd5534820a);
        

        marker_48ebe39337a76115c0815382aa6f88cc.bindPopup(popup_cfeb61ad170e25154c0df1c9aaea0f94)
        ;

        
    
    
            var marker_a40eb74e063b747f49c206655f533e35 = L.marker(
                [48.727481, 2.255914],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_9a16791054406c20293cb71f8df6fee0 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_a40eb74e063b747f49c206655f533e35.setIcon(icon_9a16791054406c20293cb71f8df6fee0);
        
    
        var popup_b98c32a4978838cd91999b3055b146c3 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_968cbdb8ea796041ffa6b2f7fc6fdf12 = $(`&lt;div id=&quot;html_968cbdb8ea796041ffa6b2f7fc6fdf12&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;AAC 3000&lt;br&gt;zac de vilmorin&lt;br&gt;massy&lt;br&gt;Nombre de candidats:119&lt;/div&gt;`)[0];
            popup_b98c32a4978838cd91999b3055b146c3.setContent(html_968cbdb8ea796041ffa6b2f7fc6fdf12);
        

        marker_a40eb74e063b747f49c206655f533e35.bindPopup(popup_b98c32a4978838cd91999b3055b146c3)
        ;

        
    
    
            var marker_22b31a408c4018e51e7de4a3da6febe2 = L.marker(
                [48.724608, 2.260649],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_7f4b74d93893e3fca1bf71119f81684c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_22b31a408c4018e51e7de4a3da6febe2.setIcon(icon_7f4b74d93893e3fca1bf71119f81684c);
        
    
        var popup_13197f2cb5acd732cd9de430d46c63c7 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1efce409c6fa6f20457dea8cddcda70f = $(`&lt;div id=&quot;html_1efce409c6fa6f20457dea8cddcda70f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ATLANTIS&lt;br&gt;39 avenue carnot&lt;br&gt;massy&lt;br&gt;Nombre de candidats:233&lt;/div&gt;`)[0];
            popup_13197f2cb5acd732cd9de430d46c63c7.setContent(html_1efce409c6fa6f20457dea8cddcda70f);
        

        marker_22b31a408c4018e51e7de4a3da6febe2.bindPopup(popup_13197f2cb5acd732cd9de430d46c63c7)
        ;

        
    
    
            var marker_c39ef0cb571d86fbcc1f1bca0d75b4ab = L.marker(
                [48.722524, 2.262371],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_73eeb572d93c380c8d389b4feb63b668 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_c39ef0cb571d86fbcc1f1bca0d75b4ab.setIcon(icon_73eeb572d93c380c8d389b4feb63b668);
        
    
        var popup_d148c4f31942465e09a2efa6c8c0a109 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_95a6ed442428c246c9bb9253d67fd42e = $(`&lt;div id=&quot;html_95a6ed442428c246c9bb9253d67fd42e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DRIVER ACADEMY&lt;br&gt;135 av de paris&lt;br&gt;massy&lt;br&gt;Nombre de candidats:67&lt;/div&gt;`)[0];
            popup_d148c4f31942465e09a2efa6c8c0a109.setContent(html_95a6ed442428c246c9bb9253d67fd42e);
        

        marker_c39ef0cb571d86fbcc1f1bca0d75b4ab.bindPopup(popup_d148c4f31942465e09a2efa6c8c0a109)
        ;

        
    
    
            var marker_02101131caeef4edf22338a6967ba635 = L.marker(
                [48.731966, 2.288707],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_d3aca16bf445e1091a5044da4f6750cf = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_02101131caeef4edf22338a6967ba635.setIcon(icon_d3aca16bf445e1091a5044da4f6750cf);
        
    
        var popup_3f21ec5ea2390a088e3d97aac668ac83 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_798214b821f90dadaff06bfdb5c672ab = $(`&lt;div id=&quot;html_798214b821f90dadaff06bfdb5c672ab&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MAURICE&lt;br&gt;19 place de france&lt;br&gt;massy&lt;br&gt;Nombre de candidats:193&lt;/div&gt;`)[0];
            popup_3f21ec5ea2390a088e3d97aac668ac83.setContent(html_798214b821f90dadaff06bfdb5c672ab);
        

        marker_02101131caeef4edf22338a6967ba635.bindPopup(popup_3f21ec5ea2390a088e3d97aac668ac83)
        ;

        
    
    
            var marker_ba99ed234492033ad2b0105744111c28 = L.marker(
                [48.730099, 2.274256],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_7b0e93c919d870e9b578183bceebf057 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_ba99ed234492033ad2b0105744111c28.setIcon(icon_7b0e93c919d870e9b578183bceebf057);
        
    
        var popup_6ff95e8c04fb5d7b192e32c01cb10da6 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ea19bff1899ede07cc9719a630a5355a = $(`&lt;div id=&quot;html_ea19bff1899ede07cc9719a630a5355a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MN AUTOCOLE&lt;br&gt;17-19 rue de la division leclerc&lt;br&gt;massy&lt;br&gt;Nombre de candidats:45&lt;/div&gt;`)[0];
            popup_6ff95e8c04fb5d7b192e32c01cb10da6.setContent(html_ea19bff1899ede07cc9719a630a5355a);
        

        marker_ba99ed234492033ad2b0105744111c28.bindPopup(popup_6ff95e8c04fb5d7b192e32c01cb10da6)
        ;

        
    
    
            var marker_d4546c90e434cd790c8a9ed33bc4e0cd = L.marker(
                [48.723752, 2.259577],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_7afe7b178adb0cc8acd5d2499fe8ef01 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_d4546c90e434cd790c8a9ed33bc4e0cd.setIcon(icon_7afe7b178adb0cc8acd5d2499fe8ef01);
        
    
        var popup_bf655e91cc14a60e634b4cfb86a52391 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_35ccaadcc5b3b4357ba12a44f10a8322 = $(`&lt;div id=&quot;html_35ccaadcc5b3b4357ba12a44f10a8322&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;POINT CONDUITE MASSY&lt;br&gt;49 avenue carnot&lt;br&gt;massy&lt;br&gt;Nombre de candidats:214&lt;/div&gt;`)[0];
            popup_bf655e91cc14a60e634b4cfb86a52391.setContent(html_35ccaadcc5b3b4357ba12a44f10a8322);
        

        marker_d4546c90e434cd790c8a9ed33bc4e0cd.bindPopup(popup_bf655e91cc14a60e634b4cfb86a52391)
        ;

        
    
    
            var marker_66f0f7ed3735e47fde4ac9703f9f2bf7 = L.marker(
                [48.63404, 2.267106],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_3b62b4d799e87d1c3fc944950f7f4832 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_66f0f7ed3735e47fde4ac9703f9f2bf7.setIcon(icon_3b62b4d799e87d1c3fc944950f7f4832);
        
    
        var popup_9e643b1ec31f925ee92ce28c615f4c9d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_05acf049d348cd1ac51eb8a87c6e452c = $(`&lt;div id=&quot;html_05acf049d348cd1ac51eb8a87c6e452c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;137 LINAS&lt;br&gt;29 rue de la division leclerc&lt;br&gt;linas&lt;br&gt;Nombre de candidats:41&lt;/div&gt;`)[0];
            popup_9e643b1ec31f925ee92ce28c615f4c9d.setContent(html_05acf049d348cd1ac51eb8a87c6e452c);
        

        marker_66f0f7ed3735e47fde4ac9703f9f2bf7.bindPopup(popup_9e643b1ec31f925ee92ce28c615f4c9d)
        ;

        
    
    
            var marker_ab3437f0efc0ce411d72533884dd7476 = L.marker(
                [48.640017, 2.271025],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_bfb41900f19ff627689c9bb0af873bfe = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_ab3437f0efc0ce411d72533884dd7476.setIcon(icon_bfb41900f19ff627689c9bb0af873bfe);
        
    
        var popup_7e1af51f2a77716af31d839b973d65f8 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_da87419638e77166164a6e87a4ffd5c1 = $(`&lt;div id=&quot;html_da87419638e77166164a6e87a4ffd5c1&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;LINAS MONTLHERY AUTO ECOLE&lt;br&gt;1 rue bordet&lt;br&gt;montlhery&lt;br&gt;Nombre de candidats:150&lt;/div&gt;`)[0];
            popup_7e1af51f2a77716af31d839b973d65f8.setContent(html_da87419638e77166164a6e87a4ffd5c1);
        

        marker_ab3437f0efc0ce411d72533884dd7476.bindPopup(popup_7e1af51f2a77716af31d839b973d65f8)
        ;

        
    
    
            var marker_86227d0ce14b11f1665d6a02603e0e92 = L.marker(
                [48.652483, 2.275104],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_10a3e4f012e53e3bdac555b4a46b399f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_86227d0ce14b11f1665d6a02603e0e92.setIcon(icon_10a3e4f012e53e3bdac555b4a46b399f);
        
    
        var popup_89db60d57b25bb27944b38e6166a65de = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c5c3d30318c4e8539e9cc025d2cc55e7 = $(`&lt;div id=&quot;html_c5c3d30318c4e8539e9cc025d2cc55e7&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;LONGPONT CONDUITE&lt;br&gt;30 voie du mort ru&lt;br&gt;longpont / orge&lt;br&gt;Nombre de candidats:85&lt;/div&gt;`)[0];
            popup_89db60d57b25bb27944b38e6166a65de.setContent(html_c5c3d30318c4e8539e9cc025d2cc55e7);
        

        marker_86227d0ce14b11f1665d6a02603e0e92.bindPopup(popup_89db60d57b25bb27944b38e6166a65de)
        ;

        
    
    
            var marker_66606933268201579dc5ef27ed38adae = L.marker(
                [48.638611, 2.270781],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_e8840d08602aad8d317e6731b4337208 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_66606933268201579dc5ef27ed38adae.setIcon(icon_e8840d08602aad8d317e6731b4337208);
        
    
        var popup_98ed6f1ff3bc092abae302a9131dd0c7 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a833dc002a63572d38f50f5c118d49a9 = $(`&lt;div id=&quot;html_a833dc002a63572d38f50f5c118d49a9&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MC MONTLHERY&lt;br&gt;1 rue bordet  place du marche&lt;br&gt;montlhery&lt;br&gt;Nombre de candidats:25&lt;/div&gt;`)[0];
            popup_98ed6f1ff3bc092abae302a9131dd0c7.setContent(html_a833dc002a63572d38f50f5c118d49a9);
        

        marker_66606933268201579dc5ef27ed38adae.bindPopup(popup_98ed6f1ff3bc092abae302a9131dd0c7)
        ;

        
    
    
            var marker_d5b6ed653060135c6da44d895ec8cd90 = L.marker(
                [48.640325, 2.269043],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_2c68549662b083b53c7400802f63272b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_d5b6ed653060135c6da44d895ec8cd90.setIcon(icon_2c68549662b083b53c7400802f63272b);
        
    
        var popup_53785d8cbf2d72355e84a46c7d1d0329 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_0815e9e6612ae1f76aa4c1e448858404 = $(`&lt;div id=&quot;html_0815e9e6612ae1f76aa4c1e448858404&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MONTHLERY CONDUITE&lt;br&gt;16 rue du maille&lt;br&gt;montlhery&lt;br&gt;Nombre de candidats:135&lt;/div&gt;`)[0];
            popup_53785d8cbf2d72355e84a46c7d1d0329.setContent(html_0815e9e6612ae1f76aa4c1e448858404);
        

        marker_d5b6ed653060135c6da44d895ec8cd90.bindPopup(popup_53785d8cbf2d72355e84a46c7d1d0329)
        ;

        
    
    
            var marker_bff26806f745360d8358a21b4bdc6614 = L.marker(
                [48.645729, 2.26977],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_6bca88d7ef78d04f59ae9e6426f4e4fb = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_bff26806f745360d8358a21b4bdc6614.setIcon(icon_6bca88d7ef78d04f59ae9e6426f4e4fb);
        
    
        var popup_c75959b1bea0f44a0b6f7729fafa989e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_46595db8b9ae4eb21f380778ece0d084 = $(`&lt;div id=&quot;html_46595db8b9ae4eb21f380778ece0d084&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MOTO TEAM 91&lt;br&gt;73 rn20 route d&#x27;orleans&lt;br&gt;montlhery&lt;br&gt;Nombre de candidats:72&lt;/div&gt;`)[0];
            popup_c75959b1bea0f44a0b6f7729fafa989e.setContent(html_46595db8b9ae4eb21f380778ece0d084);
        

        marker_bff26806f745360d8358a21b4bdc6614.bindPopup(popup_c75959b1bea0f44a0b6f7729fafa989e)
        ;

        
    
    
            var marker_5dbff22667375113b2c97fcaea646765 = L.marker(
                [48.738048, 2.323574],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_1c652d042677554fa4d088caac22c6c8 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_5dbff22667375113b2c97fcaea646765.setIcon(icon_1c652d042677554fa4d088caac22c6c8);
        
    
        var popup_17b6775578dd6d16fbfb44d48f5356d0 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_0f3e13d5fdfbfda41fb040892c84d73e = $(`&lt;div id=&quot;html_0f3e13d5fdfbfda41fb040892c84d73e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;WISSOUS CONDUITE&lt;br&gt;37 avenue des ecoles&lt;br&gt;wissous&lt;br&gt;Nombre de candidats:130&lt;/div&gt;`)[0];
            popup_17b6775578dd6d16fbfb44d48f5356d0.setContent(html_0f3e13d5fdfbfda41fb040892c84d73e);
        

        marker_5dbff22667375113b2c97fcaea646765.bindPopup(popup_17b6775578dd6d16fbfb44d48f5356d0)
        ;

        
    
    
            var marker_ea0fd2ed4ae8c770dd9f50468922e5f9 = L.marker(
                [48.719687, 2.498175],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_105c5853d7ad269a98653d16e6e43a17 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_ea0fd2ed4ae8c770dd9f50468922e5f9.setIcon(icon_105c5853d7ad269a98653d16e6e43a17);
        
    
        var popup_e7ba69701a994e87492f230032cbfd68 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9a1afa4e2e4a52bc284f247bcec6acea = $(`&lt;div id=&quot;html_9a1afa4e2e4a52bc284f247bcec6acea&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CITIZEN CONDUITE&lt;br&gt;rue gustave caillebote&lt;br&gt;yerres&lt;br&gt;Nombre de candidats:179&lt;/div&gt;`)[0];
            popup_e7ba69701a994e87492f230032cbfd68.setContent(html_9a1afa4e2e4a52bc284f247bcec6acea);
        

        marker_ea0fd2ed4ae8c770dd9f50468922e5f9.bindPopup(popup_e7ba69701a994e87492f230032cbfd68)
        ;

        
    
    
            var marker_2aaf192bba5312363ec04aeacdb0bf37 = L.marker(
                [48.71416, 2.478825],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_3e758002b2df3786d27f92bfc66f4d8c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_2aaf192bba5312363ec04aeacdb0bf37.setIcon(icon_3e758002b2df3786d27f92bfc66f4d8c);
        
    
        var popup_b2a53f1eec82737ee7ea211c79fc9540 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_dff139b5214d5c4560cad4184a71c5db = $(`&lt;div id=&quot;html_dff139b5214d5c4560cad4184a71c5db&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ECF YERRES&lt;br&gt;2 rue  pierre de coubertin&lt;br&gt;yerres&lt;br&gt;Nombre de candidats:169&lt;/div&gt;`)[0];
            popup_b2a53f1eec82737ee7ea211c79fc9540.setContent(html_dff139b5214d5c4560cad4184a71c5db);
        

        marker_2aaf192bba5312363ec04aeacdb0bf37.bindPopup(popup_b2a53f1eec82737ee7ea211c79fc9540)
        ;

        
    
    
            var marker_5b1b1d979390e8988b4d66876541b7ab = L.marker(
                [48.705622, 2.488089],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_9620b6736502c018b94ca377fd7eb26c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_5b1b1d979390e8988b4d66876541b7ab.setIcon(icon_9620b6736502c018b94ca377fd7eb26c);
        
    
        var popup_a656904d5736e6b4468938033647c6be = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_bb99858c3a65488b0abe3dd7565c25d7 = $(`&lt;div id=&quot;html_bb99858c3a65488b0abe3dd7565c25d7&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;PERMIS SWIFT&lt;br&gt;81 rue gabriel peri&lt;br&gt;yerres&lt;br&gt;Nombre de candidats:97&lt;/div&gt;`)[0];
            popup_a656904d5736e6b4468938033647c6be.setContent(html_bb99858c3a65488b0abe3dd7565c25d7);
        

        marker_5b1b1d979390e8988b4d66876541b7ab.bindPopup(popup_a656904d5736e6b4468938033647c6be)
        ;

        
    
    
            var marker_29ad90392ff3d2c30067b57235c84738 = L.marker(
                [48.655744, 2.385463],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_a513fafcf43f9ee7e3c9a498e08d2030 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_29ad90392ff3d2c30067b57235c84738.setIcon(icon_a513fafcf43f9ee7e3c9a498e08d2030);
        
    
        var popup_5d8a7132f44e7a347285b0fc71f9430c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_84ed2e59541909494157b6d892ebce32 = $(`&lt;div id=&quot;html_84ed2e59541909494157b6d892ebce32&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;BIL&#x27;S CONDUITE&lt;br&gt;40 route de corbeil&lt;br&gt;grigny&lt;br&gt;Nombre de candidats:152&lt;/div&gt;`)[0];
            popup_5d8a7132f44e7a347285b0fc71f9430c.setContent(html_84ed2e59541909494157b6d892ebce32);
        

        marker_29ad90392ff3d2c30067b57235c84738.bindPopup(popup_5d8a7132f44e7a347285b0fc71f9430c)
        ;

        
    
    
            var marker_9314d28477107d7f8ff06a84fa7e75e0 = L.marker(
                [48.656921, 2.387862],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_95fb52be14045605c1bbbf63e910c554 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_9314d28477107d7f8ff06a84fa7e75e0.setIcon(icon_95fb52be14045605c1bbbf63e910c554);
        
    
        var popup_7cd51c2455df0425046763e2845a7158 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c4856f60d6a6e3788a330894e2dde0ac = $(`&lt;div id=&quot;html_c4856f60d6a6e3788a330894e2dde0ac&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;GRIGNY PERMIS ZEN AUTO ECOLE&lt;br&gt;44 rue pierre brossolette&lt;br&gt;grigny&lt;br&gt;Nombre de candidats:61&lt;/div&gt;`)[0];
            popup_7cd51c2455df0425046763e2845a7158.setContent(html_c4856f60d6a6e3788a330894e2dde0ac);
        

        marker_9314d28477107d7f8ff06a84fa7e75e0.bindPopup(popup_7cd51c2455df0425046763e2845a7158)
        ;

        
    
    
            var marker_d92a198edf7d0b3db901392e127a2188 = L.marker(
                [48.651954, 2.393119],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_316ff1137cfdf97f315af7d6d34de87e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_d92a198edf7d0b3db901392e127a2188.setIcon(icon_316ff1137cfdf97f315af7d6d34de87e);
        
    
        var popup_cb23ce96079ef683b9e114a18f0e05d5 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_96638c42dcdea583c5834b6a4d2e392a = $(`&lt;div id=&quot;html_96638c42dcdea583c5834b6a4d2e392a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;JEAN LUC MAURIN&lt;br&gt;02 place henri barbusse&lt;br&gt;grigny&lt;br&gt;Nombre de candidats:192&lt;/div&gt;`)[0];
            popup_cb23ce96079ef683b9e114a18f0e05d5.setContent(html_96638c42dcdea583c5834b6a4d2e392a);
        

        marker_d92a198edf7d0b3db901392e127a2188.bindPopup(popup_cb23ce96079ef683b9e114a18f0e05d5)
        ;

        
    
    
            var marker_b53d7c9d4ed3b1cea121c4d9e97cf206 = L.marker(
                [48.670492, 2.332371],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_af35182e2861eea1155fc83d6986f9f8 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_b53d7c9d4ed3b1cea121c4d9e97cf206.setIcon(icon_af35182e2861eea1155fc83d6986f9f8);
        
    
        var popup_107af1202b29aede33c5f8f4d20a7948 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d4154e0b9a34db4df776433d8e452b1b = $(`&lt;div id=&quot;html_d4154e0b9a34db4df776433d8e452b1b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;EC EPINAY&lt;br&gt;35 rue de corbeil&lt;br&gt;epinay-sur-orge&lt;br&gt;Nombre de candidats:24&lt;/div&gt;`)[0];
            popup_107af1202b29aede33c5f8f4d20a7948.setContent(html_d4154e0b9a34db4df776433d8e452b1b);
        

        marker_b53d7c9d4ed3b1cea121c4d9e97cf206.bindPopup(popup_107af1202b29aede33c5f8f4d20a7948)
        ;

        
    
    
            var marker_33aacb19e1b2f27648a1e7dcd2de0e38 = L.marker(
                [48.670492, 2.332371],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_1915dc6492e1c5250ed2680d8802dc10 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_33aacb19e1b2f27648a1e7dcd2de0e38.setIcon(icon_1915dc6492e1c5250ed2680d8802dc10);
        
    
        var popup_a76dfec7d31079a026dc1a18352dfdf1 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_f50a68abe8374311b51009967744ae85 = $(`&lt;div id=&quot;html_f50a68abe8374311b51009967744ae85&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;EPINAY&lt;br&gt;35 route de corbeil&lt;br&gt;epinay sur orge&lt;br&gt;Nombre de candidats:49&lt;/div&gt;`)[0];
            popup_a76dfec7d31079a026dc1a18352dfdf1.setContent(html_f50a68abe8374311b51009967744ae85);
        

        marker_33aacb19e1b2f27648a1e7dcd2de0e38.bindPopup(popup_a76dfec7d31079a026dc1a18352dfdf1)
        ;

        
    
    
            var marker_cd8590f2efcfd4c5d0757929b4b44dce = L.marker(
                [48.675743, 2.322972],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_18e292b6374d4df1572ec27c273c0139 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_cd8590f2efcfd4c5d0757929b4b44dce.setIcon(icon_18e292b6374d4df1572ec27c273c0139);
        
    
        var popup_fb9bd24ebfb66d00f4e25ea081ffb164 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9b96a4c26a4fc08771dc06b9da45b1d1 = $(`&lt;div id=&quot;html_9b96a4c26a4fc08771dc06b9da45b1d1&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;EPINAY TREMPLIN&lt;br&gt;76 grande rue&lt;br&gt;epinay sur orge&lt;br&gt;Nombre de candidats:38&lt;/div&gt;`)[0];
            popup_fb9bd24ebfb66d00f4e25ea081ffb164.setContent(html_9b96a4c26a4fc08771dc06b9da45b1d1);
        

        marker_cd8590f2efcfd4c5d0757929b4b44dce.bindPopup(popup_fb9bd24ebfb66d00f4e25ea081ffb164)
        ;

        
    
    
            var marker_0712e6849bccd2038b4af4301e6be79e = L.marker(
                [48.744278, 2.281287],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_b1b447757aef7f775a06a38ad4e66ea7 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_0712e6849bccd2038b4af4301e6be79e.setIcon(icon_b1b447757aef7f775a06a38ad4e66ea7);
        
    
        var popup_37771f95749baa67f045f501ce3789db = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_5213ead5e5c07ecd663baf3288e7658a = $(`&lt;div id=&quot;html_5213ead5e5c07ecd663baf3288e7658a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;NTER FORMATIONS SR&lt;br&gt;3 rue marius hue&lt;br&gt;verrières le buisson&lt;br&gt;Nombre de candidats:107&lt;/div&gt;`)[0];
            popup_37771f95749baa67f045f501ce3789db.setContent(html_5213ead5e5c07ecd663baf3288e7658a);
        

        marker_0712e6849bccd2038b4af4301e6be79e.bindPopup(popup_37771f95749baa67f045f501ce3789db)
        ;

        
    
    
            var marker_222cd0d83ad62ae1ad498b91187a6109 = L.marker(
                [48.738691, 2.267106],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_8034ae72f625e632ac2a7f6219f0676e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_222cd0d83ad62ae1ad498b91187a6109.setIcon(icon_8034ae72f625e632ac2a7f6219f0676e);
        
    
        var popup_919e1566921a315a4fd0054cac6f232d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_5626a50874450bfca4e3b95fa4c1a29c = $(`&lt;div id=&quot;html_5626a50874450bfca4e3b95fa4c1a29c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;PRELUDE AUTO MOTO ECOLE&lt;br&gt;70 av gabriel peri&lt;br&gt;verrieres le buisson&lt;br&gt;Nombre de candidats:95&lt;/div&gt;`)[0];
            popup_919e1566921a315a4fd0054cac6f232d.setContent(html_5626a50874450bfca4e3b95fa4c1a29c);
        

        marker_222cd0d83ad62ae1ad498b91187a6109.bindPopup(popup_919e1566921a315a4fd0054cac6f232d)
        ;

        
    
    
            var marker_225ab7e9bac33f59607450babadc8895 = L.marker(
                [48.747941, 2.266266],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_c2c39189be213fb58da208264512f65a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_225ab7e9bac33f59607450babadc8895.setIcon(icon_c2c39189be213fb58da208264512f65a);
        
    
        var popup_fb72781594e9fc787bcedd0bc4dd312f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2a03f0766175fea5de4970684277b471 = $(`&lt;div id=&quot;html_2a03f0766175fea5de4970684277b471&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;VERRIERES CENTRE DE CONDUITE&lt;br&gt;25 rue d estienne d orves&lt;br&gt;verrieres le buisson&lt;br&gt;Nombre de candidats:124&lt;/div&gt;`)[0];
            popup_fb72781594e9fc787bcedd0bc4dd312f.setContent(html_2a03f0766175fea5de4970684277b471);
        

        marker_225ab7e9bac33f59607450babadc8895.bindPopup(popup_fb72781594e9fc787bcedd0bc4dd312f)
        ;

        
    
    
            var marker_a047279d4a102fe926cfb931504514ac = L.marker(
                [48.702588, 2.32098],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_df9a864ceac79cd6274bb838a0b058f4 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_a047279d4a102fe926cfb931504514ac.setIcon(icon_df9a864ceac79cd6274bb838a0b058f4);
        
    
        var popup_5ca4e5e0ddfaf5a811d21b84fa3e1b35 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_50d2d0cca4894b95cbce0c31f027e8c2 = $(`&lt;div id=&quot;html_50d2d0cca4894b95cbce0c31f027e8c2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CER CHILLY - REVOLUTION PERMIS&lt;br&gt;place de la libération&lt;br&gt;chilly mazarin&lt;br&gt;Nombre de candidats:103&lt;/div&gt;`)[0];
            popup_5ca4e5e0ddfaf5a811d21b84fa3e1b35.setContent(html_50d2d0cca4894b95cbce0c31f027e8c2);
        

        marker_a047279d4a102fe926cfb931504514ac.bindPopup(popup_5ca4e5e0ddfaf5a811d21b84fa3e1b35)
        ;

        
    
    
            var marker_5575a3f272683a7aa3f1105aac747b86 = L.marker(
                [48.701166, 2.319115],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_cc5421c5853c24644c85e530813898c2 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_5575a3f272683a7aa3f1105aac747b86.setIcon(icon_cc5421c5853c24644c85e530813898c2);
        
    
        var popup_0c5a7798f7fef11ea0514efeb9b8bf48 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c8bd4fabf1213a2f444d232fd11fbd47 = $(`&lt;div id=&quot;html_c8bd4fabf1213a2f444d232fd11fbd47&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ECF CHILLY MAZARIN&lt;br&gt;11 ave pierre brossolette&lt;br&gt;chilly mazarin&lt;br&gt;Nombre de candidats:717&lt;/div&gt;`)[0];
            popup_0c5a7798f7fef11ea0514efeb9b8bf48.setContent(html_c8bd4fabf1213a2f444d232fd11fbd47);
        

        marker_5575a3f272683a7aa3f1105aac747b86.bindPopup(popup_0c5a7798f7fef11ea0514efeb9b8bf48)
        ;

        
    
    
            var marker_7a17f563da84d1f3866172c6e582c03e = L.marker(
                [48.69462, 2.309317],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_f017fb0ef7800bd76cb8cc8eac4abc46 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_7a17f563da84d1f3866172c6e582c03e.setIcon(icon_f017fb0ef7800bd76cb8cc8eac4abc46);
        
    
        var popup_f81d36e447299e999089583f23aa9444 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_41a2495581d4984c09aeb5e2290ad471 = $(`&lt;div id=&quot;html_41a2495581d4984c09aeb5e2290ad471&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MELISSA CONDUITE&lt;br&gt;73 rue de gravigny&lt;br&gt;chilly mazarin&lt;br&gt;Nombre de candidats:160&lt;/div&gt;`)[0];
            popup_f81d36e447299e999089583f23aa9444.setContent(html_41a2495581d4984c09aeb5e2290ad471);
        

        marker_7a17f563da84d1f3866172c6e582c03e.bindPopup(popup_f81d36e447299e999089583f23aa9444)
        ;

        
    
    
            var marker_cec2a54f005b32fa1941878c6aaac45d = L.marker(
                [48.658909, 2.340412],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_4de15c60cf1da5c6023172ef96a3f739 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_cec2a54f005b32fa1941878c6aaac45d.setIcon(icon_4de15c60cf1da5c6023172ef96a3f739);
        
    
        var popup_49926a08241504b192d47381e317b6cb = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d4663f7d988cf9e0846a1e242d17e405 = $(`&lt;div id=&quot;html_d4663f7d988cf9e0846a1e242d17e405&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ECIR&lt;br&gt;122 rue jean raynal&lt;br&gt;morsang sur orge&lt;br&gt;Nombre de candidats:97&lt;/div&gt;`)[0];
            popup_49926a08241504b192d47381e317b6cb.setContent(html_d4663f7d988cf9e0846a1e242d17e405);
        

        marker_cec2a54f005b32fa1941878c6aaac45d.bindPopup(popup_49926a08241504b192d47381e317b6cb)
        ;

        
    
    
            var marker_1fd6263e47dfd3e50264d5c78359acfb = L.marker(
                [48.653464, 2.357245],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_962a178b138290ab9b687f2a725fe3ec = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_1fd6263e47dfd3e50264d5c78359acfb.setIcon(icon_962a178b138290ab9b687f2a725fe3ec);
        
    
        var popup_b79f5e5a4e5ba7719779fe4e832d59d2 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7714ae9f95bcbba48b6b9fed6a30f235 = $(`&lt;div id=&quot;html_7714ae9f95bcbba48b6b9fed6a30f235&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;LIBERTY&lt;br&gt;53 voie de compiegne&lt;br&gt;morsang sur orge&lt;br&gt;Nombre de candidats:41&lt;/div&gt;`)[0];
            popup_b79f5e5a4e5ba7719779fe4e832d59d2.setContent(html_7714ae9f95bcbba48b6b9fed6a30f235);
        

        marker_1fd6263e47dfd3e50264d5c78359acfb.bindPopup(popup_b79f5e5a4e5ba7719779fe4e832d59d2)
        ;

        
    
    
            var marker_b54c205e658d8730aa0571ce77bb24d8 = L.marker(
                [48.697552, 2.183022],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_fe1e944c254bb41d56359e433e5464ec = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_b54c205e658d8730aa0571ce77bb24d8.setIcon(icon_fe1e944c254bb41d56359e433e5464ec);
        
    
        var popup_c845aa8ab63be67e1312cb5b59614e18 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_37ffd42d5ffba208443792259e0b03ea = $(`&lt;div id=&quot;html_37ffd42d5ffba208443792259e0b03ea&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DE LA GARE D ORSAY&lt;br&gt;35 boulevard dubreuil&lt;br&gt;orsay&lt;br&gt;Nombre de candidats:192&lt;/div&gt;`)[0];
            popup_c845aa8ab63be67e1312cb5b59614e18.setContent(html_37ffd42d5ffba208443792259e0b03ea);
        

        marker_b54c205e658d8730aa0571ce77bb24d8.bindPopup(popup_c845aa8ab63be67e1312cb5b59614e18)
        ;

        
    
    
            var marker_b9f13c49a45b4e99038b4fe549dee6c5 = L.marker(
                [48.702869, 2.191347],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_6e68501b9dd0a11e3c7e4f70c9f90dcf = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_b9f13c49a45b4e99038b4fe549dee6c5.setIcon(icon_6e68501b9dd0a11e3c7e4f70c9f90dcf);
        
    
        var popup_a92d684c88498ab481c4619771d36fb6 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_b2ccda0785bdf35e82500070ecb48aad = $(`&lt;div id=&quot;html_b2ccda0785bdf35e82500070ecb48aad&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DRIVING CENTER&lt;br&gt;43 rue charles de gaulle&lt;br&gt;orsay&lt;br&gt;Nombre de candidats:59&lt;/div&gt;`)[0];
            popup_a92d684c88498ab481c4619771d36fb6.setContent(html_b2ccda0785bdf35e82500070ecb48aad);
        

        marker_b9f13c49a45b4e99038b4fe549dee6c5.bindPopup(popup_a92d684c88498ab481c4619771d36fb6)
        ;

        
    
    
            var marker_652d67d7ef3f19e8cc59611d822b0239 = L.marker(
                [48.702869, 2.191347],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_65d260ec622d868d0aa3070df69040e3 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_652d67d7ef3f19e8cc59611d822b0239.setIcon(icon_65d260ec622d868d0aa3070df69040e3);
        
    
        var popup_030ed530876f119b2a87486f99065984 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7c4cde422ebf0acef0c2c419f3014b5f = $(`&lt;div id=&quot;html_7c4cde422ebf0acef0c2c419f3014b5f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DRIVING CENTER&lt;br&gt;43 rue charles de gaulle&lt;br&gt;orsay&lt;br&gt;Nombre de candidats:59&lt;/div&gt;`)[0];
            popup_030ed530876f119b2a87486f99065984.setContent(html_7c4cde422ebf0acef0c2c419f3014b5f);
        

        marker_652d67d7ef3f19e8cc59611d822b0239.bindPopup(popup_030ed530876f119b2a87486f99065984)
        ;

        
    
    
            var marker_aaaf96e7f8279c42e5a711f2612e7783 = L.marker(
                [48.702869, 2.191347],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_84f291be4c6c513bc19f38c8744bb49a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_aaaf96e7f8279c42e5a711f2612e7783.setIcon(icon_84f291be4c6c513bc19f38c8744bb49a);
        
    
        var popup_a561375858a8c3a106fd8779ffc78aab = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c37dfd41eb5e3227b3b4632fb9856d9d = $(`&lt;div id=&quot;html_c37dfd41eb5e3227b3b4632fb9856d9d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MOULIN&lt;br&gt;43 rue charles de gaulle&lt;br&gt;orsay&lt;br&gt;Nombre de candidats:66&lt;/div&gt;`)[0];
            popup_a561375858a8c3a106fd8779ffc78aab.setContent(html_c37dfd41eb5e3227b3b4632fb9856d9d);
        

        marker_aaaf96e7f8279c42e5a711f2612e7783.bindPopup(popup_a561375858a8c3a106fd8779ffc78aab)
        ;

        
    
    
            var marker_bb06f0e0ee2c2f9d183e2d1feeeba126 = L.marker(
                [48.702869, 2.191347],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_891d790729af1b7e4f3abb44394a8ad9 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_bb06f0e0ee2c2f9d183e2d1feeeba126.setIcon(icon_891d790729af1b7e4f3abb44394a8ad9);
        
    
        var popup_523175fe6239094cf156108083de677c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_0b7c3493dd961ba56732e2899d397e7e = $(`&lt;div id=&quot;html_0b7c3493dd961ba56732e2899d397e7e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MOULIN&lt;br&gt;43 rue charles de gaulle&lt;br&gt;orsay&lt;br&gt;Nombre de candidats:66&lt;/div&gt;`)[0];
            popup_523175fe6239094cf156108083de677c.setContent(html_0b7c3493dd961ba56732e2899d397e7e);
        

        marker_bb06f0e0ee2c2f9d183e2d1feeeba126.bindPopup(popup_523175fe6239094cf156108083de677c)
        ;

        
    
    
            var marker_479d240cc634c336ebd657feac220f21 = L.marker(
                [48.731264, 2.164587],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_4f25a5988f220563b045de5953308737 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_479d240cc634c336ebd657feac220f21.setIcon(icon_4f25a5988f220563b045de5953308737);
        
    
        var popup_690dd31aac4c03108dd126ddb485e852 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_6213ab67812f8558250d168cb1ef2198 = $(`&lt;div id=&quot;html_6213ab67812f8558250d168cb1ef2198&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ECF GRANDES ECOLES&lt;br&gt;1 route de bievres&lt;br&gt;saclay&lt;br&gt;Nombre de candidats:118&lt;/div&gt;`)[0];
            popup_690dd31aac4c03108dd126ddb485e852.setContent(html_6213ab67812f8558250d168cb1ef2198);
        

        marker_479d240cc634c336ebd657feac220f21.bindPopup(popup_690dd31aac4c03108dd126ddb485e852)
        ;

        
    
    
            var marker_c1f791a6a46401d8cd400b3088609b24 = L.marker(
                [48.705028, 2.19099],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_a840c2a460e71429ec3b2764bf527e82 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_c1f791a6a46401d8cd400b3088609b24.setIcon(icon_a840c2a460e71429ec3b2764bf527e82);
        
    
        var popup_ec74fccce1c859e4bf16d7867309ddb6 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_277a912cfc7b174dd22b7d349baad8cd = $(`&lt;div id=&quot;html_277a912cfc7b174dd22b7d349baad8cd&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;LE GUICHET&lt;br&gt;1 bis rue de versailles&lt;br&gt;orsay&lt;br&gt;Nombre de candidats:32&lt;/div&gt;`)[0];
            popup_ec74fccce1c859e4bf16d7867309ddb6.setContent(html_277a912cfc7b174dd22b7d349baad8cd);
        

        marker_c1f791a6a46401d8cd400b3088609b24.bindPopup(popup_ec74fccce1c859e4bf16d7867309ddb6)
        ;

        
    
    
            var marker_b8d0fccba9730ff647d416077c2dbbe1 = L.marker(
                [48.683272, 2.183368],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_201f712f5374115498200fa18e63cf9b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_b8d0fccba9730ff647d416077c2dbbe1.setIcon(icon_201f712f5374115498200fa18e63cf9b);
        
    
        var popup_a1e6460347c91e76f815ff1260c3fe1b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1087bd793e9646af34e11056fecf6e85 = $(`&lt;div id=&quot;html_1087bd793e9646af34e11056fecf6e85&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MONDETOUR&lt;br&gt;22 rue des paquerettes&lt;br&gt;orsay&lt;br&gt;Nombre de candidats:28&lt;/div&gt;`)[0];
            popup_a1e6460347c91e76f815ff1260c3fe1b.setContent(html_1087bd793e9646af34e11056fecf6e85);
        

        marker_b8d0fccba9730ff647d416077c2dbbe1.bindPopup(popup_a1e6460347c91e76f815ff1260c3fe1b)
        ;

        
    
    
            var marker_ec37205ffff393e704a7fd8357ea3e69 = L.marker(
                [48.697111, 2.18526],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_e27a897569d9b275a571f1b16a041fe7 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_ec37205ffff393e704a7fd8357ea3e69.setIcon(icon_e27a897569d9b275a571f1b16a041fe7);
        
    
        var popup_9de66438205f23131cb73fa4c63c8dc2 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8e937bf63cda868d1e82e604d647c4f1 = $(`&lt;div id=&quot;html_8e937bf63cda868d1e82e604d647c4f1&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ORSAY ECOLE DE CONDUITE&lt;br&gt;24  rue archangé&lt;br&gt;orsay&lt;br&gt;Nombre de candidats:144&lt;/div&gt;`)[0];
            popup_9de66438205f23131cb73fa4c63c8dc2.setContent(html_8e937bf63cda868d1e82e604d647c4f1);
        

        marker_ec37205ffff393e704a7fd8357ea3e69.bindPopup(popup_9de66438205f23131cb73fa4c63c8dc2)
        ;

        
    
    
            var marker_9c00fcb727c8458db449e7f64d3d1d96 = L.marker(
                [48.531634, 2.010312],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_283ca42e67ff61bad292f0bc94857eb5 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_9c00fcb727c8458db449e7f64d3d1d96.setIcon(icon_283ca42e67ff61bad292f0bc94857eb5);
        
    
        var popup_347730f61006f9886cebd98e77734578 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_fbd17e15bcac3abe1204f45b99b8c6a4 = $(`&lt;div id=&quot;html_fbd17e15bcac3abe1204f45b99b8c6a4&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;AME DOURDAN&lt;br&gt;4  avenue carnot&lt;br&gt;dourdan&lt;br&gt;Nombre de candidats:212&lt;/div&gt;`)[0];
            popup_347730f61006f9886cebd98e77734578.setContent(html_fbd17e15bcac3abe1204f45b99b8c6a4);
        

        marker_9c00fcb727c8458db449e7f64d3d1d96.bindPopup(popup_347730f61006f9886cebd98e77734578)
        ;

        
    
    
            var marker_2128a9e5ea882d005595ec1161d6166e = L.marker(
                [48.528979, 2.013584],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_fcf7704a012fad14627f4155410772f9 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_2128a9e5ea882d005595ec1161d6166e.setIcon(icon_fcf7704a012fad14627f4155410772f9);
        
    
        var popup_d2237f055f60f766965db60846f85325 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_4fb294ed95f8dcf71edce41817f9654e = $(`&lt;div id=&quot;html_4fb294ed95f8dcf71edce41817f9654e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DU CENTRE&lt;br&gt;26 bis rue saint pierre&lt;br&gt;dourdan&lt;br&gt;Nombre de candidats:98&lt;/div&gt;`)[0];
            popup_d2237f055f60f766965db60846f85325.setContent(html_4fb294ed95f8dcf71edce41817f9654e);
        

        marker_2128a9e5ea882d005595ec1161d6166e.bindPopup(popup_d2237f055f60f766965db60846f85325)
        ;

        
    
    
            var marker_1b4374ce218331e91396139393823b67 = L.marker(
                [48.528937, 2.002975],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_d9ef800661c263a210dc25335223f578 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_1b4374ce218331e91396139393823b67.setIcon(icon_d9ef800661c263a210dc25335223f578);
        
    
        var popup_7b6d8480d8bc68f408ac82c8f8a83ac9 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2027b8129b94b78c7457d3923d247750 = $(`&lt;div id=&quot;html_2027b8129b94b78c7457d3923d247750&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;SAINT JACQUES AUTO ECOLE&lt;br&gt;30 bis rue lebrun&lt;br&gt;dourdan&lt;br&gt;Nombre de candidats:124&lt;/div&gt;`)[0];
            popup_7b6d8480d8bc68f408ac82c8f8a83ac9.setContent(html_2027b8129b94b78c7457d3923d247750);
        

        marker_1b4374ce218331e91396139393823b67.bindPopup(popup_7b6d8480d8bc68f408ac82c8f8a83ac9)
        ;

        
    
    
            var marker_b15f0f861ce6201b08c809e5b8516ac2 = L.marker(
                [48.700505, 2.326067],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_97afd6803cc248fbc531d683f8368f36 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_b15f0f861ce6201b08c809e5b8516ac2.setIcon(icon_97afd6803cc248fbc531d683f8368f36);
        
    
        var popup_07fb115142a16f4e4d846bb5875a9c06 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2d7acfd7c169b081d2ab103b009e0356 = $(`&lt;div id=&quot;html_2d7acfd7c169b081d2ab103b009e0356&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CONDUITE DE L AVENIR&lt;br&gt;75 avenue gabriel peri&lt;br&gt;morangis&lt;br&gt;Nombre de candidats:79&lt;/div&gt;`)[0];
            popup_07fb115142a16f4e4d846bb5875a9c06.setContent(html_2d7acfd7c169b081d2ab103b009e0356);
        

        marker_b15f0f861ce6201b08c809e5b8516ac2.bindPopup(popup_07fb115142a16f4e4d846bb5875a9c06)
        ;

        
    
    
            var marker_17556089f179600fde1cbababae747be = L.marker(
                [48.707511, 2.329953],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_8ae785193ad6ade2eeee4cd8f4805c89 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_17556089f179600fde1cbababae747be.setIcon(icon_8ae785193ad6ade2eeee4cd8f4805c89);
        
    
        var popup_5410d4d7f9c1beaf74916af8f9a9456c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_014d026f191afd6ea3240e5d769d17fb = $(`&lt;div id=&quot;html_014d026f191afd6ea3240e5d769d17fb&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MORANGIS CONDUITE&lt;br&gt;16 rue du general leclerc&lt;br&gt;morangis&lt;br&gt;Nombre de candidats:120&lt;/div&gt;`)[0];
            popup_5410d4d7f9c1beaf74916af8f9a9456c.setContent(html_014d026f191afd6ea3240e5d769d17fb);
        

        marker_17556089f179600fde1cbababae747be.bindPopup(popup_5410d4d7f9c1beaf74916af8f9a9456c)
        ;

        
    
    
            var marker_fd1fe64c4a9fec7fa968df7130c37e79 = L.marker(
                [48.741212, 2.227385],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_514a216831c9f13358cf0809d5e870ca = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_fd1fe64c4a9fec7fa968df7130c37e79.setIcon(icon_514a216831c9f13358cf0809d5e870ca);
        
    
        var popup_497007a4877edaeca2199673d96bc320 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1d5ae434aa2d4ee7c3e9b0760a8240a2 = $(`&lt;div id=&quot;html_1d5ae434aa2d4ee7c3e9b0760a8240a2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ACCESS PERMIS&lt;br&gt;5 clos des 3 arpents&lt;br&gt;igny&lt;br&gt;Nombre de candidats:73&lt;/div&gt;`)[0];
            popup_497007a4877edaeca2199673d96bc320.setContent(html_1d5ae434aa2d4ee7c3e9b0760a8240a2);
        

        marker_fd1fe64c4a9fec7fa968df7130c37e79.bindPopup(popup_497007a4877edaeca2199673d96bc320)
        ;

        
    
    
            var marker_50eda720534c0399626ec8ecb489dec5 = L.marker(
                [48.732289, 2.221452],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_7b570a8a0551b547158ebfdcf141e62d = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_50eda720534c0399626ec8ecb489dec5.setIcon(icon_7b570a8a0551b547158ebfdcf141e62d);
        
    
        var popup_6e75bbf919ea88d294caae33ea731f4f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_d22f0faad661f255e9225f25a2db69aa = $(`&lt;div id=&quot;html_d22f0faad661f255e9225f25a2db69aa&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ECF IGNY&lt;br&gt;31 rue jules ferry&lt;br&gt;igny&lt;br&gt;Nombre de candidats:254&lt;/div&gt;`)[0];
            popup_6e75bbf919ea88d294caae33ea731f4f.setContent(html_d22f0faad661f255e9225f25a2db69aa);
        

        marker_50eda720534c0399626ec8ecb489dec5.bindPopup(popup_6e75bbf919ea88d294caae33ea731f4f)
        ;

        
    
    
            var marker_67a42c63d9fa97df047f87c774fdd70c = L.marker(
                [48.691512, 2.151205],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_37e41bbe4f0ad3054120b3d78b9eb949 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_67a42c63d9fa97df047f87c774fdd70c.setIcon(icon_37e41bbe4f0ad3054120b3d78b9eb949);
        
    
        var popup_ecab8a2c5c4f16407be40bcdd01b164e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_432ef0cde13a326f2b131b94c1e0cad8 = $(`&lt;div id=&quot;html_432ef0cde13a326f2b131b94c1e0cad8&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DRIVEBOOK AUTO ECOLE&lt;br&gt;52 rue de la haquiniere&lt;br&gt;bures sur yvette&lt;br&gt;Nombre de candidats:145&lt;/div&gt;`)[0];
            popup_ecab8a2c5c4f16407be40bcdd01b164e.setContent(html_432ef0cde13a326f2b131b94c1e0cad8);
        

        marker_67a42c63d9fa97df047f87c774fdd70c.bindPopup(popup_ecab8a2c5c4f16407be40bcdd01b164e)
        ;

        
    
    
            var marker_1b2d1d486772e5ca2c9f279a56baa147 = L.marker(
                [48.696963, 2.162467],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_4a3a79b1963a80b5323cb8f5a2d15c36 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_1b2d1d486772e5ca2c9f279a56baa147.setIcon(icon_4a3a79b1963a80b5323cb8f5a2d15c36);
        
    
        var popup_1ef54a085905a99005d1c2c69288ca72 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_787426258a1ecdd6001d6ebc3bef1611 = $(`&lt;div id=&quot;html_787426258a1ecdd6001d6ebc3bef1611&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;IFCAM BURES&lt;br&gt;2 place du souvenir&lt;br&gt;bures sur yvette&lt;br&gt;Nombre de candidats:89&lt;/div&gt;`)[0];
            popup_1ef54a085905a99005d1c2c69288ca72.setContent(html_787426258a1ecdd6001d6ebc3bef1611);
        

        marker_1b2d1d486772e5ca2c9f279a56baa147.bindPopup(popup_1ef54a085905a99005d1c2c69288ca72)
        ;

        
    
    
            var marker_7e1e9783e45d66741ab2bc859f207d15 = L.marker(
                [48.696729, 2.166265],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_297af2c1bfb91625b40b231ccde39324 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_7e1e9783e45d66741ab2bc859f207d15.setIcon(icon_297af2c1bfb91625b40b231ccde39324);
        
    
        var popup_e7ebd23462e9c945f0314abd98676c32 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_17ab0ef266fa56edc49a75e646d9169c = $(`&lt;div id=&quot;html_17ab0ef266fa56edc49a75e646d9169c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;VILLEBON CONDUITE&lt;br&gt;40 av general de gaulle&lt;br&gt;villebon / yvette&lt;br&gt;Nombre de candidats:134&lt;/div&gt;`)[0];
            popup_e7ebd23462e9c945f0314abd98676c32.setContent(html_17ab0ef266fa56edc49a75e646d9169c);
        

        marker_7e1e9783e45d66741ab2bc859f207d15.bindPopup(popup_e7ebd23462e9c945f0314abd98676c32)
        ;

        
    
    
            var marker_5d3491da9f583681abc770069e645a12 = L.marker(
                [48.642452, 2.228747],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_243f03aaf953a1db3355e35fabb223fe = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_5d3491da9f583681abc770069e645a12.setIcon(icon_243f03aaf953a1db3355e35fabb223fe);
        
    
        var popup_8c473401b67cf061c9f84b21e8adc894 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_00001f8fb2cc4b2290f433b79168f915 = $(`&lt;div id=&quot;html_00001f8fb2cc4b2290f433b79168f915&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DU VILLAGE&lt;br&gt;7 rue eugne moutard martin&lt;br&gt;marcoussis&lt;br&gt;Nombre de candidats:153&lt;/div&gt;`)[0];
            popup_8c473401b67cf061c9f84b21e8adc894.setContent(html_00001f8fb2cc4b2290f433b79168f915);
        

        marker_5d3491da9f583681abc770069e645a12.bindPopup(popup_8c473401b67cf061c9f84b21e8adc894)
        ;

        
    
    
            var marker_63829319a96f31264107d4c78607f59d = L.marker(
                [48.629585, 2.046958],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_e7efe86f29abd08cb591df7608337d9d = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_63829319a96f31264107d4c78607f59d.setIcon(icon_e7efe86f29abd08cb591df7608337d9d);
        
    
        var popup_3858563eba8dd26489258eabc705435d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_92c35bc8d356abc231c786debf71286c = $(`&lt;div id=&quot;html_92c35bc8d356abc231c786debf71286c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;PLEIN PHARE LIMOURS&lt;br&gt;22 route de chartres&lt;br&gt;limours&lt;br&gt;Nombre de candidats:108&lt;/div&gt;`)[0];
            popup_3858563eba8dd26489258eabc705435d.setContent(html_92c35bc8d356abc231c786debf71286c);
        

        marker_63829319a96f31264107d4c78607f59d.bindPopup(popup_3858563eba8dd26489258eabc705435d)
        ;

        
    
    
            var marker_b38b05bd728b61b2529dcd85e5ac18a9 = L.marker(
                [48.680868, 2.534922],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_0bf29229b9ae637fe630ff3191c2d8a1 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_b38b05bd728b61b2529dcd85e5ac18a9.setIcon(icon_0bf29229b9ae637fe630ff3191c2d8a1);
        
    
        var popup_83d98aed47f3a1f72c1cc9c9a5aa5192 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_f34c12f474f4c3f0c7872143bd76e6a1 = $(`&lt;div id=&quot;html_f34c12f474f4c3f0c7872143bd76e6a1&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MAURICE CONDUITE QUINCY&lt;br&gt;rue des 2 communes&lt;br&gt;quincy senart&lt;br&gt;Nombre de candidats:185&lt;/div&gt;`)[0];
            popup_83d98aed47f3a1f72c1cc9c9a5aa5192.setContent(html_f34c12f474f4c3f0c7872143bd76e6a1);
        

        marker_b38b05bd728b61b2529dcd85e5ac18a9.bindPopup(popup_83d98aed47f3a1f72c1cc9c9a5aa5192)
        ;

        
    
    
            var marker_47bb0683941a8ed066675df0fbc2984a = L.marker(
                [48.675305, 2.532471],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_6bf3580818b88c71afaf04dc56d6d87f = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_47bb0683941a8ed066675df0fbc2984a.setIcon(icon_6bf3580818b88c71afaf04dc56d6d87f);
        
    
        var popup_bbbb7fba42cebe3263d97543dce86a4b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2319df124f98fb3223399846ffbb002a = $(`&lt;div id=&quot;html_2319df124f98fb3223399846ffbb002a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;PERMIS 2.0&lt;br&gt;25 rue de brunoy&lt;br&gt;quincy sous senart&lt;br&gt;Nombre de candidats:115&lt;/div&gt;`)[0];
            popup_bbbb7fba42cebe3263d97543dce86a4b.setContent(html_2319df124f98fb3223399846ffbb002a);
        

        marker_47bb0683941a8ed066675df0fbc2984a.bindPopup(popup_bbbb7fba42cebe3263d97543dce86a4b)
        ;

        
    
    
            var marker_631dddf51d9cbcf72a42e5191e944a47 = L.marker(
                [48.403402, 2.468592],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_0d775b7cbf2f3ed2019f2932afd26486 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_631dddf51d9cbcf72a42e5191e944a47.setIcon(icon_0d775b7cbf2f3ed2019f2932afd26486);
        
    
        var popup_d768a7b0a3bc162e33abc990c18d846e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1fc05cffc29f629e301ac430fea70ba3 = $(`&lt;div id=&quot;html_1fc05cffc29f629e301ac430fea70ba3&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MILLY CONDUITE ET FORMATION&lt;br&gt;24 rue langlois&lt;br&gt;milly la foret&lt;br&gt;Nombre de candidats:50&lt;/div&gt;`)[0];
            popup_d768a7b0a3bc162e33abc990c18d846e.setContent(html_1fc05cffc29f629e301ac430fea70ba3);
        

        marker_631dddf51d9cbcf72a42e5191e944a47.bindPopup(popup_d768a7b0a3bc162e33abc990c18d846e)
        ;

        
    
    
            var marker_777cc6098a482668e485f7e559ee5098 = L.marker(
                [48.518501, 2.262762],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_d2dd0761a602a69f595e113591938c52 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_777cc6098a482668e485f7e559ee5098.setIcon(icon_d2dd0761a602a69f595e113591938c52);
        
    
        var popup_1271dbacf6eebd48e9ed362436b3f10d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8f2a6e87e114ff9339703744f9850a39 = $(`&lt;div id=&quot;html_8f2a6e87e114ff9339703744f9850a39&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;LARDY CONDUITE&lt;br&gt;42 grande rue&lt;br&gt;lardy&lt;br&gt;Nombre de candidats:160&lt;/div&gt;`)[0];
            popup_1271dbacf6eebd48e9ed362436b3f10d.setContent(html_8f2a6e87e114ff9339703744f9850a39);
        

        marker_777cc6098a482668e485f7e559ee5098.bindPopup(popup_1271dbacf6eebd48e9ed362436b3f10d)
        ;

        
    
    
            var marker_29711aef9f2048225bbae81ab4a74370 = L.marker(
                [48.580038, 2.229026],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_be0f7c3bc3d6596cd75d11185fd4d6f4 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_29711aef9f2048225bbae81ab4a74370.setIcon(icon_be0f7c3bc3d6596cd75d11185fd4d6f4);
        
    
        var popup_f3f796d69c0651ac272b87ca39105248 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_5041a8df4e46e077457533389562b93f = $(`&lt;div id=&quot;html_5041a8df4e46e077457533389562b93f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ECFR D EGLY&lt;br&gt;16 rue moliere&lt;br&gt;egly&lt;br&gt;Nombre de candidats:228&lt;/div&gt;`)[0];
            popup_f3f796d69c0651ac272b87ca39105248.setContent(html_5041a8df4e46e077457533389562b93f);
        

        marker_29711aef9f2048225bbae81ab4a74370.bindPopup(popup_f3f796d69c0651ac272b87ca39105248)
        ;

        
    
    
            var marker_3fdf79db55722fe2da12d5219adcc40a = L.marker(
                [48.580009, 2.222775],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_51d788deff4dda14d77964dcc872cc53 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_3fdf79db55722fe2da12d5219adcc40a.setIcon(icon_51d788deff4dda14d77964dcc872cc53);
        
    
        var popup_98aebbefc1f284d81a79c95491b7eaaf = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1cd942e2ad4c4fd22a7ebca34f236bfd = $(`&lt;div id=&quot;html_1cd942e2ad4c4fd22a7ebca34f236bfd&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;EGLY&lt;br&gt;18 bis grande rue&lt;br&gt;egly&lt;br&gt;Nombre de candidats:378&lt;/div&gt;`)[0];
            popup_98aebbefc1f284d81a79c95491b7eaaf.setContent(html_1cd942e2ad4c4fd22a7ebca34f236bfd);
        

        marker_3fdf79db55722fe2da12d5219adcc40a.bindPopup(popup_98aebbefc1f284d81a79c95491b7eaaf)
        ;

        
    
    
            var marker_11a8b5bf934b8b657fe8d22e4c5f84d8 = L.marker(
                [48.553184, 2.123249],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_6a27dabf9815f98387a4f6ea5b955d04 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_11a8b5bf934b8b657fe8d22e4c5f84d8.setIcon(icon_6a27dabf9815f98387a4f6ea5b955d04);
        
    
        var popup_2d6c8b3dd31be9dba1f0e168120fbb2b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_074476b0b2ebb5984a9f291922860b89 = $(`&lt;div id=&quot;html_074476b0b2ebb5984a9f291922860b89&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ECFR SAINT CHERON&lt;br&gt;2  rue aristide briand&lt;br&gt;saint cheron&lt;br&gt;Nombre de candidats:33&lt;/div&gt;`)[0];
            popup_2d6c8b3dd31be9dba1f0e168120fbb2b.setContent(html_074476b0b2ebb5984a9f291922860b89);
        

        marker_11a8b5bf934b8b657fe8d22e4c5f84d8.bindPopup(popup_2d6c8b3dd31be9dba1f0e168120fbb2b)
        ;

        
    
    
            var marker_8d1bb0ca0ef023b80f987da462a9077f = L.marker(
                [48.564989, 2.43785],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_9d076104cb3afe017ff9d6aa9bc04b5b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_8d1bb0ca0ef023b80f987da462a9077f.setIcon(icon_9d076104cb3afe017ff9d6aa9bc04b5b);
        
    
        var popup_189747e6ce80a5caf54e812450642359 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_84ebf0e6f4c28bd3bc7d1437ec0d93f4 = $(`&lt;div id=&quot;html_84ebf0e6f4c28bd3bc7d1437ec0d93f4&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;JB FORMATIONS&lt;br&gt;47 boulevard charles de gaulle&lt;br&gt;mennecy&lt;br&gt;Nombre de candidats:64&lt;/div&gt;`)[0];
            popup_189747e6ce80a5caf54e812450642359.setContent(html_84ebf0e6f4c28bd3bc7d1437ec0d93f4);
        

        marker_8d1bb0ca0ef023b80f987da462a9077f.bindPopup(popup_189747e6ce80a5caf54e812450642359)
        ;

        
    
    
            var marker_fea3c46e6aabd3d0e175f391fdc0b6c2 = L.marker(
                [48.554435, 2.422091],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_ff9e1e682b5e04f91e1443c20eecb646 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_fea3c46e6aabd3d0e175f391fdc0b6c2.setIcon(icon_ff9e1e682b5e04f91e1443c20eecb646);
        
    
        var popup_668687b546ca9962277871cd314f3b56 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_3c745a212957b74defe581f92fc230e4 = $(`&lt;div id=&quot;html_3c745a212957b74defe581f92fc230e4&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;LA VERVILLE&lt;br&gt;cc la verville&lt;br&gt;mennecy&lt;br&gt;Nombre de candidats:78&lt;/div&gt;`)[0];
            popup_668687b546ca9962277871cd314f3b56.setContent(html_3c745a212957b74defe581f92fc230e4);
        

        marker_fea3c46e6aabd3d0e175f391fdc0b6c2.bindPopup(popup_668687b546ca9962277871cd314f3b56)
        ;

        
    
    
            var marker_2a0bd5de241fcef4f7c5d690a7dfefe6 = L.marker(
                [48.563257, 2.440638],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_f063ea395ef2f8331188c6fc7fd0636b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_2a0bd5de241fcef4f7c5d690a7dfefe6.setIcon(icon_f063ea395ef2f8331188c6fc7fd0636b);
        
    
        var popup_7ac43d1908a4b93be071966499dc84eb = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a31cfaaa90fb27215675997f7c2f447d = $(`&lt;div id=&quot;html_a31cfaaa90fb27215675997f7c2f447d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;LES AUNETTES AGUADO AUTO ECOLE&lt;br&gt;20  rue paul cézanne&lt;br&gt;mennecy&lt;br&gt;Nombre de candidats:127&lt;/div&gt;`)[0];
            popup_7ac43d1908a4b93be071966499dc84eb.setContent(html_a31cfaaa90fb27215675997f7c2f447d);
        

        marker_2a0bd5de241fcef4f7c5d690a7dfefe6.bindPopup(popup_7ac43d1908a4b93be071966499dc84eb)
        ;

        
    
    
            var marker_22e43d841790f964a4cc4e1776d3871b = L.marker(
                [48.566532, 2.434429],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_b5e98f52f8e4574acfe3c1ef2e0b5011 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_22e43d841790f964a4cc4e1776d3871b.setIcon(icon_b5e98f52f8e4574acfe3c1ef2e0b5011);
        
    
        var popup_e5f1c03b47f9e55624b4a1b864f7dd9b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7937f00ffde094e4f554a86ad547e33f = $(`&lt;div id=&quot;html_7937f00ffde094e4f554a86ad547e33f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MC MENNECY AUTO ECOLE&lt;br&gt;3  rue de la croix boissée&lt;br&gt;mennecy&lt;br&gt;Nombre de candidats:70&lt;/div&gt;`)[0];
            popup_e5f1c03b47f9e55624b4a1b864f7dd9b.setContent(html_7937f00ffde094e4f554a86ad547e33f);
        

        marker_22e43d841790f964a4cc4e1776d3871b.bindPopup(popup_e5f1c03b47f9e55624b4a1b864f7dd9b)
        ;

        
    
    
            var marker_d95f83e82d618a7581f80c9359ea4c92 = L.marker(
                [48.565236, 2.433887],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_a209bfdf986e3b44f1a4785415699071 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_d95f83e82d618a7581f80c9359ea4c92.setIcon(icon_a209bfdf986e3b44f1a4785415699071);
        
    
        var popup_0e989885ef14d0f7b6d2a0fe6327011b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9a05997c02712eb6871f72bfcfd5314b = $(`&lt;div id=&quot;html_9a05997c02712eb6871f72bfcfd5314b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MENNECY 2000&lt;br&gt;15 rue de milly&lt;br&gt;mennecy&lt;br&gt;Nombre de candidats:155&lt;/div&gt;`)[0];
            popup_0e989885ef14d0f7b6d2a0fe6327011b.setContent(html_9a05997c02712eb6871f72bfcfd5314b);
        

        marker_d95f83e82d618a7581f80c9359ea4c92.bindPopup(popup_0e989885ef14d0f7b6d2a0fe6327011b)
        ;

        
    
    
            var marker_57af67446f147af80489d1f248e77259 = L.marker(
                [48.705844, 2.362094],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_0a68630d4d1103cde7272e8b3d8f31e2 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_57af67446f147af80489d1f248e77259.setIcon(icon_0a68630d4d1103cde7272e8b3d8f31e2);
        
    
        var popup_83e24d3adb90a3fca88cb9c501cb08b2 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_cfdea82b94363baea57e881ed2f33a3b = $(`&lt;div id=&quot;html_cfdea82b94363baea57e881ed2f33a3b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;PARAY ATHIS&lt;br&gt;104 avenue de verdun&lt;br&gt;paray vieille poste&lt;br&gt;Nombre de candidats:76&lt;/div&gt;`)[0];
            popup_83e24d3adb90a3fca88cb9c501cb08b2.setContent(html_cfdea82b94363baea57e881ed2f33a3b);
        

        marker_57af67446f147af80489d1f248e77259.bindPopup(popup_83e24d3adb90a3fca88cb9c501cb08b2)
        ;

        
    
    
            var marker_9d5fab335eb052fb6811e0f2ad2d41c1 = L.marker(
                [48.716113, 2.460485],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_b41ecf8e6650b21b6c85369a07cfe421 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_9d5fab335eb052fb6811e0f2ad2d41c1.setIcon(icon_b41ecf8e6650b21b6c85369a07cfe421);
        
    
        var popup_8aabc5f8dcc1f7efa92e0881e3eb2b92 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_16a55d63d2d8d85ba7491abb90853a49 = $(`&lt;div id=&quot;html_16a55d63d2d8d85ba7491abb90853a49&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;AUTO ROUTE 66&lt;br&gt;2 rue de schotten&lt;br&gt;crosne&lt;br&gt;Nombre de candidats:73&lt;/div&gt;`)[0];
            popup_8aabc5f8dcc1f7efa92e0881e3eb2b92.setContent(html_16a55d63d2d8d85ba7491abb90853a49);
        

        marker_9d5fab335eb052fb6811e0f2ad2d41c1.bindPopup(popup_8aabc5f8dcc1f7efa92e0881e3eb2b92)
        ;

        
    
    
            var marker_0de2f4519c539c25a50b1d30f5a6ad4c = L.marker(
                [48.716503, 2.4583],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_e2437cb5aa5c47032590222d8883e23c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_0de2f4519c539c25a50b1d30f5a6ad4c.setIcon(icon_e2437cb5aa5c47032590222d8883e23c);
        
    
        var popup_db014070750001573cd201ea1027fa5f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_82a1ce09854962907fa25af94708eee4 = $(`&lt;div id=&quot;html_82a1ce09854962907fa25af94708eee4&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CROSNE AUTO ECOLE&lt;br&gt;66 avenue jean jaures&lt;br&gt;crosnes&lt;br&gt;Nombre de candidats:24&lt;/div&gt;`)[0];
            popup_db014070750001573cd201ea1027fa5f.setContent(html_82a1ce09854962907fa25af94708eee4);
        

        marker_0de2f4519c539c25a50b1d30f5a6ad4c.bindPopup(popup_db014070750001573cd201ea1027fa5f)
        ;

        
    
    
            var marker_7f47693b29f4b87083d32f9be2a68fe9 = L.marker(
                [48.714324, 2.46131],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_4aa1e5525ad49d7c3a9c63ab09796bf2 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_7f47693b29f4b87083d32f9be2a68fe9.setIcon(icon_4aa1e5525ad49d7c3a9c63ab09796bf2);
        
    
        var popup_87044938e01ec713519d225c865e0d5b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_39df8dc7f861cdd139688d569accb072 = $(`&lt;div id=&quot;html_39df8dc7f861cdd139688d569accb072&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;SOLUTION PERMIS&lt;br&gt;17 avenue jean jaures&lt;br&gt;crosnes&lt;br&gt;Nombre de candidats:248&lt;/div&gt;`)[0];
            popup_87044938e01ec713519d225c865e0d5b.setContent(html_39df8dc7f861cdd139688d569accb072);
        

        marker_7f47693b29f4b87083d32f9be2a68fe9.bindPopup(popup_87044938e01ec713519d225c865e0d5b)
        ;

        
    
    
            var marker_b86710c5641236755db8aa753d8b480b = L.marker(
                [48.751743, 2.216276],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_a5d2283ed3114eeebc9bee4a4bda9d0b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_b86710c5641236755db8aa753d8b480b.setIcon(icon_a5d2283ed3114eeebc9bee4a4bda9d0b);
        
    
        var popup_a2265113e4ec416ed98f2981cbf37fbb = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8cda6a9f27f05af39e1c0d857dc6581e = $(`&lt;div id=&quot;html_8cda6a9f27f05af39e1c0d857dc6581e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;BIEVRES ACCESS PERMIS&lt;br&gt;14 avenue de la gare&lt;br&gt;bievres&lt;br&gt;Nombre de candidats:48&lt;/div&gt;`)[0];
            popup_a2265113e4ec416ed98f2981cbf37fbb.setContent(html_8cda6a9f27f05af39e1c0d857dc6581e);
        

        marker_b86710c5641236755db8aa753d8b480b.bindPopup(popup_a2265113e4ec416ed98f2981cbf37fbb)
        ;

        
    
    
            var marker_045a448584ab4fbbe3c1ee02ff2637ec = L.marker(
                [48.493315, 2.189476],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_66ef0465b5972f9e60ef153905181382 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_045a448584ab4fbbe3c1ee02ff2637ec.setIcon(icon_66ef0465b5972f9e60ef153905181382);
        
    
        var popup_c004e100154ec009a565be49fea7af78 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_c86a989cf651d419fd8bb473bbe9d54c = $(`&lt;div id=&quot;html_c86a989cf651d419fd8bb473bbe9d54c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DE LA MAIRIE ETRECHY&lt;br&gt;07 place charles de gaulle&lt;br&gt;etrechy&lt;br&gt;Nombre de candidats:102&lt;/div&gt;`)[0];
            popup_c004e100154ec009a565be49fea7af78.setContent(html_c86a989cf651d419fd8bb473bbe9d54c);
        

        marker_045a448584ab4fbbe3c1ee02ff2637ec.bindPopup(popup_c004e100154ec009a565be49fea7af78)
        ;

        
    
    
            var marker_c1208238098814f189d199db10efed2f = L.marker(
                [48.48153, 2.348313],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_5afbf3a692f332a1d6756b07e757a2c8 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_c1208238098814f189d199db10efed2f.setIcon(icon_5afbf3a692f332a1d6756b07e757a2c8);
        
    
        var popup_0424c4f9871f571dee3131b6b7bc0f35 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9063e967bab91bc69da62e0240ca08e0 = $(`&lt;div id=&quot;html_9063e967bab91bc69da62e0240ca08e0&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;FERTE ALAIS&lt;br&gt;16 bis rue st firmin&lt;br&gt;la ferte alais&lt;br&gt;Nombre de candidats:194&lt;/div&gt;`)[0];
            popup_0424c4f9871f571dee3131b6b7bc0f35.setContent(html_9063e967bab91bc69da62e0240ca08e0);
        

        marker_c1208238098814f189d199db10efed2f.bindPopup(popup_0424c4f9871f571dee3131b6b7bc0f35)
        ;

        
    
    
            var marker_7ae4665fca98ffbdf45d6977e3e2222b = L.marker(
                [48.67665, 2.350125],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_3924c3252a2338258720c9c0db4f0222 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_7ae4665fca98ffbdf45d6977e3e2222b.setIcon(icon_3924c3252a2338258720c9c0db4f0222);
        
    
        var popup_6491e150fc8cf69d821ed7522c485bd9 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2b071af80fe4ce0e064d04b30b8c9439 = $(`&lt;div id=&quot;html_2b071af80fe4ce0e064d04b30b8c9439&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ESR SAVIGNY&lt;br&gt;9 av charles de gaulle&lt;br&gt;savigny sur orge&lt;br&gt;Nombre de candidats:167&lt;/div&gt;`)[0];
            popup_6491e150fc8cf69d821ed7522c485bd9.setContent(html_2b071af80fe4ce0e064d04b30b8c9439);
        

        marker_7ae4665fca98ffbdf45d6977e3e2222b.bindPopup(popup_6491e150fc8cf69d821ed7522c485bd9)
        ;

        
    
    
            var marker_ab1e56921ea21bd087ce4667da8406a5 = L.marker(
                [48.685583, 2.346408],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_1dbe47902b19f6e977b3d82a90948a78 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_ab1e56921ea21bd087ce4667da8406a5.setIcon(icon_1dbe47902b19f6e977b3d82a90948a78);
        
    
        var popup_8977f22fac5dc6f3428a7608126d2c83 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_f5f58ff9a71533096293c4401e9a922e = $(`&lt;div id=&quot;html_f5f58ff9a71533096293c4401e9a922e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;SAVIGNY&lt;br&gt;81 boulevard aristide briand&lt;br&gt;savigny sur orge&lt;br&gt;Nombre de candidats:135&lt;/div&gt;`)[0];
            popup_8977f22fac5dc6f3428a7608126d2c83.setContent(html_f5f58ff9a71533096293c4401e9a922e);
        

        marker_ab1e56921ea21bd087ce4667da8406a5.bindPopup(popup_8977f22fac5dc6f3428a7608126d2c83)
        ;

        
    
    
            var marker_464a8a1eb089be0a020301001f27c1a3 = L.marker(
                [48.676182, 2.351206],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_982b526dd09e902d75132a0c09652f55 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_464a8a1eb089be0a020301001f27c1a3.setIcon(icon_982b526dd09e902d75132a0c09652f55);
        
    
        var popup_fb9c9dcf5086e19d24c34bc6a9c2f8d7 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_99fd43282a42f8bb0b034e42161a3855 = $(`&lt;div id=&quot;html_99fd43282a42f8bb0b034e42161a3855&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;TREMPLIN GARE SAVIGNY&lt;br&gt;2 place de la gare&lt;br&gt;savigny sur orge&lt;br&gt;Nombre de candidats:294&lt;/div&gt;`)[0];
            popup_fb9c9dcf5086e19d24c34bc6a9c2f8d7.setContent(html_99fd43282a42f8bb0b034e42161a3855);
        

        marker_464a8a1eb089be0a020301001f27c1a3.bindPopup(popup_fb9c9dcf5086e19d24c34bc6a9c2f8d7)
        ;

        
    
    
            var marker_fb62212c7d5f6ae973946599c123adb7 = L.marker(
                [48.527568, 2.37352],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_d3d74be33ed52a7f05576190c5ba2b0e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_fb62212c7d5f6ae973946599c123adb7.setIcon(icon_d3d74be33ed52a7f05576190c5ba2b0e);
        
    
        var popup_c85212bff2f022bcaa3e40b7604d39fd = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_eb75de3949c023c9a1e7b62da3395625 = $(`&lt;div id=&quot;html_eb75de3949c023c9a1e7b62da3395625&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ECP VAL D ESSONNE&lt;br&gt;31  rue de la papeterie&lt;br&gt;ballancourt&lt;br&gt;Nombre de candidats:182&lt;/div&gt;`)[0];
            popup_c85212bff2f022bcaa3e40b7604d39fd.setContent(html_eb75de3949c023c9a1e7b62da3395625);
        

        marker_fb62212c7d5f6ae973946599c123adb7.bindPopup(popup_c85212bff2f022bcaa3e40b7604d39fd)
        ;

        
    
    
            var marker_b44994dfd71eceac169b3cca11bef36f = L.marker(
                [48.659913, 2.242052],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_e4e5fb0b422e37a564148f856b2e2e9a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_b44994dfd71eceac169b3cca11bef36f.setIcon(icon_e4e5fb0b422e37a564148f856b2e2e9a);
        
    
        var popup_f9ce54aae201d44ee457a3c4709ac8fb = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9e1159e9c91e32321543532173274f1d = $(`&lt;div id=&quot;html_9e1159e9c91e32321543532173274f1d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;AUTO ECOLE DE NOZAY&lt;br&gt;2 bis place de la mairie&lt;br&gt;nozay&lt;br&gt;Nombre de candidats:102&lt;/div&gt;`)[0];
            popup_f9ce54aae201d44ee457a3c4709ac8fb.setContent(html_9e1159e9c91e32321543532173274f1d);
        

        marker_b44994dfd71eceac169b3cca11bef36f.bindPopup(popup_f9ce54aae201d44ee457a3c4709ac8fb)
        ;

        
    
    
            var marker_0f8add9a08ff9bb38901fa4c8d37e1b8 = L.marker(
                [48.66096, 2.268075],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_b324f85355a66566b2528a4bcbd9b655 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_0f8add9a08ff9bb38901fa4c8d37e1b8.setIcon(icon_b324f85355a66566b2528a4bcbd9b655);
        
    
        var popup_d1a54b755128ebd81e45e5d4cc8c120b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8ba579fe016e9d69fd2446aee99fc278 = $(`&lt;div id=&quot;html_8ba579fe016e9d69fd2446aee99fc278&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;LA VILLE DU BOIS AUTO MOTO ECOLE&lt;br&gt;1  rue du grand noyer&lt;br&gt;la ville du bois&lt;br&gt;Nombre de candidats:74&lt;/div&gt;`)[0];
            popup_d1a54b755128ebd81e45e5d4cc8c120b.setContent(html_8ba579fe016e9d69fd2446aee99fc278);
        

        marker_0f8add9a08ff9bb38901fa4c8d37e1b8.bindPopup(popup_d1a54b755128ebd81e45e5d4cc8c120b)
        ;

        
    
    
            var marker_6b62b17792205c4a3a1330b17af1ffe7 = L.marker(
                [48.561176, 2.303128],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_cb56655d576c7ca6b37a4ea00055630c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_6b62b17792205c4a3a1330b17af1ffe7.setIcon(icon_cb56655d576c7ca6b37a4ea00055630c);
        
    
        var popup_c5e84e68d1954f67e47edf68f568d722 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_28a77f955cf22782f762b23508fdf83a = $(`&lt;div id=&quot;html_28a77f955cf22782f762b23508fdf83a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;JOLY AGUADO AUTO ECOLE&lt;br&gt;4  bis grande rue&lt;br&gt;marolles en hurepoix&lt;br&gt;Nombre de candidats:102&lt;/div&gt;`)[0];
            popup_c5e84e68d1954f67e47edf68f568d722.setContent(html_28a77f955cf22782f762b23508fdf83a);
        

        marker_6b62b17792205c4a3a1330b17af1ffe7.bindPopup(popup_c5e84e68d1954f67e47edf68f568d722)
        ;

        
    
    
            var marker_ddf54c21d5224925895c76b9d2e19db7 = L.marker(
                [48.563744, 2.293679],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_ae45d0950f8aab6af7bcddbdc755544c = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_ddf54c21d5224925895c76b9d2e19db7.setIcon(icon_ae45d0950f8aab6af7bcddbdc755544c);
        
    
        var popup_bc172621b61c4eaaddeb355bd58957f0 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_38561d5949c53624c930fbb872d1c57c = $(`&lt;div id=&quot;html_38561d5949c53624c930fbb872d1c57c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MAROLLES AUTO ECOLE&lt;br&gt;31 bis  avenue charles de gaulles&lt;br&gt;marolles&lt;br&gt;Nombre de candidats:160&lt;/div&gt;`)[0];
            popup_bc172621b61c4eaaddeb355bd58957f0.setContent(html_38561d5949c53624c930fbb872d1c57c);
        

        marker_ddf54c21d5224925895c76b9d2e19db7.bindPopup(popup_bc172621b61c4eaaddeb355bd58957f0)
        ;

        
    
    
            var marker_920c1426c09e35acb6d41a0dc494d551 = L.marker(
                [48.62414, 2.124893],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_ba9e2ee5cf9e9e102608c0fd47aadf62 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_920c1426c09e35acb6d41a0dc494d551.setIcon(icon_ba9e2ee5cf9e9e102608c0fd47aadf62);
        
    
        var popup_af7d115a267422282c5f1a265d3bb8a1 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_0735935e90938ab7438edbdd6eaf1472 = $(`&lt;div id=&quot;html_0735935e90938ab7438edbdd6eaf1472&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;BRIIS CONDUIT&lt;br&gt;1 rue de l armee patton&lt;br&gt;briis sous forge&lt;br&gt;Nombre de candidats:146&lt;/div&gt;`)[0];
            popup_af7d115a267422282c5f1a265d3bb8a1.setContent(html_0735935e90938ab7438edbdd6eaf1472);
        

        marker_920c1426c09e35acb6d41a0dc494d551.bindPopup(popup_af7d115a267422282c5f1a265d3bb8a1)
        ;

        
    
    
            var marker_5c694f1b5711d217a87091bcb19e5a4b = L.marker(
                [48.566147, 2.170858],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_124a5002fa20ec365cd717ffb04072ed = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_5c694f1b5711d217a87091bcb19e5a4b.setIcon(icon_124a5002fa20ec365cd717ffb04072ed);
        
    
        var popup_bddff4fe76af0dee436956ab7d52c63b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a02da5d08b9ee799089bd0c93ed9b83d = $(`&lt;div id=&quot;html_a02da5d08b9ee799089bd0c93ed9b83d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;BREUILLET&lt;br&gt;5 grande rue&lt;br&gt;breuillet&lt;br&gt;Nombre de candidats:152&lt;/div&gt;`)[0];
            popup_bddff4fe76af0dee436956ab7d52c63b.setContent(html_a02da5d08b9ee799089bd0c93ed9b83d);
        

        marker_5c694f1b5711d217a87091bcb19e5a4b.bindPopup(popup_bddff4fe76af0dee436956ab7d52c63b)
        ;

        
    
    
            var marker_68340f97b9bdfd68bda78f5feb9c6cc3 = L.marker(
                [48.316053, 2.08677],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_e367b89f57525dd4e7043db3d9cd6cfd = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_68340f97b9bdfd68bda78f5feb9c6cc3.setIcon(icon_e367b89f57525dd4e7043db3d9cd6cfd);
        
    
        var popup_1bf1c7ed26d422a8acb53d44ca1ac1ea = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2a8e841b94d1f016cbd0aa55c8a53549 = $(`&lt;div id=&quot;html_2a8e841b94d1f016cbd0aa55c8a53549&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MEREVILLE CONDUITE&lt;br&gt;8 rue carnot&lt;br&gt;mereville&lt;br&gt;Nombre de candidats:52&lt;/div&gt;`)[0];
            popup_1bf1c7ed26d422a8acb53d44ca1ac1ea.setContent(html_2a8e841b94d1f016cbd0aa55c8a53549);
        

        marker_68340f97b9bdfd68bda78f5feb9c6cc3.bindPopup(popup_1bf1c7ed26d422a8acb53d44ca1ac1ea)
        ;

        
    
    
            var marker_0d6a6377b400715501dc482999697038 = L.marker(
                [48.647255, 2.327073],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_ff63e5795cf1fdac925a7da84600748a = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_0d6a6377b400715501dc482999697038.setIcon(icon_ff63e5795cf1fdac925a7da84600748a);
        
    
        var popup_5b6318c9ad9890be0e70236822066edd = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ba0ac3e62a6696e8f48fdebced251f5b = $(`&lt;div id=&quot;html_ba0ac3e62a6696e8f48fdebced251f5b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;AEC CONDUITE&lt;br&gt;130-134 avenue gabriel peri&lt;br&gt;sainte genevieve des bois&lt;br&gt;Nombre de candidats:160&lt;/div&gt;`)[0];
            popup_5b6318c9ad9890be0e70236822066edd.setContent(html_ba0ac3e62a6696e8f48fdebced251f5b);
        

        marker_0d6a6377b400715501dc482999697038.bindPopup(popup_5b6318c9ad9890be0e70236822066edd)
        ;

        
    
    
            var marker_2809ba610654dcc87442a3d9c4f7fcd2 = L.marker(
                [48.637618, 2.329076],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_daf2f424fb69204ce003e35ebd806655 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_2809ba610654dcc87442a3d9c4f7fcd2.setIcon(icon_daf2f424fb69204ce003e35ebd806655);
        
    
        var popup_9937b5754889b627dc8808f3ff8dd4bf = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a6e75165871b012179c5fa9f68259891 = $(`&lt;div id=&quot;html_a6e75165871b012179c5fa9f68259891&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;AUTO ECOLE NIEMEN&lt;br&gt;43/45 avenue du regiment normandie niemen&lt;br&gt;sainte genevieve des bois&lt;br&gt;Nombre de candidats:88&lt;/div&gt;`)[0];
            popup_9937b5754889b627dc8808f3ff8dd4bf.setContent(html_a6e75165871b012179c5fa9f68259891);
        

        marker_2809ba610654dcc87442a3d9c4f7fcd2.bindPopup(popup_9937b5754889b627dc8808f3ff8dd4bf)
        ;

        
    
    
            var marker_ef319c8a5e69bcf5918df94bedc39945 = L.marker(
                [48.636887, 2.335969],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_a4edd75a2486db9582e44e29da380ca2 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_ef319c8a5e69bcf5918df94bedc39945.setIcon(icon_a4edd75a2486db9582e44e29da380ca2);
        
    
        var popup_c77a0b980b86e305dbbfd037d549c0dc = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1fefeb876dbf0dea4350fa4c4c9c0a04 = $(`&lt;div id=&quot;html_1fefeb876dbf0dea4350fa4c4c9c0a04&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CER PARC PIERRE&lt;br&gt;23 avenue jacques duclos&lt;br&gt;sainte gennevieve des bois&lt;br&gt;Nombre de candidats:55&lt;/div&gt;`)[0];
            popup_c77a0b980b86e305dbbfd037d549c0dc.setContent(html_1fefeb876dbf0dea4350fa4c4c9c0a04);
        

        marker_ef319c8a5e69bcf5918df94bedc39945.bindPopup(popup_c77a0b980b86e305dbbfd037d549c0dc)
        ;

        
    
    
            var marker_66c8339cc178d07389cc371c56fb2e96 = L.marker(
                [48.65162, 2.314337],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_026c92104b820c059444cdb65670cae7 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_66c8339cc178d07389cc371c56fb2e96.setIcon(icon_026c92104b820c059444cdb65670cae7);
        
    
        var popup_ac8d576b4f36c7cdbb70e5c1f9839dc3 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_1e9883175713c1103c7ee95788121f46 = $(`&lt;div id=&quot;html_1e9883175713c1103c7ee95788121f46&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ECF Sainte Genevieve Des Bois&lt;br&gt;12 avenue georges pitard&lt;br&gt;sainte genevieve des bois&lt;br&gt;Nombre de candidats:577&lt;/div&gt;`)[0];
            popup_ac8d576b4f36c7cdbb70e5c1f9839dc3.setContent(html_1e9883175713c1103c7ee95788121f46);
        

        marker_66c8339cc178d07389cc371c56fb2e96.bindPopup(popup_ac8d576b4f36c7cdbb70e5c1f9839dc3)
        ;

        
    
    
            var marker_d7506e770c5aaa5eab0643844cd93e3d = L.marker(
                [48.639919, 2.349212],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_b174846592da47d64925a9cd3196e904 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_d7506e770c5aaa5eab0643844cd93e3d.setIcon(icon_b174846592da47d64925a9cd3196e904);
        
    
        var popup_82105c5c66786afc4b4d2efa8e821cd2 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_3d750dcc796faeda32934ad283250d30 = $(`&lt;div id=&quot;html_3d750dcc796faeda32934ad283250d30&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;EINSTEIN CONDUITE 91&lt;br&gt;4 avenue chalie chaplin&lt;br&gt;sainte genevieve des bois&lt;br&gt;Nombre de candidats:34&lt;/div&gt;`)[0];
            popup_82105c5c66786afc4b4d2efa8e821cd2.setContent(html_3d750dcc796faeda32934ad283250d30);
        

        marker_d7506e770c5aaa5eab0643844cd93e3d.bindPopup(popup_82105c5c66786afc4b4d2efa8e821cd2)
        ;

        
    
    
            var marker_bd6f0d81f23d3357e63dc4453166ec99 = L.marker(
                [48.637983, 2.360258],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_61f3b45840d4e4854f12dec343a216b7 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_bd6f0d81f23d3357e63dc4453166ec99.setIcon(icon_61f3b45840d4e4854f12dec343a216b7);
        
    
        var popup_dbabd01a7aec362cd5e8c8d1bf72b505 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_26f053205656cbb2b444d8126e126124 = $(`&lt;div id=&quot;html_26f053205656cbb2b444d8126e126124&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;FLEURY CONDUITE&lt;br&gt;67 rosa park&lt;br&gt;fleury merogis&lt;br&gt;Nombre de candidats:227&lt;/div&gt;`)[0];
            popup_dbabd01a7aec362cd5e8c8d1bf72b505.setContent(html_26f053205656cbb2b444d8126e126124);
        

        marker_bd6f0d81f23d3357e63dc4453166ec99.bindPopup(popup_dbabd01a7aec362cd5e8c8d1bf72b505)
        ;

        
    
    
            var marker_91c08973feef9bfeffdfef0665a46b6c = L.marker(
                [48.639919, 2.349212],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_9fee8904498bea2863e955e781030690 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_91c08973feef9bfeffdfef0665a46b6c.setIcon(icon_9fee8904498bea2863e955e781030690);
        
    
        var popup_1213fc7c65b2bab6e71f8875632bc5cb = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_e98f0fb23189f6807d2bdff631e6ac35 = $(`&lt;div id=&quot;html_e98f0fb23189f6807d2bdff631e6ac35&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MC SAINTE GENEVIEVE&lt;br&gt;4 avenue charli chaplin&lt;br&gt;sainte genevieve des bois&lt;br&gt;Nombre de candidats:34&lt;/div&gt;`)[0];
            popup_1213fc7c65b2bab6e71f8875632bc5cb.setContent(html_e98f0fb23189f6807d2bdff631e6ac35);
        

        marker_91c08973feef9bfeffdfef0665a46b6c.bindPopup(popup_1213fc7c65b2bab6e71f8875632bc5cb)
        ;

        
    
    
            var marker_f120040c2bafbf3373aa98f8e2a7c9a2 = L.marker(
                [48.651043, 2.317472],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_cf2dccf59508162d8493d690ab594a3b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_f120040c2bafbf3373aa98f8e2a7c9a2.setIcon(icon_cf2dccf59508162d8493d690ab594a3b);
        
    
        var popup_45efec26075c996c5bf1a8fdc49db893 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_83e69d7ab2ec3750baf595f83e31f62b = $(`&lt;div id=&quot;html_83e69d7ab2ec3750baf595f83e31f62b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;REVOLUTION PERMIS&lt;br&gt;39 avenue gabriel peri&lt;br&gt;sainte genevieve des bois&lt;br&gt;Nombre de candidats:117&lt;/div&gt;`)[0];
            popup_45efec26075c996c5bf1a8fdc49db893.setContent(html_83e69d7ab2ec3750baf595f83e31f62b);
        

        marker_f120040c2bafbf3373aa98f8e2a7c9a2.bindPopup(popup_45efec26075c996c5bf1a8fdc49db893)
        ;

        
    
    
            var marker_8c51336b933b3cb28dfca072d7a4fb0a = L.marker(
                [48.631311, 2.337732],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_c6de287f8410ba1cc66d94f219055220 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_8c51336b933b3cb28dfca072d7a4fb0a.setIcon(icon_c6de287f8410ba1cc66d94f219055220);
        
    
        var popup_fc7e6d3e21746a9cd67bda04f97cf74e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a99a2e7f0301e9db68cd31817ef9bdc1 = $(`&lt;div id=&quot;html_a99a2e7f0301e9db68cd31817ef9bdc1&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;SPRINT ESSONNE&lt;br&gt;254 route de corbeil&lt;br&gt;sainte genevieve des bois&lt;br&gt;Nombre de candidats:48&lt;/div&gt;`)[0];
            popup_fc7e6d3e21746a9cd67bda04f97cf74e.setContent(html_a99a2e7f0301e9db68cd31817ef9bdc1);
        

        marker_8c51336b933b3cb28dfca072d7a4fb0a.bindPopup(popup_fc7e6d3e21746a9cd67bda04f97cf74e)
        ;

        
    
    
            var marker_90aa167f7363c8e67570ca1e73ffd2ae = L.marker(
                [48.392301, 2.391672],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_e6b6caa46e091cbcaeba307918c08745 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_90aa167f7363c8e67570ca1e73ffd2ae.setIcon(icon_e6b6caa46e091cbcaeba307918c08745);
        
    
        var popup_9a5bddbb7a1122689c9d7dd84aee3786 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_7a7a8f65719861824c88f63b438092ff = $(`&lt;div id=&quot;html_7a7a8f65719861824c88f63b438092ff&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MAISSE ECOLE DE CONDUITE&lt;br&gt;2 rue de buno bonneveaux&lt;br&gt;maisse&lt;br&gt;Nombre de candidats:43&lt;/div&gt;`)[0];
            popup_9a5bddbb7a1122689c9d7dd84aee3786.setContent(html_7a7a8f65719861824c88f63b438092ff);
        

        marker_90aa167f7363c8e67570ca1e73ffd2ae.bindPopup(popup_9a5bddbb7a1122689c9d7dd84aee3786)
        ;

        
    
    
            var marker_a84652ef8447f955b8634a5360e9760d = L.marker(
                [48.554881, 2.212252],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_ada049866ba9a6685bb635814ffc7dee = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_a84652ef8447f955b8634a5360e9760d.setIcon(icon_ada049866ba9a6685bb635814ffc7dee);
        
    
        var popup_f6d82bf245cf7c972034d3aee00d6cba = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_ea098c242ed10c462be200034737c3f5 = $(`&lt;div id=&quot;html_ea098c242ed10c462be200034737c3f5&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;BOISSY AUTO ECOLE&lt;br&gt;rue pasteur centre commercial&lt;br&gt;boissy sous saint yon&lt;br&gt;Nombre de candidats:81&lt;/div&gt;`)[0];
            popup_f6d82bf245cf7c972034d3aee00d6cba.setContent(html_ea098c242ed10c462be200034737c3f5);
        

        marker_a84652ef8447f955b8634a5360e9760d.bindPopup(popup_f6d82bf245cf7c972034d3aee00d6cba)
        ;

        
    
    
            var marker_b24299aff505f39f31c59f97bfd920b9 = L.marker(
                [48.702231, 2.486977],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_2515c41499b919da870a80d179ce612b = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_b24299aff505f39f31c59f97bfd920b9.setIcon(icon_2515c41499b919da870a80d179ce612b);
        
    
        var popup_a01a464928944278b4b05229a051eb78 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_a43b1538c20fe5134a912c3b156c1908 = $(`&lt;div id=&quot;html_a43b1538c20fe5134a912c3b156c1908&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ANTICI PASSION&lt;br&gt;121-123 rue gabriel peri&lt;br&gt;brunoy&lt;br&gt;Nombre de candidats:158&lt;/div&gt;`)[0];
            popup_a01a464928944278b4b05229a051eb78.setContent(html_a43b1538c20fe5134a912c3b156c1908);
        

        marker_b24299aff505f39f31c59f97bfd920b9.bindPopup(popup_a01a464928944278b4b05229a051eb78)
        ;

        
    
    
            var marker_9009e94eb66a585510ebca550de91a8e = L.marker(
                [48.694543, 2.504114],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_b0c175263e925be025eeb4f6a3491581 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_9009e94eb66a585510ebca550de91a8e.setIcon(icon_b0c175263e925be025eeb4f6a3491581);
        
    
        var popup_58f7453bfcdb586937f12218e7010d54 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_eabfe9bb1d0c7714b31838a77b69651f = $(`&lt;div id=&quot;html_eabfe9bb1d0c7714b31838a77b69651f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ECF PRO CONDUITE BRUNOY&lt;br&gt;3 boulevard charles de gaulle&lt;br&gt;brunoy&lt;br&gt;Nombre de candidats:228&lt;/div&gt;`)[0];
            popup_58f7453bfcdb586937f12218e7010d54.setContent(html_eabfe9bb1d0c7714b31838a77b69651f);
        

        marker_9009e94eb66a585510ebca550de91a8e.bindPopup(popup_58f7453bfcdb586937f12218e7010d54)
        ;

        
    
    
            var marker_bc207a9990222c1011c8d0356045a92f = L.marker(
                [48.69829, 2.504823],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_e2209ab7c5f2ea01ccf59d47d4215a27 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_bc207a9990222c1011c8d0356045a92f.setIcon(icon_e2209ab7c5f2ea01ccf59d47d4215a27);
        
    
        var popup_d718bcb8722a8f4aae2ad68208d5b748 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_78ba785bc5a9b841f8e4b546acdbde46 = $(`&lt;div id=&quot;html_78ba785bc5a9b841f8e4b546acdbde46&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;IFLR CONDUITE&lt;br&gt;9  rue de la gare&lt;br&gt;brunoy&lt;br&gt;Nombre de candidats:158&lt;/div&gt;`)[0];
            popup_d718bcb8722a8f4aae2ad68208d5b748.setContent(html_78ba785bc5a9b841f8e4b546acdbde46);
        

        marker_bc207a9990222c1011c8d0356045a92f.bindPopup(popup_d718bcb8722a8f4aae2ad68208d5b748)
        ;

        
    
    
            var marker_76721f52be1103a78ef7d044bd536a05 = L.marker(
                [48.689402, 2.494992],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_9c60a8982bf36369107ef09ea86902f4 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_76721f52be1103a78ef7d044bd536a05.setIcon(icon_9c60a8982bf36369107ef09ea86902f4);
        
    
        var popup_4380e6da5f98d1391771d86bece10001 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_fb5f99ed096afeb3a7015a9bda010b80 = $(`&lt;div id=&quot;html_fb5f99ed096afeb3a7015a9bda010b80&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ONE CONDUITE&lt;br&gt;80 avenue du general leclerc&lt;br&gt;brunoy&lt;br&gt;Nombre de candidats:134&lt;/div&gt;`)[0];
            popup_4380e6da5f98d1391771d86bece10001.setContent(html_fb5f99ed096afeb3a7015a9bda010b80);
        

        marker_76721f52be1103a78ef7d044bd536a05.bindPopup(popup_4380e6da5f98d1391771d86bece10001)
        ;

        
    
    
            var marker_0501b5a124b853d7279bcde9a87c1177 = L.marker(
                [48.707702, 2.510359],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_7f7be1a2c940f6e9b4cbc74dd0eb28c6 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_0501b5a124b853d7279bcde9a87c1177.setIcon(icon_7f7be1a2c940f6e9b4cbc74dd0eb28c6);
        
    
        var popup_fb36015e489661c567d827fbe50358e3 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_b9c17f99e28f3b1dac426ca8cc520a60 = $(`&lt;div id=&quot;html_b9c17f99e28f3b1dac426ca8cc520a60&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;SAUVAGEON AUTO ECOLE&lt;br&gt;38 ter rue de villecresnes&lt;br&gt;brunoy&lt;br&gt;Nombre de candidats:73&lt;/div&gt;`)[0];
            popup_fb36015e489661c567d827fbe50358e3.setContent(html_b9c17f99e28f3b1dac426ca8cc520a60);
        

        marker_0501b5a124b853d7279bcde9a87c1177.bindPopup(popup_fb36015e489661c567d827fbe50358e3)
        ;

        
    
    
            var marker_28baa2855c918f1892e032eafe069b5e = L.marker(
                [48.689377, 2.500316],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_dcef7588e7fab136c352a123d4064b7e = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_28baa2855c918f1892e032eafe069b5e.setIcon(icon_dcef7588e7fab136c352a123d4064b7e);
        
    
        var popup_9483a8e8a1fb9e7230a9251f7cb17154 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_55b7a1f58891d067e1eee4ad87c16283 = $(`&lt;div id=&quot;html_55b7a1f58891d067e1eee4ad87c16283&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;TALMA&lt;br&gt;21 rue dupont chaumont&lt;br&gt;brunoy&lt;br&gt;Nombre de candidats:105&lt;/div&gt;`)[0];
            popup_9483a8e8a1fb9e7230a9251f7cb17154.setContent(html_55b7a1f58891d067e1eee4ad87c16283);
        

        marker_28baa2855c918f1892e032eafe069b5e.bindPopup(popup_9483a8e8a1fb9e7230a9251f7cb17154)
        ;

        
    
    
            var marker_bf170eff8e4dec2110f057410c055c41 = L.marker(
                [48.437687, 2.373562],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_f572e78d6bd19461a25a1c8c5b623699 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_bf170eff8e4dec2110f057410c055c41.setIcon(icon_f572e78d6bd19461a25a1c8c5b623699);
        
    
        var popup_9be6fd6039eae7ecfad17af7af571df3 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_eaff225b977d384de64d08b2d6c30940 = $(`&lt;div id=&quot;html_eaff225b977d384de64d08b2d6c30940&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;DU GATINAIS&lt;br&gt;37 bis rue de la ferte alais&lt;br&gt;boutigny sur essonne&lt;br&gt;Nombre de candidats:34&lt;/div&gt;`)[0];
            popup_9be6fd6039eae7ecfad17af7af571df3.setContent(html_eaff225b977d384de64d08b2d6c30940);
        

        marker_bf170eff8e4dec2110f057410c055c41.bindPopup(popup_9be6fd6039eae7ecfad17af7af571df3)
        ;

        
    
    
            var marker_d79bdd589a02542e680236a691b089ff = L.marker(
                [48.566633, 2.483324],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_56630c5c9710234b30039439e0e76b05 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_d79bdd589a02542e680236a691b089ff.setIcon(icon_56630c5c9710234b30039439e0e76b05);
        
    
        var popup_3bc7db89a40fc864061341a1c8ff3225 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_2fcb4d532193347423551bdce4f97ab4 = $(`&lt;div id=&quot;html_2fcb4d532193347423551bdce4f97ab4&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CER COUDRAY MONTCEAUX&lt;br&gt;28/30 av du general de gaulle&lt;br&gt;le coudray montceaux&lt;br&gt;Nombre de candidats:84&lt;/div&gt;`)[0];
            popup_3bc7db89a40fc864061341a1c8ff3225.setContent(html_2fcb4d532193347423551bdce4f97ab4);
        

        marker_d79bdd589a02542e680236a691b089ff.bindPopup(popup_3bc7db89a40fc864061341a1c8ff3225)
        ;

        
    
    
            var marker_3796cd9319be84390d5854e6f911aaa4 = L.marker(
                [48.693712, 2.515185],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_fc4cdb7d8b3069711e79346afac88ba6 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_3796cd9319be84390d5854e6f911aaa4.setIcon(icon_fc4cdb7d8b3069711e79346afac88ba6);
        
    
        var popup_53da802005babb925ec253680419bebc = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_04a7dc5dc1177c724ffd6d01b4ee027a = $(`&lt;div id=&quot;html_04a7dc5dc1177c724ffd6d01b4ee027a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;MAUBOUSSIN AUTO ECOLE&lt;br&gt;25  place du général de gaulle&lt;br&gt;epinay sous senart&lt;br&gt;Nombre de candidats:176&lt;/div&gt;`)[0];
            popup_53da802005babb925ec253680419bebc.setContent(html_04a7dc5dc1177c724ffd6d01b4ee027a);
        

        marker_3796cd9319be84390d5854e6f911aaa4.bindPopup(popup_53da802005babb925ec253680419bebc)
        ;

        
    
    
            var marker_5c1497fceb2e6027ec0eca59ae6f24f5 = L.marker(
                [48.68275, 2.163968],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_f3d75790f4c7f11aa00e905b8b3ffe68 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_5c1497fceb2e6027ec0eca59ae6f24f5.setIcon(icon_f3d75790f4c7f11aa00e905b8b3ffe68);
        
    
        var popup_7c5ca48c4d1c5b7670f255da4e951132 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_bffae901f221b06b4adc3d754b158681 = $(`&lt;div id=&quot;html_bffae901f221b06b4adc3d754b158681&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;CER VALLEE DE CHEVREUSE&lt;br&gt;4 rue de vendee&lt;br&gt;les ulis&lt;br&gt;Nombre de candidats:58&lt;/div&gt;`)[0];
            popup_7c5ca48c4d1c5b7670f255da4e951132.setContent(html_bffae901f221b06b4adc3d754b158681);
        

        marker_5c1497fceb2e6027ec0eca59ae6f24f5.bindPopup(popup_7c5ca48c4d1c5b7670f255da4e951132)
        ;

        
    
    
            var marker_e654cb51cf9e1cc3d340ecf79f9fa39e = L.marker(
                [48.684877, 2.177692],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_6a3cc5e59449e3daa4905c7c4d7a6fe9 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_e654cb51cf9e1cc3d340ecf79f9fa39e.setIcon(icon_6a3cc5e59449e3daa4905c7c4d7a6fe9);
        
    
        var popup_4e7980901ae67b19d7447ed6f07af971 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_9c8cee7d85e76a08497dbcd5981bc5ff = $(`&lt;div id=&quot;html_9c8cee7d85e76a08497dbcd5981bc5ff&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;LA PARISIENNE&lt;br&gt;centre commercial des boutiques&lt;br&gt;les ulis&lt;br&gt;Nombre de candidats:58&lt;/div&gt;`)[0];
            popup_4e7980901ae67b19d7447ed6f07af971.setContent(html_9c8cee7d85e76a08497dbcd5981bc5ff);
        

        marker_e654cb51cf9e1cc3d340ecf79f9fa39e.bindPopup(popup_4e7980901ae67b19d7447ed6f07af971)
        ;

        
    
    
            var marker_0ac76b3da2123f86cb60d52d67144e32 = L.marker(
                [48.684877, 2.177692],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_1625dc328ac01bfc5b7b1845537b7fb7 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_0ac76b3da2123f86cb60d52d67144e32.setIcon(icon_1625dc328ac01bfc5b7b1845537b7fb7);
        
    
        var popup_d52946ee0fb909ca16e785aeb5d6df30 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_8ac7b397f4cf14b9b24972a15d7d69aa = $(`&lt;div id=&quot;html_8ac7b397f4cf14b9b24972a15d7d69aa&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;LA PARISIENNE AUTO ECOLE&lt;br&gt;centre commercial les boutiques&lt;br&gt;les ulis&lt;br&gt;Nombre de candidats:89&lt;/div&gt;`)[0];
            popup_d52946ee0fb909ca16e785aeb5d6df30.setContent(html_8ac7b397f4cf14b9b24972a15d7d69aa);
        

        marker_0ac76b3da2123f86cb60d52d67144e32.bindPopup(popup_d52946ee0fb909ca16e785aeb5d6df30)
        ;

        
    
    
            var marker_11d285034c186c5ad6e773198687f7bc = L.marker(
                [48.682193, 2.169415],
                {}
            ).addTo(map_e702c6a9dd177ded27b22e0aa262378e);
        
    
            var icon_b0308eea3997bb28063b606089c1edc8 = L.AwesomeMarkers.icon(
                {&quot;extraClasses&quot;: &quot;fa-rotate-0&quot;, &quot;icon&quot;: &quot;car&quot;, &quot;iconColor&quot;: &quot;white&quot;, &quot;markerColor&quot;: &quot;blue&quot;, &quot;prefix&quot;: &quot;fa&quot;}
            );
            marker_11d285034c186c5ad6e773198687f7bc.setIcon(icon_b0308eea3997bb28063b606089c1edc8);
        
    
        var popup_424d135c09cd41580452a331bae5a4eb = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});

        
            var html_059e0b3254f144627efa0d3043669896 = $(`&lt;div id=&quot;html_059e0b3254f144627efa0d3043669896&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;LES ULIS AUTO ECOLE&lt;br&gt;1 rue du morvan&lt;br&gt;les ulis&lt;br&gt;Nombre de candidats:348&lt;/div&gt;`)[0];
            popup_424d135c09cd41580452a331bae5a4eb.setContent(html_059e0b3254f144627efa0d3043669896);
        

        marker_11d285034c186c5ad6e773198687f7bc.bindPopup(popup_424d135c09cd41580452a331bae5a4eb)
        ;

        
    
    
            map_e702c6a9dd177ded27b22e0aa262378e.fitBounds(
                [[48.707787, 2.240003], [48.731966, 2.288707]],
                {}
            );
        
&lt;/script&gt;" style="position:absolute;width:100%;height:100%;left:0;top:0;border:none !important;" allowfullscreen webkitallowfullscreen mozallowfullscreen></iframe></div></div>

{{< /rawhtml >}}

Vous pouvez aller plus loin avec l'exercice suivant

{{% box status="exercise" title="Exercise" icon="fas fa-pencil-alt" %}}

**Quelles sont les auto-écoles les plus proches de chez moi ?**

On va supposer que vous cherchez, dans un rayon donné autour d'un centre ville,
les auto-écoles disponibles.

:one: Pour commencer, utiliser l'[API geo](https://geo.api.gouv.fr/decoupage-administratif)

:two: Voici une fonction pour créer un cercle autour d'un point (source [ici](https://gis.stackexchange.com/questions/289044/creating-buffer-circle-x-kilometers-from-point-using-python/289923))

``` python
from functools import partial
import pyproj
from shapely.ops import transform
from shapely.geometry import Point

proj_wgs84 = pyproj.Proj('+proj=longlat +datum=WGS84')


def geodesic_point_buffer(lat, lon, km):
    # Azimuthal equidistant projection
    aeqd_proj = '+proj=aeqd +lat_0={lat} +lon_0={lon} +x_0=0 +y_0=0'
    project = partial(
        pyproj.transform,
        pyproj.Proj(aeqd_proj.format(lat=lat, lon=lon)),
        proj_wgs84)
    buf = Point(0, 0).buffer(km * 1000)  # distance in metres
    return transform(project, buf).exterior.coords[:]
```

L'appliquer au centre ville de Palaiseau

:three: Pour se convaincre, on peut représenter une carte

``` python
import matplotlib.pyplot as plt
import contextily as ctx

fig,ax = plt.subplots(figsize=(10, 10))
circle.to_crs("EPSG:3857").plot(ax = ax, color = 'red')
pal.to_crs("EPSG:3857").plot(ax = ax, color = 'green')
ctx.add_basemap(ax, source = ctx.providers.Stamen.Toner)
ax
```

    <AxesSubplot:>

<img src="index_files/figure-gfm/cell-31-output-2.png" width="789" height="780" />

On a bien un cercle centré autour de Palaiseau:

![](map_buffer.png)

3.  *To be continued*: améliorer la constitutoin du cercle puis merge spatial

{{% /box %}}

# Exercices supplémentaires

{{% box status="exercise" title="Exercise" icon="fas fa-pencil-alt" %}}

**Exercice 2 : Retrouver des produits dans l'openfood facts :pizza:**

Voici une liste de code-barres:
`3274080005003,  5449000000996, 8002270014901, 3228857000906, 3017620421006, 8712100325953`

Utiliser l'[API d'openfoodfacts](https://world.openfoodfacts.org/data)
(l'API, pas depuis le CSV !)
pour retrouver les produits correspondant
et leurs caractéristiques nutritionnelles.

Le panier paraît-il équilibré ? :chocolate_bar:

Pour vous aidez, vous pouvez regarder une exemple de structure du json ici : https://world.openfoodfacts.org/api/v0/product/3274080005003.json en particulier la catégorie `nutriments`.

Récupérer l'URL d'une des images et l'afficher dans votre navigateur. Par exemple,
celle-ci:

![](https://images.openfoodfacts.org/images/products/544/900/000/0996/front_en.596.200.jpg)

{{% /box %}}

[^1]: Le JSON est un format très apprécié dans le domaine du *big data*
    car il permet de stocker de manière intelligente des données
    de structures diverses. Il
    s'agit d'un des formats privilégiés du paradigme No-SQL pour lequel
    cet [excellent cours](http://b3d.bdpedia.fr/) propose plus de détails

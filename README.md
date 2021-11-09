# Web des données : Sénateurs de la Cinquième République

Ce répertoire comprend les fichiers sur lesquels nous travaillons pour fournir un graphe de connaissances sur les sénateurs.

## Sources des informations

Nos données viennent principalement de trois tableaux C.S.V., disponibles sur la [Plateforme des données ouvertes du Sénat](https://data.senat.fr/les-senateurs/) :

  — [`ODSEN_GENERAL.csv`](./csv/ODSEN_GENERAL.csv) fournit les données du fichier [`général.ttl`](./ttl/général.ttl) : nom de chaque sénateur, appartenance actuelle au Sénat, dates de naissance et de décès, commission au Sénat, circonscription, catégorie socio-professionnelle, métier.

  — [`ODSEN_ELUSEN.csv`](./csv/ODSEN_ELUSEN.csv) est transcrit dans [`éluSén.ttl`](./ttl/éluSén.ttl), qui donne le début et la fin de chaque mandat sénatorial.

  — [`ODSEN_HISTOGROUPES.csv`](./csv/ODSEN_HISTOGROUPES.csv) permet de remplir [`histoGroupes.ttl`](./ttl/histoGroupes.ttl), fournissant les dates de début et de fin d’appartenance de chaque sénateur à des groupes politiques.

Les informations contenues dans [`circonscriptions.ttl`](./ttl/circonscriptions.ttl) et dans [`groupes.ttl`](./ttl/groupes.ttl), qui permettent de retrouver respectivement le nom de chaque circonscription, et le nom et les valeurs politiques de chaque groupe, ont été remplies à l’aide de Wikipédia et de nos connaissances personnelles.

## Transformation des données

Les données des trois tableaux cités ont été extraites et transformées en triplets Turtle à l’aide de l’outil [TARQL](https://github.com/tarql/tarql) et des fichiers SPARQL présents dans le dossier [`sparql`](./sparql). Pour les fichiers `groupes.ttl` et `circonscriptions.ttl`, les fichiers SPARQL correspondant ont permis de créer une base, mais de nombreuses informations ont été ajoutées à la main.

Les fichiers Turtle ainsi formés permettent de créer une base de connaissances que l’on peut interroger en SPARQL.

## Exemples de requêtes

Le fichier [`exemples.rq`](./exemples.rq) contient une série de requêtes en SPARQL à exécuter sur la base de connaissances formées par les fichiers Turtle du dépôt, chacun de ces fichiers constituant un graphe nommé. Par exemple, la requête suivante renvoie la liste des sénateurs en fonction.

```tarql
PREFIX custom: <https://github.com/Ajamelot56/Dana-Senateurs/>
PREFIX schema: <http://schema.org/>

SELECT ?subject
FROM custom:general
WHERE {
  ?subject custom:actif true
}
```
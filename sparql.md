<a id="top"></a>
## Table of Contents ##
* [Meta](#meta)
  * [Classes by Provider](#classes-provider)
  * [Other Classes by Provider](#other-classes-provider)
  * [Properties by Provider](#properties-provider)
  * [Other Properties by Provider](#other-properties-provider)
  * [Properties by Count](#properties-count)
* [Vocabulary](#vocabulary)
* [Organization](#organization)
  * [Logo](#resource-logo)
* [Dataset](#dataset)
  * [License](#dataset-license)
<hr/>

<a id="meta"></a>
## Meta ##

<a id="classes-provider"></a>
### Classes by Provider ###
```
SELECT DISTINCT ?graph ?class
WHERE {
  GRAPH ?graph {
    ?s a ?class
  }
  FILTER (?graph != <http://www.w3.org/2002/07/owl#>)
  FILTER (?graph != <http://www.openlinksw.com/schemas/virtrdf#>)
  FILTER (?graph != <http://localhost:8890/sparql>)
  FILTER (?graph != <http://geolink>)
}
ORDER BY ?graph ?class
```
w. COUNT
```
SELECT DISTINCT ?graph ?class COUNT(?class) as ?instances
WHERE {
  GRAPH ?graph {
    ?s a ?class
  }
  FILTER (?graph != <http://www.w3.org/2002/07/owl#>)
  FILTER (?graph != <http://www.openlinksw.com/schemas/virtrdf#>)
  FILTER (?graph != <http://localhost:8890/sparql>)
  FILTER (?graph != <http://geolink>)
}
ORDER BY ?graph ?class
```
<a id="other-classes-provider"></a>
### Other Classes by Provider ###
```
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?graph ?class
WHERE {
  GRAPH ?graph {
    ?s schema:additionalType ?class
  }
  FILTER (?graph != <http://www.w3.org/2002/07/owl#>)
  FILTER (?graph != <http://www.openlinksw.com/schemas/virtrdf#>)
  FILTER (?graph != <http://localhost:8890/sparql>)
  FILTER (?graph != <http://geolink>)
}
ORDER BY ?graph ?class
```
w. COUNT
```
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?graph ?class COUNT(?class) AS ?instances
WHERE {
  GRAPH ?graph {
    ?s schema:additionalType ?class
  }
  FILTER (?graph != <http://www.w3.org/2002/07/owl#>)
  FILTER (?graph != <http://www.openlinksw.com/schemas/virtrdf#>)
  FILTER (?graph != <http://localhost:8890/sparql>)
  FILTER (?graph != <http://geolink>)
}
ORDER BY ?graph ?class
```

<a id="properties-provider"></a>
### Properties by Provider ###
```
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?graph ?class ?property
WHERE {
  GRAPH ?graph {
    ?s a ?class .
    ?s ?property ?o
  }
  FILTER (?graph != <http://www.w3.org/2002/07/owl#>)
  FILTER (?graph != <http://www.openlinksw.com/schemas/virtrdf#>)
  FILTER (?graph != <http://localhost:8890/sparql>)
  FILTER (?graph != <http://geolink>)
  FILTER (?property != <http://www.w3.org/2000/01/rdf-schema#seeAlso>)
  FILTER (?property != <http://www.w3.org/1999/02/22-rdf-syntax-ns#type>)
  FILTER (REGEX(?property, "http://schema.org", "i"))
}
ORDER BY ?graph ?class ?property
```

<a id="other-properties-provider"></a>
### Other Properties by Provider ###
```
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?graph ?class ?property
WHERE {
  GRAPH ?graph {
    ?s a ?class .
    ?s ?property ?o
  }
  FILTER (?graph != <http://www.w3.org/2002/07/owl#>)
  FILTER (?graph != <http://www.openlinksw.com/schemas/virtrdf#>)
  FILTER (?graph != <http://localhost:8890/sparql>)
  FILTER (?graph != <http://geolink>)
  FILTER (?property != <http://www.w3.org/2000/01/rdf-schema#seeAlso>)
  FILTER (?property != <http://www.w3.org/1999/02/22-rdf-syntax-ns#type>)
  FILTER (!REGEX(?property, "http://schema.org", "i"))
}
ORDER BY ?graph ?class ?property
```
<a id="properties-count"></a>
### Properties by Count ###
```
SELECT ?property (COUNT(*) AS ?used) 
WHERE {
  GRAPH ?graph {
    ?s ?property ?o .
    FILTER (?graph != <http://www.w3.org/2002/07/owl#>)
    FILTER (?graph != <http://www.openlinksw.com/schemas/virtrdf#>)
    FILTER (?graph != <http://localhost:8890/sparql>)
    FILTER (?graph != <http://geolink>)
  }
} GROUP BY ?property ORDER BY DESC(?used)
```
<a id="vocabulary"></a>
## Vocabulary ##

<a id="organization"></a>
## Organization ##
### Logo ###
```
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?graph ?logo_url
WHERE {
  GRAPH ?graph {
    ?resource rdf:type schema:Organization .
    ?resource schema:logo [ schema:url ?logo_url ] .
  }
}
ORDER BY ?graph
```
<a id="dataset"></a>
## Dataset ##

<a id="dataset-license"></a>
### License ###
```
SELECT DISTINCT ?graph ?license ?class
WHERE { 
  GRAPH ?graph { 
    ?s <http://schema.org/license> ?license .
    OPTIONAL { ?s a ?class }
  }
}
```
### License Count by Provider ###
```
SELECT DISTINCT ?graph COUNT(DISTINCT ?s) as ?number_of_licenses
WHERE { 
  GRAPH ?graph { 
    ?s <http://schema.org/license> ?license .
  }
} 
ORDER BY DESC(?number_of_licenses)
```


Back to [Top](#top)

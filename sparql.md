<a id="top"></a>
## Table of Contents ##
* [Meta](#meta)
  * [Triple Count](#triple-count)
  * [Entity Count](#entity-count)
  * [Distinct Resource URI Count](#resource-count)
  * [Classes by Provider](#classes-provider)
  * [Other Classes by Provider](#other-classes-provider)
  * [Properties by Provider](#properties-provider)
  * [Other Properties by Provider](#other-properties-provider)
  * [Properties by Count](#properties-count)
* [Vocabulary](#vocabulary)
  * [Identifier Count](#vocab-identifier-count)
* [Organization](#organization)
  * [Logo](#resource-logo)
* [Dataset](#dataset)
  * [License](#dataset-license)
  * [Identifier Type](#identifier-type)
  * [Identifier Scheme(#identifier-scheme)
<hr/>

<a id="meta"></a>
## Meta ##

<a id="triple-count"></a>
### Triple Count ###
```
SELECT (COUNT(*) AS ?triple_count) 
WHERE { 
  GRAPH ?graph { ?s ?p ?o } 
  FILTER (?graph != <http://www.w3.org/2002/07/owl#>)
  FILTER (?graph != <http://www.openlinksw.com/schemas/virtrdf#>)
  FILTER (?graph != <http://localhost:8890/sparql>)
  FILTER (?graph != <http://geolink>)
  FILTER (?graph != <http://www.w3.org/ns/ldp#>)
  FILTER (?graph != <http://localhost:8890/DAV/>)
} 
```
### Triple Count by Provider ###
```
SELECT DISTINCT ?graph COUNT(?s) as ?num_triples 
WHERE { 
  GRAPH ?graph { ?s ?p ?o } 
  FILTER (?graph != <http://www.w3.org/2002/07/owl#>)
  FILTER (?graph != <http://www.openlinksw.com/schemas/virtrdf#>)
  FILTER (?graph != <http://localhost:8890/sparql>)
  FILTER (?graph != <http://geolink>)
  FILTER (?graph != <http://www.w3.org/ns/ldp#>)
  FILTER (?graph != <http://localhost:8890/DAV/>)
} 
ORDER BY DESC(?num_triples)
```

<a id="entity-count"></a>
### Entity Count ###
```
SELECT (COUNT(*) AS ?entity_count) 
WHERE { 
  GRAPH ?graph { ?s a [] } 
  FILTER (?graph != <http://www.w3.org/2002/07/owl#>)
  FILTER (?graph != <http://www.openlinksw.com/schemas/virtrdf#>)
  FILTER (?graph != <http://localhost:8890/sparql>)
  FILTER (?graph != <http://geolink>)
  FILTER (?graph != <http://www.w3.org/ns/ldp#>)
  FILTER (?graph != <http://localhost:8890/DAV/>)
} 
```
### Entity Count by Provider ###
```
SELECT DISTINCT ?graph (COUNT(*) AS ?entity_count)
WHERE { 
  GRAPH ?graph { ?s a [] } 
  FILTER (?graph != <http://www.w3.org/2002/07/owl#>)
  FILTER (?graph != <http://www.openlinksw.com/schemas/virtrdf#>)
  FILTER (?graph != <http://localhost:8890/sparql>)
  FILTER (?graph != <http://geolink>)
  FILTER (?graph != <http://www.w3.org/ns/ldp#>)
  FILTER (?graph != <http://localhost:8890/DAV/>)
} ORDER BY DESC(?entity_count)
```

<a id="resource-count"></a>
### Distinct Resource URI Count ###
```
SELECT (COUNT(DISTINCT ?s ) AS ?resource_count)
WHERE { 
  GRAPH ?graph { { ?s ?p ?o  } UNION { ?o ?p ?s } FILTER(!isBlank(?s) && !isLiteral(?s)) } 
  FILTER (?graph != <http://www.w3.org/2002/07/owl#>)
  FILTER (?graph != <http://www.openlinksw.com/schemas/virtrdf#>)
  FILTER (?graph != <http://localhost:8890/sparql>)
  FILTER (?graph != <http://geolink>)
  FILTER (?graph != <http://www.w3.org/ns/ldp#>)
  FILTER (?graph != <http://localhost:8890/DAV/>)
} ORDER BY DESC(?resource_count)
```
### Distinct Resource URI Count by Provider###
```
SELECT DISTINCT ?graph (COUNT(DISTINCT ?s ) AS ?resource_count)
WHERE { 
  GRAPH ?graph { { ?s ?p ?o  } UNION { ?o ?p ?s } FILTER(!isBlank(?s) && !isLiteral(?s)) } 
  FILTER (?graph != <http://www.w3.org/2002/07/owl#>)
  FILTER (?graph != <http://www.openlinksw.com/schemas/virtrdf#>)
  FILTER (?graph != <http://localhost:8890/sparql>)
  FILTER (?graph != <http://geolink>)
  FILTER (?graph != <http://www.w3.org/ns/ldp#>)
  FILTER (?graph != <http://localhost:8890/DAV/>)
} ORDER BY DESC(?resource_count)
```

<a id="class-instance-count"></a>
### Class Instance Count ###
```
SELECT ?class (COUNT(?s) AS ?count )
WHERE { 
  GRAPH ?graph { ?s a ?class } 
  FILTER (?graph != <http://www.w3.org/2002/07/owl#>)
  FILTER (?graph != <http://www.openlinksw.com/schemas/virtrdf#>)
  FILTER (?graph != <http://localhost:8890/sparql>)
  FILTER (?graph != <http://geolink>)
  FILTER (?graph != <http://www.w3.org/ns/ldp#>)
  FILTER (?graph != <http://localhost:8890/DAV/>)
} GROUP BY ?class ORDER BY DESC(?count)
```
### Class Instance Count by Provider ###


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

<a id="vocab-identifier-count"></a>
### Schema.org Identifier Count ###
```
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?graph ?class ?id_scheme COUNT(?identifier) as ?identifier_count
WHERE { 
  GRAPH ?graph { 
   ?s a ?class .
   ?s schema:identifier ?identifier .
   ?identifier schema:propertyID ?id_scheme .
  }
} 
GROUP BY ?graph ?class ?id_scheme
ORDER BY ?identifier_count
```

### ORCID Count by Provider ###
```
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?g COUNT(DISTINCT ?s) as ?orcids

WHERE { 
  GRAPH ?g {
   ?s ?p ?o
   FILTER REGEX(str(?s), "orcid.org", "i")
  }
} 
```

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

<a id="identifier-type"></a>
### Identifier Type ###
```
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?graph ?class IF(isLiteral(?identifier), "literal", "resource") as ?id_type
WHERE { 
  GRAPH ?graph { 
   ?s a schema:Dataset .
   ?s schema:identifier ?identifier .
   OPTIONAL { ?s a ?class } 
   FILTER (?graph != <http://www.w3.org/2002/07/owl#>)
   FILTER (?graph != <http://www.openlinksw.com/schemas/virtrdf#>)
   FILTER (?graph != <http://localhost:8890/sparql>)
   FILTER (?graph != <http://geolink>)
   FILTER (?graph != <http://www.w3.org/ns/ldp#>)
   FILTER (?graph != <http://localhost:8890/DAV/>)
  }
} 
```

<a id="identifier-scheme"></a>
### Identifier Scheme ###
```
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?graph ?id_scheme
WHERE { 
  GRAPH ?graph { 
   ?s a schema:Dataset .
   ?s schema:identifier ?identifier .
   ?identifier schema:propertyID ?id_scheme .
  }
} 
```

Back to [Top](#top)

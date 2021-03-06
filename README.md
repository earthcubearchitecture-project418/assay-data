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
  * [Identifier in schema:url](#vocab-identifier-url)
  * [ORCID Count by Provider](#vocab-orcid-count-provider)
  * [PropertyValue by Predicate](#vocab-propertyvalue-predicate)
* [Organization](#organization)
  * [Logo](#resource-logo)
  * [Potential Action Endpoints](#org-potential-action)
* [Dataset](#dataset)
  * [License](#dataset-license)
  * [Authors](#dataset-authors)
  * [Identifier Usage](#identifier)
  * [Identifier Scheme](#identifier-scheme)
  * [VariableMeasured Usage](#dataset-variable)
  * [Funder](#dataset-funder)
  * [Distributions](#dataset-distribution)
  * [Spatial](#dataset-spatial)
  * [Temporal](#dataset-temporal)
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

<a id="vocab-identifier-url"></a>
### Identifiers found through schema:url ###
```
PREFIX schema: <http://schema.org/>
SELECT ?graph ?propertyID COUNT (?propertyID) as ?property_id_by_url_count
WHERE { 
  GRAPH ?graph { 
    ?s a schema:PropertyValue . 
    ?o schema:url ?s .
    OPTIONAL { ?s schema:propertyID ?propertyID . }
  } 
  FILTER (?graph != <http://www.w3.org/2002/07/owl#>)
  FILTER (?graph != <http://www.openlinksw.com/schemas/virtrdf#>)
  FILTER (?graph != <http://localhost:8890/sparql>)
  FILTER (?graph != <http://geolink>)
  FILTER (?graph != <http://www.w3.org/ns/ldp#>)
  FILTER (?graph != <http://localhost:8890/DAV/>)
} 
ORDER BY ?graph ?propertyID
```

<a id="vocab-orcid-count-provider"></a>
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

<a id="vocab-propertyvalue-predicate"></a>
### PropertyValue by Predicate ###
```
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?p
#(COUNT(?class) AS ?class_count) 
WHERE { 
  GRAPH ?graph { 
    ?s a schema:PropertyValue . ?o ?p ?s . 
    OPTIONAL { ?o a ?class . }
    OPTIONAL { ?o schema:additionalType ?type }
  } 
  FILTER (?graph != <http://www.w3.org/2002/07/owl#>)
  FILTER (?graph != <http://www.openlinksw.com/schemas/virtrdf#>)
  FILTER (?graph != <http://localhost:8890/sparql>)
  FILTER (?graph != <http://geolink>)
  FILTER (?graph != <http://www.w3.org/ns/ldp#>)
  FILTER (?graph != <http://localhost:8890/DAV/>)
} 
ORDER BY ?graph ?class ?type ?p
#ORDER BY DESC(?class_count)
```

### PropertyValue by Predicate Count ###
```
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?p (COUNT(?s) AS ?count) 
WHERE { 
  GRAPH ?graph { 
    ?s a schema:PropertyValue . ?o ?p ?s . 
    OPTIONAL { ?o a ?class . }
    OPTIONAL { ?o schema:additionalType ?type }
  } 
  FILTER (?graph != <http://www.w3.org/2002/07/owl#>)
  FILTER (?graph != <http://www.openlinksw.com/schemas/virtrdf#>)
  FILTER (?graph != <http://localhost:8890/sparql>)
  FILTER (?graph != <http://geolink>)
  FILTER (?graph != <http://www.w3.org/ns/ldp#>)
  FILTER (?graph != <http://localhost:8890/DAV/>)
} 
ORDER BY DESC(?count)
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

<a id="org-potential-action"></a>
### Organization Potential Action Endpoints ###
```
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?g ?class IF(?url_template, ?url_template, ?target) as ?action_url ?p ?o
WHERE { 
  GRAPH ?g {
    ?s schema:potentialAction ?action .
    ?s a ?class . 
    OPTIONAL { 
      FILTER NOT EXISTS { ?action rdf:type ?o }
      FILTER NOT EXISTS { ?action rdfs:seeAlso ?o }
      OPTIONAL { 
        ?action schema:target ?target . 
        OPTIONAL { 
          ?target a schema:EntryPoint . 
          ?target schema:urlTemplate ?url_template .
          ?target ?p ?o
        }
      }
      OPTIONAL { 
        ?action schema:query-input ?query_input . 
      }
    }
  }
}
ORDER BY ?g ?class ?action_url ?query_input
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

<a id="dataset-authors"></a>
### Authors ###
```
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?g ?role IF(BOUND(?role_type), ?role_type, ?person_type) as ?type
WHERE { 
  VALUES ?role { schema:creator schema:contributor schema:author }
  GRAPH ?g {
    ?s a schema:Dataset .
    ?s ?role ?author .
    ?author a ?person_type .
    OPTIONAL {
      ?author a schema:Role .
      ?author ?role [ rdf:type ?role_type ] .
    }
  }
}
ORDER BY ?g
```

<a id="identifier"></a>
### Identifier Usage ###
```
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?graph ?class IF(isLiteral(?identifier), "literal", "resource") as ?id_type
WHERE { 
  GRAPH ?graph { 
   ?s a schema:Dataset .
   ?s schema:identifier ?identifier .
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

<a id="dataset-funder"></a>
### Funder ###
```
PREFIX schema: <http://schema.org/>
PREFIX gdx: <https://geodex.org/voc/>
SELECT DISTINCT ?g
WHERE { 
  GRAPH ?g {
    ?s a schema:Dataset .
    ?s schema:funder ?funder
  }
}
ORDER BY ?g
```

<a id="dataset-variable"></a>
### VariableMeasured Usage ###
```
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?g
WHERE { 
  GRAPH ?g {
   ?s a schema:Dataset .
   ?s schema:variableMeasured ?var .
  }
} 
ORDER BY ?g
```

<a id="dataset-distribution"></a>
### Distribution Usage ###
```
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?g
WHERE { 
  GRAPH ?g {
   ?s a schema:Dataset .
   ?s schema:distribution ?distro .
  }
} 
ORDER BY ?g
```

### Distribution Properties by Provider ###
```
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?g ?p
WHERE { 
  GRAPH ?g {
   ?s a schema:Dataset .
   ?s schema:distribution ?distro .
   OPTIONAL { 
     ?distro ?p ?o 
     FILTER NOT EXISTS { ?distro rdfs:seeAlso ?o }
   }
  }
} 
ORDER BY ?g ?p
```
### Distribution properties by popularity ###
```
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?p COUNT(DISTINCT ?g) as ?num_providers
WHERE { 
  GRAPH ?g {
   ?s a schema:Dataset .
   ?s schema:distribution ?distro .
   OPTIONAL { 
     ?distro ?p ?o 
     FILTER NOT EXISTS { ?distro rdfs:seeAlso ?o }
   }
  }
} 
GROUP BY ?p
ORDER BY DESC(?num_providers)
```

<a id="dataset-spatial"></a>
### Spatial Coverage ###
```
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?g COUNT(?spatial_coverage) as ?num_coverages
WHERE { 
  GRAPH ?g {
    ?s a schema:Dataset .
    ?s schema:spatialCoverage ?spatial_coverage .
  }
}
ORDER BY ?g
```

<a id="dataset-temporal"></a>
### Temporal Coverage ###
```
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?g COUNT(?temporal_coverage) as ?num_coverages
WHERE { 
  GRAPH ?g {
    ?s a schema:Dataset .
    ?s schema:temporalCoverage ?temporal_coverage .
  }
}
ORDER BY ?g
```

Back to [Top](#top)

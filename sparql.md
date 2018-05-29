<a id="top"></a>
## Table of Contents ##
* [Organization](#organization)
  * [Logo](#resource-logo)
* [Dataset](#dataset)
<hr/>

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

Back to [Top](#top)

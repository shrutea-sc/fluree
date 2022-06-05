# Fluree Query
## Basic Query
### Select Key
The select-array can include any combination of the following items in any order.An *:
,Predicate Names: Namespaced or Not
,A map, crawling the graph.
,Reversely-referenced Predicates
or A map with sub-select options
### From key
A from key is used where your select options are applied to the field.
``` json
{
  "select": ["*", { "chat/_person": ["*", { "_as": "chperson" }] }],
  "from": [87960930223082, ["person/handle", "jdoe"]]
}
```
## Analytical Query
``` json

```

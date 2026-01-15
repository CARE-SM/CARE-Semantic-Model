# CARE-SM Schema

## SKOS

File: [care-sm.skos](https://github.com/CARE-SM/CARE-Semantic-Model/tree/main/schema/care-sm.skos)

CARE-SM contains its own w3id identifiers to describe each of its data model representations. Using SKOS (Simple Knowledge Organization System), these identifiers are linked to a description and to the CARE-SM documentation page that describes each data model.

## RDF-Quad Validation

File: [schema.sparql](https://github.com/CARE-SM/CARE-Semantic-Model/tree/main/schema/schema.sparql)

CARE-SM uses **pure SPARQL** to validate the RDF-Quads representation of CARE-SM. This approach is used to ensure full control and compatibility with RDF named graphs, since ShEx and SHACL representations cannot be used to validate RDF Quads.

The validation query uses `FILTER NOT EXISTS` to detect violations by checking for the absence of required triples. If the result set is empty, the dataset is considered valid.
# RDF-Quad Validation using SPARQL

This project uses **pure SPARQL queries** to validate RDF-Quads data. Traditional. To ensure full control and compatibility with RDF named graphs (i.e., quads).

## How It Works

- The query uses `FILTER NOT EXISTS` to find violations by checking the absence of required triples.
- If the result set is empty, the dataset is considered valid.

The main validation is stored [here](https://github.com/CARE-SM/CARE-Semantic-Model/tree/main/schema/care-sm.ttl)

# ct413-final-year-project
CT413 Final Year Project: Using LLMS to infer relationships from online discussion of Irish traditional music 

KG hosted at https://michael-mccurtin.github.io/ct413-final-year-project/kg/trad_kg.ttl

# How to deploy via Blazegraph:
1. Download .ttl file [here](https://github.com/michael-mccurtin/ct413-final-year-project/blob/main/kg/trad_kg.ttl)
2. Pull docker image:
```sh
docker pull lyrasis/blazegraph
```
3. Build and run docker image:
```sh
docker build -t blazegraph:2.1.5 2.1.5/
docker run --name blazegraph -d -p 8889:8080 blazegraph:2.1.5
```
4. Upload .ttl file: [http://localhost:8889/bigdata/#update](http://localhost:8889/bigdata/#update)
5. SPARQL endpoint available at [http://localhost:8889/bigdata/#query](http://localhost:8889/bigdata/#query)

# Sample query:
The following query will select all tunes *composed by* Turlough O’Carolan:
```sparql
PREFIX fyp: <https://michael-mccurtin.github.io/ct413-final-year-project/fyp-ontology#>
SELECT (SAMPLE(?subjectDescription) AS ?tuneName)
WHERE {
    {
        ?subject fyp:composedBy ?object .
        ?object fyp:description "Turlough O’Carolan"^^xsd:string .
    }

    ?subject fyp:description ?subjectDescription .
}
GROUP BY LCASE(STR(?subjectDescription))
```
It will return the following:

![image](https://github.com/user-attachments/assets/9e6abbbc-18a3-4080-97ba-ac91060d874a)

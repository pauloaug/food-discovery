
# Food Discovery

Food Discovery using a Knowledge Base.

This example shows how to use semantic web technologies (OWL ontology and RDF data) to get inferences about restaurants menus and food.

Inspired by this [Uber Engineering Blog post](https://eng.uber.com/uber-eats-query-understanding/).

Schema.org is an ontology that helps websites to enrich the data, so it can be easier to find.

  Schema.org is a collaborative, community activity with a mission to create, maintain, and promote schemas for structured data on the Internet, on web pages, in email messages, and beyond.

We can reuse this concepts already defined at Schema.org to model our food and restaurant domain, in order to get rich queries and inferences.

StarDog provides an HTTP REST API and a CLI to send SPARQL queries to the graph database.
It also has a [built-in](https://www.stardog.com/docs/#_graphql_queries) [GraphQL](https://graphql.org/learn/) HTTP interface.
So, we can send a GraphQL request, like:
  stardog graphql mySpatialDb2 "{ Dish { name }}"
and get as a response:
```
  {
  "data" : [ {
    "name" : "sushi"
  }, {
    "name" : "feijoada"
  }, {
    "name" : "ceviche"
  } ]
}
```

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

1. [Install StarDog DB and license key](https://www.stardog.com/docs/#_introduction) according to the documentation.

2. Start the StarDog server:

  stardog-admin server start

2. Create the graph database in your terminal:

  stardog-admin db create -o spatial.enabled=true -n mySpatialDb2 example1.ttl

3. In your terminal, run the following CLI commands to get the response of the queries to the database:

 

### Query 1
Select Restaurants that has 'bean' as an ingredient in the menu.

   stardog query --reasoning mySpatialDb2 query1.rq

```
SELECT ?restaurant {
  ?restaurant schema:hasMenu/schema:hasMenuItem/schema:ingredients :bean.
}```

### Query 2
What kind of Cuisines each restaurant serves?

  stardog query --reasoning mySpatialDb2 query2.rq

```
SELECT ?restaurant ?cuisine{
  ?restaurant schema:servesCuisine ?cuisine.
}```


### Prerequisites

- StarDog DB


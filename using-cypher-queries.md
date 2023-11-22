# Using Cypher Queries on Example Graph Database

Click on the left-side top vertical menu icon to see the database information such as `Node labels` and `Relationship types`. You can also see the Property Keys and other DBMS information as shown in the image below.

Let’s execute a few Cypher commands to play with Neo4j graph database. 

1. Display the the graph schema visualization of this example movie database as: 

```
Call db.schema.visualization
```

It shows us `What is related, and how`
We will get following output:

![db_schema_visualization](./images/db-schema-visualization.png)



We can also use the command `:schema` to display constraints and indexes


2. Let’s count the `number of nodes` in movie database. Execute the following query:

```
MATCH ()
RETURN count(*) as count
```

**Note:** you can write the command in one line as given below:

```
MATCH () RETURN count(*) as count
```

And we get the output count `169`

![nodes-count](./images/nodes-count.png)


3. Count all the nodes with label `Movie` and  `Person` 

![Movie-and-Person-node-count](./images/Movie-and-Person-node-count.png)

Output for Movie node count is `38` and Person node count is `131`

4. Count all the relationships

```
MATCH ()-[r]->()
RETURN count(r) as count
```

This command can also be written as:
```sql
MATCH ()-->() RETURN count(*);
```

Output is `250`

![relationship-count](./images/relationships-count.png)


5. Find the count of number of relationship where the relationship type is `ACTED_IN`


```
MATCH ()-[r:ACTED_IN]->()
RETURN count(r) as count
```

Output is `172`

![ACTED_IN_relationship-count](./images/ACTED_IN_relationship-count.png)


Count relationships of multiple types like,


6. Count the total number of relationship where relationship type name is `ACTED_IN OR DIRECTED`

```
MATCH ()-[r:ACTED_IN|DIRECTED]->()
RETURN count(r) as count
```

Output is : `216`

![ACTED_IN_OR_DIRECTED_relationship-count](images/ACTED_IN_OR_DIRECTED_relationship-count.png)


7. Let’s count the relationship type with node labels. For example, count all the nodes with label `Person` with relationship type `ACTED_IN`
   
```
MATCH (:Person)-[r:ACTED_IN]->()
RETURN count(r) as count
```

Output is `172`

![Person-node-ACTED_IN-relationships](images/Person-node-ACTED_IN-relationships.png)

---
---

## Pattern Match    

```sql
MATCH p=()-[:ACTED_IN]->() RETURN p LIMIT 25;
```

## Node Creation

```sql
create (:Person {name:"Faaiz"})
```

## Relationship Creation

```sql
MATCH (p:Person), (m:Movie)
WHERE a.name = 'Faaiz' AND m.title = 'The Matrix'
CREATE (p)-[:ACTED_IN]->(m)
RETURN a, c
```

## Basic Queries

### Retrieve generic nodes and relationships

```sql

MATCH (n1)-[r]->(n2) 
RETURN r, n1, n2 LIMIT 25
```

### Create a new node with labels and relationship types

```sql
// Hello World!
CREATE (database:Database {name:"TestDB"})-[r:SAYS]->(message:Message {name:"Hello World!"}) 
RETURN database, message, r
```

### Create Example Data on Neo4j dataset

```sql
// Movie Graph
:play movie-graph
```

### Get list of node labels

```sql
CALL db.labels()
```

### Get list of relationship types

```sql
CALL db.relationshipTypes()
```
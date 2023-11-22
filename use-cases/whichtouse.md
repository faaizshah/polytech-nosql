## Difference between cypher statements of CREATE, MATCH and MERGE ? 

In Neo4j, `CREATE`, `MATCH`, and `MERGE` are fundamental commands used for different purposes.

1. **CREATE**

`Usage:` CREATE is used to create new nodes and relationships in the database

`When to Use:` Use CREATE when you are certain that the entities you're adding do not exist in the database. It always creates new data

Example: 
```sql
// Create a new user
CREATE (:User {name: "John Doe", age: 30})

```


2. **MATCH**
   
`Usage:` MATCH is used to read or **retrieve data** from the database. It finds nodes and relationships that match a specified pattern.

`When to Use:` Use MATCH when you want to find and possibly manipulate existing data in the database.

Example:

```sql
// Find a user named John Doe
MATCH (u:User {name: "John Doe"}) RETURN u
```

3. **MERGE**
`Usage:` MERGE either creates new nodes/relationships **if they do not exist or matches and returns existing ones**.

`When to Use:` Use MERGE when you want to ensure that such a node or relationship exists. If it doesn't exist, it will be created; if it does, MERGE will match it instead of creating a duplicate.

Example:
```sql
// Create a new user only if they don't already exist
MERGE (:User {name: "Jane Smith", age: 25})

```

## Comparisons and Best Practices:

### CREATE vs. MERGE:

`CREATE` is straightforward but can lead to duplicate data if not used carefully.

`MERGE` is safer in scenarios where you want to avoid duplicates. It acts like an 'upsert' operation (update or insert).

### MATCH vs. MERGE:

`MATCH` is purely for querying and doesn't alter the database.

`MERGE` can be used both for querying and ensuring the existence of data, with the potential to modify the database.


### Combining MATCH and MERGE:

You can combine `MATCH` and `MERGE` in complex operations, like finding a specific node with `MATCH` and then using `MERGE` to create a relationship to it, if the relationship doesn't already exist.
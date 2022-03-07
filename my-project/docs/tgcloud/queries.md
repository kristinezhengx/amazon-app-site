# Queries! 

After you finish creating your schema, mapping and loading data, and exploring, you are ready to use queries to analyze, update, and compute information from the graph! Move to the Write Queries part of the side bar to start. 

Read about TigerGraph's [query documentation](https://docs.tigergraph.com/gsql-ref/current/querying/query-operations)

## Relevant Examples:

### General 

* Finds all products under certain category
```sql
CREATE QUERY productWithCategory(STRING CatID) FOR GRAPH ProductGraph { 
  prod = {Product.*}; // get all products into a set
  
  results = SELECT p FROM prod:p -(PRODUCT_HAS_CATEGORY)-> Category:c WHERE c.id == CatID;
  PRINT CatID, results;
}
```

### Accumulators 
These next two queries uses accumulators, a special type of variables that gather information about the graph during its traversal and exploration. 

* Recommends product by reviewer username and the categories of products they have reviewed. 
```sql
CREATE QUERY recommendProd(STRING username, int k) FOR GRAPH ProductGraph SYNTAX V2{ 
  SetAccum<VERTEX> @@usedProd;
  prod = {Product.*};
  
  vset1 = SELECT p FROM User:u-(USER_REVIEWS_PRODUCT>:e1)-prod:p-(PRODUCT_HAS_CATEGORY>:e2)-Category-(reverse_PRODUCT_HAS_CATEGORY>:e3)-prod:p
        WHERE u.id == username
        ACCUM @@usedProd += p;
  PRINT vset1;
}
```



* Recommends products for a user based highest average rating and number of reviews. 
```sql
CREATE QUERY recommender(STRING username, int k) FOR GRAPH ProductGraph RETURNS (SET<VERTEX>) SYNTAX v2 { 
  SetAccum<VERTEX> @@usedProd;
  AvgAccum @avgRating;
  SumAccum<INT> @numRating;
  prod = {Product.*};
  
  vset1 = SELECT p FROM prod:p-(reverse_USER_REVIEWS_PRODUCT>:e)- User
           ACCUM p.@avgRating += e.rating, p.@numRating +=1;
  
  vset2 = SELECT p FROM User:u-(USER_REVIEWS_PRODUCT>:e1)-prod:p1-(PRODUCT_HAS_CATEGORY>:e2)-Category-(reverse_PRODUCT_HAS_CATEGORY>:e3)-vset1:p
        WHERE u.id == username
        ACCUM @@usedProd += p1;

 result = SELECT v FROM vset2:v-(reverse_USER_REVIEWS_PRODUCT>:e)-User
          Where v not in @@usedProd
          ORDER BY v.@avgRating DESC, v.@numRating DESC
          LIMIT k;
  
  PRINT result[result.name, result.@avgRating, result.@numRating]; 
  RETURN result;
}
```



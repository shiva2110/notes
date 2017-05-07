### Take care of connection pool exhaustions
* It is possible that some errors might prevent connections from getting returned to connection pool. In following example, statement.close() can throw exception and cause connections to be not returned to pool.

```
 try {
    statement = getStmt();
    connection = pool.get();
 } finally {
    if (statement != null) {
       statement.close();  // this can throw exception
    } 
    
    if (connection != null) {
        connection.close();
    }
 }
```

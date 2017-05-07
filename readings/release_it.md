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

### Run longevity tests
* Often systems are prone to failure with stress that happen over long period of time. In test environments, we often do not test for longevity, i.e subject the system under stress for longer period of time, ~10 days. This long running tests, can check for memory leaks, or other issues.

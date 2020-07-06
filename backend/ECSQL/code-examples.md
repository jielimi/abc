# Example

## withPreparedStatement

```
    const sql = "SELECT * FROM bis.Element";

    this.imodelDb.withPreparedStatement(sql, (stmt: ECSqlStatement) => {
      while (stmt.step() === DbResult.BE_SQLITE_ROW) {
        const row = stmt.getRow();
        console.log("Element count: " + row.id);
      }
    });
```




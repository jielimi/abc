# Example

## withPreparedStatement

```
    方式一
    const sql = "SELECT * FROM bis.Element";

    this.imodelDb.withPreparedStatement(sql, (stmt: ECSqlStatement) => {
      while (stmt.step() === DbResult.BE_SQLITE_ROW) {
        const row = stmt.getRow();
        console.log("Element count: " + row.id);
      }
    });
    方式二
    
  function HandleRow(stmt: ECSqlStatement) {
    while (stmt.step() === DbResult.BE_SQLITE_ROW) {
      const row: any = stmt.getRow();
      console.log("Element count: " + row.id);
    }
  }
  const sql = "SELECT * FROM bis.Element";
  const statement = this.imodelDb.prepareSqliteStatement(sql);
  HandleRow(statement);
  statement.dispose();//释放；
    
```




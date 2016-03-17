# Introduction #

This page describes maven configuration required to get dependecies


# Details #

  * [Check latest version](http://mvnrepository.com/search.html?query=sqlsheet) and add required dependencies
```
      <dependency>
          <groupId>com.google.code.sqlsheet</groupId>
          <artifactId>sqlsheet</artifactId>
          <version>6.5</version>
      </dependency>
```
  * Use it
```
Class.forName("com.googlecode.sqlsheet.Driver");

Connection writeConnection = DriverManager.getConnection("jdbc:xls:file:test.xlsx");

Statement writeStatement = writeConnection.createStatement();

writeStatement.executeUpdate("CREATE TABLE TEST_INSERT(COL1 INT, COL2 VARCHAR(255), COL3 DATE)");

PreparedStatement writeStatement2 = 
writeConnection.prepareStatement("INSERT INTO TEST_INSERT(COL1, COL2, COL3) VALUES(?,?,?)");

for(int i = 0; i<3;i++){
  writeStatement2.setDouble(1, i);
  writeStatement2.setString(2, "Row" + i);
  writeStatement2.setDate(3, new java.sql.Date(new Date().getTime()));
  writeStatement2.execute();
}

writeStatement.close();
writeStatement2.close();
writeConnection.close();
```
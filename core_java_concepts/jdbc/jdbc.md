Absolutely! Let’s go through JDBC (Java Database Connectivity) from basic to advanced level in a clear and structured way.

JDBC in Java — Basic to Advanced
1. What is JDBC?

JDBC is a Java API to connect and execute queries with databases.

It provides methods to query and update data in a database.

It acts as a bridge between Java programs and database servers.

2. JDBC Architecture

JDBC API — Java API used by developers.

JDBC Driver Manager — Manages different database drivers.

JDBC Driver — Connects to specific databases (MySQL, Oracle, PostgreSQL, etc.).

Database — Actual database server.

3. Basic Steps for Using JDBC

Load the JDBC driver.

Establish a connection to the database.

Create a statement object.

Execute SQL queries.

Process the result set.

Close the connection.

4. Basic JDBC Example
import java.sql.*;

public class JDBCBasicExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/testdb";
        String user = "root";
        String password = "password";

        try {
            // 1. Load JDBC driver (optional for modern JDBC)
            Class.forName("com.mysql.cj.jdbc.Driver");

            // 2. Establish connection
            Connection conn = DriverManager.getConnection(url, user, password);

            // 3. Create statement
            Statement stmt = conn.createStatement();

            // 4. Execute query
            ResultSet rs = stmt.executeQuery("SELECT * FROM employees");

            // 5. Process result set
            while (rs.next()) {
                System.out.println("ID: " + rs.getInt("id") + ", Name: " + rs.getString("name"));
            }

            // 6. Close resources
            rs.close();
            stmt.close();
            conn.close();

        } catch (ClassNotFoundException | SQLException e) {
            e.printStackTrace();
        }
    }
}

5. JDBC Driver Types

Type 1: JDBC-ODBC Bridge driver (deprecated)

Type 2: Native-API driver

Type 3: Network Protocol driver

Type 4: Thin driver (Pure Java driver, commonly used)

6. PreparedStatement (Recommended over Statement)

Prevents SQL injection.

Supports parameterized queries.

More efficient for repeated queries.

Example:

String query = "INSERT INTO employees (id, name) VALUES (?, ?)";
PreparedStatement pstmt = conn.prepareStatement(query);
pstmt.setInt(1, 101);
pstmt.setString(2, "John Doe");
pstmt.executeUpdate();
pstmt.close();

7. Handling Transactions

Disable auto-commit mode.

Commit or rollback transactions manually.

conn.setAutoCommit(false);

try {
    // Execute multiple statements
    pstmt1.executeUpdate();
    pstmt2.executeUpdate();
    conn.commit();
} catch (SQLException e) {
    conn.rollback();
}

8. Working with ResultSet

Scrollable result sets: Move cursor forwards/backwards.

Updatable result sets: Update rows in the ResultSet and reflect in the DB.

Statement stmt = conn.createStatement(
    ResultSet.TYPE_SCROLL_INSENSITIVE,
    ResultSet.CONCUR_UPDATABLE
);

ResultSet rs = stmt.executeQuery("SELECT * FROM employees");
rs.absolute(2); // move cursor to 2nd row
rs.updateString("name", "New Name");
rs.updateRow();

9. Batch Processing

Execute multiple SQL commands as a batch.

Improves performance for bulk inserts/updates.

PreparedStatement pstmt = conn.prepareStatement("INSERT INTO employees (id, name) VALUES (?, ?)");

for (int i = 0; i < 10; i++) {
    pstmt.setInt(1, i);
    pstmt.setString(2, "Employee" + i);
    pstmt.addBatch();
}

int[] results = pstmt.executeBatch();

10. Using DataSource for Connection Pooling

Instead of DriverManager, use DataSource for better connection management.

Supports connection pooling.

import javax.sql.DataSource;
import com.zaxxer.hikari.HikariDataSource;

HikariDataSource ds = new HikariDataSource();
ds.setJdbcUrl("jdbc:mysql://localhost:3306/testdb");
ds.setUsername("root");
ds.setPassword("password");

Connection conn = ds.getConnection();

11. Handling Large Data

Use Blob and Clob for binary and character large objects.

// Writing a Blob
InputStream input = new FileInputStream("image.png");
PreparedStatement pstmt = conn.prepareStatement("INSERT INTO images (data) VALUES (?)");
pstmt.setBlob(1, input);
pstmt.executeUpdate();

12. Advanced: Metadata

Use DatabaseMetaData and ResultSetMetaData to get info about DB and result sets.

DatabaseMetaData dbMeta = conn.getMetaData();
System.out.println("Database Product: " + dbMeta.getDatabaseProductName());

ResultSetMetaData rsMeta = rs.getMetaData();
int columnCount = rsMeta.getColumnCount();
for (int i = 1; i <= columnCount; i++) {
    System.out.println("Column " + i + ": " + rsMeta.getColumnName(i));
}

13. Handling Exceptions

Use SQLException methods like getErrorCode(), getSQLState() for detailed errors.

Chain exceptions can be retrieved by getNextException().

14. Best Practices

Always close ResultSet, Statement, Connection (try-with-resources recommended).

Use PreparedStatement over Statement.

Use connection pooling (e.g., HikariCP, Apache DBCP).

Handle transactions properly.

Avoid hardcoding credentials; use config files or environment variables.

15. Sample Full Advanced Example
import java.sql.*;

public class JDBCTutorial {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/testdb";
        String user = "root";
        String password = "password";

        String insertSQL = "INSERT INTO employees (id, name) VALUES (?, ?)";
        String selectSQL = "SELECT * FROM employees";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            conn.setAutoCommit(false);

            try (PreparedStatement pstmt = conn.prepareStatement(insertSQL)) {
                pstmt.setInt(1, 200);
                pstmt.setString(2, "Jane Smith");
                pstmt.executeUpdate();
            }

            conn.commit();

            try (Statement stmt = conn.createStatement();
                 ResultSet rs = stmt.executeQuery(selectSQL)) {

                while (rs.next()) {
                    System.out.println(rs.getInt("id") + ": " + rs.getString("name"));
                }
            }

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
To achieve your objective, you'll first need to install a database management system (DBMS) such as MySQL or Oracle, then create a table to store user details, and finally write a Java program or servlet to connect to the database, extract data from the table, and insert new user details. Below are the steps you can follow:

### Step 1: Install MySQL or Oracle

- **MySQL**: Download and install MySQL from the official website (https://dev.mysql.com/downloads/).
- **Oracle**: Download and install Oracle Database from the official website (https://www.oracle.com/database/technologies/).

### Step 2: Create a User Table

Connect to your database server and create a table to store user details. Below is an example SQL statement to create a user table:

```sql
CREATE TABLE Users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    password VARCHAR(100),
    email VARCHAR(100),
    phone VARCHAR(20)
);
```

### Step 3: Write Java Program or Servlet

You can use JDBC to connect to the database, execute SQL queries, and manipulate data. Below is a simple Java program that connects to the database, retrieves data from the Users table, and inserts new user details:

```java
import java.sql.*;

public class UserDatabaseManager {

    private static final String JDBC_URL = "jdbc:mysql://localhost:3306/your_database_name";
    private static final String USERNAME = "your_username";
    private static final String PASSWORD = "your_password";

    public static void main(String[] args) {
        try {
            // Connect to the database
            Connection conn = DriverManager.getConnection(JDBC_URL, USERNAME, PASSWORD);

            // Retrieve data from the Users table
            Statement stmt = conn.createStatement();
            ResultSet rs = stmt.executeQuery("SELECT * FROM Users");
            while (rs.next()) {
                System.out.println("Name: " + rs.getString("name"));
                System.out.println("Email: " + rs.getString("email"));
                System.out.println("Phone: " + rs.getString("phone"));
                System.out.println();
            }

            // Insert new user details
            String insertQuery = "INSERT INTO Users (name, password, email, phone) VALUES (?, ?, ?, ?)";
            PreparedStatement pstmt = conn.prepareStatement(insertQuery);
            pstmt.setString(1, "New User");
            pstmt.setString(2, "newpassword");
            pstmt.setString(3, "newuser@example.com");
            pstmt.setString(4, "1234567890");
            pstmt.executeUpdate();

            // Close resources
            pstmt.close();
            rs.close();
            stmt.close();
            conn.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### Step 4: Run the Java Program

Compile the Java program and run it. Make sure to replace `your_database_name`, `your_username`, and `your_password` with your actual database credentials.

This program will connect to the database, retrieve data from the Users table, display it, and then insert a new user into the table.

You can also integrate this logic into a servlet or JSP to interact with your web application. The process involves similar JDBC code within your servlet or JSP to connect to the database, execute queries, and handle user registration requests.
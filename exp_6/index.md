Certainly! Below is a simple Java program that illustrates JDBC connectivity to a Microsoft Access database and implements a basic servlet for querying books from the database:

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import java.sql.*;

public class BookQueryServlet extends HttpServlet {

    public void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        Connection conn = null;
        Statement stmt = null;
        try {
            // Load the JDBC-ODBC bridge driver
            Class.forName("sun.jdbc.odbc.JdbcOdbcDriver");

            // Establish a connection to the MS Access database
            String url = "jdbc:odbc:BooksDB"; // assuming BooksDB is the ODBC DSN
            conn = DriverManager.getConnection(url);

            // Create a statement for executing SQL queries
            stmt = conn.createStatement();

            // Execute a simple query to retrieve all books
            String query = "SELECT * FROM Books";
            ResultSet rs = stmt.executeQuery(query);

            // Display the query results
            out.println("<html><head><title>Book Query Results</title></head><body>");
            out.println("<h1>Book Query Results</h1>");
            out.println("<table border='1'><tr><th>Title</th><th>Author</th><th>Price</th></tr>");
            while (rs.next()) {
                out.println("<tr><td>" + rs.getString("title") + "</td><td>" + rs.getString("author") + "</td><td>" + rs.getDouble("price") + "</td></tr>");
            }
            out.println("</table>");
            out.println("</body></html>");

            // Clean-up
            rs.close();
            stmt.close();
            conn.close();
        } catch (Exception e) {
            out.println("Exception: " + e.getMessage());
        } finally {
            // Close resources in a finally block to ensure they're released
            try {
                if (stmt != null) stmt.close();
                if (conn != null) conn.close();
            } catch (SQLException e) {
                out.println("SQLException in closing: " + e.getMessage());
            }
        }
    }
}
```

To compile and execute this servlet, you need to set up your development environment with Apache Tomcat or another servlet container. Additionally, you'll need to create an ODBC connection to your Microsoft Access database (let's call it "BooksDB"):

1. Set up an ODBC data source named "BooksDB" pointing to your MS Access database file.
2. Save the above servlet code to a file named `BookQueryServlet.java`.
3. Compile the servlet using `javac` command.
4. Place the compiled `.class` file in the appropriate directory in your servlet container (e.g., `webapps/ROOT/WEB-INF/classes` in Tomcat).
5. Access the servlet through your web browser by navigating to its URL, which would typically be something like `http://localhost:8080/BookQueryServlet`.

This servlet will connect to the "BooksDB" database using JDBC and retrieve all records from the "Books" table, displaying them in a simple HTML table format.

Make sure to adjust the database connection URL (`url`) and query (`SELECT * FROM Books`) according to your database schema and configuration.
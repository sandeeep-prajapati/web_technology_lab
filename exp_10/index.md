Below is an example of a JSP page that includes a registration form to insert details of users into a database and a login form to authenticate users using their username and password.

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>User Registration and Login</title>
</head>
<body>

<%
    // Import necessary Java classes
    Class.forName("com.mysql.jdbc.Driver");
    Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/mydatabase", "username", "password");
    Statement stmt = con.createStatement();

    // Check if registration form submitted
    if (request.getParameter("register") != null) {
        String username = request.getParameter("username");
        String password = request.getParameter("password");
        String email = request.getParameter("email");
        
        // Insert user details into database
        String sql = "INSERT INTO users (username, password, email) VALUES ('" + username + "', '" + password + "', '" + email + "')";
        int rowsAffected = stmt.executeUpdate(sql);
        if (rowsAffected > 0) {
            out.println("<p>Registration successful!</p>");
        } else {
            out.println("<p>Registration failed. Please try again.</p>");
        }
    }

    // Check if login form submitted
    if (request.getParameter("login") != null) {
        String username = request.getParameter("username");
        String password = request.getParameter("password");
        
        // Authenticate user
        String sql = "SELECT * FROM users WHERE username='" + username + "' AND password='" + password + "'";
        ResultSet rs = stmt.executeQuery(sql);
        if (rs.next()) {
            out.println("<p>Login successful!</p>");
        } else {
            out.println("<p>Login failed. Invalid username or password.</p>");
        }
    }
%>

<h2>User Registration</h2>
<form method="post">
    Username: <input type="text" name="username" required><br>
    Password: <input type="password" name="password" required><br>
    Email: <input type="email" name="email" required><br>
    <input type="submit" name="register" value="Register">
</form>

<h2>User Login</h2>
<form method="post">
    Username: <input type="text" name="username" required><br>
    Password: <input type="password" name="password" required><br>
    <input type="submit" name="login" value="Login">
</form>

</body>
</html>
```

This JSP page includes two forms: one for user registration and another for user login. It connects to a MySQL database to insert user details during registration and to authenticate users during login. Replace `"jdbc:mysql://localhost:3306/mydatabase"`, `"username"`, and `"password"` with your MySQL database URL, username, and password respectively. Also, ensure that you have the appropriate MySQL JDBC driver in your classpath.
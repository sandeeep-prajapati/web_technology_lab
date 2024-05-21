Below is a basic example of a Java Servlet that implements the described functionality:

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class LoginServlet extends HttpServlet {
    public void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {

        // Get user id and password entered in the login form
        String userId = request.getParameter("userId");
        String password = request.getParameter("password");

        // Create a Cookie to store user ids and passwords
        Cookie cookie = new Cookie("userCredentials", userId + ":" + password);
        cookie.setMaxAge(60 * 60 * 24 * 30); // Cookie will expire in 30 days
        response.addCookie(cookie);

        // Set response content type
        response.setContentType("text/html");

        PrintWriter out = response.getWriter();
        String title = "Login Confirmation";

        out.println("<html>\n" +
                "<head><title>" + title + "</title></head>\n" +
                "<body bgcolor=\"#f0f0f0\">\n" +
                "<h1 align=\"center\">" + title + "</h1>\n" +
                "<ul>\n" +
                "  <li><b>User ID:</b> " + userId + "</li>\n" +
                "  <li><b>Password:</b> " + password + "</li>\n" +
                "</ul>\n" +
                "</body></html>");
    }

    public void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {

        // Get cookies associated with this domain
        Cookie[] cookies = request.getCookies();

        // Get user id and password from the cookies
        String userId = null;
        String password = null;
        if (cookies != null) {
            for (Cookie cookie : cookies) {
                if (cookie.getName().equals("userCredentials")) {
                    String[] credentials = cookie.getValue().split(":");
                    userId = credentials[0];
                    password = credentials[1];
                    break;
                }
            }
        }

        // Get user id and password entered in the login form
        String enteredUserId = request.getParameter("userId");
        String enteredPassword = request.getParameter("password");

        // Authenticate user
        boolean isAuthenticated = false;
        if (userId != null && password != null &&
                userId.equals(enteredUserId) && password.equals(enteredPassword)) {
            isAuthenticated = true;
        }

        // Set response content type
        response.setContentType("text/html");

        PrintWriter out = response.getWriter();
        String title = "Login Result";

        out.println("<html>\n" +
                "<head><title>" + title + "</title></head>\n" +
                "<body bgcolor=\"#f0f0f0\">\n" +
                "<h1 align=\"center\">" + title + "</h1>\n" +
                "<p align=\"center\">Authentication " + (isAuthenticated ? "successful" : "failed") + "</p>\n" +
                "</body></html>");
    }
}
```

This servlet handles both POST and GET requests. When a user submits the login form via POST, it creates a cookie storing the user id and password. When a user accesses the servlet via GET, it reads the user id and password from the cookie and compares them with the values entered in the login form to authenticate the user.
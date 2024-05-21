To achieve your objective of installing and configuring Apache Tomcat and Apache HTTP Server (commonly referred to as Apache), and then accessing static web pages for a book website through these servers, follow these steps:

1. **Install Apache Tomcat**:
   - Download the latest version of Apache Tomcat from the official website (https://tomcat.apache.org/).
   - Follow the installation instructions provided in the documentation for your operating system.
   - After installation, start the Tomcat server.

2. **Install Apache HTTP Server**:
   - Download the latest version of Apache HTTP Server from the official website (https://httpd.apache.org/).
   - Follow the installation instructions provided in the documentation for your operating system.
   - After installation, start the Apache HTTP Server.

3. **Deploy Static Web Pages**:
   - Place your static web pages for the book website in the appropriate directory for each server:
     - For Tomcat, typically you would place them in the `webapps` directory of your Tomcat installation. You can create a new directory for your book website, for example, `webapps/bookwebsite`.
     - For Apache HTTP Server, place them in the directory specified by the `DocumentRoot` directive in your Apache configuration file (`httpd.conf`). This is usually something like `/var/www/html` on Linux or `C:\Program Files\Apache Software Foundation\Apache2.4\htdocs` on Windows.

4. **Access the Web Pages**:
   - For Tomcat: Open your web browser and navigate to `http://localhost:8080/bookwebsite` (assuming you deployed your website under `/bookwebsite` context path).
   - For Apache HTTP Server: Open your web browser and navigate to `http://localhost` (or `http://localhost/bookwebsite` if you configured a subdirectory). 

By following these steps, you'll have Apache Tomcat and Apache HTTP Server installed and configured, and you'll be able to access your static web pages for the book website through these servers. Adjust paths and configurations as needed based on your specific setup and requirements.
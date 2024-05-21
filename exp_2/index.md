Creating a complete system to design an entry form for student details and store the data in a database involves several steps. The key components are:

1. **HTML Form**: For capturing student details.
2. **Server-Side Script**: To process the form data and insert it into a database.
3. **Database Setup**: A database server (SQL, Oracle, or MS Access) to store the student data.

Here is a step-by-step guide:

### Step 1: Create the HTML Form (student_form.html)
This HTML form will capture the student details.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Entry Form</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            padding: 20px;
        }
        .container {
            max-width: 600px;
            margin: auto;
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h2 {
            text-align: center;
            color: #333;
        }
        form {
            display: flex;
            flex-direction: column;
        }
        label {
            margin-bottom: 5px;
            color: #333;
        }
        input, select {
            margin-bottom: 10px;
            padding: 10px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
        input[type="submit"] {
            background-color: #007BFF;
            color: white;
            border: none;
            cursor: pointer;
        }
        input[type="submit"]:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Student Entry Form</h2>
        <form action="process_form.php" method="post">
            <label for="student_name">Student Name:</label>
            <input type="text" id="student_name" name="student_name" required>

            <label for="email">Email:</label>
            <input type="email" id="email" name="email" required>

            <label for="phone">Phone:</label>
            <input type="tel" id="phone" name="phone" required>

            <label for="address">Address:</label>
            <input type="text" id="address" name="address" required>

            <label for="course">Course:</label>
            <select id="course" name="course" required>
                <option value="BSc">BSc</option>
                <option value="MSc">MSc</option>
                <option value="PhD">PhD</option>
            </select>

            <input type="submit" value="Submit">
        </form>
    </div>
</body>
</html>
```

### Step 2: Create the Server-Side Script (process_form.php)
This script will process the form data and insert it into a database. We will use PHP for this example.

#### Database Setup
Assuming you're using MySQL, ensure you have a database and a table set up. Here's an example SQL script to create a table:

```sql
CREATE DATABASE student_db;

USE student_db;

CREATE TABLE students (
    id INT AUTO_INCREMENT PRIMARY KEY,
    student_name VARCHAR(100),
    email VARCHAR(100),
    phone VARCHAR(15),
    address VARCHAR(255),
    course VARCHAR(50)
);
```

#### PHP Script to Process Form Data and Insert into Database

```php
<?php
$servername = "localhost";
$username = "root"; // Your database username
$password = ""; // Your database password
$dbname = "student_db";

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

// Prepare and bind
$stmt = $conn->prepare("INSERT INTO students (student_name, email, phone, address, course) VALUES (?, ?, ?, ?, ?)");
$stmt->bind_param("sssss", $student_name, $email, $phone, $address, $course);

// Set parameters and execute
$student_name = $_POST['student_name'];
$email = $_POST['email'];
$phone = $_POST['phone'];
$address = $_POST['address'];
$course = $_POST['course'];
$stmt->execute();

echo "New records created successfully";

$stmt->close();
$conn->close();
?>
```

### Explanation:
1. **HTML Form**: The form uses the `POST` method to send data to `process_form.php`.
2. **PHP Script**: 
    - Connects to the MySQL database.
    - Prepares an SQL statement to insert the form data into the `students` table.
    - Binds form data to the SQL statement.
    - Executes the SQL statement to insert data into the database.

### Hosting the Form and Script
1. Save `student_form.html` and `process_form.php` in the root directory of your web server (e.g., Apache or Nginx).
2. Ensure the PHP server is running and can process the form.

### Conclusion
This basic setup captures student details via an HTML form and stores the data in a MySQL database using a PHP script. You can expand and secure this setup by adding validation, error handling, and security measures like prepared statements to prevent SQL injection.
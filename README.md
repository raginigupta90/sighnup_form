# Sign-Up Form with MySQL Database Integration

This repository contains the code for creating and designing a sign-up form. When the user submits the form, the HTML form data is inserted into a MySQL server database.

## Prerequisites

### Technical Knowledge

Before setting up the application, you should have a basic understanding of:

- HTML
- PHP (Database connectivity)
- SQL queries

### Software Requirements

You will need to install the following software:

1. **XAMPP Server**
   - XAMPP is a free and open-source cross-platform web server solution stack package developed by Apache Friends, consisting mainly of the Apache HTTP Server, MariaDB database, and interpreters for scripts written in the PHP and Perl programming languages.
   - Download XAMPP from the official [Apache Friends website](https://www.apachefriends.org/index.html).

2. **phpMyAdmin**
   - phpMyAdmin is a free and open-source tool written in PHP, intended to handle the administration of MySQL over the Web. It can perform various tasks such as creating, modifying, or deleting databases, tables, fields, or rows; executing SQL statements; or managing users and permissions.
   - Download phpMyAdmin from the official [phpMyAdmin website](https://www.phpmyadmin.net/).
   - After downloading, unzip the phpMyAdmin files and place the folder in the following location:
     ```plaintext
     C:\xampp\htdocs
     ```
   - Unzipping the file anywhere else won’t work correctly. Just unzip the contents in the specified location.

3. **Text Editor**
   - Any text editor like Notepad++ or even the default Notepad will suffice for editing code files.

4. **Web Browser**
   - Any JavaScript-enabled web browser (such as Chrome, Firefox, or Edge) will be adequate for running and testing the application.

## Application Overview

The task is to create and design a sign-up form in which the user-entered details are inserted into a MySQL server database. The approach involves:

1. **Creating a MySQL Database and Table**
   - First, we need to create our MySQL server database and a table according to our requirements.
   
2. **Connecting to MySQL Database**
   - We connect to our MySQL server database using the PHP `mysqli_connect()` function, which takes four arguments: "servername", "username", "password", and "database".

### Note

No CSS code is used in this implementation as we are using Bootstrap for styling in the PHP code. You can apply additional CSS and styles as per your application requirements.

### Implementation Details

1. **Create Database and Table**
   - Use phpMyAdmin to create a new database (e.g., `signup_db`).
   - Create a table (e.g., `users`) with appropriate fields (e.g., `id`, `username`, `email`, `password`).

2. **PHP Code for Database Connection and Data Insertion**
   - Create a PHP file to handle the form submission, connect to the database, and insert the form data into the table.

### Example PHP Code

```php
<?php
$servername = "localhost";
$username = "root";
$password = "";
$database = "signup_db";

// Create connection
$conn = mysqli_connect($servername, $username, $password, $database);

// Check connection
if (!$conn) {
    die("Connection failed: " . mysqli_connect_error());
}

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $username = $_POST['username'];
    $email = $_POST['email'];
    $password = $_POST['password'];

    $sql = "INSERT INTO users (username, email, password) VALUES ('$username', '$email', '$password')";

    if (mysqli_query($conn, $sql)) {
        echo "New record created successfully";
    } else {
        echo "Error: " . $sql . "<br>" . mysqli_error($conn);
    }

    mysqli_close($conn);
}
?>

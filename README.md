What is a LAMP STACk?

A LAMP is a stack of open-source software used for hosting web applications. I wanted to create this repo for beginners and make it as simple as possible. It includes:

Linux: The operating system.
Apache: The web server.
MySQL/MariaDB: The database (optional in this project, I used MariaDB).
PHP: The server-side scripting language.

In this project:

Linux: Debian 12 as the OS (I repurposed an old Chromebook for this project).
Apache: Serves the web application and routes requests.
PHP: Processes user inputs and calls the Python script.
Python: I made a LAMP to perform backend calculations for a loot drop calculator I made in Python.

LAMP Stack Setup

Install Apache:

    sudo apt update
    sudo apt install apache2 -y

Start and enable the service:

    sudo systemctl start apache2
    sudo systemctl enable apache2

Test: Open your browser and visit http://localhost. You should see the default Apache page.

Install PHP:

    sudo apt install php libapache2-mod-php -y

Test: Create a test PHP file:

    echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/test.php

Visit http://localhost/test.php to confirm PHP is working.

Install MariaDB:

    sudo apt install mariadb-server mariadb-client -y

Secure MariaDB:

    sudo mysql_secure_installation

Start the service:

    sudo systemctl start mariadb
    sudo systemctl enable mariadb

Install Python:

    sudo apt install python3 python3-pip -y

Confirm Python version:

    python3 --version

-----------------------------------------------------------------------------------------------------------------------

Integrating Python with LAMP

The project demonstrates how to use PHP as the bridge to execute Python scripts in a LAMP environment.

Project Files:

    sample_file.py: The Python script for loot drop calculations.
    sample_file.php: The PHP frontend that calls the Python script.

Both files are stored in the Apache web root directory:

/var/www/html/

Make the Python script executable:

    sudo chmod +x /var/www/html/sample_file.py

Ensure the PHP file is readable:

    sudo chmod 644 /var/www/html/sample_file.php

PHP Calls Python:

The PHP script uses shell_exec() to run the Python script and pass user inputs:

    $output = shell_exec("python3 /var/www/html/sample_file.py $drop_rate $planned_attempts 2>&1");

How to Test

Start Apache:

    sudo systemctl start apache2

Visit the PHP file:

     http://localhost/sample.php

Why Use Python in a LAMP Stack?

Flexibility: Python is well-suited for backend logic and calculations.
Powerful Libraries: Python’s simplicity and extensive libraries make it ideal for tasks beyond simple web scripting.
Bridge to PHP: Using shell_exec() in PHP allows seamless integration with Python for complex calculations.













# Set up psr4 (psr-4) PHP project with composer dependency management

## About

This is a demo project with psr4 (psr-4), which provides composer dependency management and class auto-loading support.

This project can be used as a starting point to add other dependencies and write sample code.

Run below command prior to running the project to install any dependencies. 

```bash
composer install
```

Instead of downloading this project you can also manually create this project with the below steps or use the bash script provided below.

## Manual creation of this project

### How to set up PSR-4 class autoloading support in a PHP project?

PSR-4 is a PHP-FIG standard that defines how namespaces should map to file paths. It simplifies autoloading of classes in a project. To get started, follow these steps:

Step 1: Create the project structure

Create a new directory for your PHP project. Inside this directory, set up the following structure:

```
my_project/
|-- src/
|   |-- MyClass.php
|-- composer.json
|-- index.php
```

Step 2: Set up Composer

Composer is a dependency manager for PHP that will help us manage the class autoloading. If you haven't already installed Composer, you can download and install it from the official website: https://getcomposer.org/

Step 3: Configure autoloading

In the `composer.json` file, define the PSR-4 autoloading configuration under the `autoload` section. This will tell Composer how to autoload classes in the `src` directory:

```json
{
    "autoload": {
        "psr-4": {
            "MyProject\\": "src/"
        }
    }
}
```

Step 4: Create a sample class

Inside the `src` directory, create a sample class named `MyClass.php`:

```php
<?php

namespace MyProject;

class MyClass
{
    public function sayHello()
    {
        return "Hello, PSR-4 autoloading!";
    }
}
```

Step 5: Generate the autoload files

Run the following command in the terminal inside your project directory to generate the autoload files:

```
composer dump-autoload
```

This command will create an `autoload.php` file inside the `vendor` directory. This file handles the class autoloading for you.

Step 6: Test the autoloading

In the `index.php` file, use the `MyClass` without manually including the file:

```php
<?php

require 'vendor/autoload.php';

use MyProject\MyClass;

$myClass = new MyClass();
echo $myClass->sayHello();
```

Step 7: Run the project

Run the `index.php` file in your web server or through the command line:

```
php index.php
```

You should see the output: "Hello, PSR-4 autoloading!" which indicates that the PSR-4 autoloading is working correctly.

Now you have a PHP project with PSR-4 class autoloading support. You can add more classes to the `src` directory, and Composer will handle the autoloading for you.



### Bash script for the above steps

Below is a bash script that sets up the PHP project with PSR-4 class autoloading support, as described in the previous steps:

```bash
#!/bin/bash

# Step 1: Create the project directory and structure
mkdir my_project
cd my_project
mkdir src

# Step 2: Install Composer if not already installed
if ! command -v composer &> /dev/null
then
    echo "Composer not found. Installing Composer..."
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer
    php -r "unlink('composer-setup.php');"
    echo "Composer installed successfully!"
else
    echo "Composer is already installed."
fi

# Step 3: Configure autoloading in composer.json
cat <<EOT > composer.json
{
    "autoload": {
        "psr-4": {
            "MyProject\\\\": "src/"
        }
    }
}
EOT

# Step 4: Create a sample class
cat <<EOT > src/MyClass.php
<?php

namespace MyProject;

class MyClass
{
    public function sayHello()
    {
        return "Hello, PSR-4 autoloading!";
    }
}
EOT

# Step 5: Generate the autoload files
composer dump-autoload

# Step 6: Create index.php to test the autoloading
cat <<EOT > index.php
<?php

require 'vendor/autoload.php';

use MyProject\MyClass;

\$myClass = new MyClass();
echo \$myClass->sayHello() . PHP_EOL;
EOT

# Step 7: Run the project
php index.php

echo "Project setup completed. PSR-4 class autoloading is working correctly."
```

Save the script into a file (e.g., `setup_project.sh`), and then make the script executable with the following command:

```bash
chmod +x setup_project.sh
```

Finally, run the script with:

```bash
./setup_project.sh
```

The script will create the PHP project structure, set up Composer, configure autoloading, create the sample class, and test the autoloading by running the `index.php` file. After the script finishes, you'll have a PHP project with PSR-4 class autoloading support.
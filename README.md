# Working-With-Functions
**This project demonstrates how to use functions in shell script.**

## What Are Functions?

### A function is a reusable block of code that performs a specific task. Instead of writing the same code multiple times, you define it once and call it whenever needed.

### Think of a function like a microwave preset button:
* You program it once (e.g., "Popcorn – 2 minutes, high power").
* Later, you just press the button instead of setting time and power manually each time.

## Why do we use functions
1. Functions are used to avoid repetation(DRY Principle - Don't Repeat Yourself). Consider the following script, without function and refactored with function

```bash
#!/bin/bash
echo "Welcome, Alice!"
echo "Your account balance is $100"

echo "Welcome, Bob!"
echo "Your account balance is $200"

echo "Welcome, Charlie!"
echo "Your account balance is $50"
```
### Same script with functions,Changed the greeting format in one place instead of everywhere.
```bash
greet_user() {
    echo "Welcome, $1!"
    echo "Your account balance is $2"
}

greet_user "Alice" 100
greet_user "Bob" 200
greet_user "Charlie" 50
```
2. Organize Better code/ script. Consider the following script without functions and with function. Notice the difference.

### Without function(messy script)
```bash
# Backup database
mysqldump -u root -p mydb > backup.sql
tar -czf backup.tar.gz backup.sql

# Log the backup
echo "$(date): Backup completed" >> backup.log

# Send email notification
echo "Backup successful" | mail -s "Backup Status" admin@example.com
```

### With function (structured script). Easier to read, debug, and modify.
```bash
backup_database() {
    mysqldump -u root -p mydb > backup.sql
    tar -czf backup.tar.gz backup.sql
}

log_action() {
    echo "$(date): $1" >> backup.log
}

send_email() {
    echo "$1" | mail -s "Backup Status" admin@example.com
}

# Main script
backup_database
log_action "Backup completed"
send_email "Backup successful"
```
### some other benefit includes, writence once any reuse any where. eg calling a fucntion inside another function or passing a fucntion as an argument or parameter to another function.

## Function Syntax
```bash
function_name() {"\n    # Function body\n    # You can place any commands or logic here\n"}

```
* function_name: This is th name of the function. You should choose a descriptive that suugest the intent of the function.
* ()Brackets are usually used to define the function, they can also house the parameters.
* {} Curly braces wraps the body of the function, inside the curly braces, you define the command or logic that the function executes.

### Lets look at another script with and without functions versions.
### Script Without function
```bash
#!/bin/bash

# Checking the number of arguments
if [ "$#" -ne 0 ]; then
    echo "Usage: $0 <environment>"
    exit 1
fi

# Accessing the first argument
ENVIRONMENT=$1

# Acting based on the argument value
if [ "$ENVIRONMENT" == "local" ]; then
  echo "Running script for Local Environment..."
elif [ "$ENVIRONMENT" == "testing" ]; then
  echo "Running script for Testing Environment..."
elif [ "$ENVIRONMENT" == "production" ]; then
  echo "Running script for Production Environment..."
else
  echo "Invalid environment specified. Please use 'local', 'testing', or 'production'."
  exit 2
fi
```

### A refactored version of the script will look like the code below:

```bash
#!/bin/bash

# Environment variables
ENVIRONMENT=$1

check_num_of_args() {"\n# Checking the number of arguments\nif [ \"$#\" -ne 0 ]; then\n    echo \"Usage: $0 <environment>\"\n    exit 1\nfi\n"}

activate_infra_environment() {"\n# Acting based on the argument value\nif [ \"$ENVIRONMENT\" == \"local\" ]; then\n  echo \"Running script for Local Environment...\"\nelif [ \"$ENVIRONMENT\" == \"testing\" ]; then\n  echo \"Running script for Testing Environment...\"\nelif [ \"$ENVIRONMENT\" == \"production\" ]; then\n  echo \"Running script for Production Environment...\"\nelse\n  echo \"Invalid environment specified. Please use 'local', 'testing', or 'production'.\"\n  exit 2\nfi\n"}

check_num_of_args
activate_infra_environment

```
### The refactored version is way better than the initial version. It is more readable, structred and very maintainable.

## Calling a Function.
### A function after creation and implementing commands or tasks you want the function to perform. It does not really perform the tasks defined untill you call the function. Examine the script below.
```bash
add() {
    result=$(( $1 + $2 ))
    echo "Result: $result"
}

subtract() {
    result=$(( $1 - $2 ))
    echo "Result: $result"
}

# Function call
add 5 3       # Output: Result: 8
subtract 10 4 # Output: Result: 6
```
### Function call Demonstration

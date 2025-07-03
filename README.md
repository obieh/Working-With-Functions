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


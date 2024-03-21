#!/usr/bin/expect -f

spawn sudo mysql -u root mysql

expect "mysql>"
send "create database glpi;\r"
expect "mysql>"
send "CREATE USER 'glpi'@'localhost' IDENTIFIED BY 'glpi';\r"
expect "mysql>"
send "GRANT ALL PRIVILEGES ON \`glpi\`.* TO 'glpi'@'localhost' WITH GRANT OPTION;\r"
expect "mysql>"
send "exit;\r"

spawn mysql -u root -p glpi < glpidb.sql
expect "Enter password:"
send "glpi\r"
expect eof
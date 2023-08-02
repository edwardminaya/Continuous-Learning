# Technical Interview

This is my prepartion document for my technical interview for a Solutions Engineer role. I'll be showing how in Ruby and Python.

Programming experience

- Scripting (powershell, bash, python, or similar)
- Writing SQL queries
- Making REST API calls

Experience with the following technologies

- Windows and Linux Operating Systems and administration
- Enterprise networking, troubleshooting, architecture
- Deploying and troubleshooting remote applications

# Prompt

Write code to pull data from a SQL database and peform HTTP POST requests to a JSON API

# SQL Database Interaction

### Explain how you would connect to a SQL database, execute a SQL query to retrieve data from a specific table in the database and read the content.

cursor() - The curosor method in Python is used to create a cursor object from a database connection. This cursor object is then used to execute SQL queries and fetch the results

Python -> SQLite

```python
import sqlite3

# Connect to SQLite3 database
connection = sqlite3.connect('example.db')

# Create a cursor
cursor = connection.cursor()

# Execute a SQL query to retrieve data from a specific table
query = "SELECT * FROM your_table_name"
cursor.execute(query)

# Fetch the results (if needed)
results = cursor.fetchall()

# Print the results
for row in results:
  print(row)

# Close the cursor & databse connection
cursor.close()
connection.close()
```

Ruby -> SQLite3

```ruby
require 'sqlite3'

# Connect to SQLite3 database
connection = SQLite3::Database.new('example.db')

# Execute a SQL query to retrieve data from a specific table
query = "SELECT * FROM your_table_name"
results = connection.execute(query)

# Print the results
results.each do |row|
  puts row
end

# Close the database connection
connection.close
```

Python -> MySQL

```python
import mysql.connector

# Connect to a MySQL database
connection = mysql.connector.connect(
  host='your_mysql_host',
  user='your_username',
  password='your_password',
  database='your_database_name'
)

# Create a cursor
cursor = connection.cursor()

# Execute a SQL query to retrieve data from a specific database
query = "SELECT * FROM your_table_name"
cursor.execute(query)

# Fetch the results (if needed)
results = cursor.fetchall()

# Print the results
for row in results:
  print(row)

# Close the cursor and database connection
cursor.close()
connection.close()
```

Ruby -> MySQL

```ruby
require 'mysql2'

# Connect to a MySQL database
client = Mysql2::Client.new(
  host: 'your_mysql_host',
  username: 'your_username',
  password: 'your_password',
  database: 'your_database_name'
)

# Execute a SQL query to retrieve data from a specific table
query = "SELECT * FROM your_table_name"
results = client.query(query)

# Print the results
results.each do |row|
  puts row
end

# Close the database connection
client.close
```

Python -> PostgreSQL

```python
import psycopg2

# Connect to PostgreSQL database
connection = psycopg2.connect(
  host='your_postgres_host',
  databse='your_database_name',
  user='your_username',
  password='your_password'
)

# Create a cursor
cursor = connection.cursor()

# Execute a SQL query to retrieve data from a specific table
query = "SELECT * FROM your_table_name"
cursor.execute(query)

# Fetch the results (if needed)
results = cursor.fetchall()

# Print the results
for row in results:
  print(row)

# Close the cursor and database connection
cursor.close()
connection.close()
```

Ruby -> PostgreSQL

```ruby
require 'pg'

# Connect to a PostgresSQL database
connection = PG.connect(
  host: 'your_postgres_host',
  dbname: 'your_database_name',
  user: 'your_username',
  password: 'your_password'
)

# Execute a SQL query to retrieve data from a specific table
query = "SELECT * FROM your_table_name"
results = connection.exec(query)

# Print the results
results.each do |row|
  puts row
end

# Close the database connection
connection.close
```

# HTTP POST requests and JSON API

### How do you perform an HTTP POST request?

Python

```python
# First, ensure you have 'requests' library installed.
# Import the necessary libraries in your Python script.
import requests

# Define the URL of the JSON API endpoint where you want to send the POST request
url = 'https://api.example.com/data'

# Prepare the data you want to send in the request body. This data should be in Python dictionary format
data = {
  'key1': 'value1',
  'key2': 'value2',
}

# Perform the HTTP POST request using the request.post() method
response = requests.post(url, json=data)

# Check the response to see if the request was successful and process the response data if needed
if response.status_code == 200:
  print('POST request was successful')
  print('Response content: ')
  print(respons.json()) # Get the response data in JSON format
else:
  print(f"POST request failed with status code {response.status_code}")
```

Ruby

```ruby
# Net::HTTP is part of the Ruby standard library
# Import the necessary libraries in your Ruby script
require 'net/http'
require 'json'

# Define the URL of the JSON API endpoint where you want to send the POST request
url = URI.parse('https://api.example.com/data')

# Prepare the data you want to send in the request body. This data should be in a Ruby hash format
data = {
  'key1' => 'value1',
  'key2' => 'value2'
}

# Creat an HTTP POST request with the JSON data in the request body
http = Net::HTTP.new(url.host, url.port)
http.use_ssl = (url.scheme == 'https')

request = Net::HTTP::Post.new(url.path, { 'Content-Type' => 'application/json'})
request.body = data.to_json

# Perform the HTTP OST request and get the response
response = http.request(request)

# Check the response to see if the request was successful and process the response dat if needed
if response.code.to_i == 200
  puts "POST request was successful"
  puts "Response content: "
  puts JSON.parse(response.body) # Get the response data as a Ruby hash
else
  puts "POST request failed with status code #{response.code}"
end
```

Can you explain the difference between GET and POST requests in the context of API calls?
When making an HTTP POST request to a JSON API, how would you send JSON data as part of the request body?
In the case the API responds with an error status code, how would you handle error responses?

# Integrating SQL Database and JSON API

Suppose you have data stored in a SQL database. How would you retrieve that data and send it to a JSON API?
When pulling data from a SQL database, how would you ensure the data is in the correct format to be sent to a JSON API?
How might you handle a large dataset when pulling data from the database and processing it before sending it to the API?

# Error Handling and Data Validation

How would you handle exceptions and errors that may occur during the process of making API requests or interacting with the SQL database?
What kind of data validation would you consider implementing when pulling data from the database and preparing it for the API request?
In case the API response contains unexpected data or is not in the expected JSON format, how would you handle such a situation in your code?

# Security and Authentication

If the API requires authentication, how would you pass the necessary credentials in the HTTP POST request headers?
What security considerations would you keep in mind when interacting with a JSON API and a SQL database in your application?

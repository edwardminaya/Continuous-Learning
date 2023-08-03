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
  print(response.json()) # Get the response data in JSON format
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

### Can you explain the difference between GET and POST requests in the context of API calls?

GET requests are used for retrieving data from the server without changing anything on the server, and they typically include data in the URL's query parameters. On the other hand, POST requests are used for sending data to the server to create or modify resources, and they include data in the request body.

### When making an HTTP POST request to a JSON API, how would you send JSON data as part of the request body?

You need to specify the 'Content-Type' headers as 'application/json' and encode your data in JSON format. You can achieve this using the 'requests' library in Python or 'Net::HTTP' library in Ruby.

Python

```python
import requests
import json

url = 'https://api.example.com/data'

# Data to be sent in the request body (as a Python dictionary)
data = {
  'key1': 'value1',
  'key2': 'value2'
}

# Convert the data to JSON format
json_data = json.dumps(data)

# Set the headers to indicate JSON data is in the request body
headers = {
  'Content-Type': 'application/json'
}

# Perform the HTTP POST request with JSON data in the request boyd
response = requests.post(url, data=json_data, headers=headers)

# Process the response
if response.status_code == 200
  print('POST request was successful.')
  print(response.json())
else:
  print(f"POST request failed with status code {response.status_code}")
```

Ruby

```ruby
require 'net/http'
require 'json'

url = URI.parse('https://api.example.com/data')

# Data to be sent in the reqest body (as a Ruby hash)
data = {
  'key1' => 'value1',
  'key2' => 'value2'
}

# Convert the data to JSON format
json_data = data.to_json

# Set the headers to indicate JSON data in the request body
headers = {
  'Content-Type' => 'application/json'
}

# Create an HTTP POST request with JSON data in the request body
http = Net::HTTP.new(url.host, url.port)
http.use_ssl = (url.scheme == 'https')

request = Net::HTTP::Post.new(url.path, headers)
request.body = json_data

# Perform the HTTP POST request
response = http.request(request)

# Process the response
if response.code.to_i == 200
  puts "POST request was succesful"
  puts JSON.parse(response.body)
else
  puts "POST request failed with status code #{response.code}"
end
```

### In the case the API responds with an error status code, how would you handle error responses?

It's essential to handle error responses appropiately to provide meaningful feedback to users to take appropiate action in your application.

Python

```python
# Check for successful response (2xx status code)
if response.status_code / 100 == 2:
  print('POST request was successful.')
  print(response.json()) # Get the response data in JSON format
else:
  #Handle error responses here
  print(f"POST request failed with status code {response.status_code}")
  print("Error message: ", response.json())
```

Ruby

```ruby
if response.code.to_i / 100 == 2
  puts 'POST request was successful.'
  puts JSON.parse(response.body)
else
  # Handle error responses here
  puts "POST request failed with status code #{response.code}"
  puts "Error message: ", JSON.parse(response.body)
end
```

# Integrating SQL Database and JSON API

### Suppose you have data stored in a SQL database. How would you retrieve that data and send it to a JSON API?

Python -> SQLite3

```python
import requests
import json
import sqlite3

# Establish connection to SQLite3 database
conn = sqlite3.connect('your_database.db')
cursor = conn.cursor()

# Fetch data from database
query = "SELECT * FROM your_table_name"
cursor.execute(query)
results = cursor.fetchall()

# Convert data to JSON format
json_data = json.dumps(results)

# Send JSON data to JSON API
url = 'https://api.example.com/data'
headers = {
  'Content-Type': 'application/json'
}
response = request.post(url, data=json_data, headers=headers)

# Handle API request response
if response.status_code / 100 == 2:
  print('Data sent to API successfully')
  print(response.json())
else:
  print(f"Failed to send data to API. Status code: {response.status_code}")
```

Python -> MySQL

```python
import requests
import json
import mysql.connector

# Establish connection to MySQL database
conn = mysql.connector.connect(
  host='your_mysql_host',
  user='your_mysql_user',
  password='your_mysql_password',
  database='your_mysql_database',
)
cursor = conn.cursor()

# Fetch data from database
query = "SELECT * FROM your_table_name"
cursor.execute(query)
results = cursor.fetchall()

# Convert data to JSON format
json_data = json_dumps(results)

# Send JSON data to JSON API
url = "https://api.example.com/data"
headers = {
  'Content-Type': 'application/json'
}
response = requests.post(url, data=json_data, headers=headers)

# Handle API request response
if response.status_code / 100 == 2:
  print('Data sent to API successfully')
  print(response.json())
else:
  print(f"Failed to sen data to API. Status code: {response.status_code}")
```

Python -> PostgreSQL

```python
import requests
import json
import psycopg2

# Establish connection to PostgreSQL database
conn = psycopg2.connect(
  host='your_host_name',
  database='your_database_name',
  user='your_username',
  password='your_password'
)
cursor = conn.cursor()

# Fetch data from database
query = "SELECT * FROM your_table_name"
cursor.execute(query)
results = cursor.fetchall()

# Convert data to JSON format
json_data = json.dumps(results)

# Send JSON data to JSON API
url = "https://api.example.com/data"
headers = {
  'Content-Type': 'application/json'
}
response = requests.post(url, data=json_data, headers=headers)

if response.status_code / 100 == 2:
  print('Data sent to API successfully')
  print(response.json())
else:
  print(f"Failed to send data to API. Status code: {response.status_code}")
```

Ruby -> SQLite3

```ruby
require 'sqlite3'
require 'json'
require 'net/http'

# Establish connection to SQLite3 database
db = SQLite3::Database.new('your_database.db')

# Fetch data from database
query = "SELECT * FROM your_table_name"
results = db.execute(query)

# Convert data to JSON format
json_data = results.to_json

# Send JSON data to JSON API
url = URI.parse('https://api.example.com/data')
http = Net::HTTP.new(url.host, url.port)
http.use_ssl = (url.scheme == 'https')

request = Net::HTTP::Post.new(url.path, { 'Content-Type' => 'application/json'})
request.body = json_data
response = http.request(request)

# Handle API request response
if response.code.to_i / 100 == 2
  puts 'Data sent to API successfull'
  puts JSON.parse(response.body)
else
  puts "Failed to send data to API. Status code: #{response.code}"
end
```

Ruby -> MySQL

```ruby
require 'mysql2'
require 'json'
require 'net/http'

# Establish connection to MySQL database
client = Mysql2::Client.new(
  host: 'your_mysql_host',
  username: 'your_mysql_user',
  password: 'your_mysql_password',
  database: 'your_database'
)

# Fetch data from database
query = "SELECT * FROM your_table_name"
results = client.query(query).to_a

# Convert data to JSON format
json_data = results.to_json

# Send JSON data to JSON API
url = URI.parse('https://api.example.com/data')
http = Net::HTTP.new(url.host, url.port)
http.use_ssl = (url.scheme == 'https')

request = Net::HTTP::Post.new(url.path, { 'Content-Type' => 'application/json' })
request.body = json_data

response = http.request(request)

# Handle API request response
if response.code.to_i / 100 == 2
  puts 'Data sent to API successfully.'
  puts JSON.parse(response.body)
else
  puts "Failed to send data to API. Status code: #{response.code}"
end
```

Ruby -> PostgreSQL

```ruby
require 'pg'
require 'json'
require 'net/http'

# Establish connection to PostgreSQL database
conn = PG.connect(
  host: 'your_postgres_host',
  user: 'your_postgres_user',
  password: 'your_postgres_password',
  dbname: 'your_database'
)

# Fetch data from database
query = "SELECT * FROM your_table_name"
results = conn.exec(query).to_a

# Convert data to JSON format
json_data = results.to_json

# Send JSON data to JSON API
url = URI.parse('https://api.example.com/data')
http = Net::HTTP.new(url.host, url.port)
http.use_ssl = (url.scheme == 'https')

request = Net::HTTP::Post.new(url.path, { 'Content-Type' => 'application/json' })
request.body = json_data

response = http.request(request)

# Handle API request response
if response.code.to_i / 100 == 2
  puts 'Data sent to API successfully.'
  puts JSON.parse(response.body)
else
  puts "Failed to send data to API. Status code: #{response.code}"
end
```

### When pulling data from a SQL database, how would you ensure the data is in the correct format to be sent to a JSON API?

1. RETRIEVE THE DATA - Use SQL queries to fetch the data from the database table(s).

2. CONVERT DATA TO APPROPIATE DATA STRUCTURES - Depending on the database library used, the data may be returned as tuples, dictionaries, etc.

- Python (lists or dictionaries)
- Ruby (arrays or hashes)

3. HANDLE DATA TYPES - Ensure data types of the retrieved values are compatible with JSON serialization

- strings
- integers
- floats
- booleans

4. CLEANSE THE DATA - Validate and sanitize the retrieved data to prevent security vulnerabilities or unexpected behaviors.

5. CONVERT DATA TO JSON - Serialize data into JSON format using the appropiate functions

- Python -> json.dumps()
- Ruby -> .to_json

Python -> PostgreSQL

```python
import json
import psycopg2

# Establish connection to the PostgreSQL database
conn = psycopg2.connect(
  host="",
  database="",
  user="",
  password=""
)
cursor = conn.cursor()

# Fetch data from the database
query = "SELECT * FROM your_table_name"
cursor.execute(query)
results = cursor.fetchall()

# Convert data to Python data structures (lists and dictionaries)
# Assuming the data is in the form of list of tuples
formatted_data = []
for row in results:
  formatted_data.append({
    'id': row[0],
    'name': row[1],
    'age': row[2],
    # ... Add other fields as needed
  })

# Convert the data to JSON format
json_data = json.dumps(formatted_data)

# Optionally validate the JSON data
try:
  validated_json = json.loads(json_data)
  print('JSON data is valid')
except json.JSONDecodeError as e:
  print('JSON data is not valid: ', str(e))

# Now you can send the validated JSON data to the JSON API
```

### How might you handle a large dataset when pulling data from the database and processing it before sending it to the API?

Use Pagination: Instead of fetching the entire dataset at once, consider using pagination to retrieve data in smaller chunks. This way, you can process and send one chunk at a time, reducing memory usage and processing load.

Batch Processing: If the dataset is too large to be processed in a single batch, break it into smaller batches and process each batch separately. This allows you to manage memory more efficiently and reduces the risk of running out of resources.

Streaming: If your database and API support streaming, consider streaming data directly from the database to the API without loading the entire dataset into memory. This can significantly reduce memory usage and improve processing efficiency.

Use Generators or Iterators: In Python, use generators or iterators instead of lists when dealing with large datasets. Generators allow you to lazily load data one item at a time, avoiding the need to load the entire dataset into memory.

Data Filtering: If possible, filter the data at the database level before retrieval. Use SQL queries or database-specific filters to fetch only the necessary data, reducing the amount of data that needs to be processed.

Optimize Queries: Optimize your SQL queries to retrieve data efficiently. Ensure that you have appropriate indexes on columns used in the queries and avoid retrieving unnecessary data.

Chunked Processing: Process the data in chunks rather than loading the entire dataset into memory at once. For example, read a chunk of data from the database, process it, and then send it to the API before moving on to the next chunk.

Asynchronous Processing: Consider using asynchronous processing to fetch data from the database, process it, and send it to the API concurrently. This can improve overall processing time for large datasets.

Data Compression: If the dataset contains large text or binary data, consider compressing the data before sending it to the API. Compression can reduce the size of the data and lower the network latency.

Monitor Resource Usage: Keep track of memory usage, CPU utilization, and network performance during the data processing and API calls. Monitor for any potential bottlenecks or performance issues.

# Error Handling and Data Validation

How would you handle exceptions and errors that may occur during the process of making API requests or interacting with the SQL database?
What kind of data validation would you consider implementing when pulling data from the database and preparing it for the API request?
In case the API response contains unexpected data or is not in the expected JSON format, how would you handle such a situation in your code?

# Security and Authentication

If the API requires authentication, how would you pass the necessary credentials in the HTTP POST request headers?
What security considerations would you keep in mind when interacting with a JSON API and a SQL database in your application?

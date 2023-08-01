## Technical Interview

This is my prepartion document for my technical interview for a Solutions Engineer role. I'll be showing how in Ruby and Python.

Programming experience

- Scripting (powershell, bash, python, or similar)
- Writing SQL queries
- Making REST API calls

Experience with the following technologies

- Windows and Linux Operating Systems and administration
- Enterprise networking, troubleshooting, architecture
- Deploying and troubleshooting remote applications

## Prompt

Write code to pull data from a SQL database and peform HTTP POST requests to a JSON API

## SQL Database Interaction

##### How would you connect to a SQL database?

SQLite

```
import sqlite3

# Connect to SQLite3 database
connection = sqlite3.connect('example.db')
```

Explain how you would execute a SQL query to retrieve data from a specific table in the database.
Can you demonstrate how to read the content of a SQL table?

#### HTTP POST requests and JSON API

How do you perform an HTTP POST request?
Can you explain the difference between GET and POST requests in the context of API calls?
When making an HTTP POST request to a JSON API, how would you send JSON data as part of the request body?
In the case the API responds with an error status code, how would you handle error responses?

#### Integrating SQL Database and JSON API

Suppose you have data stored in a SQL database. How would you retrieve that data and send it to a JSON API?
When pulling data from a SQL database, how would you ensure the data is in the correct format to be sent to a JSON API?
How might you handle a large dataset when pulling data from the database and processing it before sending it to the API?

#### Error Handling and Data Validation

How would you handle exceptions and errors that may occur during the process of making API requests or interacting with the SQL database?
What kind of data validation would you consider implementing when pulling data from the database and preparing it for the API request?
In case the API response contains unexpected data or is not in the expected JSON format, how would you handle such a situation in your code?

#### Security and Authentication

If the API requires authentication, how would you pass the necessary credentials in the HTTP POST request headers?
What security considerations would you keep in mind when interacting with a JSON API and a SQL database in your application?

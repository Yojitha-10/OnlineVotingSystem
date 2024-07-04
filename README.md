# Online Voting System

This is a simple online voting system implemented in Java. The system includes functionalities for user registration, login, casting votes, viewing results, and admin operations.

## Table of Contents

Prerequisites
Database Setup
Project Structure
How to Run
Entry Point

## Prerequisites

Before you begin, ensure you have the following software installed on your system:

- Java Development Kit (JDK) 8 or higher
- MySQL Server
- An IDE or text editor of your choice

## Database Setup

1. Start your MySQL server.
2. Create a new database named `voting`.
3. Use the following SQL commands to create the necessary tables:

```sql
CREATE DATABASE voting;

USE voting;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    password VARCHAR(50) NOT NULL,
    is_admin BOOLEAN DEFAULT FALSE
);
CREATE TABLE votes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id VARCHAR(50),
    candidate_id INT,
    FOREIGN KEY (candidate_id) REFERENCES candidates(id)
);

CREATE TABLE candidates (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    party VARCHAR(50) NOT NULL
);

INSERT INTO candidates (name, party) VALUES 
    ('Ram', 'TDP'),
    ('Sam', 'BJP'),
    ('Pawan Kalyan', 'Janasena');

SELECT v.id AS vote_id, u.username, v.candidate_id
FROM votes v
JOIN users u ON v.user_id = u.id;

##Project Structure

src
├── com
│   └── java
│       └── Networkbean
│           ├── Administration.java
│           ├── UserRegistration.java
│           ├── Votecounting.java
│           ├── Votingdemo.java
│           └── Votingmodule.java
├── com
│   └── mynetworking
│       ├── client
│       │   └── Votingclient.java
│       └── server
│           └── Votingserver.java


How to Run

    Clone this repository or download the source code.
    Open the project in your IDE or text editor.
    Ensure you have added the MySQL JDBC driver to your project's classpath.
    Update the database connection details in the Votingmodule.java file if necessary:

java

private Connection connect() {
    String url = "jdbc:mysql://localhost:3306/voting";
    String user = "root";
    String password = "Yojitha@2003";
    Connection conn = null;
    try {
        conn = DriverManager.getConnection(url, user, password);
    } catch (SQLException e) {
        System.out.println("Connection failed: " + e.getMessage());
    }
    return conn;
}

    Compile the Java source files. You can do this from the command line or your IDE.

sh

javac src/com/java/Networkbean/*.java src/com/mynetworking/client/*.java src/com/mynetworking/server/*.java

    Start the server by running the Votingserver class.

sh

java src/com/mynetworking/server/Votingserver

    Run the client by running the Votingclient class.

sh

java src/com/mynetworking/client/Votingclient

Entry Point

The entry point of the application is the Votingdemo class. This class contains the main method which provides a menu-driven interface for interacting with the online voting system.

java

public class Votingdemo {
    public static void main(String[] args) {
        // Code for the menu and application logic
    }
}


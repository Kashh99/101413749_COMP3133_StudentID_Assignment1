# Employee Management System (EMS) Backend
---

## Overview

This project is a backend implementation of an Employee Management System (EMS) using **Node.js**, **Express**, **GraphQL (Apollo Server)**, and **MongoDB**. It provides a secure authentication system with JWT and a set of API endpoints to manage employee data efficiently.

---

## Features

- **User Authentication:**
  - Secure signup and login with JWT-based authentication.
- **Employee Management:**
  - Retrieve all employees.
  - Fetch employee details by ID.
  - Search employees by department or designation.
  - Add, update, and delete employee records.
- **Validation & Error Handling:**
  - Input validation using `express-validator`.
  - Robust error handling to ensure API stability.

---

## Project Structure

```
COMP3133_Assignment1/
├── .env                  # Environment configuration
├── .gitignore            # Files and directories to ignore in Git
├── package.json          # Project dependencies and scripts
├── README.md             # Project documentation (this file)
└── src/
    ├── config/
    │   ├── db.js         # MongoDB connection configuration
    │   └── jwt.js        # JWT token generation and verification
    ├── middleware/
    │   ├── auth.js       # Authentication middleware
    │   └── validators.js # Input validation using express-validator
    ├── models/
    │   ├── Employee.js   # Mongoose schema for employees
    │   └── User.js       # Mongoose schema for users
    ├── resolvers/
    │   ├── employeeResolver.js  # GraphQL resolvers for employees
    │   ├── userResolver.js      # GraphQL resolvers for authentication
    │   └── index.js             # Combined resolvers
    ├── typeDefs/
    │   ├── employee.graphql     # GraphQL schema for employee operations
    │   ├── user.graphql         # GraphQL schema for user authentication
    │   └── index.js             # Merged type definitions
    ├── utils/
    │   └── errorHandler.js      # Optional custom error handling
    └── server.js         # Entry point for the server
```

---

## Installation

1. **Clone the Repository:**

   ```bash
   git clone https://github.com/yourusername/Student#_COMP3133_StudentID_Assignment1.git
   cd Student#_COMP3133_StudentID_Assignment1
   ```

2. **Install Dependencies:**

   ```bash
   npm install
   ```

3. **Set Up Environment Variables:**

   Create a `.env` file in the project root with the following content:

   ```ini
   PORT=4000
   MONGODB_URI=<your_mongodb_connection_string>
   JWT_SECRET=<your_jwt_secret>
   TOKEN_EXPIRES_IN=1h
   ```

4. **Run the Server:**

   ```bash
   npm start
   ```
   *For development with auto-restart, use:*
   ```bash
   npx nodemon src/server.js
   ```

---

## API Usage

### GraphQL Playground

Access the GraphQL Playground at:
```
http://localhost:4000/graphql
```

For protected operations, include the JWT token in your HTTP headers:

```json
{
  "Authorization": "Bearer <your_jwt_token>"
}
```

### Example Operations

#### **User Authentication**

- **Signup:**

  ```graphql
  mutation {
    signup(username: "testuser", email: "test@example.com", password: "password123") {
      token
      user {
        id
        username
        email
      }
    }
  }
  ```

- **Login:**

  ```graphql
  query {
    login(usernameOrEmail: "testuser", password: "password123") {
      token
      user {
        id
        username
        email
      }
    }
  }
  ```

#### **Employee Operations** *(Requires Authorization)*

- **Get All Employees:**

  ```graphql
  query {
    getAllEmployees {
      id
      first_name
      last_name
      email
      designation
      department
      salary
      date_of_joining
    }
  }
  ```

- **Get Employee by ID:**

  ```graphql
  query {
    getEmployeeById(id: "employee_id_here") {
      id
      first_name
      last_name
      email
      gender
      designation
      salary
      date_of_joining
      department
      employee_photo
    }
  }
  ```

- **Search Employee by Department/Designation:**

  ```graphql
  query {
    searchEmployeeByDeptDesg(department: "Engineering", designation: "Developer") {
      id
      first_name
      last_name
      email
      designation
      department
    }
  }
  ```

- **Add Employee:**

  ```graphql
  mutation {
    addEmployee(
      first_name: "John",
      last_name: "Doe",
      email: "john.doe@example.com",
      gender: "Male",
      designation: "Developer",
      salary: 1500,
      date_of_joining: "2023-01-15",
      department: "Engineering",
      employee_photo: "john_doe.png"
    ) {
      id
      first_name
      last_name
      email
    }
  }
  ```

---

## Git & Repository Management

- Ensure frequent commits with descriptive commit messages.
- Use the provided `.gitignore` file to exclude unnecessary files.
- Submit the repository link as required by the assignment guidelines.

---

## License

This project is for educational purposes. © 2025 Kashyap Mavani | George Brown College

---

## Contact

For questions or issues, please contact:  
[Kashyap Mavani] – [kashyapmavani@gmail.com]

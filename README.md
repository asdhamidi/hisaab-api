# Hisaab API

**Hisaab API** is a backend service designed to manage shared expenses, built using Flask, MongoDB, and JWT-based authentication. This API enables users to manage their expenses by allowing them to create, retrieve, update, and delete expense entries. It also tracks who owes whom and supports user registration, login, and registration code generation.

## Key Features

- **User Authentication**: Allows user registration, login, and secure access to routes using JWT tokens.
- **Expense Management**: Supports operations to create, view, update, and delete expense entries.
- **Access Control**: Ensures that only the user who created an expense entry can update or delete it.
- **Registration Codes**: Provides functionality to generate and validate registration codes for user sign-up.
- **Cross-Origin Resource Sharing (CORS)**: CORS is enabled for all routes to support cross-origin requests.

## Getting Started

### Prerequisites

To run the Hisaab API, you will need:

- Python 3.7 or higher
- MongoDB
- Pipenv or virtualenv (recommended for managing dependencies)

### Installation

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/asdhamidi/hisaab-api.git
   ```

2. **Navigate to the Project Directory:**
   ```bash
   cd hisaab-api
   ```

3. **Install Required Packages:**
   ```bash
   pip install -r requirements.txt
   ```

### Running the Application

1. **Start the Flask Server:**
   ```bash
   cd api/
   flask run
   ```

2. The server will start on `http://127.0.0.1:5000/`. You can use tools like Postman or `curl` to interact with the API.

## API Overview

### Public Endpoints

- **`GET /`**: Returns a welcome message.
- **`POST /register`**: Registers a new user.
- **`POST /login`**: Authenticates a user and generates a JWT token.

### Protected Endpoints (Require JWT Token)

- **`GET /entries`**: Fetches all expense entries.
- **`GET /entries/<id>`**: Fetches a specific expense entry by its ID.
- **`POST /entries`**: Creates a new expense entry.
- **`PUT /entries/<id>`**: Updates an existing expense entry, accessible only to the entry creator.
- **`DELETE /entries/<id>`**: Deletes an existing expense entry, accessible only to the entry creator.
- **`POST /generate_code`**: Generates a registration code for user sign-up.
- **`POST /stats/daily`**: Fetches daily expense statistics for a specified month.
- **`POST /stats/daily_person`**: Fetches daily expense statistics grouped by person for a specified month.
- **`GET /clear/month`**: Clears all entries for the current month.
- **`GET /users`**: Retrieves all registered usernames.

### Authentication

JWT tokens are required for accessing protected routes. Include the JWT token in the `Authorization` header as `Bearer <your_token>`.

## Example API Requests

### Register a New User

```bash
curl -X POST http://127.0.0.1:5000/register \
-H "Content-Type: application/json" \
-d '{
    "username": "john_doe",
    "password": "secure_password",
    "register_code": "123456"
}'
```

### Login and Obtain JWT Token

```bash
curl -X POST http://127.0.0.1:5000/login \
-H "Content-Type: application/json" \
-d '{
    "username": "john_doe",
    "password": "secure_password"
}'
```

### Create a New Expense Entry

```bash
curl -X POST http://127.0.0.1:5000/entries \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <your_token>" \
-d '{
    "items": ["Dinner", "Drinks"],
    "price": 150,
    "owed_all": false,
    "owed_by": {"user1", "user2"},
    "notes": "Team outing"
}'
```

### Get Daily Expense Stats for a Month

```bash
curl -X POST http://127.0.0.1:5000/stats/daily \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <your_token>" \
-d '{
    "month": "8/24"
}'
```

### Get Daily Expense Stats Grouped by Person for a Month

```bash
curl -X POST http://127.0.0.1:5000/stats/daily_person \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <your_token>" \
-d '{
    "month": "8/24"
}'
```

## License

The Hisaab API is released into the public domain. You are free to use, modify, distribute, or simply ignore it as you see fit.
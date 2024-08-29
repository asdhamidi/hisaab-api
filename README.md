# Hisaab API

**Hisaab API** is a backend service for managing shared expenses. Built with Flask, MongoDB, and JWT-based authentication, it allows users to create, retrieve, update, and delete expense entries while keeping track of who owes whom. The API also includes user registration, login, and registration code generation features.

## Features

- **User Authentication**: Register, login, and secure routes using JWT tokens.
- **Expense Management**: Create, view, update, and delete expense entries.
- **Access Control**: Restrict update and delete operations to the user who created the entry.
- **Registration Codes**: Generate and validate registration codes for user sign-up.
- **Cross-Origin Resource Sharing (CORS)**: Enabled for all routes.

## Installation

### Prerequisites

- Python 3.7+
- MongoDB
- Pipenv or virtualenv (optional but recommended for managing dependencies)

### Setup & Installation

1. Clone the repository:
    ```bash
    git clone https://github.com/asdhamidi/hisaab-api.git
    ```

2. Navigate to the project directory:
    ```bash
    cd hisaab-api
    ```

3. Install the required packages:
    ```bash
    pip install -r requirements.txt
    ```

## Usage

1. Start the Flask server:
    ```bash
    cd api/
    flask run
    ```

2. The server will run on `http://127.0.0.1:5000/`. You can use tools like Postman or curl to interact with the API endpoints.

## API Endpoints

### Public Endpoints

- **`GET /`**: Welcome message.
- **`POST /register`**: Register a new user.
- **`POST /login`**: User login and JWT token generation.

### Protected Endpoints

- **`GET /entries`**: Retrieve all expense entries.
- **`GET /entries/<id>`**: Retrieve a specific expense entry by ID.
- **`POST /entries`**: Create a new expense entry (requires JWT token).
- **`PUT /entries/<id>`**: Update an existing expense entry (requires JWT token and ownership).
- **`DELETE /entries/<id>`**: Delete an existing expense entry (requires JWT token and ownership).
- **`POST /generate_code`**: Generate a registration code (requires JWT token).
- **`POST /stats/daily`**: Get daily expense statistics for a specified month (requires month parameter).
- **`POST /stats/daily_person`**: Get daily expense statistics grouped by person for a specified month (requires month parameter).
- **`GET /clear/month`**: Clear all entries for the current month (requires JWT token).
- **`GET /users`**: Retrieve all registered usernames.

### Authentication

JWT tokens are required for accessing protected routes. Include the token in the `Authorization` header as `Bearer <your_token>`.

## Usage Example

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

### Login

```bash
curl -X POST http://127.0.0.1:5000/login \
-H "Content-Type: application/json" \
-d '{
    "username": "john_doe",
    "password": "secure_password"
}'
```

### Create a New Entry

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

### Get Daily Stats for a Month

```bash
curl -X POST http://127.0.0.1:5000/stats/daily \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <your_token>" \
-d '{
    "month": "8/24"
}'
```

### Get Daily Stats Grouped by Person for a Month

```bash
curl -X POST http://127.0.0.1:5000/stats/daily_person \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <your_token>" \
-d '{
    "month": "8/24"
}'
```

## License

This project is licensed under... well, no specific license. Feel free to use it however you like. Consider it public domain—use it, modify it, share it, or just ignore it.

---

### Key Changes Made in README

- **Updated Protected Endpoints**: Added new endpoints for daily stats and grouped stats (`/stats/daily` and `/stats/daily_person`).
- **Example Usage Section**: Added examples for the new `POST /stats/daily` and `POST /stats/daily_person` endpoints to demonstrate how to use them.
- **Protected Endpoints Summary**: Adjusted the list to reflect the new methods and their requirements.
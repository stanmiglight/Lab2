# User Management API

This project is a RESTful API built with [FastAPI](https://fastapi.tiangolo.com/) to manage user data. It allows you to perform CRUD (Create, Read, Update, Delete) operations on a simulated user database.

## Features
- Retrieve a list of all users or a specific user by ID.
- Add a new user to the database.
- Update an existing user's information.
- Delete a user from the database.

## Requirements

Before running the API, ensure you have the following installed:
- Python 3.7+
- FastAPI
- Uvicorn (for running the server)

## Installation

1. Clone this repository or copy the `main.py` file.
2. Install the required Python packages:
   ```bash
   pip install fastapi uvicorn pydantic
   ```

## Running the API

To run the API locally, execute the following command in your terminal:
```bash
uvicorn main:app --reload
```

- The server will start at `http://127.0.0.1:8000`.

## Endpoints

### Retrieve Users

**GET** `/users`

#### Query Parameters:
- `user_id` (optional): The ID of the user to retrieve.

#### Response:
- If `user_id` is provided and found:
  ```json
  {
      "status": "ok",
      "result": {
          "user_id": <id>,
          "name": "<name>"
      }
  }
  ```
- If `user_id` is provided but not found:
  ```json
  {
      "error": "User not found"
  }
  ```
- If no `user_id` is provided:
  ```json
  {
      "status": "ok",
      "result": [
          {
              "user_id": 1,
              "name": "John Doe"
          },
          ...
      ]
  }
  ```

### Create User

**POST** `/users`

#### Request Body:
- `user_id` (int): The unique ID of the user.
- `name` (str): The name of the user.

#### Response:
- If the user is successfully created:
  ```json
  {
      "status": "ok",
      "result": {
          "user_id": <id>,
          "name": "<name>"
      }
  }
  ```
- If the `user_id` already exists:
  ```json
  {
      "error": "User ID already exists"
  }
  ```

### Update User

**PUT** `/users/{user_id}`

#### Path Parameters:
- `user_id` (int): The ID of the user to update.

#### Request Body:
- `user_id` (int): The ID of the user (must match the path parameter).
- `name` (str): The new name of the user.

#### Response:
- If the user is successfully updated:
  ```json
  {
      "status": "ok",
      "updated_data": {
          "user_id": <id>,
          "name": "<name>"
      }
  }
  ```
- If the `user_id` does not exist:
  ```json
  {
      "error": "User not found. Cannot update record"
  }
  ```

### Delete User

**DELETE** `/users/{user_id}`

#### Path Parameters:
- `user_id` (int): The ID of the user to delete.

#### Response:
- If the user is successfully deleted:
  ```json
  {
      "status": "ok",
      "removed_data": {
          "user_id": <id>,
          "name": "<name>"
      }
  }
  ```
- If the `user_id` does not exist:
  ```json
  {
      "error": "User not found. Cannot delete record"
  }
  ```

## Notes
- The `users_db` is a simulated in-memory database and is reset every time the server restarts.
- The API is designed to demonstrate basic CRUD operations and can be expanded further for real-world use.

## Contributions
Feel free to submit issues or pull requests if you have improvements or suggestions!

#  Pizza Restaurant API

A RESTful Flask API for managing pizza restaurants, their menus, and associated pizzas. This backend was built as part of a Phase 4 code challenge at Moringa School.

##  Features

- View all restaurants
- View a specific restaurant and its available pizzas
- Delete a restaurant and its associated records
- View all pizzas
- Associate pizzas with restaurants at specific prices (with validation)

---

##  Tech Stack

- **Python 3**
- **Flask**
- **SQLAlchemy**
- **Flask-Migrate**
- **PostgreSQL / SQLite**
- **Postman** (for API testing)

---

##  Data Models

### Restaurant
- `id`: Integer (Primary Key)
- `name`: String
- `address`: String

### Pizza
- `id`: Integer (Primary Key)
- `name`: String
- `ingredients`: String

### RestaurantPizza (Join Table)
- `id`: Integer (Primary Key)
- `price`: Integer (1 to 30)
- `restaurant_id`: ForeignKey
- `pizza_id`: ForeignKey

---

## Setup Instructions

### 1. Clone the repository

```bash
git clone https://github.com/gabucodes/python-phase-4-code-challenge-pizza.git
cd python-phase-4-code-challenge-pizza


#  Install dependencies

pipenv install
pipenv shell


# Set up the database

export FLASK_APP=server/app.py
flask db init
flask db migrate -m "Initial migration"
flask db upgrade
python server/seed.py


# Start the Flask server

python server/app.py


API Endpoints
GET /restaurants
Returns a list of all restaurants.

json

[
  {
    "id": 1,
    "name": "Karen's Pizza Shack",
    "address": "address1"
  }
]
GET /restaurants/<int:id>
Returns one restaurant and its associated pizzas.

json

{
  "id": 1,
  "name": "Karen's Pizza Shack",
  "address": "address1",
  "restaurant_pizzas": [
    {
      "id": 1,
      "price": 5,
      "pizza_id": 1,
      "restaurant_id": 1,
      "pizza": {
        "id": 1,
        "name": "Emma",
        "ingredients": "Dough, Tomato Sauce, Cheese"
      }
    }
  ]
}
If the restaurant doesn’t exist:

json

{
  "error": "Restaurant not found"
}
DELETE /restaurants/<int:id>
Deletes a restaurant and all related RestaurantPizza entries.

Success: 204 No Content
If not found:

json

{
  "error": "Restaurant not found"
}
GET /pizzas
Returns all pizzas.

json
[
  {
    "id": 1,
    "name": "Emma",
    "ingredients": "Dough, Tomato Sauce, Cheese"
  }
]
POST /restaurant_pizzas
Associates a pizza with a restaurant at a specific price.

Request Body:
json

{
  "price": 5,
  "pizza_id": 1,
  "restaurant_id": 3
}
Success Response:
json

{
  "id": 4,
  "price": 5,
  "pizza_id": 1,
  "restaurant_id": 3,
  "pizza": {
    "id": 1,
    "name": "Emma",
    "ingredients": "Dough, Tomato Sauce, Cheese"
  },
  "restaurant": {
    "id": 3,
    "name": "Kiki's Pizza",
    "address": "address3"
  }
}
Validation Error (e.g., price > 30):
json

{
  "errors": ["price must be between 1 and 30"]
}


# Testing
You can test this API using:

✅ Postman

Postman collection: challenge-1-pizzas.postman_collection.json


Author
Gabriel Kipkoech
Moringa School - Phase 4

# license
 at LICENCE.md
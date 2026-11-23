# E-commerce Microservices Application

A basic e-commerce application built with Node.js, Express.js, and MongoDB, following a Microservices Architecture.

## Project Structure

- **API Gateway (Port 3000):** Single entry point, routes requests, handles JWT verification and rate limiting.
- **User Service (Port 3001):** Manages user registration, login, and profiles.
- **Product Service (Port 3002):** Manages product catalog (CRUD).
- **Order Service (Port 3003):** Manages order placement and history.
- **Cart Service (Port 3004):** Manages user shopping carts.

## Tech Stack

- **Runtime:** Node.js
- **Framework:** Express.js
- **Database:** MongoDB with Mongoose ODM
- **Authentication:** JWT (JSON Web Token)
- **Password Hashing:** bcryptjs
- **Inter-service Communication:** REST API
- **Environment Variables:** dotenv
- **Middleware:** http-proxy-middleware, express-rate-limit, cors, helmet, morgan

## Prerequisites

- Node.js installed
- MongoDB installed and running locally (or provide a cloud URI)

## Setup and Installation

1. Clone the repository.
2. Navigate to each service directory and install dependencies:
   ```bash
   cd user-service && npm install
   cd ../product-service && npm install
   cd ../order-service && npm install
   cd ../cart-service && npm install
   cd ../api-gateway && npm install
   ```
3. Create a `.env` file in each service directory based on the `.env.example` provided in each folder.
4. Update the `MONGO_URI` in each `.env` file if necessary.

## Running the Services

To run all services simultaneously, you can open separate terminal windows for each service or use a tool like `concurrently`.

**Using separate terminals:**
```bash
# Terminal 1
cd user-service && npm start
# Terminal 2
cd product-service && npm start
# Terminal 3
cd order-service && npm start
# Terminal 4
cd cart-service && npm start
- Terminal 5
cd api-gateway && npm start
```

## Data Seeding

You can seed the database with sample users and products:

**Seed Users:**
```bash
cd user-service
node seeder.js
```

**Seed Products:**
```bash
cd product-service
node seeder.js
```

**Destroy Data:**
To clear the data, use the `-d` flag:
```bash
node seeder.js -d
```

## Postman Collection

A Postman collection is provided in the root directory: `postman_collection.json`.

1. Import `postman_collection.json` into Postman.
2. The collection uses a `base_url` variable (default: `http://localhost:3000`).
3. To use protected routes:
   - Run the **Login User** request. It will automatically save the JWT token to the `token` environment/collection variable.
   - Subsequent requests will use this token in the Authorization header.

## API Endpoints (via API Gateway - Port 3000)

### User Service
- `POST /api/users/register` - Register a new user
- `POST /api/users/login` - Login and get JWT
- `GET /api/users/profile` - Get user profile (Protected)
- `PUT /api/users/profile` - Update user profile (Protected)

### Product Service
- `GET /api/products` - Get all products (Paginated)
- `GET /api/products/:id` - Get single product
- `POST /api/products` - Create product (Admin Only)
- `PUT /api/products/:id` - Update product (Admin Only)
- `DELETE /api/products/:id` - Delete product (Admin Only)

### Order Service
- `POST /api/orders` - Place new order (Protected)
- `GET /api/orders` - Get user's orders (Protected)
- `GET /api/orders/:id` - Get order details (Protected/Admin)
- `PUT /api/orders/:id/status` - Update order status (Admin Only)

### Cart Service
- `GET /api/cart` - Get user's cart (Protected)
- `POST /api/cart/add` - Add item to cart (Protected)
- `PUT /api/cart/update` - Update item quantity (Protected)
- `DELETE /api/cart/remove/:id` - Remove item from cart (Protected)
- `DELETE /api/cart/clear` - Clear cart (Protected)

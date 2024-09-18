# Online Sales System API

This project is an API for managing an online sales system. It provides functionality for user registration, authentication, address management, and product orders. The system implements role-based access control, caching for frequently used data, and JWT-based authentication, all while interacting with a PostgreSQL database via TypeORM.

## Features

- **User Registration**: Register new users with validation and password hashing.
- **Authentication**: Secure login and token-based access control (JWT).
- **Address Management**: Associate addresses with users for delivery purposes.
- **Product Management**: Manage product listings and availability.
- **Order Management**: Create, update, and track orders.
- **Role-Based Access Control**: Different access levels for users and administrators.
- **Caching**: Improves performance for frequently accessed data (e.g., cities and states).
  
## Technologies Used

- **NestJS**: Framework for building the server-side application.
- **TypeORM**: ORM for database management.
- **PostgreSQL**: Relational database for storing users, addresses, products, and orders.
- **JWT (JSON Web Token)**: For authentication and access control.
- **Bcrypt**: For secure password hashing.
- **CacheManager**: For caching frequently used data and improving performance.
- **Class-Validator**: For request validation.

## Project Structure

```bash
src/
│
├── address/             # Address management module
├── auth/                # Authentication and authorization module
├── cache/               # Caching services
├── city/                # City management module
├── state/               # State management module
├── user/                # User management module
├── product/             # Product management module
├── order/               # Order management module
├── decorators/          # Custom decorators for roles and user identification
├── guards/              # Role-based access control guards
└── main.ts              # Application bootstrap
```

## Endpoints

### Auth
- `POST /auth`: Login and retrieve an access token.
  - **Body**: `{ "email": "user@example.com", "password": "password" }`
  - **Response**: `{ "accessToken": "token", "user": { ... } }`

### Users
- `POST /user`: Create a new user.
  - **Body**: `{ "name": "John Doe", "email": "john@example.com", "cpf": "123456789", "phone": "123-456-7890", "password": "password" }`
  - **Response**: User entity.
  
- `GET /user`: Retrieve all users.
  - **Response**: List of user entities.

- `GET /user/:userId`: Retrieve a user by ID.
  - **Response**: User entity with related addresses.

### Addresses
- `POST /address`: Create a new address for a user (Authenticated).
  - **Body**: `{ "complement": "Apartment 101", "numberAddress": 101, "cep": "12345-678", "cityId": 1 }`
  - **Response**: Address entity.

### Cities
- `GET /city/:stateId`: Get cities by state ID.
  - **Response**: List of city entities.

### States
- `GET /state`: Retrieve all states.
  - **Response**: List of state entities.

### Products
- `POST /product`: Add a new product (Admin only).
  - **Body**: `{ "name": "Product Name", "description": "Product description", "price": 100, "quantity": 10 }`
  - **Response**: Product entity.

- `GET /products`: Retrieve all products.
  - **Response**: List of product entities.

- `GET /product/:productId`: Retrieve a product by ID.
  - **Response**: Product entity.

### Orders
- `POST /order`: Place a new order (Authenticated).
  - **Body**: `{ "productId": 1, "quantity": 2, "addressId": 1 }`
  - **Response**: Order entity.

- `GET /orders`: Retrieve all orders for the logged-in user.
  - **Response**: List of order entities.

## Installation

1. **Clone the repository**:

   ```bash
   git clone https://github.com/your-repository.git
   ```

2. **Install dependencies**:

   ```bash
   npm install
   ```

3. **Set up environment variables**:
   
   Create a `.env.development.local` file in the root of the project with the following:

   ```env
   DB_HOST=your_postgres_host
   DB_PORT=5432
   DB_USERNAME=your_postgres_username
   DB_PASSWORD=your_postgres_password
   DB_DATABASE=your_postgres_db_name
   JWT_SECRET=your_jwt_secret
   JWT_EXPIRES_IN=3600
   ```

4. **Run migrations**:

   Make sure to have PostgreSQL running and then run:

   ```bash
   npm run migration:run
   ```

5. **Run the application**:

   ```bash
   npm run start:dev
   ```

   The application will be running on `http://localhost:3000`.

## Running Tests

Run unit tests:

```bash
npm run test
```

Run e2e tests:

```bash
npm run test:e2e
```

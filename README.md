# Project CODE - E-commerce API

This repository contains a RESTful API for an e-commerce system developed as part of the Project CODE  initiative. The API provides comprehensive functionality for managing users, products, shopping carts, and orders.

## Technologies Used

- **Node.js** for backend development
- **Express.js** for creating a robust and scalable web application
- **MongoDB** for storing product, user, and order data
- **JWT (JSON Web Tokens)** for user authentication and authorization
- **RESTful API** designed and implemented to allow access to backend functionality from external clients, such as a web frontend or mobile app
- **Git** for code version control

## Repository Structure

The repository is organized as follows:

- **src/**: Source code directory
  - **config/**: Configuration files
    - **database.js**: Database configuration
    - **jwt.js**: JWT configuration
  - **controllers/**: Application controllers
    - **authController.js**: Authentication management
    - **cartController.js**: Cart management
    - **orderController.js**: Order management
    - **productController.js**: Product management
  - **middleware/**: Application middleware
    - **auth.js**: JWT authentication
    - **admin.js**: Admin authorization
  - **models/**: Database models
    - **User.js**: User model
    - **Product.js**: Product model
    - **Cart.js**: Cart model
    - **Order.js**: Order model
  - **routes/**: API routes
    - **auth.js**: Authentication endpoints
    - **products.js**: Product management endpoints
    - **cart.js**: Cart management endpoints
    - **orders.js**: Order management endpoints
  - **utils/**: Utilities
    - **errorHandler.js**: Error handling
    - **adminWhitelist.js**: Admin email whitelist
  - **app.js**: Main application file
  - **server.js**: Server startup file

- **docs/**: Documentation
  - **api-docs.md**: API documentation
  - **postman-collection.json**: Postman collection for testing the API

## API Endpoints

### Authentication API

- `POST /api/auth/register`: Allows generic users to register by providing necessary information such as name, email, and password.
- `POST /api/auth/admin/register`: Allows admin users to register by providing necessary information such as name, email, and password. Implements email verification against a whitelist of email addresses authorized for Admin access.
- `POST /api/auth/login`: Allows users to log in using their credentials.
- `GET /api/auth/logout`: Allows users to log out.
- `GET /api/auth/user`: Returns information about the currently authenticated user (generic or Admin).

### Product Management API

- `GET /api/products`: Returns the complete list of products available in the catalog.
  - Optional: Implements a pagination system to improve API performance.
- `GET /api/products/:id`: Returns the details of a single product (identified by its ID).
- `POST /api/products`: Allows Admin users to add a new product to the catalog.
- `PUT /api/products/:id`: Allows Admin users to modify the information of an existing product.
- `DELETE /api/products/:id`: Allows Admin users to remove a product from the catalog.

### Shopping Cart Management API

- `GET /api/cart`: Returns the current contents of the user's cart.
- `POST /api/cart/add/:id`: Adds a product to the user's cart.
- `DELETE /api/cart/remove/:id`: Removes a product from the user's cart.
- `DELETE /api/cart/clear`: Empties the user's cart.

### Order Management API

- `GET /api/orders`: Returns the user's order history.
  - Optional: Implements a pagination system to improve API performance.
- `POST /api/orders`: Allows users to create a new order from the products currently in the cart, with the addition of necessary shipping data:
  - First Name
  - Last Name
  - Address
  - Zip Code
  - City
  - Region
  - Country
- `GET /api/orders/:id`: Returns the details of a single order identified by its ID.
- `PUT /api/orders/:id`: Allows administrators to update the status of an existing order.
- `DELETE /api/orders/:id`: Allows administrators to cancel an order. Suggestion: modify the order status.

## Data Models

### User Model
```javascript
{
  name: String,
  email: String,
  password: String,
  role: String, // "user" or "admin"
  createdAt: Date,
  updatedAt: Date
}
```

### Product Model
```javascript
{
  name: String,
  description: String,
  price: Number,
  imageUrl: String,
  category: String,
  stock: Number,
  createdAt: Date,
  updatedAt: Date
}
```

### Cart Model
```javascript
{
  userId: ObjectId,
  items: [
    {
      productId: ObjectId,
      quantity: Number,
      price: Number
    }
  ],
  totalPrice: Number,
  updatedAt: Date
}
```

### Order Model
```javascript
{
  userId: ObjectId,
  items: [
    {
      productId: ObjectId,
      name: String,
      quantity: Number,
      price: Number
    }
  ],
  totalPrice: Number,
  shippingDetails: {
    firstName: String,
    lastName: String,
    address: String,
    zipCode: String,
    city: String,
    region: String,
    country: String
  },
  status: String, // "pending", "processing", "shipped", "delivered", "cancelled"
  createdAt: Date,
  updatedAt: Date
}
```

## Getting Started

To use this API:

1. Clone this repository
```bash
git clone https://github.com/yourusername/code-project-work.git
cd code-project-work
```

2. Install dependencies
```bash
npm install
```

3. Configure environment variables
   - Create a `.env` file in the root directory
   - Add the following variables:
     ```
     PORT=3000
     MONGODB_URI=your_mongodb_connection_string
     JWT_SECRET=your_jwt_secret
     ADMIN_WHITELIST=admin1@example.com,admin2@example.com
     ```

4. Start the development server
```bash
npm run dev
```

5. The server will be available at `http://localhost:3000`

## API Documentation

Complete API documentation is available in the `docs/api-docs.md` file. You can also import the Postman collection from `docs/postman-collection.json` to explore and test all available endpoints.

## Requirements

- Node.js (v14 or higher)
- MongoDB
- npm or yarn

## Contributing

This project was developed as part of the CODE Project initiative. To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

*This repository was created as part of the educational journey at CODE Project.*
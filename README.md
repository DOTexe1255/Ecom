# Ecom – Cosmetics E-Commerce Website

A full-stack PHP/MySQL e-commerce web application for a cosmetics store, featuring a customer-facing storefront and a complete admin panel.

---

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Database Schema](#database-schema)
- [Getting Started](#getting-started)
- [Configuration](#configuration)
- [Admin Panel](#admin-panel)
- [Screenshots](#screenshots)
- [License](#license)

---

## Features

### Customer Storefront
- Browse and search products by category
- Detailed product pages with images and descriptions
- Customer reviews and ratings (1–5 stars)
- User registration, login, and password reset (via PHPMailer)
- Shopping cart and checkout flow
- Multiple payment methods: Credit Card, PayPal, Bank Transfer, Cash on Delivery
- Shipping address management
- Wishlist
- User dashboard (order history, profile)

### Admin Panel
- Secure admin login
- Product management (add / edit / delete, with category assignment)
- Category management
- Order management with status updates (Pending → Processing → Shipped → Delivered → Cancelled)
- Payment management and refunds
- User management (view / edit / delete)
- Audit logs for tracking admin actions
- Site settings

---

## Tech Stack

| Layer      | Technology |
|------------|------------|
| Backend    | PHP 8+ (procedural + MVC-style controllers/models) |
| Database   | MySQL (PDO) |
| Frontend   | HTML5, CSS3, JavaScript |
| Email      | [PHPMailer](https://github.com/PHPMailer/PHPMailer) |
| Web Server | Apache / Nginx (any PHP-capable server) |

---

## Project Structure

```
cosmetics_website/
├── admin/                  # Admin panel pages
│   ├── index.php           # Dashboard
│   ├── login.php
│   ├── manage_products.php
│   ├── manage_categories.php
│   ├── manage_users.php
│   ├── manage_orders.php
│   ├── manage_payments.php
│   ├── settings.php
│   └── ...
│
├── public_html/            # Customer-facing pages
│   ├── index.php           # Homepage
│   ├── products.php
│   ├── product_detail.php
│   ├── cart.php
│   ├── checkout.php
│   ├── login.php / register.php
│   ├── user_dashboard.php
│   ├── reviews.php
│   └── ...
│
├── controllers/            # MVC controllers
│   ├── product_controller.php
│   ├── user_controller.php
│   ├── order_controller.php
│   └── payment_controller.php
│
├── models/                 # MVC models (DB operations)
│   ├── product_model.php
│   ├── user_model.php
│   ├── order_model.php
│   ├── payment_model.php
│   └── category_model.php
│
├── includes/               # Shared PHP includes
│   ├── db_connection.php   # PDO database connection (singleton)
│   ├── header.php
│   ├── footer.php
│   ├── admin_header.php
│   └── admin_footer.php
│
├── PHPMailer/              # PHPMailer library (password reset emails)
├── docs/                   # Documentation
│   └── setup_guide.md
├── create_tables.sql       # SQL script to initialise the database
└── file_system.txt         # Project structure reference
```

---

## Database Schema

The database (`cosmetics_db`) contains the following tables:

| Table              | Description |
|--------------------|-------------|
| `users`            | Registered customers and admins (role-based) |
| `categories`       | Product categories |
| `products`         | Product catalogue (name, price, stock, image, category) |
| `orders`           | Customer orders with status tracking |
| `order_items`      | Individual line items within an order |
| `reviews`          | Product reviews with 1–5 star ratings |
| `shipping_addresses` | Saved shipping addresses per user |
| `payments`         | Payment records linked to orders |
| `wishlist`         | Saved/wishlisted products per user |
| `audit_logs`       | Admin action tracking |
| `settings`         | Key-value site configuration |

Full schema: [`create_tables.sql`](create_tables.sql)

---

## Getting Started

### Prerequisites
- PHP 8.0 or higher
- MySQL 5.7+ or MariaDB 10+
- A web server (Apache with `mod_rewrite`, Nginx, or XAMPP/WAMP locally)
- Composer (optional, if reinstalling PHPMailer)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/DOTexe1255/Ecom.git
   cd Ecom
   ```

2. **Set up the database**
   ```bash
   mysql -u root -p < create_tables.sql
   ```
   This creates the `cosmetics_db` database and all required tables.

3. **Configure the database connection**  
   Open `includes/db_connection.php` and update the credentials:
   ```php
   $host = 'localhost';
   $db   = 'cosmetics_db';
   $user = 'your_db_user';
   $pass = 'your_db_password';
   ```

4. **Configure email (password reset)**  
   Update PHPMailer settings in the relevant controller/reset file with your SMTP credentials.

5. **Point your web server** document root at the repository root, or place the project inside your server's `htdocs` / `www` folder.

6. **Open in browser**
   ```
   http://localhost/Ecom/public_html/
   ```

---

## Configuration

| File | What to configure |
|------|-------------------|
| `includes/db_connection.php` | Database host, name, username, password |
| PHPMailer settings | SMTP host, port, username, password, sender address |

---

## Admin Panel

Access the admin panel at:
```
http://localhost/Ecom/admin/
```

Create an admin user by inserting a record with `role = 'admin'` into the `users` table (password must be stored as a PHP `password_hash()` hash):

```sql
INSERT INTO users (username, password, email, role)
VALUES ('admin', '<hashed_password>', 'admin@example.com', 'admin');
```

---

## License

This project is for educational purposes. See [LICENSE](LICENSE) if one is present, otherwise all rights are reserved by the author.

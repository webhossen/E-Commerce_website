# BD-Fashion — Digital Product Marketplace

BD-Fashion is a full-stack digital product marketplace built with **PHP (7.4+)** and **MySQL (MariaDB)**, featuring a responsive Bootstrap front-end and a companion Android app built with **Capacitor**.

---

## Table of Contents

- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Database](#database)
- [File & Folder Count](#file--folder-count)
- [Features](#features)
- [Admin Panel & Role System](#admin-panel--role-system)
- [Admin Roles Explained](#admin-roles-explained)
- [Mobile App](#mobile-app)
- [Quick Start](#quick-start)
- [Security](#security)
- [Customization](#customization)

---

## Tech Stack

| Layer        | Technology                                      |
| ------------ | ----------------------------------------------- |
| **Backend**  | PHP >= 7.4 (procedural + OOP), PDO, PHPMailer   |
| **Database** | MySQL / MariaDB (InnoDB, utf8mb4)               |
| **Frontend** | HTML5, CSS3, Bootstrap 5, JavaScript, Chart.js  |
| **Mobile**   | Apache Cordova / Capacitor 6 (Android)          |
| **Deps**     | Composer, npm                                   |

---

## Project Structure

```
BD-Fashion/
├── admin/              # Admin panel (51 files)
├── api/                # API endpoints (OTP, etc.)
├── assets/             # CSS, JS, images, uploads
│   ├── css/
│   ├── img/
│   ├── js/
│   └── uploads/
├── config/             # DB config, email, SMS, OTP
├── cron/               # Scheduled cleanup scripts
├── mobile-app/         # Android app (Capacitor)
├── rider/              # Rider delivery panel
├── smtp/               # Legacy SMTP mailer
├── sql/                # Database schema dump
├── templates/          # Shared header/footer
├── tmp/                # Session storage
├── uploads/            # User-uploaded files
├── vendor/             # Composer dependencies
├── node_modules/       # npm dependencies
├── .env.example        # Environment template
├── .htaccess           # Apache rewrite rules
├── composer.json       # PHP dependencies
├── manifest.json       # PWA manifest
├── service-worker.js   # PWA service worker
└── *.php               # 40+ frontend pages
```

---

## Database

**Engine:** MySQL / MariaDB with InnoDB and utf8mb4 collation.

**Database name (dev):** `bd_fashion`

The schema contains **25 tables**:

| Table                  | Purpose                                 |
| ---------------------- | --------------------------------------- |
| `admins`               | Admin users with role-based access      |
| `users`                | Registered customers                    |
| `products`             | Digital product catalog                 |
| `categories`           | Product categories                      |
| `product_variants`     | Product options (size, color, etc.)     |
| `product_screenshots`  | Product gallery images                  |
| `product_reviews`      | Customer ratings & reviews              |
| `orders`               | Customer orders                         |
| `order_items`          | Line items within orders                |
| `order_tracking`       | Order status history                    |
| `coupons`              | Discount coupons                        |
| `cart` / `cart_items`  | Shopping cart                           |
| `addresses`            | Customer shipping addresses             |
| `settings`             | Admin-configurable site settings        |
| `faqs`                 | Frequently Asked Questions              |
| `tickets`              | Support tickets                         |
| `ticket_replies`       | Support ticket responses                |
| `newsletters`          | Email newsletter subscribers            |
| `email_templates`      | Transactional email templates           |
| `email_verifications`  | Email OTP verification                  |
| `password_resets`      | Password reset tokens                   |
| `riders`               | Delivery riders                         |
| `rider_orders`         | Rider-to-order assignments              |
| `product_returns`      | Product return requests                 |
| `wallet_transactions`  | Customer wallet transactions            |

---

## File & Folder Count

Measured against the project root (`C:\xampp\htdocs\BD-Fashion`):

| Metric                      | Count  |
| --------------------------- | ------ |
| **Total files (all)**       | 2,705  |
| **Total folders (all)**     | 725    |
| **App files** (excl. vendor & node_modules) | 921    |
| **App folders** (excl. vendor & node_modules) | 369    |
| **Root-level files**        | 51     |
| **Root-level directories**  | 15     |
| **PHP source files**        | 243    |
| **JavaScript files**        | 643    |
| **CSS files**               | 2      |
| **Admin panel files**       | 51     |
| **Database tables**         | 25     |

---

## Features

### User-Facing
- User registration, login, OTP verification, password reset
- Product catalog with categories, search, and filtering
- Product detail with screenshots, variants, and reviews
- Shopping cart and checkout
- Multi-gateway payment (Stripe + manual/MFS)
- Order history, invoices, digital download access
- Support tickets with reply system
- Newsletter subscription
- FAQ page
- Contact form
- PWA support (service worker + manifest)

### Admin Panel
- Dashboard with KPI cards, charts, and tables
- Product CRUD with image upload and gallery
- Category management
- Coupon management
- Order management with status tracking
- User management with toggle enable/disable
- Support ticket management
- Review moderation
- Return request handling
- Rider management and order assignment
- Site settings (payment gateway, shipping, currency, SMTP)
- Email template editor
- Reports and export
- Stock count monitoring (auto-refresh)

### Rider Panel
- Rider login/logout
- View assigned orders
- Update delivery status (picked, out for delivery, delivered)
- Upload delivery photo proof

### Mobile App
- Android app built with Capacitor
- Wraps the web app for mobile distribution
- Build scripts for Capacitor Android

---

## Admin Panel & Role System

The admin panel is located in the `/admin/` directory and uses a **role-based access control (RBAC)** system defined in `admin/auth.php`.

### Login
- URL: `admin/login.php`
- Default credentials after DB import:
  - **Username:** `admin`
  - **Password:** `Admin@123`

### Three Admin Roles

| Role             | Level | Capabilities                                                    |
| ---------------- | ----- | --------------------------------------------------------------- |
| `super_admin`    | 3     | Full access — dashboard, products, orders, users, settings, FAQ, riders, reports, coupons, tickets, reviews, returns |
| `order_admin`    | 2     | Order management — view orders, update status, manage returns, access reports |
| `product_admin`  | 1     | Product management — add/edit/delete products, manage categories, reviews, stock |

### Admin Interface Pages

| Page                           | Description                              |
| ------------------------------ | ---------------------------------------- |
| `admin/index.php`              | Dashboard with KPIs, charts, recent data |
| `admin/products.php`           | Product list                             |
| `admin/product_form.php`       | Add / edit product                       |
| `admin/product_save.php`       | Save product handler                     |
| `admin/product_delete.php`     | Delete product                           |
| `admin/categories.php`         | Manage categories                        |
| `admin/orders.php`             | Order list                               |
| `admin/order_detail.php`       | Single order view                        |
| `admin/order_receipt.php`      | Print order receipt                      |
| `admin/users.php`              | Customer list                            |
| `admin/user_orders.php`        | Orders by a specific user                |
| `admin/user_toggle.php`        | Enable / disable user                    |
| `admin/coupons.php`            | Coupon list                              |
| `admin/coupon_form.php`        | Add / edit coupon                        |
| `admin/coupon_save.php`        | Save coupon handler                      |
| `admin/coupon_delete.php`      | Delete coupon                            |
| `admin/reviews.php`            | Product reviews                          |
| `admin/review_view.php`        | View single review                       |
| `admin/review_toggle.php`      | Approve / reject review                  |
| `admin/review_delete.php`      | Delete review                            |
| `admin/returns.php`            | Product return requests                  |
| `admin/return_detail.php`      | Single return view                       |
| `admin/tickets.php`            | Support tickets                          |
| `admin/ticket_view.php`        | View single ticket                       |
| `admin/ticket_reply.php`       | Reply to ticket                          |
| `admin/riders.php`             | Rider list                               |
| `admin/rider_form.php`         | Add / edit rider                         |
| `admin/rider_save.php`         | Save rider handler                       |
| `admin/rider_orders.php`       | Rider order assignments                  |
| `admin/faqs.php`               | FAQ management                           |
| `admin/newsletters.php`        | Newsletter subscribers                   |
| `admin/settings.php`           | Site-wide settings                       |
| `admin/email_templates.php`    | Transactional email templates            |
| `admin/reports.php`            | Sales / order reports                    |
| `admin/export_report.php`      | Export report as CSV                     |
| `admin/wallet.php`             | Wallet transactions                      |
| `admin/wallet_transfer.php`    | Manual wallet transfer                   |
| `admin/wallet_invoices.php`    | Wallet invoices                          |
| `admin/stock_count.php`        | Stock count JSON endpoint                |
| `admin/toggle_order_status.php`| Quick order status toggle                |
| `admin/login.php`              | Admin login                              |
| `admin/logout.php`             | Admin logout                             |

---

## Admin Roles Explained

### Super Admin (Level 3)
The super admin has unrestricted access to every feature in the admin panel. Responsibilities include:
- Full configuration of site settings (payment gateways, shipping rules, currency, SMTP)
- User and admin management
- Access to financial reports and data export
- Coupon creation and management
- FAQ and support ticket oversight
- Rider management and order assignment
- Review moderation and product return resolution
- System-wide maintenance mode control

### Order Admin (Level 2)
The order admin handles all order-related operations:
- Viewing and managing customer orders
- Updating order statuses (pending, processing, paid, delivered, cancelled)
- Processing product return requests
- Viewing sales reports and revenue data
- Managing support tickets related to orders
- Accessing wallet transaction records

### Product Admin (Level 1)
The product admin manages the product catalog:
- Adding, editing, and deleting products
- Managing categories
- Uploading product images and screenshots
- Moderating product reviews
- Monitoring stock levels (in stock / out of stock)
- Configuring product variants

---

## Mobile App

The `mobile-app/` directory contains a **Capacitor 6** Android project:

```
mobile-app/
├── package.json          # Capacitor dependencies
├── node_modules/         # npm dependencies
└── android/              # Generated Android project (after build)
```

**Commands:**
```bash
cd mobile-app
npm run sync     # Sync web assets to Android
npm run build    # Build Android APK
npm run open     # Open in Android Studio
```

---

## Quick Start

1. Copy the project folder into your web server root (e.g., `C:\xampp\htdocs\BD-Fashion`).
2. Create a MySQL database and import `sql/bd_fashion.sql`.
3. Copy `.env.example` to `.env` and update database credentials:
   ```
   DB_HOST=localhost
   DB_NAME=bd_fashion
   DB_USER=root
   DB_PASS=
   BASE_URL=/BD-Fashion
   ```
4. Set Stripe API keys via the admin panel at `admin/settings.php` (or configure directly in the database `settings` table).
5. Configure SMTP in the admin panel for transactional emails.
6. Access the site at `http://localhost/BD-Fashion/`.
7. Log in to the admin panel at `http://localhost/BD-Fashion/admin/login.php`.

---

## Security

- **CSRF Protection** — Separate tokens for frontend and admin (`csrfTokenFront` / `csrfToken`)
- **Password Hashing** — `password_hash()` with bcrypt
- **Session Security** — Sessions stored in a dedicated `tmp/sessions/` directory
- **Prepared Statements** — All database queries use PDO prepared statements to prevent SQL injection
- **Input Escaping** — `htmlspecialchars()` used on all output
- **Maintenance Mode** — Blocks all non-admin traffic when enabled
- **OTP Verification** — Email-based OTP for sensitive operations
- **Role-Based Access** — Admin pages check permissions before rendering

---

## Customization

- Replace `assets/img/` with your brand assets and product images.
- Update color scheme by editing `assets/css/style.css`.
- Modify email templates in the admin panel at `admin/email_templates.php`.
- Add or modify payment gateways in the settings panel.
- Extend the PWA manifest in `manifest.json` for custom app name and icons.

# 🛒 Madura Mart — Grocery Store Management System

![Laravel](https://img.shields.io/badge/Laravel-11-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)
![PHP](https://img.shields.io/badge/PHP-8.2-777BB4?style=for-the-badge&logo=php&logoColor=white)
![MySQL](https://img.shields.io/badge/Database-MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Bootstrap](https://img.shields.io/badge/UI-Bootstrap_5-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white)
![Midtrans](https://img.shields.io/badge/Payment-Midtrans-002855?style=for-the-badge)

> Web-based product and inventory management system built with **Laravel** and **MySQL** for **Madura Mart**, a grocery store. It covers product and stock management (stock in, stock out, and stock opname), online ordering with **Midtrans** payment, and owner sales reports with **Excel and PDF** export.

---

## 📌 Project Overview

Madura Mart needed one place to manage its products, keep stock accurate, sell online, and see how the store is performing. The system has three roles:

- **Customer** — searches products, orders online, and pays with Midtrans.
- **Admin** — manages products, categories, stock movements, and incoming orders.
- **Owner** — monitors sales, shipping costs, best-selling products, and user accounts.

---

## 🚀 Key Features

### 🛍️ Customer
- Register, log in, and manage the profile.
- Search products and view product details.
- Shopping cart and checkout with **Midtrans Snap** (a flat shipping fee is added to each order).
- Order history.

### 🧑‍💼 Admin
- Admin dashboard.
- Product management (CRUD) with purchase price and selling price.
- Category management (CRUD).
- **Stock in** and **stock out** records, each exportable to PDF.
- **Stock opname** (physical stock count) with adjustment history and PDF export.
- Transaction list and delivery confirmation.

### 📈 Owner
- Owner dashboard.
- Sales report with search and **Excel / PDF** export.
- Sales chart.
- Best-selling products.
- Shipping cost (ongkir) report with Excel / PDF export.
- User list.

---

## 🛠️ Technology Stack

| Component | Technology | Purpose |
| :--- | :--- | :--- |
| **Framework** | [Laravel 11](https://laravel.com/) (PHP 8.2) | Web application |
| **Database** | MySQL | Data storage |
| **Views** | Blade, [Bootstrap 5](https://getbootstrap.com/), Bootstrap Icons | User interface |
| **Payment Gateway** | [Midtrans](https://midtrans.com/) (`midtrans/midtrans-php`, Snap) | Online payment |
| **Excel Export** | [Laravel Excel](https://laravel-excel.com/) (`maatwebsite/excel`) | Sales and shipping reports |
| **PDF Export** | [DomPDF](https://github.com/barryvdh/laravel-dompdf), TCPDF | Reports and stock documents |
| **Authentication** | Laravel Fortify, role middleware (`admin`, `owner`) | Login and role-based access |

---

## 🌐 System Architecture

```text
Customer ──► Search & cart ──► Checkout ──► Midtrans payment ──► Transaction saved
                                                                     │
Admin ───► Products · Categories · Stock in/out · Stock opname ──────┤──► Delivery confirmation
                                                                     │
Owner ───► Sales report · Chart · Best sellers · Shipping report ◄────┘   (Excel / PDF export)
```

---

## 📁 Project Structure

```text
app/
├── Exports/               # LaporanExport, OngkirExport (Laravel Excel)
├── Http/Controllers/      # produk, kategori, Transaksi, Laporan, Midtrans, Search, user_control
└── Models/                # produk, kategori, Transaction, DetailTransaksi, StokMasuk,
                           # StokKeluar, StokOpname, StokHistori, HistoriOpname, User
resources/views/
├── auth/                  # Login
├── dashboard_admin/       # Admin: products, categories, transactions
├── dashboard_owner/       # Owner: reports, chart, best sellers, shipping report, users
├── order.blade.php        # Customer storefront
├── keranjang.blade.php    # Shopping cart
└── profile.blade.php      # Customer profile
routes/web.php             # Routes grouped by role
toko_aldi.sql              # Full MySQL database dump (schema + sample data)
```

---

## ⚙️ Installation & Setup

### Prerequisites
- PHP 8.2+ and Composer
- Node.js & npm
- MySQL / MariaDB (for example via Laragon or XAMPP)
- A [Midtrans](https://dashboard.midtrans.com/) account (sandbox is fine for testing)

### Steps
```bash
git clone https://github.com/Aldidwiirawan/sembako.git
cd sembako
composer install
npm install
cp .env.example .env
php artisan key:generate
```

Create a MySQL database named `toko_aldi` and import the full dump, which contains every table the app uses:
```bash
mysql -u root -p toko_aldi < toko_aldi.sql
```
> The Laravel migrations in this repository do not create all tables (for example the transaction and stock tables), so importing `toko_aldi.sql` is the required setup step.

Then link the storage folder for product images:
```bash
php artisan storage:link
```

---

## 🔐 Environment Variables

| Variable | Description |
| :--- | :--- |
| `DB_CONNECTION` | `mysql` |
| `DB_HOST`, `DB_PORT`, `DB_DATABASE`, `DB_USERNAME`, `DB_PASSWORD` | MySQL connection (`DB_DATABASE=toko_aldi`) |
| `MIDTRANS_SERVER_KEY` | Midtrans server key |
| `MIDTRANS_CLIENT_KEY` | Midtrans client key |
| `MIDTRANS_IS_PRODUCTION` | `false` for sandbox, `true` for production |

> ⚠️ Never commit the `.env` file or your Midtrans keys.

---

## ▶️ How to Run

```bash
php artisan serve
```
Open `http://127.0.0.1:8000`. The login page redirects each role to its own dashboard.

---

## 👨‍💻 Author

Built during the **Web Developer internship at Dinas Kominfo Kabupaten Kediri** (June–August 2025) by a team of three interns.

**Aldi Dwi Irawan** — built the customer, admin, and owner modules
- GitHub: [@Aldidwiirawan](https://github.com/Aldidwiirawan)
- Portfolio: [aldidwiirawan.vercel.app](https://aldidwiirawan.vercel.app)
- Email: aldidwiirawan2004@gmail.com

# FieldWork — Pest Control Management System

A full-stack web application built for a pest control company to manage clients, products, work orders and generate legally compliant service reports.

> ⚠️ This is a private commercial project. The repository is intentionally hollow — source code is not publicly available.

---

## Overview

FieldWork digitizes the entire workflow of a pest control operation — from registering clients and chemical products, to generating work orders in the field and producing print-ready compliance reports with digital signatures.

The app is currently in production use at a pest control company in Rosario, Argentina.

---

## Features

### Client Management
- Full CRUD for clients (individuals and businesses)
- Search by name or company
- Active/inactive status to track dropped clients
- Pagination for large datasets

### Product / Chemical Catalog
- Registry of pest control products with regulatory data (registration number, toxicity class, active ingredient, application method)
- Batch number and expiry date tracking
- Expiry warning system — banner notification and dashboard alert for products expiring within 30 days

### Work Orders
- Fast work order creation with intelligent auto-fill — selecting a client pre-populates all fields from the last work order for that client
- Searchable dropdowns for client and product selection (Tom Select)
- Month/year filter on work order index
- Full data snapshot on save — client and product details are frozen at the time of the order, ensuring historical accuracy even if records change later
- Per-order toggle for including technician and operator signatures on reports

### Print-Ready Compliance Reports
- Generated directly from the browser — no external PDF library required
- Includes company logo, regulatory registration numbers, legal disclaimer
- Digital signatures for the operator and the responsible technician
- 30-day validity date calculated automatically from the work order date
- Print-optimized CSS layout

### Dashboard
- Orders count for the current month
- Expiring products alert
- Last 5 work orders at a glance
- Renewal reminders — clients whose last service was 25+ days ago

### User Management & Roles
- Two roles: Admin and Technician
- Admins manage all records, users and settings
- Technicians create work orders and view client/product data
- Role-based access control throughout the app

### Settings
- Company information (name, CUIT, address, contact, regulatory numbers)
- Company logo upload
- Responsible technician profile (name, title, license number, signature image)
- All settings reflected dynamically in printed reports

### Bulk Management (Gestión)
- Bulk delete work orders filtered by client name, month or year
- Bulk delete clients filtered by name
- Select all on current page

### Security
- Secure authentication (Rails 8 built-in)
- Session-based login with cookie management
- Role-based authorization on all sensitive actions
- HTTPS enforced in production (Let's Encrypt SSL)
- Environment variables for all credentials
- Password authentication disabled on server — SSH key only

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language | Ruby 3.4 |
| Framework | Rails 8.1 |
| Database | PostgreSQL 14 |
| Frontend | Hotwire (Turbo + Stimulus) |
| CSS | Custom — no framework |
| JS dropdowns | Tom Select |
| Pagination | Pagy 9 |
| File uploads | Active Storage (local disk) |
| Web server | Puma + Nginx |
| SSL | Let's Encrypt (Certbot) |
| Deployment | Git bare repo + post-receive hook |
| Hosting | Ubuntu 22.04 VPS |

---

## Architecture Highlights

**Data integrity via snapshots** — Work orders store a frozen copy of client and product data at the time of creation. If a client's address or a product's batch number changes later, historical reports remain accurate.

**Auto-fill UX** — The work order form uses Stimulus and JSON endpoints to fetch the last work order for a selected client and pre-fill all fields, reducing data entry to a few clicks in the field.

**Print-first report design** — The compliance report is a dedicated Rails view with a separate print layout, `@media print` CSS, and browser-native print-to-PDF — no external gem required.

**Responsive design** — The app is fully usable on mobile phones and tablets. Technicians can create work orders in the field from their phones via a hamburger-menu navbar and single-column form layout.

**Role-based access** — Authentication uses Rails 8's built-in generator. Authorization is handled via controller-level guards and view-level conditionals — no external gem required.

---

## Deployment

The app is deployed on a VPS with:
- Nginx as reverse proxy
- Puma as application server (Unix socket)
- Systemd service for automatic startup and crash recovery
- Git bare repository with a `post-receive` hook for zero-downtime deploys
- Let's Encrypt SSL certificate with automatic renewal
- UFW firewall — only ports 22, 80 and 443 open

Deployments are triggered with a single command from the developer's machine:
```
git push production main
```

---

## Screenshots

> Coming soon

---

## Status

✅ In production — actively used by the client company.

---

## Author

Developed by **bachatron** as a freelance project.
Built from scratch over several weeks including requirements gathering, full-stack development, server setup and production deployment.

---

*This README is for portfolio purposes. The source code is private and not available for public access.*

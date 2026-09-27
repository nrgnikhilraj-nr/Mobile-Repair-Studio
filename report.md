# Project Report — RepairOS: Mobile Repair Studio Management System

## 1. Introduction

RepairOS is a web-based workshop management application developed for a mobile phone repair studio. The system enables the store to digitally manage its day-to-day operations including customer intake, repair tracking, parts inventory, and billing — replacing manual paper-based processes.

## 2. Problem Statement

Mobile repair workshops face challenges in:
- Tracking multiple simultaneous repair jobs
- Maintaining customer records and device history
- Managing spare parts inventory and reorder levels
- Generating and tracking invoices

This project addresses all four pain points in a single integrated application.

## 3. Technologies Used

| Technology | Role |
|---|---|
| HTML5 | Application structure and markup |
| CSS3 + Custom Properties | Responsive styling and theming |
| Vanilla JavaScript (ES6+) | Application logic, in-memory database, DOM rendering |
| Google Fonts (Inter, JetBrains Mono) | Typography |

## 4. System Modules

### 4.1 Dashboard
Real-time summary of operations: active repair count, today's completions, monthly revenue, total customers. Displays recent tickets, issue-type breakdown (progress bars), and low-stock alerts.

### 4.2 Repair Ticket Management
- Create tickets with customer info, device details, issue type, technician assignment, priority, IMEI, and device password
- Update status through the workflow: Pending → Diagnosing → In Progress → Ready → Completed
- Filter tickets by status
- Global search across ticket ID, customer name, phone, model

### 4.3 Customer Management
Customer records are auto-derived from ticket data. Each unique phone number maps to one customer profile. Profile shows total repairs, total amount spent, and last visit date.

### 4.4 Inventory Management
Parts catalogue with SKU system. Each part shows compatible models, supplier, cost/sell price, profit margin, and current stock. A stock-level bar and "Low Stock" badge appear when quantity reaches the reorder threshold.

### 4.5 Billing & Invoicing
Invoice generator takes a completed ticket and calculates: Labour + Parts − Discount = Total. Invoices are logged with INV-XXXX numbering and marked Paid on creation.

## 5. Database Design

The application uses an in-memory JavaScript object (`db`) structured as four relational tables: `tickets`, `customers`, `inventory`, and `invoices`. See `docs/schema.md` for full field definitions and relationships.

In a production environment, this would be implemented as:
- **Backend:** Node.js / Express or Python Flask
- **Database:** MySQL or PostgreSQL
- **ORM:** Sequelize / SQLAlchemy

## 6. Key Features

- Auto-incrementing IDs (TKT-XXXX, CUS-XXX, SKU-XXX, INV-XXXX)
- Live KPI recalculation on every state change
- Sidebar badge updates for pending ticket count
- Toast notification system for user feedback
- Responsive layout (works on tablets and desktops)
- Dark theme with accessible color contrast

## 7. Conclusion

RepairOS demonstrates a complete CRUD application with relational data management, real-time UI updates, and a professional interface — all implemented without any external libraries or frameworks, using only standard web technologies.

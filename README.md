# RepairOS — Mobile Repair Studio Management System

A full-featured workshop management application built as a college project.

## 📋 Project Overview

**Course:** Web Development & Database Management  
**Project:** Mobile Repair Studio — Workshop Management Application  
**Tech Stack:** HTML5, CSS3, Vanilla JavaScript (ES6+)

## 🚀 Features

- **Dashboard** — Live KPIs, recent tickets, issue breakdown, low stock alerts
- **Repair Tickets** — Full CRUD, status workflow, priority, technician assignment
- **Customer Management** — Auto-aggregated profiles, repair history, spend tracking
- **Parts Inventory** — SKU system, stock level bars, margin calculator, reorder alerts
- **Billing & Invoicing** — Invoice generator with labour, parts, and discount fields

## 🗂️ Project Structure

```
RepairOS-Project/
├── index.html        ← Main application (single-file SPA)
├── README.md         ← This file
└── docs/
    ├── schema.md     ← Database schema documentation
    └── report.md     ← Project report
```

## 🏃 How to Run

1. Open `index.html` in any modern browser — no server needed.
2. All data is stored in-memory (JavaScript).
3. Use the sidebar to navigate between modules.

## 🔧 Key Technical Decisions

| Decision | Reason |
|---|---|
| Single-file SPA | No build tools needed; easy to submit/demo |
| In-memory JS DB | Simulates SQL tables without backend setup |
| CSS Custom Properties | Consistent theming across all components |
| ES6 Modules | Clean separation of data, logic, and rendering |

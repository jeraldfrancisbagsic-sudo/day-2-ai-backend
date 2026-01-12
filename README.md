# Day 2: AI-Assisted Backend Development

**Time:** 60 minutes  
**Objective:** Build a FastAPI inventory system using AI-assisted development

## Overview

Follow each step by copying the prompt to your AI assistant. Each step builds on the previous one.

---

## Step 0 — Project Setup

**Prompt for AI:**
```
Create a FastAPI project for an inventory system.
- Use app/ as the root folder with subfolders: routers, services, schemas, db, tests.
- Add __init__.py to app/ and all subfolders.
- Add conftest.py at project root to add the directory to sys.path.
- Include main.py with a basic FastAPI app.
- Show folder structure and setup instructions (venv, install, run server, open docs).
```

**Expected Output:**
```
conftest.py
app/
├── __init__.py
├── main.py
├── routers/
│   └── __init__.py
├── services/
│   └── __init__.py
├── schemas/
│   └── __init__.py
├── db/
│   └── __init__.py
└── tests/
    └── __init__.py
```

---

## Step 1 — Environment Variables

**Prompt for AI:**
```
Create a .env file at project root with:
- SUPABASE_DB_URL (PostgreSQL connection pooler URL, port 6543)
- SUPABASE_API_KEY

Include instructions to get the URL from Supabase Dashboard.
```

**Expected Output:**
```
.env
```
```env
SUPABASE_DB_URL=postgresql://postgres.[PROJECT-REF]:[YOUR-PASSWORD]@aws-0-[REGION].pooler.supabase.com:6543/postgres
SUPABASE_API_KEY=your-anon-key-here
```

---

## Step 2 — Pydantic Schemas

**Prompt for AI:**
```
Create Pydantic schemas for:
- categories: id (UUID), name (unique), description (optional)
- products: id (UUID), name, sku (unique), description, price, current_stock, category_id, created_at
- stock_movements: id (UUID), product_id, quantity, type (restock/sale/return/adjustment), created_at

Include Base, Create, Update, and Response schemas with validation.
```

**Expected Output:**
```
app/schemas/
├── category.py
├── product.py
└── stock_movement.py
```

---

## Step 3 — Database Connection

**Prompt for AI:**
```
Set up SQLAlchemy database connection.
- Load SUPABASE_DB_URL from .env.
- Create session factory and Base class.
- Create models for categories, products, stock_movements matching existing tables.
- Use extend_existing=True. Do NOT create tables.
- Fallback to SQLite if connection fails.
```

**Expected Output:**
```
app/db/
└── database.py
```

---

## Step 4 — Service Layer

**Prompt for AI:**
```
Create services for:
- CategoryService: CRUD, get products in category
- ProductService: CRUD, search by name/SKU
- StockMovementService: create movements, auto-update product stock, get history

Handle errors with HTTP exceptions. Use transactions for stock updates.
```

**Expected Output:**
```
app/services/
├── category_service.py
├── product_service.py
└── stock_movement_service.py
```

---

## Step 5 — API Routers

**Prompt for AI:**
```
Create routers for:
- /api/categories: GET, POST, PUT, DELETE
- /api/products: GET (with category filter), POST, PUT, DELETE
- /api/stock-movements: GET (with product filter), POST

Use schemas and connect to services.
```

**Expected Output:**
```
app/routers/
├── category_router.py
├── product_router.py
└── stock_movement_router.py
```

---

## Step 6 — Update main.py

**Prompt for AI:**
```
Update main.py to:
- Set title "Inventory Management API", version "1.0.0"
- Include all routers with /api prefix
- Add root and health check endpoints
- Do NOT call create_all()
```

**Expected Output:**
```
app/main.py (updated)
```

---

## Step 7 — Test Cases

**Prompt for AI:**
```
Create pytest tests for all endpoints.
- Test CRUD for categories, products, stock-movements.
- Test stock updates on movements.
- Test invalid and not-found cases.
- Use .env or fallback to SQLite.
```

**Expected Output:**
```
app/tests/
└── test_inventory.py
```

---

## Step 8 — Requirements + README

**Prompt for AI:**
```
Create requirements.txt with: fastapi[standard], uvicorn[standard], sqlalchemy, pydantic, psycopg2-binary, python-dotenv, pytest, httpx.

Create README.md with setup instructions, .env setup, run commands, and API summary.
```

**Expected Output:**
```
requirements.txt
README.md
```

---

## Step 9 — Run the Project

```powershell
py -m venv venv
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
.\venv\Scripts\activate
pip install -r requirements.txt
fastapi dev app/main.py
```

Open: **http://127.0.0.1:8000/docs**

Run tests:
```powershell
pytest -v
```

---

## Final Project Structure

```
day-2-ai-backend/
├── .env
├── conftest.py
├── requirements.txt
├── README.md
└── app/
    ├── __init__.py
    ├── main.py
    ├── routers/
    │   ├── __init__.py
    │   ├── category_router.py
    │   ├── product_router.py
    │   └── stock_movement_router.py
    ├── services/
    │   ├── __init__.py
    │   ├── category_service.py
    │   ├── product_service.py
    │   └── stock_movement_service.py
    ├── schemas/
    │   ├── __init__.py
    │   ├── category.py
    │   ├── product.py
    │   └── stock_movement.py
    ├── db/
    │   ├── __init__.py
    │   └── database.py
    └── tests/
        ├── __init__.py
        └── test_inventory.py
```

---

## Deliverable

A working FastAPI inventory API with:
- Categories, Products, Stock Movements
- Supabase PostgreSQL connection
- Automatic stock updates
- Pytest tests
- Swagger docs at http://127.0.0.1:8000/docs

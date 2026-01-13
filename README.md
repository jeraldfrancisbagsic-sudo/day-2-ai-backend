# Day 2: AI-Assisted Backend Development

**Time:** 60 minutes  
**Objective:** Build a FastAPI inventory system using AI-assisted development

## Overview

Follow each step by copying the prompt to your AI assistant. Each step builds on the previous one.

---

## Step 0 — Project Setup

**Prompt for AI:**
```
Generate a basic FastAPI project for an inventory system with categories, products, and stock movements.
- Use an app/ folder as the root directory for all project code.
- Include folders for routers, services, schemas, db, and tests.
- Include a main.py file.
- Add an __init__.py file inside app/ and each subfolder (routers, services, schemas, db, tests) to make them Python packages.
- Add a conftest.py file at the project root that adds the project directory to sys.path for pytest compatibility.
- Show the resulting folder structure.
- Include simple instructions for setting up a virtual environment, installing dependencies, running the server, and opening API docs.
```

**Expected Folder Structure:**
```
app/
├── main.py
├── routers/
├── services/
├── schemas/
├── db/
└── tests/
```

---

## Step 0.5 — Environment Variables

**Prompt for AI:**
```
Create a file named `.env` at the root of the project with the following content:

# Use Supabase Connection Pooler (port 6543) for reliable connections
SUPABASE_DB_URL=postgresql://postgres.[PROJECT-REF]:[YOUR-PASSWORD]@aws-0-[REGION].pooler.supabase.com:6543/postgres
SUPABASE_API_KEY=your-anon-key-here

Instructions:
1. Go to Supabase Dashboard → Settings → Database
2. Find "Connection Pooling" section
3. Copy the "URI" connection string (uses port 6543)
4. Replace [YOUR-PASSWORD] with your database password
5. Save the file and make sure python-dotenv is installed
```

---

## Step 1 — Models/Schemas

**Prompt for AI:**
```
Create Pydantic schemas to match this existing Supabase database schema:

Tables:
1. categories: id (UUID), name (text, unique), description (text, optional)
2. products: id (UUID), name (text), sku (text, unique), description (text, optional), price (decimal), current_stock (int), category_id (UUID foreign key), created_at (timestamp)
3. stock_movements: id (UUID), product_id (UUID foreign key), quantity (int), type (enum: restock, sale, return, adjustment), created_at (timestamp)

Requirements:
- Create Base, Create, Update, and Response schemas for each table
- Use UUID for all id fields
- Use Optional for nullable fields
- Include proper validation (e.g., price > 0, stock >= 0)
- Keep schemas simple and easy to understand
```

---

## Step 2 — Database & Supabase Connection

**Prompt for AI:**
```
Set up database connection to Supabase using SQLAlchemy with Connection Pooling.

Requirements:
- Load database URL from .env (SUPABASE_DB_URL)
- Use Supabase Connection Pooler URL format (port 6543)
- Create a session factory and Base class for models
- Create SQLAlchemy models matching this existing schema:

  categories: id (UUID PK), name (unique), description
  products: id (UUID PK), name, sku (unique), description, price, current_stock, category_id (FK), created_at
  stock_movements: id (UUID PK), product_id (FK), quantity, type (enum), created_at

- Do NOT create tables (they already exist in Supabase)
- Use reflect=True or set extend_existing=True to work with existing tables
- Add fallback to SQLite if Supabase connection fails
```

---

## Step 3 — Service Layer

**Prompt for AI:**
```
Create service layers to handle business logic for:

1. CategoryService:
   - CRUD operations for categories
   - Get all products in a category

2. ProductService:
   - CRUD operations for products
   - Update stock when stock movements occur
   - Search products by name or SKU

3. StockMovementService:
   - Create stock movements (restock, sale, return, adjustment)
   - Automatically update product's current_stock based on movement type
   - Get movement history for a product

Requirements:
- Connect to database session
- Return Pydantic schemas for responses
- Handle not found errors with proper HTTP exceptions
- Use transactions for stock updates
```

---

## Step 4 — Routers

**Prompt for AI:**
```
Create API endpoints for the inventory system:

1. /api/categories
   - GET / - List all categories
   - GET /{id} - Get category by ID
   - POST / - Create category
   - PUT /{id} - Update category
   - DELETE /{id} - Delete category

2. /api/products
   - GET / - List all products (with optional category filter)
   - GET /{id} - Get product by ID
   - POST / - Create product
   - PUT /{id} - Update product
   - DELETE /{id} - Delete product

3. /api/stock-movements
   - GET / - List movements (with optional product filter)
   - GET /{id} - Get movement by ID
   - POST / - Create movement (auto-updates product stock)

Requirements:
- Use request/response schemas
- Connect to service layer and database session
- Include query parameters for filtering
- Keep routes simple and RESTful
```

---

## Step 5 — Include Routers in main.py

**Prompt for AI:**
```
Update main.py to include FastAPI app and all routers.
- Set API metadata (title: "Inventory Management API", description, version: "1.0.0")
- Include routers with prefix /api
- Add root endpoint with welcome message
- Add health check endpoint
- Do NOT call create_all() since tables exist in Supabase
```

---

## Step 6 — Pytest Test Cases

**Prompt for AI:**
```
Generate test cases for inventory CRUD operations using FastAPI TestClient.

Requirements:
1. Test all endpoints: categories, products, stock-movements
2. Test create, read, update, delete operations
3. Test stock movement creates and updates product stock correctly
4. Test valid, invalid, and not-found cases
5. Load database URL from .env using python-dotenv
6. If .env is missing or connection fails, use SQLite in-memory database
7. Make tests runnable with: pytest -v
8. Keep tests simple and clear for students
```

---

## Step 7 — Requirements + README

**Prompt for AI:**
```
Generate requirements.txt and a project README.md.

requirements.txt should include:
- fastapi[standard]
- uvicorn[standard]
- sqlalchemy
- pydantic
- psycopg2-binary
- python-dotenv
- pytest
- httpx

README.md should include:
- Project description (Inventory Management API with Categories, Products, Stock Movements)
- Setup instructions (venv, install dependencies)
- How to get Supabase Connection Pooler URL
- .env file setup with pooler URL format
- Running the server
- Swagger docs URL (http://127.0.0.1:8000/docs)
- Running tests
- API endpoints summary
```

---

## Step 8 — Run the Project

After completing all steps, run the following commands in PowerShell:

### 1. Create and activate virtual environment
```powershell
# Create virtual environment
py -m venv venv

# Allow script execution (required for Windows)
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process

# Activate virtual environment
.\venv\Scripts\activate
```

### 2. Install dependencies
```powershell
pip install -r requirements.txt
```

### 3. Run the FastAPI server
```powershell
fastapi dev app/main.py
```

### 4. Open API Documentation
Open your browser and go to: **http://127.0.0.1:8000/docs**

### 5. Run tests
```powershell
pytest -v
```

---

## Deliverable

A working FastAPI inventory API with:
- Categories, Products, and Stock Movements
- Supabase PostgreSQL with Connection Pooling
- Pydantic schemas matching existing database
- Automatic stock updates on movements
- Pytest test cases
- Complete documentation

**Swagger Docs:** `http://127.0.0.1:8000/docs`

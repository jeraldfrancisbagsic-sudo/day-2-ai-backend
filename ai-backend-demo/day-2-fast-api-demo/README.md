# Day 2: AI-Assisted Backend Development

**Time:** 60 minutes  
**Objective:** Build a FastAPI inventory system using AI-assisted development

## Overview

Follow each step by copying the prompt to your AI assistant. Each step builds on the previous one.

---

## Step 0 — Project Setup

**Prompt for AI:**
```
Generate a basic FastAPI project for a simple inventory system.
- Use an app/ folder as the root directory for all project code.
- Include folders for routers, services, schemas, database, and tests.
- Include a main.py file.
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

SUPABASE_DB_URL=postgresql://postgres:letsgosupabase@db.mmgyxxmrpynjpqnkjdpx.supabase.co:5432/postgres
SUPABASE_API_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im1tZ3l4eG1ycHluanBxbmtqZHB4Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3NjgwOTgwODIsImV4cCI6MjA4MzY3NDA4Mn0.YEFa3q2BkhKK1UnqwjQaq2-0KusuFMTDs2ntzZg3eYg

Save the file and make sure python-dotenv is installed to load these variables in Python.
```

---

## Step 1 — Models/Schemas

**Prompt for AI:**
```
Create models and schemas for inventory items.
- Include fields for id, name, quantity, and price.
- Use schemas for request/response validation.
- Include create, update, and read models.
- Keep it simple and easy to understand.
```

---

## Step 2 — Database & Supabase Connection

**Prompt for AI:**
```
Set up database connection to Supabase using SQLAlchemy.
- Load database URL from .env.
- Create a session and a base class for models.
- Create an Item model with fields matching the schemas.
- Include instructions to create tables and test database session.
```

---

## Step 3 — Service Layer

**Prompt for AI:**
```
Create a service layer to handle business logic for inventory items.
- Include CRUD operations: create, read, update, delete.
- Connect to the database session.
- Return the schemas for responses.
- Handle item not found errors.
```

---

## Step 4 — Routers

**Prompt for AI:**
```
Create API endpoints for inventory items using FastAPI.
- Include endpoints for all CRUD operations.
- Use request/response schemas.
- Connect to the service layer and database session.
- Keep the routes simple and easy to understand.
```

---

## Step 5 — Include Router in main.py

**Prompt for AI:**
```
Update main.py to include FastAPI app and the inventory router.
- Set API metadata (title, description, version).
- Include the router with a prefix like /api.
```

---

## Step 6 — Pytest Test Cases

**Prompt for AI:**
```
Generate test cases for inventory CRUD operations using FastAPI TestClient.

Requirements:
1. Test create, read, update, delete operations.
2. Test valid, invalid, and not-found cases.
3. Load database URL from .env using python-dotenv.
4. If .env is missing or connection fails, use SQLite in-memory database for tests.
5. Make tests runnable with Python: python -m pytest -q
6. Keep tests simple, clear, and easy to understand for students.
```

---

## Step 7 — Requirements + README

**Prompt for AI:**
```
Generate requirements.txt and README.md.
- requirements.txt should include FastAPI, Uvicorn, SQLAlchemy, Pydantic, psycopg2-binary, python-dotenv, pytest.
- README.md should include setup instructions, .env creation, running server, Swagger docs URL, running tests.
```

---

## Deliverable

A working FastAPI inventory API with:
- CRUD endpoints
- Supabase database connection
- Pydantic schemas
- Pytest test cases
- Complete documentation

**Swagger Docs:** `http://127.0.0.1:8000/docs`

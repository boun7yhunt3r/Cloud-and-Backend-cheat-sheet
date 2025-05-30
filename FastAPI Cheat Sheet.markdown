# FastAPI Cheat Sheet

A concise, visually organized guide to essential FastAPI concepts, setup, and code snippets for building modern, high-performance APIs in Python.

---

## **1. Setup & Installation**

### **Install FastAPI**
- **Purpose**: Install FastAPI and Uvicorn (ASGI server)
- **Command**:
  ```bash
  pip install fastapi uvicorn
  ```
- **Notes**:
  - FastAPI: Framework for building APIs
  - Uvicorn: Runs the app asynchronously

### **Basic Project Structure**
- **Purpose**: Organize your FastAPI project
- **Example**:
  ```
  myapp/
  ├── main.py           # Core app file
  ├── models/           # Pydantic models
  ├── routers/          # Route modules
  ├── schemas/          # Data schemas
  └── requirements.txt  # Dependencies
  ```

---

## **2. Creating a FastAPI App**

### **Basic App Setup**
- **Purpose**: Initialize a FastAPI application
- **Code**:
  ```python
  from fastapi import FastAPI

  app = FastAPI()

  @app.get("/")
  async def root():
      return {"message": "Hello, FastAPI!"}
  ```
- **Run**:
  ```bash
  uvicorn main:app --reload
  ```
- **Notes**:
  - `main:app`: `main` is the file, `app` is the FastAPI instance
  - `--reload`: Auto-reload for development

### **Key App Parameters**
- **Purpose**: Configure FastAPI app instance
- **Options**:
  - `title` — App name for docs (e.g., `"My API"`)
  - `description` — API description
  - `version` — API version (e.g., `"1.0.0"`)
- **Example**:
  ```python
  app = FastAPI(
      title="My FastAPI App",
      description="A sample API",
      version="1.0.0"
  )
  ```

---

## **3. Defining Routes**

### **Path Operations**
- **Purpose**: Define API endpoints
- **Methods**: `GET`, `POST`, `PUT`, `DELETE`, etc.
- **Code**:
  ```python
  from fastapi import FastAPI

  app = FastAPI()

  @app.get("/items/{item_id}")
  async def read_item(item_id: int):
      return {"item_id": item_id}

  @app.post("/items/")
  async def create_item(item: dict):
      return {"item": item}
  ```
- **Notes**:
  - Path params: `{item_id}` in URL
  - Type hints (e.g., `int`) enable auto-validation

### **Query Parameters**
- **Purpose**: Handle URL query params (e.g., `/items/?skip=0&limit=10`)
- **Code**:
  ```python
  @app.get("/items/")
  async def read_items(skip: int = 0, limit: int = 10):
      return {"skip": skip, "limit": limit}
  ```
- **Notes**:
  - Default values: `skip=0`, `limit=10`
  - Auto-documented in API docs

---

## **4. Request Body & Pydantic Models**

### **Pydantic Models**
- **Purpose**: Define and validate request/response data
- **Code**:
  ```python
  from pydantic import BaseModel
  from fastapi import FastAPI

  app = FastAPI()

  class Item(BaseModel):
      name: str
      price: float
      is_offer: bool = False

  @app.post("/items/")
  async def create_item(item: Item):
      return item
  ```
- **Notes**:
  - `BaseModel`: Validates data types
  - Optional fields: `is_offer = False`

### **Response Model**
- **Purpose**: Define and validate response structure
- **Code**:
  ```python
  @app.get("/items/{item_id}", response_model=Item)
  async def read_item(item_id: int):
      return {"name": "Sample", "price": 9.99, "is_offer": True}
  ```
- **Notes**:
  - Ensures response matches `Item` schema

---

## **5. Handling Responses**

### **Status Codes**
- **Purpose**: Customize HTTP status codes
- **Code**:
  ```python
  from fastapi import FastAPI, status

  app = FastAPI()

  @app.post("/items/", status_code=status.HTTP_201_CREATED)
  async def create_item(name: str):
      return {"name": name}
  ```
- **Notes**:
  - Common codes: `201` (Created), `200` (OK), `404` (Not Found)

### **Custom Exceptions**
- **Purpose**: Raise and handle errors
- **Code**:
  ```python
  from fastapi import FastAPI, HTTPException

  app = FastAPI()

  @app.get("/items/{item_id}")
  async def read_item(item_id: int):
      if item_id < 0:
          raise HTTPException(status_code=404, detail="Item not found")
      return {"item_id": item_id}
  ```
- **Notes**:
  - `HTTPException`: Custom status and message

---

## **6. Dependencies**

### **Dependency Injection**
- **Purpose**: Reuse logic (e.g., auth, DB connection)
- **Code**:
  ```python
  from fastapi import FastAPI, Depends

  app = FastAPI()

  async def get_query_param(q: str | None = None):
      return q if q else "default"

  @app.get("/items/")
  async def read_items(query: str = Depends(get_query_param)):
      return {"query": query}
  ```
- **Notes**:
  - `Depends`: Injects result of `get_query_param`

---

## **7. API Documentation**

### **Auto-Generated Docs**
- **Purpose**: Interactive API docs
- **Access**:
  - Swagger UI: `/docs`
  - ReDoc: `/redoc`
- **Notes**:
  - Auto-generated from code
  - Customizable via `app` params (title, etc.)

### **Customizing Docs**
- **Purpose**: Add descriptions to routes
- **Code**:
  ```python
  @app.get("/items/", summary="Get Items", description="Retrieve a list of items")
  async def read_items():
      return ["item1", "item2"]
  ```
- **Notes**:
  - `summary`: Short title
  - `description`: Detailed explanation

---

## **8. Running & Testing**

### **Run the App**
- **Purpose**: Start FastAPI with Uvicorn
- **Command**:
  ```bash
  uvicorn main:app --host 0.0.0.0 --port 8000 --reload
  ```
- **Options**:
  - `--host` — Bind to host (e.g., `0.0.0.0`)
  - `--port` — Port to run on
  - `--reload` — Auto-reload for dev

### **Test Endpoints**
- **Purpose**: Test API endpoints
- **Tools**:
  - **cURL**:
    ```bash
    curl -X GET "http://localhost:8000/items/?skip=0&limit=10"
    ```
  - **Python Requests**:
    ```python
    import requests
    response = requests.get("http://localhost:8000/items/")
    print(response.json())
    ```

---

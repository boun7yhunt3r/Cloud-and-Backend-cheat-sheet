## **1. Relational Databases**

### **PostgreSQL**
- **Purpose**: Manage structured data for backend apps
- **Key Commands**:
  - **Create DB**: `createdb mydb`
  - **Connect**: `psql -d mydb`
  - **Create Table**:
    ```sql
    CREATE TABLE users (
        id SERIAL PRIMARY KEY,
        username VARCHAR(100) NOT NULL,
        email VARCHAR(255) UNIQUE,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    );
    ```
  - **Insert**: `INSERT INTO users (username, email) VALUES ('user1', 'user1@example.com');`
  - **Query**: `SELECT * FROM users WHERE created_at > '2025-01-01';`
- **Notes**:
  - Scalable, robust for MATVIS data needs
  - Learn: Indexing, transactions, connection pooling

### **MySQL**
- **Purpose**: Handle relational data with high performance
- **Key Commands**:
  - **Create DB**: `CREATE DATABASE mydb;`
  - **Use DB**: `USE mydb;`
  - **Create Table**:
    ```sql
    CREATE TABLE orders (
        id INT AUTO_INCREMENT PRIMARY KEY,
        product VARCHAR(100),
        quantity INT,
        order_date DATETIME
    );
    ```
  - **Insert**: `INSERT INTO orders (product, quantity) VALUES ('Widget', 5);`
  - **Query**: `SELECT * FROM orders ORDER BY order_date DESC;`
- **Notes**:
  - Common in backend systems
  - Learn: Joins, optimization, replication

---

## **2. API Security**

### **Authentication (OAuth2)**
- **Purpose**: Secure API access with tokens
- **Key Approach**:
  - Use OAuth2 for user authentication
- **Code**:
  ```python
  from fastapi import FastAPI, Depends
  from fastapi.security import OAuth2PasswordBearer
  app = FastAPI()
  oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")
  @app.get("/secure-endpoint")
  async def secure_route(token: str = Depends(oauth2_scheme)):
      return {"token": token}
  ```
- **Notes**:
  - Protects MATVIS APIs for AI security
  - Learn: JWT validation, refresh tokens

### **Input Validation & Rate Limiting**
- **Purpose**: Prevent attacks and abuse
- **Key Practices**:
  - **Validation**: Use Pydantic for data checks
    ```python
    from pydantic import BaseModel
    from fastapi import FastAPI
    app = FastAPI()
    class User(BaseModel):
        username: str
        email: str
    @app.post("/users/")
    async def create_user(user: User):
        return user
    ```
  - **Rate Limiting**: Limit requests
    ```python
    from fastapi import FastAPI
    from slowapi import Limiter, _rate_limit_exceeded_handler
    from slowapi.util import get_remote_address
    app = FastAPI()
    limiter = Limiter(key_func=get_remote_address)
    app.state.limiter = limiter
    app.add_exception_handler(429, _rate_limit_exceeded_handler)
    @app.get("/limited")
    @limiter.limit("5/minute")
    async def limited_route():
        return {"message": "Rate-limited endpoint"}
    ```
- **Notes**:
  - Guards against SQL injection, DDoS
  - Install: `pip install slowapi`

---

## **3. Performance Optimization**

### **Database Performance**
- **Purpose**: Boost query and data efficiency
- **Key Techniques**:
  - **Indexing**: Speed up queries
    ```sql
    CREATE INDEX idx_user_email ON users(email);
    ```
  - **Query Optimization**: Analyze performance
    ```sql
    EXPLAIN SELECT * FROM users WHERE email = 'user1@example.com';
    ```
- **Notes**:
  - Critical for MATVIS backend scalability
  - Learn: Partitioning, caching

### **API Performance**
- **Purpose**: Enhance endpoint speed, throughput
- **Key Tools**:
  - **Caching (Redis)**: Store frequent results
    ```bash
    redis-cli SET cache:key "response"
    redis-cli GET cache:key
    ```
  - **Async Endpoints**: Handle concurrency
    ```python
    from fastapi import FastAPI
    app = FastAPI()
    @app.get("/async-data")
    async def async_route():
        await asyncio.sleep(1)  # Simulate async work
        return {"message": "Fast async response"}
    ```
- **Notes**:
  - Improves MATVIS API responsiveness
  - Install: `pip install redis`, use async/await

---

## **4. Cloud Services**

### **AWS (Amazon Web Services)**
- **Purpose**: Deploy scalable backend solutions
- **Key Services**:
  - **S3**: Store data, backups
    ```bash
    aws s3 cp data.sql s3://my-bucket/
    ```
  - **EC2**: Host API servers
    ```bash
    aws ec2 start-instances --instance-ids i-1234567890abcdef0
    ```
  - **Elastic Beanstalk**: Simplify app deployment
- **Notes**:
  - Key for MATVIS cloud integration
  - Learn: Security groups, RDS

### **Google Cloud Platform (GCP)**
- **Purpose**: Leverage cloud for reliability
- **Key Services**:
  - **Cloud Storage**: Store backups
    ```bash
    gsutil cp data.sql gs://my-bucket/
    ```
  - **Compute Engine**: Run servers
  - **Cloud SQL**: Managed databases
- **Notes**:
  - Supports MATVIS scalability
  - Learn: Load balancing, monitoring

---

## **5. DevOps & CI/CD**

### **Jenkins**
- **Purpose**: Automate CI/CD pipelines
- **Key Steps**:
  - **Install**: Run via Docker
    ```bash
    docker run -p 8080:8080 jenkins/jenkins:lts
    ```
  - **Pipeline** (in `Jenkinsfile`):
    ```groovy
    pipeline {
        agent any
        stages {
            stage('Build') {
                steps {
                    sh 'python -m build'
                }
            }
            stage('Test') {
                steps {
                    sh 'pytest'
                }
            }
        }
    }
    ```
- **Notes**:
  - Streamlines MATVIS deployment
  - Learn: Plugins, pipeline setup

### **GitHub Actions**
- **Purpose**: CI/CD within GitHub
- **Key Workflow** (e.g., `.github/workflows/ci.yml`):
  ```yaml
  name: CI
  on: [push]
  jobs:
    build:
      runs-on: ubuntu-latest
      steps:
        - uses: actions/checkout@v3
        - name: Set up Python
          uses: actions/setup-python@v4
          with:
            python-version: '3.9'
        - name: Install deps
          run: pip install -r requirements.txt
        - name: Run tests
          run: pytest
  ```
- **Notes**:
  - Automates MATVIS testing, deployment
  - Learn: Secrets, multi-stage builds

---

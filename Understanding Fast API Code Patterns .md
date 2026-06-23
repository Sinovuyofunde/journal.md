
---

# FastAPI Exercise Submission

## Understanding FastAPI Code Patterns

---

# Part 1: Analysis of Code Patterns

## 1. Repository Pattern

The Repository pattern is used to separate **database logic** from **business logic**.

### In this code:

* `Repository[T]` is a generic base class for database operations
* `UserRepository` extends it for user-specific queries

### Why it is used:

* Keeps SQL queries in one place
* Makes code reusable across different models
* Improves maintainability
* Makes testing easier (repositories can be mocked)

### Summary:

> The service layer does not talk to the database directly. It uses repositories as an abstraction layer.

---

## 2. Generic[T] in Repository

The `Generic[T]` allows the repository to work with **any database model**.

### Meaning:

* `T` can be `User`, `Product`, etc.
* The same repository structure works for all models

### Benefit:

* Avoids rewriting CRUD logic for every model
* Improves scalability
* Enforces type safety

### Summary:

> One repository design works for all database tables.

---

## 3. Dependency Injection (DI)

FastAPI automatically injects dependencies using `Depends()`.

### Layers in this system:

#### 1. Database Layer

```python
get_db()
```

#### 2. Authentication Layer

```python
get_current_user()
```

Depends on:

* JWT token
* database session

#### 3. Service Layer

```python
UserService
```

Depends on:

* Repository

#### 4. Endpoint Layer

```python
/admin/users/
```

Depends on:

* DB session
* current user

### Why DI is used:

* Removes manual object creation
* Improves modularity
* Makes testing easier

---

## 4. Role-Based Access Control (RBAC)

RBAC is implemented using a decorator:

```python
@requires_role("admin")
```

### How it works:

1. User is authenticated via JWT
2. `current_user` is passed to wrapper
3. Role is checked:

   * If not admin → 403 Forbidden
   * If admin → request continues

### Summary:

> Authentication checks identity, RBAC checks permissions.

---

# Part 2: Execution Flow for `/admin/users/`

## Step-by-step request lifecycle:

### 1. Request enters FastAPI

```
GET /admin/users/
```

---

### 2. Middleware runs

* `TimingMiddleware` starts timer
* Request is passed forward

---

### 3. Dependency Injection begins

#### a) Database session created

```python
Depends(get_db)
```

#### b) User authentication

```python
Depends(get_current_user)
```

JWT process:

* Token extracted
* Token decoded
* Username retrieved
* User fetched from DB

---

### 4. Authorization check (RBAC)

```python
@requires_role("admin")
```

* If user is not superuser → 403 error
* If superuser → continue

---

### 5. Business logic runs

```python
UserRepository.list()
```

* Queries database
* Returns user list

---

### 6. Response formatting

* Data is converted to `UserSchema`
* Returned as JSON

---

### 7. Middleware finishes

* Execution time calculated
* Added to response header

---

### Final Flow Summary:

```
Request
 ↓
Middleware (timing)
 ↓
JWT authentication
 ↓
User lookup
 ↓
RBAC check
 ↓
Repository query
 ↓
Response formatting
 ↓
Response returned
```

---

# Part 3: Simplifying Complex Concepts

## 1. lifespan (asynccontextmanager)

### What it does:

Runs code at:

* Application startup
* Application shutdown

### Simple explanation:

> It is a setup and cleanup system for the FastAPI app.

### Example:

* Connect database on startup
* Close resources on shutdown

---

## 2. TimingMiddleware

### What it does:

Measures how long each request takes.

### Simple flow:

1. Start timer
2. Run request
3. Stop timer
4. Attach result to response

### Output example:

```
X-Process-Time: 12.4ms
```

---

## 3. JWT Authentication Flow

### Simple explanation:

#### Login:

* User logs in
* Server creates token with username inside

#### Future requests:

* Client sends token
* Server decodes token
* Gets username
* Finds user in database

### Key idea:

> JWT is a “signed ID card” the user sends with every request.

---

# Part 4: Logging System Implementation

## Goal:

Log:

* logins
* admin actions

---

## 1. Create Logging Model

```python
class UserActionLog(Base):
    __tablename__ = "user_logs"

    id: int
    user_id: int
    action: str
    timestamp: datetime
```

---

## 2. Repository Layer

```python
class UserLogRepository(Repository[UserActionLog]):
    async def create_log(self, db: AsyncSession, user_id: int, action: str):
        log = UserActionLog(
            user_id=user_id,
            action=action,
            timestamp=datetime.utcnow()
        )
        db.add(log)
        await db.commit()
        return log
```

---

## 3. Service Layer

```python
class LoggingService:
    def __init__(self, repo: UserLogRepository):
        self.repo = repo

    async def log_action(self, db, user_id, action):
        return await self.repo.create_log(db, user_id, action)
```

---

## 4. Integrate into Login Endpoint

```python
await logging_service.log_action(db, user.id, "LOGIN")
```

---

## 5. Integrate into Admin Endpoint

```python
await logging_service.log_action(db, current_user.id, "VIEW_ADMIN_USERS")
```

---

# Reflection

## 1. What this exercise teaches about architecture:

* Code is split into layers
* Each layer has a single responsibility
* FastAPI handles dependency wiring automatically

---

## 2. Most important design patterns:

* Repository Pattern → database abstraction
* Dependency Injection → automatic wiring
* Middleware → cross-cutting logic
* RBAC → security control
* JWT → stateless authentication

---

## 3. How to explain DI simply:

> “FastAPI builds everything I need for a request automatically and passes it into my function.”

---

## 4. How tracing helped:

It shows exactly:

* where authentication happens
* where authorization happens
* where database queries happen

---

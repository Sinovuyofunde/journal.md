
# Security settings
SECRET_KEY = "secret-key"
ALGORITHM = "HS256"
ACCESS_TOKEN_EXPIRE_MINUTES = 30

# Fake user database
fake_users = {
    "student": {
        "username": "student",
        "hashed_password": "example_hash"
    }
}

pwd_context = CryptContext(schemes=["bcrypt"])
oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

# Token model
class Token(BaseModel):
    access_token: str
    token_type: str

# Create token
def create_token(data: dict):
    expire = datetime.utcnow() + timedelta(minutes=ACCESS_TOKEN_EXPIRE_MINUTES)
    data.update({"exp": expire})
    return jwt.encode(data, SECRET_KEY, algorithm=ALGORITHM)

# Login endpoint
@app.post("/token", response_model=Token)
def login(form_data: OAuth2PasswordRequestForm = Depends()):
    token = create_token({"sub": form_data.username})
    return {"access_token": token, "token_type": "bearer"}

# Protected route
@app.get("/profile")
def profile(token: str = Depends(oauth2_scheme)):
    try:
        data = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])
        return {"user": data.get("sub")}
    except JWTError:
        raise HTTPException(status_code=401, detail="Invalid token")
Step 3: Run API
uvicorn main:app --reload
Step 4: Test
Open: http://127.0.0.1:8000/docs

POST /token (username: student)

Copy token

Use token in:

Authorization: Bearer <token>
GET /profile

Mental Model Translation
Old Concept	FastAPI Equivalent
Views	Functions (@app.get)
Middleware	Dependencies
Forms	Pydantic models
Authentication	Dependency system
Routing	Decorators
Key Mental Shift
Instead of “controllers and views”

FastAPI uses functions + type hints + dependencies

Final Summary
What I learned
FastAPI uses type hints and dependencies

Authentication uses dependency injection

FastAPI is more structured than Flask/Django

JWT is easier with FastAPI tools

APIs are clean and modular

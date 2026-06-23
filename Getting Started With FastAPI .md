"A simple API to manage to-do tasks"

# 
# Data Models
 
class TodoCreate(BaseModel):
    title: str
    description: Optional[str] = None


class Todo(BaseModel):
    id: int
    title: str
    description: Optional[str] = None
    completed: bool = False


#
# In-memory database

todos: List[Todo] = []
todo_id = 1


#
# Create To-Do

@app.post("/todos")
def create_todo(todo: TodoCreate):
    global todo_id

    new_todo = Todo(
        id=todo_id,
        title=todo.title,
        description=todo.description,
        completed=False
    )

    todos.append(new_todo)
    todo_id += 1

    return new_todo


# 
# Get To-Dos (with filterin

@app.get("/todos")
def get_todos(status: Optional[str] = None):
    if status == "completed":
        return [t for t in todos if t.completed]

    if status == "pending":
        return [t for t in todos if not t.completed]

    return todos


#
# Mark To-Do as Completed

@app.put("/todos/{todo_id}")
def complete_todo(todo_id: int):
    for todo in todos:
        if todo.id == todo_id:
            todo.completed = True
            return todo

    raise HTTPException(status_code=404, detail="Todo not found")


# 
# Delete To-Do

@app.delete("/todos/{todo_id}")
def delete_todo(todo_id: int):
    for todo in todos:
        if todo.id == todo_id:
            todos.remove(todo)
            return {"message": "Todo deleted"}

    raise HTTPException(status_code=404, detail="Todo not found")


# 
# Root Endpoint

@app.get("/")
def root():
    return {
        "message": "To-Do API is running",
        "docs": "/docs"
    }

# Django Models Question

## Question 3

Django Models are the mapping from python objects to a relational database. For the TODO app, which models did you use? Where did you implement them? Explain and show.

After adding models, what was the next step in the app development?

**Choices:**
- Run the application
- Add the models to the admin panel
- Run migrations
- Create a makefile

## Answer

### Which models did I use?

For the TODO app, I created a single model called **`Todo`**.

### Where did I implement it?

The model is implemented in [todos/models.py](file:///C:/Users/roson/.gemini/antigravity/scratch/django_todo_app/todos/models.py):

```python
from django.db import models

class Todo(models.Model):
    title = models.CharField(max_length=200)
    description = models.TextField(blank=True, null=True)
    due_date = models.DateField(blank=True, null=True)
    resolved = models.BooleanField(default=False)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.title

    class Meta:
        ordering = ['-created_at']
```

### Model Fields Explanation:

- **`title`**: CharField - The todo title (required, max 200 characters)
- **`description`**: TextField - Optional detailed description
- **`due_date`**: DateField - Optional due date for the todo
- **`resolved`**: BooleanField - Completion status (defaults to False)
- **`created_at`**: DateTimeField - Auto-generated timestamp when todo is created

The `__str__` method returns the title for string representation, and the `Meta` class orders todos by creation date (newest first).

### What was the next step after adding models?

**The answer is: Run migrations**

Here's why and what I did:

#### Step 1: Create migrations (`makemigrations`)
```bash
.venv\Scripts\python manage.py makemigrations
```

This command analyzes your models and creates migration files that describe the database schema changes. For the `Todo` model, it created `todos/migrations/0001_initial.py`.

#### Step 2: Apply migrations (`migrate`)
```bash
.venv\Scripts\python manage.py migrate
```

This command takes the migration files and actually applies them to the database, creating the necessary tables.

### Why migrations?

Django models are Python classes, but databases understand SQL tables. **Migrations are the bridge** that translates your Python model definitions into SQL `CREATE TABLE` statements and keeps your database schema in sync with your code.

### Why not the other options?

- **Run the application**: Won't work - the database tables don't exist yet
- **Add models to admin panel**: Optional feature, not required for the app to function
- **Create a makefile**: Not part of the Django workflow

### Migration Example

When I ran migrations, Django created this database table structure:

```
todos_todo table:
- id (auto-generated primary key)
- title (VARCHAR 200)
- description (TEXT)
- due_date (DATE)
- resolved (BOOLEAN)
- created_at (DATETIME)
```

This allows Django to store and retrieve `Todo` objects from the database using Python code, without writing any SQL.

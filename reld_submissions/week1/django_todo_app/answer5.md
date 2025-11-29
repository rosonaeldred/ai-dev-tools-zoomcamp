# Django Templates Question

## Question 5

Templates. After the logic comes the templates. You'll need at least two, the base one and the home one.

- Why those two?
- What does base do? What does home do?
- What did you name base? (base.html?)
- What did you name home? (home.html?)

Where do you need to register the directory with the templates?

**Choices:**
- INSTALLED_APPS in project's settings.py
- TEMPLATES['DIRS'] in project's settings.py
- TEMPLATES['APP_DIRS'] in project's settings.py
- In the app's urls.py

What does registration of a template do?

## Answer

### Why those two templates?

Actually, I created **more than two** templates, but let me explain the core concept:

1. **Base template** - Provides the common HTML structure (header, styles, layout) that all pages share
2. **"Home" template** - The main page users see (in my case, the todo list)

You need at least these two because of Django's **template inheritance** system - it prevents code duplication. Instead of repeating the same HTML structure on every page, you write it once in the base template and extend it.

### What does base do? What does home do?

#### Base Template

File: [todos/templates/todos/base.html](file:///C:/Users/roson/.gemini/antigravity/scratch/django_todo_app/todos/templates/todos/base.html)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}Todo App{% endblock %}</title>
    <style>
        /* Shared CSS for all pages */
    </style>
</head>
<body>
    <div class="container">
        {% block content %}{% endblock %}  <!-- Child templates fill this -->
    </div>
</body>
</html>
```

**What it does:**
- Defines the HTML structure (doctype, head, body)
- Includes common CSS/styling
- Defines `{% block %}` sections where child templates can insert content
- Ensures consistent look and feel across all pages

#### "Home" Template

File: [todos/templates/todos/todo_list.html](file:///C:/Users/roson/.gemini/antigravity/scratch/django_todo_app/todos/templates/todos/todo_list.html)

```html
{% extends 'todos/base.html' %}  <!-- Inherits from base -->

{% block title %}Todo List{% endblock %}  <!-- Fills the title block -->

{% block content %}
    <!-- The actual todo list content goes here -->
    <h1>My Todo List</h1>
    {% for todo in todos %}
        <!-- Display each todo -->
    {% endfor %}
{% endblock %}
```

**What it does:**
- Extends (inherits from) base.html
- Fills in the `{% block %}` sections with specific content
- Displays the dynamic todo list data
- Gets all the styling from base.html automatically

### What did I name them?

- **Base:** `base.html` ✅
- **Home:** `todo_list.html` (NOT `home.html`)

I followed Django naming conventions - naming templates after what they display/do rather than generic names like "home". Since this page lists todos, it's called `todo_list.html`.

### Where do you register the template directory?

**The answer is: `TEMPLATES['APP_DIRS']` in project's settings.py**

Here's the relevant section from [config/settings.py](file:///C:/Users/roson/.gemini/antigravity/scratch/django_todo_app/config/settings.py#L54-L67):

```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],  # Project-level template directories (I didn't use this)
        'APP_DIRS': True,  # ← THIS IS THE KEY SETTING
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

#### Why `APP_DIRS: True`?

When `APP_DIRS` is set to `True`, Django automatically looks for templates in each installed app's `templates/` directory.

My template structure:
```
todos/
    templates/
        todos/
            base.html
            todo_list.html
            todo_form.html
            todo_confirm_delete.html
```

The nested `todos/` directory inside `templates/` is a Django convention to namespace templates and avoid conflicts between apps.

### Why not the other options?

- **`INSTALLED_APPS`**: This registers the app itself, not templates specifically
- **`TEMPLATES['DIRS']`**: This is for project-level template directories (when you want templates outside of any particular app)
- **`urls.py`**: This is for URL routing, not template discovery

### What does registration of a template do?

"Registration" (via `APP_DIRS: True`) tells Django **where to look for templates**.

#### The Template Discovery Process

When a view renders a template like this:
```python
class TodoListView(ListView):
    template_name = 'todos/todo_list.html'  # References a template
```

Django needs to know where to find that file. The discovery process:

1. Django checks that `APP_DIRS` is `True` in settings
2. Looks in each installed app's `templates/` directory
3. Finds `todos/templates/todos/todo_list.html`
4. Loads and renders it

**Without proper registration** (if `APP_DIRS` were `False`), Django would raise a `TemplateDoesNotExist` error even if the file exists.

### Benefits of Template Inheritance

Using base.html + child templates provides:

1. **No code duplication** - Write HTML structure once
2. **Consistent styling** - All pages look the same
3. **Easy maintenance** - Change the base template, all pages update
4. **Modular design** - Each page only defines its unique content

### My Complete Template Structure

I actually created **4 templates** total:

1. **base.html** - Base layout with common styling
2. **todo_list.html** - Main page showing all todos (the "home" page)
3. **todo_form.html** - Form for creating/editing todos
4. **todo_confirm_delete.html** - Confirmation page for deleting todos

All of them extend `base.html` to maintain consistent styling and structure.

### Example: How Inheritance Works

When Django renders `todo_list.html`:

```
base.html provides:
├── HTML structure
├── CSS styling
├── Container div
└── {% block content %}
    
todo_list.html fills in:
└── {% block content %}
    ├── <h1>My Todo List</h1>
    ├── Todo cards
    └── Action buttons
    
Final rendered HTML:
├── Complete HTML structure from base
├── All styling from base
└── Todo list content from todo_list
```

This is the power of template inheritance!

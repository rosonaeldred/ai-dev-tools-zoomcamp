# Django App Registration Question

## Question
At some point, you included the app you created in the project.

What's the file you needed to edit for that?

- settings.py
- manage.py
- urls.py
- wsgi.py

Explain why, and show me where you did that.

## Answer

The answer is **settings.py**.

### Why settings.py?

When you create a new Django app, it exists as a separate module, but Django doesn't automatically know about it. You need to **register the app** in the project's `INSTALLED_APPS` list so that Django can:

- Discover and run the app's migrations
- Find and use the app's templates
- Load the app's models into the database
- Include the app in admin, if configured
- Make the app's functionality available to the project

### Where I did this:

In [settings.py](file:///C:/Users/roson/.gemini/antigravity/scratch/django_todo_app/config/settings.py#L33-L41):

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'todos',  # ← This is where I added our todos app
]
```

Without adding `'todos'` to this list, Django would not recognize the `Todo` model, wouldn't run the migrations for the `todos` app, and wouldn't be able to find the templates in `todos/templates/`.

### Why not the other files?

- **manage.py**: This is a command-line utility that's auto-generated and rarely needs manual editing
- **urls.py**: This is for URL routing (I did edit this, but to *connect* the app's URLs, not to *register* the app itself)
- **wsgi.py**: This is for deployment configuration and doesn't deal with app registration

So the registration happens in `settings.py`, and then separately I connected the URLs in `urls.py` to make the app's views accessible via web paths.

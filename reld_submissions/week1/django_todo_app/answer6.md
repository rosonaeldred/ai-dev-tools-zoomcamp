# Django Testing Command Question

## Question 6

What's the command you use for running tests in the terminal?

**Choices:**
- pytest
- python manage.py test
- python -m django run_tests
- django-admin test

## Answer

The command to run tests in the terminal is:

**`python manage.py test`**

### Explanation:
- **`python manage.py test`**: This is the standard command to run tests in a Django project. It looks for tests in all installed apps, runs them, and reports the results.
- **`pytest`**: This is a popular third-party testing framework. While very common in Django projects (usually with `pytest-django`), it's not the built-in default command.
- **`django-admin test`**: This can work if you have your environment variables (like `DJANGO_SETTINGS_MODULE`) set up perfectly, but `manage.py` is the wrapper that handles that setup for you, making it the preferred command.
- **`python -m django run_tests`**: This is not a standard command.

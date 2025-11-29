# Django Todo App Project

This repository contains a Django-based Todo application built as part of the AI Dev Tools Zoomcamp.

## 📚 Documentation Index

### 🚀 Project Overview
- **[Walkthrough](walkthrough.md)**: Detailed guide on how the app was built, including screenshots and verification results.
- **[Homework Instructions](https://github.com/DataTalksClub/ai-dev-tools-zoomcamp/blob/main/cohorts/2025/01-overview/homework.md)**: The original requirements for this assignment.

### ❓ Q&A Sessions
I've documented the answers to the homework questions in separate markdown files:

- **[Question 2: App Registration](answer2.md)**
  - *Topic*: Why we edit `settings.py` to register apps.
  
- **[Question 3: Models & Migrations](answer3.md)**
  - *Topic*: Implementing the `Todo` model and the migration process.
  
- **[Question 4: App Logic](answer4.md)**
  - *Topic*: Understanding where business logic lives in Django (`views.py`).
  
- **[Question 5: Templates](answer5.md)**
  - *Topic*: Template inheritance, naming conventions, and registration.
  
- **[Question 6: Testing](answer6.md)**
  - *Topic*: Running tests with `python manage.py test`.

### 🧪 Test Logic
- **[Test Scenarios](question6_testlogic.md)**: The plan for the implemented test suite.

## 🛠️ Quick Start

### Option 1: Using `uv` (Recommended)

1. **Install dependencies:**
   ```bash
   uv venv
   uv pip install -r requirements.txt
   ```

2. **Run migrations:**
   ```bash
   # Windows
   .venv\Scripts\python manage.py migrate
   
   # Mac/Linux
   source .venv/bin/activate
   python manage.py migrate
   ```

3. **Run the server:**
   ```bash
   # Windows
   .venv\Scripts\python manage.py runserver
   
   # Mac/Linux
   python manage.py runserver
   ```

### Option 2: Standard Python

1. **Create virtual environment:**
   ```bash
   python -m venv .venv
   ```

2. **Activate and install:**
   ```bash
   # Windows
   .venv\Scripts\activate
   pip install -r requirements.txt
   
   # Mac/Linux
   source .venv/bin/activate
   pip install -r requirements.txt
   ```

3. **Run migrations and server:**
   ```bash
   python manage.py migrate
   python manage.py runserver
   ```


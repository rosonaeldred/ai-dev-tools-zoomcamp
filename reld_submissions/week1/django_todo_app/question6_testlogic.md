# Django Tests Question

## Question 6

Tests. Let's cover our functionality with tests. Have you implemented any?

Which scenarios should we cover? Ask me if they make sense before you implement, after that, implement and run them.

## Answer

### Have I implemented any tests?

**No, I have not implemented any tests yet.** The Django app currently has no test coverage.

### Test Scenarios I Propose

Here are the test scenarios I recommend covering for the TODO app:

#### 1. **Model Tests** (test the Todo model)
- ✅ Test creating a Todo with all fields
- ✅ Test creating a Todo with only required fields (title)
- ✅ Test the `__str__` method returns the title
- ✅ Test default values (resolved=False, created_at auto-generated)
- ✅ Test ordering (newest first)

#### 2. **View Tests** (test CRUD operations)
- ✅ Test TodoListView displays all todos
- ✅ Test TodoCreateView creates a new todo
- ✅ Test TodoUpdateView updates an existing todo
- ✅ Test TodoUpdateView can mark todo as resolved
- ✅ Test TodoDeleteView deletes a todo
- ✅ Test redirects after create/update/delete

#### 3. **Form Tests** (test validation)
- ✅ Test form with valid data
- ✅ Test form without title (should fail - title required)
- ✅ Test form with optional fields (description, due_date)
- ✅ Test date field accepts valid dates

#### 4. **URL Tests** (test routing)
- ✅ Test URL resolution for each view
- ✅ Test reverse URL lookup

### Status

These scenarios have been approved and will be implemented in `todos/tests.py`.

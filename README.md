# AST Rule Engine

A powerful and flexible Abstract Syntax Tree (AST)-based rule engine that enables users to create, combine, evaluate, and manage complex business rules through both API and GUI interfaces.

---

## Key Features

- **Dynamic rule creation and management**
- **Rule combination with logical operators** (AND, OR)
- **Real-time rule evaluation**
- **Support for multiple data types**
- **User-friendly GUI interface** via Tkinter
- **RESTful API endpoints**
- **Persistent storage with SQLite**

---

## Installation

### Prerequisites

- **Python 3.8+**
- **pip** package manager
- **SQLite** (bundled with Python, or install manually if needed)

### Setup

1. **Clone the repository:**

   ```bash
   git clone https://github.com/yourusername/ast-rule-engine.git
   cd ast-rule-engine
   ```

2. **Create a virtual environment (recommended):**

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies:**

   ```bash
   pip install flask sqlalchemy
   ```

4. **Install Tkinter for GUI** (if not already installed):

   - **Windows**: Tkinter is usually bundled with Python, but if not, run the installer for Python, select "Modify," and make sure "tcl/tk and IDLE" is checked.
   - **macOS**: Tkinter is bundled with Python.
   - **Linux**: Install with:

     ```bash
     sudo apt-get install python3-tk
     ```

5. **Verify Dependencies**

   Ensure everything is installed by running:

   ```bash
   pip freeze
   ```

   You should see `Flask`, `SQLAlchemy`, and other dependencies listed.

---

## Usage

### Starting the Server

To start the backend server with the Flask application:

```bash
python main.py
```

The server will run at `http://localhost:5000`.

### Running the GUI

To interact with the GUI, run:

```bash
python tinker.py
```

This opens a Tkinter window providing a graphical interface for rule creation, combination, evaluation, and modification.

---

## Testing API Endpoints Using Thunder Client or Postman

You can use **Thunder Client** (a VS Code extension) or **Postman** to test the rule engine’s API.

### Setting Up Thunder Client (in VS Code)

1. **Install Thunder Client Extension** from the Extensions tab.
2. Open **Thunder Client** from the sidebar, and create new requests for each endpoint as described below.

### Using Postman

1. **Install Postman** from [Postman's website](https://www.postman.com/downloads/).
2. Create a new **Request** in Postman for each endpoint.

### API Endpoints

These endpoints allow interaction with the rule engine programmatically.

#### **Create Rule**

- **URL**: `POST http://localhost:5000/create_rule`
- **Headers**: `Content-Type: application/json`
- **Body (JSON)**:

   ```json
   {
       "rule_string": "(age > 30 AND department = 'Sales') OR (salary > 50000)"
   }
   ```

- **Response Example**:

   ```json
   {
       "id": 1,
       "ast": "..."
   }
   ```

#### **Combine Rules**

- **URL**: `POST http://localhost:5000/combine_rules`
- **Headers**: `Content-Type: application/json`
- **Body (JSON)**:

   ```json
   {
       "rule_ids": [1, 2]
   }
   ```

- **Response Example**:

   ```json
   {
       "id": 3,
       "combined_ast": "..."
   }
   ```

#### **Evaluate Rule**

- **URL**: `POST http://localhost:5000/evaluate_rule`
- **Headers**: `Content-Type: application/json`
- **Body (JSON)**:

   ```json
   {
       "rule_id": 3,
       "data": {
           "age": 35,
           "department": "Sales",
           "salary": 60000,
           "experience": 6
       }
   }
   ```

- **Response Example**:

   ```json
   {
       "result": true
   }
   ```

#### **Modify Rule**

- **URL**: `POST http://localhost:5000/modify_rule`
- **Headers**: `Content-Type: application/json`
- **Body (JSON)**:

   ```json
   {
       "rule_id": 1,
       "new_rule_string": "age > 40 AND department = 'HR'"
   }
   ```

- **Response Example**:

   ```json
   {
       "message": "Rule updated successfully"
   }
   ```

---

## GUI Interface

Running `tinker.py` will open the GUI, providing access to:

- **Rule Creation Panel**: Enter new rules with syntax validation.
- **Rule Combination Interface**: Combine existing rules using logical operators.
- **Rule Evaluation Window**: Input data to evaluate rules and see real-time results.
- **Rule Management Dashboard**: View and manage all created rules with modification options.

---

## Database Schema

The application uses SQLite to store rules with the following schema:

```sql
CREATE TABLE rules (
    id INTEGER PRIMARY KEY,
    field TEXT NOT NULL,
    operator TEXT NOT NULL,
    value TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## Testing

A test suite (`test.py`) automates testing of rule creation, combination, evaluation, and modification.

Run the test suite:

```bash
python test.py
```

---

## Supported Operators

### Comparison Operators

- Greater than (`>`)
- Less than (`<`)
- Greater than or equal (`>=`)
- Less than or equal (`<=`)
- Equal (`==`)
- Not equal (`!=`)

### Logical Operators

- **AND**
- **OR**

### String Operators

- **contains**
- **startswith**
- **endswith**

---

## Error Handling

The application provides comprehensive error handling for:

- Invalid rule syntax
- Non-existent rules
- Invalid data types
- Database errors
- Network issues

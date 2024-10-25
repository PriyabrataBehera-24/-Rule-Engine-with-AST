# AST Rule Engine

A powerful and flexible Abstract Syntax Tree (AST) based rule engine that allows users to create, combine, evaluate, and manage complex business rules through both API and GUI interfaces.

## Features

- ✨ **Dynamic rule creation and management**
- 🔄 **Rule combination** with logical operators (AND, OR)
- 📊 **Real-time rule evaluation**
- 🎯 **Support for multiple data types**
- 🖥️ **User-friendly GUI interface**
- 🔌 **RESTful API endpoints**
- 💾 **Persistent storage with SQLite**

## Installation

### Prerequisites

- **Python 3.8+**
- **pip** package manager

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
   pip install -r requirements.txt
   ```

## Usage

### Starting the Server

Run the main application server:

```bash
python main.py
```

The server will start at `http://localhost:5000`.

### Running the GUI

Launch the GUI interface:

```bash
python tinker.py
```

## API Endpoints

- **Create Rule**

   ```http
   POST /rules
   Content-Type: application/json
   ```

   **Sample Request Body:**

   ```json
   {
       "field": "age",
       "operator": ">",
       "value": 18
   }
   ```

- **Combine Rules**

   ```http
   POST /combine
   Content-Type: application/json
   ```

   **Sample Request Body:**

   ```json
   {
       "rule1_id": 1,
       "rule2_id": 2,
       "operator": "AND"
   }
   ```

- **Evaluate Rule**

   ```http
   POST /evaluate
   Content-Type: application/json
   ```

   **Sample Request Body:**

   ```json
   {
       "rule_id": 1,
       "data": {
           "age": 25,
           "name": "John"
       }
   }
   ```

- **Modify Rule**

   ```http
   PUT /rules/<rule_id>
   Content-Type: application/json
   ```

   **Sample Request Body:**

   ```json
   {
       "field": "age",
       "operator": ">=",
       "value": 21
   }
   ```

## GUI Interface

The GUI provides intuitive access to all functionalities, including:

- **Rule Creation Panel**
- **Rule Combination Interface**
- **Rule Evaluation Window**
- **Rule Management Dashboard**

## Database Schema

The following schema is used to store rules in SQLite:

```sql
CREATE TABLE rules (
    id INTEGER PRIMARY KEY,
    field TEXT NOT NULL,
    operator TEXT NOT NULL,
    value TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Testing

Run the test suite:

```bash
python test.py
```

## Supported Operators

- **Comparison:** `>`, `<`, `>=`, `<=`, `==`, `!=`
- **Logical:** `AND`, `OR`
- **String:** `contains`, `startswith`, `endswith`

## Error Handling

Comprehensive error handling is provided for:

- Invalid rule syntax
- Non-existent rules
- Invalid data types
- Database errors
- Network issues

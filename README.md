# AST Rule Engine

A Python-based rule engine application utilizing Flask and Tkinter for dynamic rule management and evaluation.

## Table of Contents
- [Features](#features)
- [Setup](#setup)
- [Components](#components)
- [App Components](#app-components)
- [API Endpoints](#api-endpoints)
- [Sample Curl Workflow](#sample-curl-workflow)
- [Testing](#testing)
- [Non-Functional Requirements](#non-functional-requirements)

## Features
- **Dynamic Rule Management:** Create, combine, and evaluate rules through an intuitive Tkinter UI.
- **Automated Testing:** A dedicated script to verify the functionality of the rule engine.
- **RESTful APIs:** Access rule functionalities via well-defined API endpoints.

## Setup

### Install the Required Dependencies:
Run the following command to install the necessary libraries:
```bash
pip install flask sqlalchemy
```

### Start the Flask Application:
Execute the command below to launch the application:
```bash
python main.py
```

## Components
- **Backend:** `main.py` (Flask, SQLAlchemy)
- **Frontend:** `rlg.py` (Tkinter)
- **Testing:** `test.py` (Requests for automated testing)

## App Components
- **Create Rule:** Define a new rule and display its ID within the UI.
- **Combine Rules:** Merge multiple rule IDs into a single "mega rule" with its own unique ID.
- **Evaluate Rule:** Test the combined rule using specified JSON data.

## API Endpoints

### Create Rule
- **Endpoint:** `/create_rule`
- **Method:** POST
- **Data Example:**
```json
{ "rule_string": "(age > 30 AND department = 'Sales') OR (salary > 50000)" }
```
- **Expected Response:**
```json
{ "id": 1, "ast": "..." }
```

### Combine Rules
- **Endpoint:** `/combine_rules`
- **Method:** POST
- **Data Example:**
```json
{ "rule_ids": [1, 2] }
```
- **Expected Response:**
```json
{ "id": 3, "combined_ast": "..." }
```

### Evaluate Rule
- **Endpoint:** `/evaluate_rule`
- **Method:** POST
- **Data Example:**
```json
{ "rule_id": 3, "data": { "age": 35, "department": "Sales", "salary": 60000, "experience": 6 } }
```
- **Expected Response:**
```json
{ "result": true }
```

### Modify Rule
- **Endpoint:** `/modify_rule`
- **Method:** POST
- **Data Example:**
```json
{ "rule_id": 1, "new_rule_string": "age > 40 AND department = 'HR'" }
```
- **Expected Response:**
```json
{ "message": "Rule updated successfully" }
```

## Sample Curl Workflow
Here’s a practical example demonstrating the API usage via curl commands:

1. **Creating the First Rule:**
```bash
curl -X POST http://127.0.0.1:5000/create_rule -H "Content-Type: application/json" -d '{"rule_string": "(age > 30 AND department = 'Sales') OR (salary > 50000)"}'
```

2. **Creating the Second Rule:**
```bash
curl -X POST http://127.0.0.1:5000/create_rule -H "Content-Type: application/json" -d '{"rule_string": "(experience > 5 AND department = 'Marketing')"}'
```

3. **Combining Rules (use actual IDs from the previous steps):**
```bash
curl -X POST http://127.0.0.1:5000/combine_rules -H "Content-Type: application/json" -d '{"rule_ids": [1, 2]}'
```

4. **Evaluating the Combined Rule (replace with the combined rule ID):**
```bash
curl -X POST http://127.0.0.1:5000/evaluate_rule -H "Content-Type: application/json" -d '{"rule_id": 3, "data": {"age": 35, "department": "Sales", "salary": 60000, "experience": 6}}'
```

5. **Modifying an Existing Rule (replace with the rule ID you wish to change):**
```bash
curl -X POST http://127.0.0.1:5000/modify_rule -H "Content-Type: application/json" -d '{"rule_id": 1, "new_rule_string": "age > 40 AND department = 'HR'"}'
```

## Testing
To validate the functionality of the rule engine, run the `test.py` script:
```bash
python test.py
```
This script performs automated tests for rule creation, combination, evaluation, and modification.

## Non-Functional Requirements
- **Security:** Implemented authentication measures to safeguard API endpoints.
- **Performance Optimization:** Enhanced query performance for faster response times.
- **Error Handling:** Comprehensive logging and error handling mechanisms in place.
```

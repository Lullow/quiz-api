# Quiz API

A REST API for running live quiz sessions, built with FastAPI and PostgreSQL — inspired by Kahoot.

This was my **second database lab**, built during the course *Databaser* in December 2025. The focus was on connecting a relational database to a web API: designing the schema, writing raw SQL queries in a data access layer, and exposing it all through FastAPI endpoints with Pydantic validation.

## What it does

- Create and manage users, quizzes, and questions
- Add multiple-choice answer options to questions
- Host live quiz sessions with a join code
- Players join sessions by nickname (anonymous or registered)
- Submit answers during a session — scoring is calculated automatically
- Track session status (waiting, in_progress, finished)

## How to run

```
pip install -r requirements.txt
```

Create a `.env` file with your database credentials:
```
DATABASE=your_db_name
PASSWORD=your_password
```

Set up the database schema:
```
psql -U postgres -d your_db_name -f schemas.sql
```

Start the API:
```
uvicorn app:app --reload
```

Interactive docs available at `http://localhost:8000/docs`

## Structure

- `app.py` — FastAPI endpoints
- `db.py` — data access layer (raw SQL queries)
- `db_setup.py` — database connection setup
- `schemas.py` — Pydantic models for request/response validation
- `schemas.sql` — SQL to create all tables

## API endpoints

| Method | Path | Description |
|---|---|---|
| GET | `/users` | List all users |
| POST | `/users` | Create a user |
| GET | `/users/{id}` | Get a user |
| DELETE | `/users/{id}` | Delete a user |
| GET | `/quizzes` | List all quizzes |
| POST | `/quizzes` | Create a quiz |
| GET | `/quizzes/{id}/questions` | Get questions for a quiz |
| POST | `/questions` | Create a question |
| GET | `/questions/{id}` | Get a question |
| DELETE | `/questions/{id}` | Delete a question |
| GET | `/questions/{id}/options` | Get answer options |
| POST | `/options` | Create an answer option |
| POST | `/sessions` | Create a session |
| GET | `/sessions/{id}` | Get a session |
| GET | `/sessions/by-code/{code}` | Get session by join code |
| PATCH | `/sessions/{id}/status` | Update session status |
| POST | `/session-players` | Add a player to a session |
| GET | `/sessions/{id}/players` | List players in a session |
| POST | `/session-answers` | Submit an answer |

## Tech

- Python 3
- FastAPI
- PostgreSQL
- psycopg2
- Pydantic

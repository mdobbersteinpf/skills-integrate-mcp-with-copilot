# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- Sign up for activities
- Teacher-only activity registration and removal

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

2. Run the application:

   ```
   python app.py
   ```

3. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| GET    | `/auth/status`                                                    | Check whether the current browser session is signed in as a teacher |
| POST   | `/auth/login`                                                     | Sign in as a teacher with a JSON username and password              |
| POST   | `/auth/logout`                                                    | End the current teacher session                                     |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Teacher: sign up a student for an activity                         |
| DELETE | `/activities/{activity_name}/unregister?email=student@mergington.edu` | Teacher: remove a student from an activity                       |

## Teacher Mode Configuration

Set `TEACHER_USERNAME` and `TEACHER_PASSWORD` in the server environment to enable teacher login. Set `SESSION_SECRET` to a long, random secret so signed sessions remain valid across restarts. For HTTPS deployments, set `COOKIE_SECURE=true`; local HTTP development can leave it unset. Without teacher credentials configured, teacher login is disabled. Activity browsing remains public, while signup and unregister requests require a teacher session.

## Data Model

The application uses a simple data model with meaningful identifiers:

1. **Activities** - Uses activity name as identifier:

   - Description
   - Schedule
   - Maximum number of participants allowed
   - List of student emails who are signed up

2. **Students** - Uses email as identifier:
   - Name
   - Grade level

All data is stored in memory, which means data will be reset when the server restarts.

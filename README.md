# Password Protection Lab

## Description

A Flask REST API with session-based authentication and bcrypt password hashing. Users can sign up, log in, check their session, and log out. A React frontend reflects the authenticated state.

## Features

- Secure password hashing with Flask-Bcrypt
- Session-based login/logout
- Protected `password_hash` property on the User model
- REST endpoints: `POST /signup`, `POST /login`, `GET /check_session`, `DELETE /logout`

## Tools & Resources

- [GitHub Repo](https://github.com/learn-co-curriculum/flask-password-protection-lab)
- [Flask-Bcrypt](https://flask-bcrypt.readthedocs.io/en/1.0.1/)

## Set Up

```console
$ pipenv install && pipenv shell
$ npm install --prefix client
$ cd server
$ flask db upgrade head
```

## Running the App

Flask backend (port 5555):

```console
$ python app.py
```

React frontend (port 4000) in a second terminal:

```console
$ npm start --prefix client
```

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/signup` | Create account, hash password, start session |
| POST | `/login` | Verify credentials, start session |
| GET | `/check_session` | Return user if session active, else 204 |
| DELETE | `/logout` | Clear session |

## Running Tests

```console
$ python -m pytest -x
```

## Implementation

**User model** (`server/models.py`):
- `password_hash` getter raises an Exception to prevent reading the hash
- `password_hash` setter hashes the password with `bcrypt.generate_password_hash()`
- `authenticate()` verifies a password with `bcrypt.check_password_hash()`

**Resources** (`server/app.py`):
- `Signup` — creates user, stores hashed password, saves `user_id` in session
- `CheckSession` — returns user JSON if session active, else 204
- `Login` — authenticates credentials, sets session
- `Logout` — clears `user_id` from session

## Submit your solution

Once all tests are passing, commit and push your work using `git` to submit to
CodeGrade through Canvas.

```bash
git add .
git commit -m "final solution"
git push
```

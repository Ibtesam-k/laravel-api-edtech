# EdTech REST API

A REST API built with Laravel for an educational platform where teachers can manage courses and assignments, while students can enroll in courses and submit their work.

The application includes JWT authentication, student and teacher roles, course and assignment management, submission tracking, and integration with an external API for submission logging.

## Features

- **JWT Authentication:** User registration, login, logout, token refresh, and authenticated user retrieval.
- **User Management:** Create, retrieve, update, delete, and filter users by role (student or teacher).
- **Course Management:** Create, retrieve, update, and delete courses.
- **Assignment Management:** Create, retrieve, update, and delete assignments associated with courses.
- **Submission Management:** Create, retrieve, and delete student submissions, with support for bulk submission creation.
- **Submission Logging:** Send submission data to an external API and record the results of the requests.
- **Automated Testing:** Includes tests for selected application functionality using Laravel's testing framework.
- **API Collection:** Includes a Postman collection with requests for exploring and manually testing the endpoints.

## Tech Stack

- PHP 8.2+
- Laravel 11
- SQLite
- JWT Authentication (tymon/jwt-auth)

## Project Structure

The application uses the following main models and relationships:

| Model | Description |
|---|---|
| User | Represents students and teachers, distinguished by their role. |
| Course | Belongs to a teacher and can have multiple enrolled students. |
| Assignment | Belongs to a course. |
| Submission | Represents a student's submission for an assignment. |
| SubmissionLog | Stores the results of sending submission data to an external API. |

## Submission Handling

Students can create and delete their submissions. Updating an existing submission is not supported; students can replace a submission by deleting it and creating a new one.

Bulk submission creation is also supported, with a maximum of five submissions per request.

## Getting Started

### Prerequisites

- PHP 8.2 or later
- Composer
- SQLite

### Installation (Windows)

1. Clone the repository:

   ```bash
   git clone https://github.com/Ibtesam-k/laravel-api-edtech.git
   cd laravel-api-edtech
   ```

2. Install dependencies:

   ```bash
   composer install
   ```

3. Configure the environment:

   ```bash
   copy .env.example .env
   php artisan key:generate
   ```

4. Generate the JWT secret:

   ```bash
   php artisan jwt:secret
   ```

5. Create the SQLite database file:

   ```bash
   type nul > database\database.sqlite
   ```

6. Configure the database connection in `.env`:

   ```env
   DB_CONNECTION=sqlite
   ```

7. Run migrations and seed the database:

   ```bash
   php artisan migrate:fresh --seed
   ```

## API Authentication

All API requests should include the following header:

```http
Accept: application/json
```

The following authentication endpoints are publicly accessible:

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/auth/register` | Register a new student |
| POST | `/api/auth/login` | Authenticate a user |

Additional authentication endpoints support logout, token refresh, and retrieving the authenticated user.

After logging in, include the returned JWT token in the Authorization header when accessing protected endpoints:

```http
Authorization: Bearer YOUR_TOKEN
```

### Default Seeded User

A default user is created by the database seeder and can be used for local development:

```json
{
    "email": "admin@example.com",
    "password": "password123"
}
```

**Note:** These are development credentials only. Do not use them in a production environment.

## Postman Collection

The repository includes a Postman collection:

`edtech.postman_collection.json`

Import the collection into Postman to explore and manually test the available API endpoints.

## Running Tests

The project includes automated tests covering selected application functionality.

Run the tests using:

```bash
php artisan test
```

# Student CRUD API Project

## Overview

This project is a professional, beginner-friendly Student CRUD API built with Node.js, Express, and MongoDB. It provides a secure backend for creating, reading, updating, and deleting student records, including support for image uploads and user authentication.

The API is designed to help learners understand how to build a modern RESTful service with:
- User registration and login
- JWT authentication
- Student management endpoints
- File uploads for student profile pictures
- MongoDB data storage
- Simple rate limiting and security middleware

> Note: The backend server is located in `Student-CRUD-API-Project/crud-api-project`.

## What this project does

This API lets authenticated users manage a student database. It supports:
- Registering a user account
- Logging in to receive a JWT token
- Adding new students
- Listing students with search and pagination
- Retrieving a single student record
- Updating student details and profile images
- Deleting students and their uploaded images

## Tech stack

- Node.js
- Express
- MongoDB / Mongoose
- JSON Web Tokens (JWT)
- Multer for file uploads
- Helmet for security headers
- CORS
- Express rate limiting

## Prerequisites

Make sure you have the following installed:

- Node.js (v16 or later recommended)
- npm
- MongoDB running locally or a MongoDB connection URI

## Quick start

1. Clone the repository:

```bash
git clone <your-repo-url>
```

2. Change into the API folder:

```bash
cd Student-CRUD-API-Project/crud-api-project
```

3. Install dependencies:

```bash
npm install
```

4. Confirm your environment variables in `.env`.

If `.env` is missing or you want to update it, create a file named `.env` with:

```env
PORT=3000
MONGO_URL=mongodb://localhost:27017/students-crud  # replace this with your MongoDB connection URL
JWT_SECRET=your-secret-key
```

5. Start the API server:

```bash
npm start
```

6. Open the API in your browser or use a tool like Postman / Insomnia at:

```text
http://localhost:3000
```

## Environment variables explained

- `PORT`: The port where the server listens (example: `3000`).
- `MONGO_URL`: The MongoDB connection URI.
- `JWT_SECRET`: The secret key used to sign authentication tokens.

## API endpoints

### Authentication

- `POST /api/users/register`
  - Register a new user.
  - Request body: `{ username, email, password }`

- `POST /api/users/login`
  - Log in and receive a JWT token.
  - Request body: `{ username, password }`

- `POST /api/users/logout`
  - Returns a logout confirmation message.

### Student management (protected)

> All student endpoints require an `Authorization` header with a valid token:
> `Authorization: Bearer <token>`

- `GET /api/students`
  - Retrieve student records.
  - Supports query parameters: `search`, `page`, `limit`.

- `GET /api/students/:id`
  - Get one student by ID.

- `POST /api/students`
  - Create a new student record.
  - Supports file upload field `profile_pic`.
  - Required fields: `first_name`, `last_name`, `email`, `phone`, `gender`.

- `PUT /api/students/:id`
  - Update a student record.
  - Supports updating the profile picture too.

- `DELETE /api/students/:id`
  - Remove a student record and delete the stored image.

## Student data model

A student record includes:

- `first_name`
- `last_name`
- `email`
- `phone`
- `gender` (`Male`, `Female`, `Other`)
- `profile_pic` (optional image filename)

## Notes

- Uploaded images are stored in the `uploads` folder.
- Student endpoints are protected by JWT authentication.
- The project uses MongoDB to store both user and student data.
- The server applies a rate limit to protect from too many requests.

## Optional frontend

This repository also contains a simple frontend in `Student-CRUD-API-Project/front-crud-api`.
You can open the HTML files directly in your browser to interact with the API if the frontend is configured for this backend.

## Troubleshooting

- If the server fails to connect to MongoDB, make sure MongoDB is running and `MONGO_URL` is correct.
- If login fails, verify the correct username and password and ensure `JWT_SECRET` matches the environment value used to sign tokens.
- For file upload issues, confirm requests use `multipart/form-data` and that image files are attached.

## Recommended next steps

- Explore `crud-api-project/index.js` to see middleware and route setup.
- Review `routes/students.routes.js` and `routes/users.routes.js` for full API behavior.
- Use Postman or Insomnia to test each endpoint step by step.

---

Happy coding! This project is a great way to learn backend API development with authentication, file uploads, and MongoDB CRUD operations.
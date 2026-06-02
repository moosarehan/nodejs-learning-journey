# 🎓 Student CRUD API Project

> A **full-stack student management system** with a RESTful API backend and a vanilla HTML/JS frontend — featuring JWT authentication, image uploads, pagination, search, rate limiting, and security hardening.

---

## 🎯 What Does This Project Do?

This project is a complete **Student Management System** split into two parts:

| Part | Folder | Description |
| :--- | :--- | :--- |
| **Backend API** | `crud-api-project/` | RESTful API built with Express.js, MongoDB, JWT auth, Multer image uploads |
| **Frontend UI** | `front-crud-api/` | Vanilla HTML/CSS/JS interface with Bootstrap for login, registration, and student dashboard |

### 🔄 Application Flow

```
┌─────────────────────────────────────────────────────────────────────┐
│                        FRONTEND (front-crud-api)                    │
│                                                                     │
│  ┌──────────┐     ┌──────────┐     ┌────────────────────────────┐  │
│  │ Register │────▶│  Login   │────▶│    Student Dashboard       │  │
│  │   Page   │     │   Page   │     │  (Add/View/Edit/Delete)    │  │
│  └──────────┘     └──────────┘     └────────────────────────────┘  │
│                        │                        │                   │
└────────────────────────┼────────────────────────┼───────────────────┘
                         │  JWT Token             │  API Calls
                         ▼                        ▼
┌─────────────────────────────────────────────────────────────────────┐
│                        BACKEND API (crud-api-project)               │
│                                                                     │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────────────┐  │
│  │  User Routes │  │  JWT Auth    │  │   Student Routes         │  │
│  │  /api/users  │  │  Middleware  │──▶│   /api/students          │  │
│  │  (public)    │  │  (protects)  │  │   (protected)            │  │
│  └──────────────┘  └──────────────┘  └──────────────────────────┘  │
│                                                                     │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────────────┐  │
│  │   Helmet     │  │ Rate Limiter │  │   Multer (Image Upload)  │  │
│  │  (Security)  │  │ (5 req/min)  │  │   (Profile Pictures)     │  │
│  └──────────────┘  └──────────────┘  └──────────────────────────┘  │
│                              │                                      │
│                              ▼                                      │
│                     ┌──────────────┐                                │
│                     │   MongoDB    │                                │
│                     │  (Database)  │                                │
│                     └──────────────┘                                │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

### Backend (`crud-api-project`)

| Technology | Purpose |
| :--- | :--- |
| ![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=node.js&logoColor=white) | JavaScript runtime |
| ![Express.js](https://img.shields.io/badge/Express.js-000000?style=flat-square&logo=express&logoColor=white) | Web framework & routing |
| ![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white) | NoSQL database |
| ![Mongoose](https://img.shields.io/badge/Mongoose-880000?style=flat-square&logoColor=white) | MongoDB ODM |
| ![JWT](https://img.shields.io/badge/JWT-000000?style=flat-square&logo=jsonwebtokens&logoColor=white) | Token-based authentication |
| ![bcrypt](https://img.shields.io/badge/bcryptjs-FF6F00?style=flat-square&logoColor=white) | Password hashing |
| ![Multer](https://img.shields.io/badge/Multer-FF4081?style=flat-square&logoColor=white) | File/image upload handling |
| ![Helmet](https://img.shields.io/badge/Helmet-4B0082?style=flat-square&logoColor=white) | HTTP security headers |
| ![Rate Limit](https://img.shields.io/badge/Rate_Limiter-DC143C?style=flat-square&logoColor=white) | API rate limiting (5 req/min) |
| ![CORS](https://img.shields.io/badge/CORS-0088CC?style=flat-square&logoColor=white) | Cross-origin resource sharing |
| ![dotenv](https://img.shields.io/badge/dotenv-ECD53F?style=flat-square&logoColor=black) | Environment variables |

### Frontend (`front-crud-api`)

| Technology | Purpose |
| :--- | :--- |
| ![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white) | Page structure |
| ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black) | Frontend logic & API calls |
| ![Bootstrap 5](https://img.shields.io/badge/Bootstrap_5-7952B3?style=flat-square&logo=bootstrap&logoColor=white) | Responsive UI components |

---

## 📁 Folder Structure

```
Student-CRUD-API-Project/
├── Read-Instructions.txt
│
├── crud-api-project/                  # ── BACKEND API ──
│   ├── index.js                       # Express app setup, middleware, routes
│   ├── package.json                   # Dependencies & scripts
│   ├── package-lock.json              # Locked versions
│   ├── .env                           # Environment variables (not committed)
│   │
│   ├── config/
│   │   └── database.js                # MongoDB connection with Mongoose
│   │
│   ├── middleware/
│   │   └── auth.js                    # JWT verification middleware
│   │
│   ├── models/
│   │   ├── students.model.js          # Student schema (name, email, phone, gender, pic)
│   │   └── users.models.js            # User schema (username, email, password, createdAt)
│   │
│   ├── routes/
│   │   ├── students.routes.js         # CRUD routes for students + image upload
│   │   └── users.routes.js            # Register, login, logout routes + JWT
│   │
│   └── uploads/                       # Uploaded profile pictures (auto-created)
│
└── front-crud-api/                    # ── FRONTEND UI ──
    ├── index.html                     # Login page
    ├── register.html                  # Registration page
    ├── students.html                  # Student dashboard (CRUD operations)
    └── js/
        └── script.js                  # Frontend API interaction logic
```

---

## 🚀 Getting Started

### Prerequisites

Make sure you have the following installed:

- **[Node.js](https://nodejs.org/)** (v16 or later recommended)
- **[MongoDB](https://www.mongodb.com/try/download/community)** (running locally on port `27017`)
- **[Git](https://git-scm.com/)**

---

### Step 1 — Clone the Repository

```bash
git clone https://github.com/moosarehan/nodejs-learning-journey.git
```

### Step 2 — Navigate to the Backend Folder

```bash
cd nodejs-learning-journey/Student-CRUD-API-Project/crud-api-project
```

### Step 3 — Install Backend Dependencies

```bash
npm install
```

This will install:

| Package | Purpose |
| :--- | :--- |
| `express` | Web framework |
| `mongoose` | MongoDB ODM |
| `jsonwebtoken` | JWT token generation & verification |
| `bcryptjs` | Password hashing |
| `multer` | Image upload handling |
| `helmet` | Security headers |
| `express-rate-limit` | Rate limiting |
| `cors` | Cross-origin support |
| `dotenv` | Environment variables |
| `nodemon` | Auto-restart on file changes |

### Step 4 — Create the `.env` File

Create a `.env` file in the `crud-api-project/` folder:

```env
PORT = 3000
MONGO_URL = your mongodb url
JWT_SECRET = YourSecretKeyHere123
```

> ⚠️ **Important:** Replace `YourSecretKeyHere123` with your own secret key. Keep this file private and never commit it to GitHub.

### Step 5 — Create the Uploads Folder

```bash
mkdir uploads
```

This folder is where student profile pictures will be stored.

### Step 6 — Start MongoDB

Make sure your local MongoDB server is running:

```bash
mongod
```

> 💡 **Tip:** If you're using **MongoDB Compass**, just open it — it usually starts the server automatically.

### Step 7 — Start the Backend Server

```bash
npm start
```

You should see:

```
Connected to MongoDB
Server running on port 3000
```

### Step 8 — Open the Frontend

Open the frontend by simply opening the HTML files in your browser:

| Page | File |
| :--- | :--- |
| **Login** | Open `front-crud-api/index.html` in browser |
| **Register** | Open `front-crud-api/register.html` in browser |
| **Student Dashboard** | Redirected to after login → `students.html` |

> 💡 **Tip:** You can also use a live server extension (like **Live Server** in VS Code) to serve the frontend files.

---

## 📡 API Endpoints

### 🔓 Public Routes (No Auth Required)

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/users/register` | Register a new user |
| `POST` | `/api/users/login` | Login and receive JWT token |
| `POST` | `/api/users/logout` | Logout (client-side token removal) |

### 🔐 Protected Routes (JWT Token Required)

All student routes require an `Authorization` header:
```
Authorization: Bearer <your_jwt_token>
```

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/api/students` | Get all students (with search & pagination) |
| `GET` | `/api/students/:id` | Get a single student by ID |
| `POST` | `/api/students` | Add a new student (supports image upload) |
| `PUT` | `/api/students/:id` | Update a student (supports image upload) |
| `DELETE` | `/api/students/:id` | Delete a student and their profile picture |

### 📄 Query Parameters for `GET /api/students`

| Parameter | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `search` | `string` | `""` | Search by first or last name |
| `page` | `number` | `1` | Page number for pagination |
| `limit` | `number` | `5` | Number of results per page |

**Example:**
```
GET /api/students?search=ali&page=1&limit=10
```

---

## 🔒 Security Features

| Feature | Implementation |
| :--- | :--- |
| **Password Hashing** | All passwords hashed with `bcryptjs` (10 salt rounds) before storage |
| **JWT Authentication** | Stateless token-based auth with 1-hour expiration |
| **Rate Limiting** | Max 5 requests per minute per IP address |
| **Helmet** | Sets secure HTTP headers (XSS protection, content sniffing prevention, etc.) |
| **CORS** | Cross-Origin Resource Sharing enabled for frontend-backend communication |
| **File Validation** | Only image files accepted for upload (MIME type check) |
| **File Size Limit** | Max 3MB per uploaded image |
| **Error Handling** | Global error handler for Multer errors and server errors |

---

## 🧪 Testing with Postman

### 1. Register a User
```
POST http://localhost:3000/api/users/register
Content-Type: application/json

{
  "username": "testuser",
  "email": "test@example.com",
  "password": "password123"
}
```

### 2. Login and Get Token
```
POST http://localhost:3000/api/users/login
Content-Type: application/json

{
  "username": "testuser",
  "password": "password123"
}
```
**Response:**
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

### 3. Create a Student (with the token)
```
POST http://localhost:3000/api/students
Authorization: Bearer <paste_your_token_here>
Content-Type: multipart/form-data

Fields:
  first_name: Ali
  last_name: Khan
  email: ali@example.com
  phone: 03001234567
  gender: Male
  profile_pic: (select an image file)
```

---

## 🧠 What You'll Learn

If you're a beginner, this project teaches you:

1. ✅ How to build a **RESTful CRUD API** with Express.js
2. ✅ How to implement **JWT-based authentication** (register, login, protected routes)
3. ✅ How to **hash passwords** securely with bcrypt
4. ✅ How to **upload images** using Multer with file validation
5. ✅ How to implement **server-side pagination** and **search**
6. ✅ How to add **rate limiting** to prevent API abuse
7. ✅ How to secure your API with **Helmet** security headers
8. ✅ How to enable **CORS** for frontend-backend communication
9. ✅ How to use **environment variables** with dotenv
10. ✅ How to build a **frontend** that consumes a REST API with `fetch()`
11. ✅ How to store and manage **JWT tokens** in `localStorage`
12. ✅ How to handle **global error handling** middleware in Express

---

## ⚠️ Important Notes

> [!NOTE]
> The `.env` file is **not included** in the repository for security reasons. You must create it manually (see Step 4 above).

> [!WARNING]
> The `node_modules` folder is **not included**. Always run `npm install` before starting the server.

> [!CAUTION]
> Never expose your `JWT_SECRET` in public repositories. Always use environment variables for sensitive data.

---

## 📝 License

This project is open source and available for learning purposes.

---

<p align="center">
  Made with ❤️ while learning Node.js
</p>

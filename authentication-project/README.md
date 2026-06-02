# 🔐 Authentication Project

> A complete **session-based authentication system** built with Node.js, Express, MongoDB, and EJS — featuring user registration, login, logout, password hashing, and protected routes.

---

## 🎯 What Does This Project Do?

This project demonstrates how to build a **full authentication flow from scratch** using server-side sessions — no JWT, no third-party auth providers — just the fundamentals every backend developer needs to understand.

### 🔄 User Flow

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│              │     │              │     │              │
│   Register   │────▶│    Login     │────▶│  Home Page   │
│   /register  │     │    /login    │     │      /       │
│              │     │              │     │              │
└──────────────┘     └──────────────┘     └──────┬───────┘
                                                 │
                                          ┌──────▼───────┐
                                          │              │
                                          │   Profile    │
                                          │   /profile   │
                                          │              │
                                          └──────┬───────┘
                                                 │
                                          ┌──────▼───────┐
                                          │              │
                                          │   Logout     │
                                          │   /logout    │
                                          │              │
                                          └──────────────┘
```

1. **Register** → User creates an account (password is hashed with bcrypt)
2. **Login** → User enters credentials, password is compared against hashed version
3. **Session Created** → On successful login, a session is created on the server
4. **Protected Routes** → Home (`/`) and Profile (`/profile`) are only accessible when logged in
5. **Logout** → Session is destroyed, user is redirected to login

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
| :--- | :--- | :--- |
| **Runtime** | ![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=node.js&logoColor=white) | JavaScript runtime |
| **Framework** | ![Express.js](https://img.shields.io/badge/Express.js-000000?style=flat-square&logo=express&logoColor=white) | Web server & routing |
| **Database** | ![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white) | NoSQL database for storing users |
| **ODM** | ![Mongoose](https://img.shields.io/badge/Mongoose-880000?style=flat-square&logoColor=white) | MongoDB object modeling |
| **Template Engine** | ![EJS](https://img.shields.io/badge/EJS-B4CA65?style=flat-square&logoColor=white) | Server-side HTML rendering |
| **Styling** | ![Bootstrap](https://img.shields.io/badge/Bootstrap_5-7952B3?style=flat-square&logo=bootstrap&logoColor=white) | Responsive UI components |
| **Auth** | ![bcrypt](https://img.shields.io/badge/bcryptjs-FF6F00?style=flat-square&logoColor=white) | Password hashing |
| **Sessions** | ![express-session](https://img.shields.io/badge/express--session-4B0082?style=flat-square&logoColor=white) | Server-side session management |

---

## 📁 Folder Structure

```
authentication-project/
├── index.js                   # Main app: Express server, routes, middleware, session config
├── package.json               # Project metadata and dependencies
├── package-lock.json          # Locked dependency versions
│
├── model/
│   └── user.model.js          # Mongoose schema for User (username, hashed password)
│
└── views/
    ├── login.ejs              # Login page with Bootstrap form + error alerts
    └── register.ejs           # Registration page with Bootstrap form
```

---

## 🔑 Key Concepts Covered

| Concept | How It's Used |
| :--- | :--- |
| **Password Hashing** | Passwords are hashed with `bcryptjs` (salt rounds: 10) before storing in DB |
| **Session Management** | `express-session` creates a server-side session on login |
| **Route Protection** | Custom `checkLogin` middleware blocks unauthenticated users |
| **Error Handling** | Login errors ("User not found", "Invalid Password") are displayed on the page |
| **Template Rendering** | EJS templates render dynamic HTML with error messages |

---

## 🚀 Getting Started

### Prerequisites

Make sure you have the following installed on your machine:

- **[Node.js](https://nodejs.org/)** (v16 or later recommended)
- **[MongoDB](https://www.mongodb.com/try/download/community)** (running locally on default port `27017`)
- **[Git](https://git-scm.com/)**

### 1. Clone the Repository

```bash
git clone https://github.com/moosarehan/nodejs-learning-journey.git
```

### 2. Navigate to the Project Folder

```bash
cd nodejs-learning-journey/authentication-project
```

### 3. Install Dependencies

```bash
npm install
```

This will install the following packages:

| Package | Version | Purpose |
| :--- | :--- | :--- |
| `express` | ^5.1.0 | Web framework for building the server |
| `mongoose` | ^8.13.2 | MongoDB object modeling |
| `ejs` | ^3.1.10 | Embedded JavaScript template engine |
| `express-session` | ^1.18.1 | Session middleware for Express |
| `bcryptjs` | ^3.0.2 | Password hashing library |
| `nodemon` | ^3.1.9 | Auto-restart server on file changes |

### 4. Start MongoDB

Make sure your local MongoDB server is running:

```bash
mongod
```

> 💡 **Tip:** If you're using **MongoDB Compass**, just open it — it usually starts the server automatically. The app connects to `mongodb://127.0.0.1/user-crud`.

### 5. Run the Server

```bash
npm start
```

You should see:

```
Connected!
Server running on port 3000
```

### 6. Open in Browser

| Page | URL |
| :--- | :--- |
| **Login** | [http://localhost:3000/login](http://localhost:3000/login) |
| **Register** | [http://localhost:3000/register](http://localhost:3000/register) |
| **Home** (protected) | [http://localhost:3000/](http://localhost:3000/) |
| **Profile** (protected) | [http://localhost:3000/profile](http://localhost:3000/profile) |

---

## 📡 Routes

| Method | Route | Auth Required | Description |
| :--- | :--- | :---: | :--- |
| `GET` | `/register` | ❌ | Renders the registration form |
| `POST` | `/register` | ❌ | Creates a new user with hashed password |
| `GET` | `/login` | ❌ | Renders the login form (redirects to `/` if already logged in) |
| `POST` | `/login` | ❌ | Validates credentials and creates a session |
| `GET` | `/` | ✅ | Home page — displays welcome message with username |
| `GET` | `/profile` | ✅ | Profile page — displays user info |
| `GET` | `/logout` | ✅ | Destroys the session and redirects to `/login` |

---

## 🔒 How Authentication Works (Step by Step)

### Registration
```
User submits form → Password hashed with bcrypt (10 salt rounds)
→ User document saved to MongoDB → Redirect to /login
```

### Login
```
User submits form → Find user by username in DB
→ Compare submitted password with stored hash using bcrypt
→ If match: Create session (req.session.user = username) → Redirect to /
→ If no match: Render login page with error message
```

### Route Protection
```
User requests protected route → checkLogin middleware runs
→ If req.session.user exists: Allow access (next())
→ If not: Redirect to /login
```

### Logout
```
User clicks logout → req.session.destroy() called
→ Session removed from server → Redirect to /login
```

---

## 🧠 What You'll Learn

If you're a beginner, this project teaches you:

1. ✅ How to set up an **Express.js** web server
2. ✅ How to connect to **MongoDB** using Mongoose
3. ✅ How to **hash passwords** securely with bcrypt
4. ✅ How to implement **session-based authentication**
5. ✅ How to **protect routes** with custom middleware
6. ✅ How to **render dynamic pages** with EJS templates
7. ✅ How to handle **form submissions** (POST requests)
8. ✅ How to display **server-side error messages** on the frontend

---

## ⚠️ Important Notes

> [!NOTE]
> This project uses **session-based authentication** (not JWT). Sessions are stored in server memory by default. For production, consider using a session store like `connect-mongo` to persist sessions in MongoDB.

> [!WARNING]
> The session secret (`secret123`) is hardcoded for learning purposes. In a real application, always store secrets in environment variables (`.env` file).

---

## 📝 License

This project is open source and available for learning purposes.

---

<p align="center">
  Made with ❤️ while learning Node.js
</p>

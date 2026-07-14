# 🚀 Node.js & Backend Developer Learning Journey

> Welcome to my personal dashboard of hands-on practice code, exercises, and full-stack projects built while mastering backend web development. Each project is modular and focuses on key real-world design patterns, databases, and libraries.

---

## 🗺️ Project Portfolio Map

Explore the repository by checking out each modular application below. Every directory contains its own comprehensive, beginner-friendly setup guide.

| Project Name & Directory Link | Primary Purpose | Key Features | Technical Badges |
| :--- | :--- | :--- | :--- |
| 🎓 **[Student-CRUD-API-Project](./Student-CRUD-API-Project)** | Full-Stack Student Directory | JWT authentication, image uploads, server-side pagination, search queries, rate limiting. | ![Express](https://img.shields.io/badge/Express-000000?style=flat-square&logo=express&logoColor=white) ![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white) ![JWT](https://img.shields.io/badge/JWT-black?style=flat-square&logo=JSON-web-tokens) |
| 🔐 **[authentication-project](./authentication-project)** | Session-Based Auth Boilerplate | Sign-up, Sign-in, Route shielding (Auth Guard), Password hashing, persistent session stores. | ![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=node.js&logoColor=white) ![EJS](https://img.shields.io/badge/EJS-B83B2E?style=flat-square) ![bcrypt](https://img.shields.io/badge/bcrypt-4F5D95?style=flat-square) |
| 📇 **[contact-app](./contact-app)** | MVC Contact Directory | Clean CRUD operations, paginated tables, localized stylesheets, and unified 404/500 handlers. | ![Mongoose](https://img.shields.io/badge/Mongoose-880000?style=flat-square&logo=mongoose&logoColor=white) ![Bootstrap](https://img.shields.io/badge/Bootstrap-7952B3?style=flat-square&logo=bootstrap&logoColor=white) |
| 📊 **[datatables-project](./datatables-project)** | Rich Data Grids & Exports | Interactive reports rendering mock MongoDB data with export options (Excel, PDF, CSV). | ![DataTables](https://img.shields.io/badge/DataTables-336791?style=flat-square) ![Tabulator](https://img.shields.io/badge/Tabulator-3FB449?style=flat-square) ![CORS](https://img.shields.io/badge/CORS-Orange?style=flat-square) |
| 🧩 **[ejs-project](./ejs-project)** | EJS Templating Layouts | Layout partial imports, dynamic user listings in tables, dynamic POST form responses. | ![Express](https://img.shields.io/badge/Express-000000?style=flat-square&logo=express&logoColor=white) ![EJS](https://img.shields.io/badge/EJS-B83B2E?style=flat-square) ![Bootstrap](https://img.shields.io/badge/Bootstrap-7952B3?style=flat-square&logo=bootstrap&logoColor=white) |
| 📝 **[form-validation](./form-validation)** | Form Validation & Sanitization | Field presence checks, strong password criteria, range validations, custom validators, sanitizers. | ![express-validator](https://img.shields.io/badge/express--validator-5C3E5A?style=flat-square) ![EJS](https://img.shields.io/badge/EJS-A91E50?style=flat-square&logo=ejs&logoColor=white) |
| 📤 **[file-upload](./file-upload)** | Multi-Field Upload System | Safe disk-storage configuration, size checks (Max 3MB), MIME-type filters, and error boundaries. | ![Multer](https://img.shields.io/badge/Multer-E91E63?style=flat-square) ![EJS](https://img.shields.io/badge/EJS-A91E50?style=flat-square&logo=ejs&logoColor=white) |
| 🛡️ **[session-project](./session-project)** | Persistent Store Session Manager | Cookie-to-DB mapping, session lifespan rules, in-memory leaks comparison, and custom stores. | ![express-session](https://img.shields.io/badge/express--session-00599C?style=flat-square) ![connect-mongo](https://img.shields.io/badge/connect--mongo-47A248?style=flat-square) |
| 🔑 **[oauth-project](./oauth-project)** | Google OAuth 2.0 Social Login | Passport.js Google strategy, OAuth 2.0 authorization code flow, session-based user persistence, protected route middleware. | ![Passport](https://img.shields.io/badge/Passport.js-34E27A?style=flat-square&logo=passport&logoColor=white) ![Google](https://img.shields.io/badge/Google_OAuth-4285F4?style=flat-square&logo=google&logoColor=white) ![Session](https://img.shields.io/badge/express--session-FF6C37?style=flat-square) |

---

## 🧠 Major Learning Outcomes & Architecture Design

Throughout this journey, I have implemented and mastered these core concepts:

### 1. Model-View-Controller (MVC) Pattern
Organizing files into logical concerns:
*   **Models:** Schemas defining the structure of collections via Mongoose.
*   **Views:** Interactive UI templates rendered on the server side using **EJS** or served dynamically via **static assets**.
*   **Controllers:** Request handlers that manage the app logic and orchestrate DB transactions.
*   **Routes:** HTTP path listeners routing requests cleanly to their respective controllers.

### 2. State & Identity Management
*   **Stateless vs Stateful:** Understanding cookies and session lifecycle management.
*   **Local Session Stores:** Persisting sessions to MongoDB with `connect-mongo` so client state survives server restarts.
*   **Token-Based Security:** Signing and verifying JSON Web Tokens (JWT) for secure REST API endpoints.

### 3. File Streams & Parsing
*   Handling multipart payloads (`enctype="multipart/form-data"`) in Express using the **Multer** engine.
*   Mitigating server vulnerabilities by applying strict file size limits and checking magic bytes (MIME types) on incoming streams.

### 4. Interactive Client-Side Integrations
*   Consuming REST APIs on the frontend via AJAX/Fetch.
*   Creating feature-rich interactive dashboards with advanced sorting, column filtering, search, and document exportation (Excel, CSV, PDF) using **jQuery DataTables** and **Tabulator**.

### 5. OAuth 2.0 & Social Authentication
*   Implementing the full **OAuth 2.0 Authorization Code Flow** using **Passport.js** and the `passport-google-oauth20` strategy.
*   Delegating identity verification to a trusted third-party provider (Google) so the app never handles raw passwords.
*   Managing authenticated user state across requests via `serializeUser` / `deserializeUser` and `express-session`.
*   Protecting private routes with a reusable **auth guard middleware** (`req.isAuthenticated()`).
*   Securely storing OAuth credentials (Client ID, Client Secret, Callback URL) in environment variables via `dotenv`.

---

## ⚙️ Quick Start (Run Globally)

If you wish to clone this complete learning workspace and run the projects locally, follow these steps:

### 1. Prerequisites
Ensure you have the following installed:
*   [Node.js](https://nodejs.org/) (v16.0.0 or higher)
*   [MongoDB Community Server](https://www.mongodb.com/try/download/community) running locally on the default port `27017`

### 2. Clone Workspace
```bash
git clone https://github.com/moosarehan/nodejs-learning-journey.git
cd nodejs-learning-journey
```

### 3. Choose a Project & Execute
Navigate to any project directory, install its local packages, and start it. For example, to run the **contact-app**:
```bash
cd contact-app
npm install
npm start
```

---


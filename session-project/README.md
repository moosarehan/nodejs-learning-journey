# 🛡️ Session Management with MongoDB Store (Session Project)

> A lightweight, educational Node.js application demonstrating how to implement secure, persistent **session-based state management** using Express, `express-session`, and `connect-mongo` to store sessions in MongoDB.

---

## 🎯 What is Session Management?

By default, HTTP is a **stateless protocol**—each request from a browser is treated as entirely new and independent, meaning the server cannot natively remember if a user has logged in or set a preference.

This project demonstrates how to solve this statelessness using:
1.  **Session Cookies:** Storing a small, encrypted session ID in the client's browser.
2.  **Database Session Store (MongoDB):** Mapping that session ID to a persistent database record on the server, ensuring user sessions survive server restarts and scale securely.

---

## 🛠️ Tech Stack & Badges

| Category | Technology | Badge | Purpose |
| :--- | :--- | :--- | :--- |
| **Backend Runtime** | **Node.js** | ![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white) | Core JavaScript execution engine |
| **Framework** | **Express.js v5** | ![Express.js](https://img.shields.io/badge/Express.js-000000?style=flat-square&logo=express&logoColor=white) | Lightweight web routing framework |
| **Database Store** | **MongoDB** | ![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white) | Session storage layer |
| **Session Core** | **Express Session** | ![ExpressSession](https://img.shields.io/badge/ExpressSession-00599C?style=flat-square&logo=express&logoColor=white) | Session middleware generator |
| **Store Driver** | **Connect Mongo** | ![ConnectMongo](https://img.shields.io/badge/ConnectMongo-47A248?style=flat-square&logo=mongodb&logoColor=white) | MongoDB-backed session persistence store |

---

## 🔄 Architecture & Session Lifespan Flow

Here is how the browser session maps to the MongoDB database session store:

```text
  +------------------+                   +--------------------+                  +--------------------+
  |  Client Browser  |                   |   Express Server   |                  |  MongoDB Database  |
  | (Stores Cookie)  |                   | (Verifies Session) |                  |  (Stores Session)  |
  +--------+---------+                   +---------+----------+                  +---------+----------+
           |                                       |                                       |
           | ----- 1. GET /set-username ---------> |                                       |
           |                                       | --- 2. Write session "YahuBaba" ----> |
           |                                       |    (Stores in collection 'mysessions') |
           | <---- 3. Set Cookie (Session ID) ---- |                                       |
           |                                       |                                       |
           | ----- 4. GET /get-username ---------> |                                       |
           |    (Sends Cookie: Session ID)         | --- 5. Look up Session by ID -------> |
           |                                       | <-- 6. Returns Session JSON --------- |
           | <---- 7. Responds: "YahuBaba" ------- |                                       |
           |                                       |                                       |
           | ----- 8. GET /destroy --------------> |                                       |
           |                                       | --- 9. Delete session entry --------> |
           | <---- 10. Clears cookie ------------- |                                       |
           v                                       v                                       v
```

---

## 📋 API Route Reference

The app registers four simple routes in `index.js` to illustrate session state transitions:

| HTTP Method | Endpoint | Action Description | Response Output |
| :--- | :--- | :--- | :--- |
| **GET** | `/` | Checks session status. | Displays username if set, else shows `No username found`. |
| **GET** | `/set-username` | Stores a session value (`req.session.username = "YahuBaba"`). | Writes session to MongoDB and responds: `Username has been set`. |
| **GET** | `/get-username` | Reads the session value. | Displays session username. |
| **GET** | `/destroy` | Invalidates session and deletes DB entry. | Responds: `Session destroy successfully.` |

---

## 🧠 Core Session Configuration Explained

The session initialization inside `index.js` uses key options that are critical for session stability and security:

```javascript
app.use(session({
  secret: 'secretpassword', // Encryption key used to sign the session ID cookie
  resave: false,            // Prevents saving session to store if it wasn't modified
  saveUninitialized: false, // Prevents storing empty/uninitialized sessions in database
  store: MongoStore.create({ 
    mongoUrl: 'mongodb://127.0.0.1:27017/sessiondb', // MongoDB connection target
    collectionName : 'mysessions'                    // Custom session table/collection
  }),
  cookie: { maxAge: 1000 * 60 * 60 * 24 } // Cookie expiration set to 24 hours (in ms)
}))
```

### 💡 Why use `MongoStore` instead of standard MemoryStore?
By default, `express-session` stores sessions in **memory (RAM)**. This causes two major production issues:
1.  **Memory Leaks:** Memory continues to grow as users visit, eventually crashing the application.
2.  **State Loss:** Restarting the server clears all active sessions, logging out every single active user.
Using `connect-mongo` persists sessions directly inside MongoDB so they remain safe even when the server restarts or scales horizontally.

---

## 🚀 Setup & Installation Guide

Follow these steps to run this project on your machine:

### 1. Prerequisites
*   [Node.js](https://nodejs.org/) (v16.0.0 or higher)
*   [MongoDB Community Server](https://www.mongodb.com/try/download/community) installed and running locally on port `27017`

### 2. Clone and Navigate
```bash
git clone https://github.com/moosarehan/nodejs-learning-journey.git
cd nodejs-learning-journey/session-project
```

### 3. Install Dependencies
```bash
npm install
```

### 4. Start the Application
*   **For Development (Auto-reloads on file edits):**
    ```bash
    npm start
    ```
*   **Standard Mode:**
    ```bash
    node index.js
    ```

You should see the console log:
```text
Server running on port 3000
```

### 5. Step-by-Step Test Procedure
1.  Open your browser and visit: **[http://localhost:3000/](http://localhost:3000/)**
    *   *Result:* You will see `No username found in session.`
2.  Navigate to: **[http://localhost:3000/set-username](http://localhost:3000/set-username)**
    *   *Result:* You will see `Username has been set in session.`
3.  Go back to **[http://localhost:3000/](http://localhost:3000/)** or **[http://localhost:3000/get-username](http://localhost:3000/get-username)**
    *   *Result:* The server will remember your user state and display: `Username from session is : YahuBaba`
4.  Check your database (using MongoDB Compass or Shell):
    *   Query database: `sessiondb`
    *   Collection: `mysessions`
    *   *Observation:* You will see a document containing the session cookie metadata and `{ "username": "YahuBaba" }`.
5.  Navigate to **[http://localhost:3000/destroy](http://localhost:3000/destroy)**
    *   *Result:* You will see `Session destroy successfully.`
    *   *Observation:* If you refresh MongoDB, the document inside the `mysessions` collection will have been deleted.

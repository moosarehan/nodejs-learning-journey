# 📇 Contact Management Application (Contact App)

> A production-ready, beginner-friendly **Contact Management System** built using the classic **MVC (Model-View-Controller)** architecture with **Node.js, Express, MongoDB, and EJS**. Featuring clean pagination, complete CRUD operations, and responsive styling.

---

## 🎯 Project Overview

This application serves as an ideal learning project for mastering backend web development. It demonstrates how to build a dynamic, data-driven web app from scratch, handling database persistent storage, page routing, server-side rendering, and pagination of records.

### ⚡ Key Features

*   **✨ Full CRUD Operations:** Create, read, update, and delete contacts seamlessly.
*   **📃 Server-Side Pagination:** Utilizes `mongoose-paginate-v2` for efficient pagination (4 items per page by default) with dynamic next/previous page navigation controls.
*   **🎨 Elegant Responsive UI:** Built with custom-themed Bootstrap elements, featuring a Varela Round clean font, hover transitions, and interactive visual feedback.
*   **🛡️ Robust Error Handling:** Includes custom-designed `404 Not Found` (invalid/missing IDs) and `500 Internal Server Error` views.
*   **🔧 Environment Configured:** Secure database credentials and port configurations managed via `dotenv`.

---

## 🛠️ Tech Stack & Badges

| Category | Technology | Purpose |
| :--- | :--- | :--- |
| **Backend Runtime** | ![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white) | JavaScript execution environment |
| **Framework** | ![Express.js](https://img.shields.io/badge/Express.js-000000?style=flat-square&logo=express&logoColor=white) | Fast, unopinionated minimalist web framework |
| **Database** | ![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white) | Document-based NoSQL database |
| **ODM / Mapper** | ![Mongoose](https://img.shields.io/badge/Mongoose-880000?style=flat-square&logo=mongoose&logoColor=white) | Schema-based MongoDB modeling tool |
| **Template Engine** | ![EJS](https://img.shields.io/badge/EJS-A91E50?style=flat-square&logo=ejs&logoColor=white) | Server-side rendering HTML templates |
| **Styling & Icons** | ![Bootstrap](https://img.shields.io/badge/Bootstrap-7952B3?style=flat-square&logo=bootstrap&logoColor=white) ![FontAwesome](https://img.shields.io/badge/FontAwesome-339AF0?style=flat-square&logo=fontawesome&logoColor=white) | Responsive UI component styling and font icon sets |
| **Development** | ![Nodemon](https://img.shields.io/badge/Nodemon-76D04B?style=flat-square&logo=nodemon&logoColor=white) | Hot-reloading development server utility |

---

## 📐 MVC Architecture & Data Flow

This application is strictly structured around the **Model-View-Controller (MVC)** software design pattern. Here is how data flows through the system:

```text
                  +-----------------------------------------+
                  |               Web Browser               |
                  +--------------------+--------------------+
                                       | (HTTP Request)
                                       v
                  +--------------------+--------------------+
                  |      Express Router (routes/js)         |
                  +--------------------+--------------------+
                                       | (Matches URL pattern)
                                       v
                  +--------------------+--------------------+
                  |    Controller (contacts.controller.js)  |
                  +--------------------+--------------------+
                         /                             \
       (Fetches/Saves)  /                               \  (Passes Data)
                       v                                 v
       +---------------+--------------+         +--------+--------+
       |        Mongoose Model        |         |    EJS View     |
       |     (contacts.models.js)     |         |    (views/)     |
       +---------------+--------------+         +--------+--------+
                       | (Query/Write)                   |
                       v                                 | (Renders HTML)
       +---------------+--------------+                  v
       |        MongoDB Database      |                  |
       +------------------------------+                  |
                                                         v
                                                (Displays webpage)
```

---

## 📁 Directory Structure

Below is the clean directory tree of the project:

```text
contact-app/
├── config/
│   └── database.js          # MongoDB connection initialization code
├── controller/
│   └── contacts.controller.js # CRUD controller functions
├── models/
│   └── contacts.models.js   # Mongoose Schema & paginate configuration
├── public/
│   ├── bootstrap.min.css    # Offline Bootstrap stylesheet
│   └── custom.css           # Application specific custom style overrides
├── routes/
│   └── contacts.routes.js   # Endpoint route mappings
├── views/
│   ├── partials/
│   │   ├── header.ejs       # Shared head meta, styles, and navbar
│   │   └── footer.ejs       # Shared closing tags
│   ├── 404.ejs              # Page Not Found template
│   ├── 500.ejs              # Server Error template
│   ├── add-contact.ejs      # Create contact form page
│   ├── home.ejs             # Paginated list of all contacts
│   ├── show-contact.ejs     # Read-only detailed contact view
│   └── update-contact.ejs   # Edit contact form page
├── .env                     # App configuration and connection secrets
├── index.js                 # App configuration & Server startup script
├── package.json             # App dependencies & scripts
└── README.md                # Documentation (this file)
```

---

## 📋 API Route Table

The routing is highly intuitive and corresponds to standard RESTful paradigms:

| HTTP Method | Route URL | Controller Function | Description |
| :--- | :--- | :--- | :--- |
| **GET** | `/` | `getContacts` | Renders `home.ejs` with a paginated list of all contacts (default `limit = 4`). |
| **GET** | `/show-contact/:id` | `getContact` | Renders `show-contact.ejs` displaying full details of a specific contact. |
| **GET** | `/add-contact` | `addContactPage` | Renders `add-contact.ejs` containing the contact creation form. |
| **POST** | `/add-contact` | `addContact` | Saves a new contact from request body to database, then redirects to `/`. |
| **GET** | `/update-contact/:id`| `updateContactPage`| Renders `update-contact.ejs` containing fields populated with current data. |
| **POST** | `/update-contact/:id`| `updateContact` | Updates contact details in database, then redirects to `/`. |
| **GET** | `/delete-contact/:id`| `deleteContact` | Removes the contact record from database, then redirects to `/`. |

---

## 💾 Database Schema

The **Contact Model** contains the following schema structure, defined in `models/contacts.models.js`:

```javascript
const contactSchema = mongoose.Schema({
  first_name: { type: String },
  last_name:  { type: String },
  email:      { type: String },
  phone:      { type: String },
  address:    { type: String }
});
```

*Note: The `mongoose-paginate-v2` plugin is registered onto this schema to automatically attach the `.paginate()` utility method.*

---

## 🚀 Setup & Installation Guide

Follow these steps to run the application locally on your machine.

### 1. Prerequisites
Ensure you have the following installed on your machine:
*   [Node.js](https://nodejs.org/) (v16 or higher recommended)
*   [MongoDB Community Server](https://www.mongodb.com/try/download/community) running locally (or a remote MongoDB Atlas URI)

### 2. Clone and Navigate
Clone the repository to your local directory:
```bash
git clone https://github.com/moosarehan/nodejs-learning-journey.git
cd nodejs-learning-journey/contact-app
```

### 3. Install Dependencies
Install all backend NPM packages defined in `package.json`:
```bash
npm install
```

### 4. Configure Environment Variables
Create a file named `.env` in the root of the `/contact-app` directory:
```env
PORT=3000
MONGO_URL=mongodb://127.0.0.1:27017/contacts-crud
```
*Note: If you are using a cloud-hosted database (like MongoDB Atlas), replace the local `mongodb://...` string with your Atlas connection string.*

### 5. Running the Application
You can run the application using two scripts defined in `package.json`:

*   **Development Mode (Auto-reloads on file changes):**
    ```bash
    npm start
    ```
    *This runs the app using `nodemon`.*

*   **Standard Mode:**
    ```bash
    node index.js
    ```

Once started successfully, you should see:
```text
Database Connected.
Server started Successfully on port 3000.
```

### 6. Access the Application
Open your web browser and navigate to:
👉 **[http://localhost:3000](http://localhost:3000)**

---

## 🧠 What You'll Learn from This Project

By exploring this codebase, a beginner will understand:
1.  **ES Modules in Node.js:** Modern usage of `import` and `export` rather than `require()`.
2.  **Database Seeding & Pagination:** How pagination keeps pages lightweight by requesting chunks of records dynamically.
3.  **Bootstrap Customization:** Integrating static CSS files (`custom.css` and local Bootstrap files) with Express static middleware.
4.  **Route Protection/Validation:** Standard validation of MongoDB Object IDs (`mongoose.Types.ObjectId.isValid()`) to prevent app crashes due to malformed URLs.
5.  **Form Data Parsing:** Handling `x-www-form-urlencoded` headers to bind form controls to req.body.
# 🧩 Embedded JavaScript Templates Demo (EJS Project)

> A clean, beginner-friendly Node.js application demonstrating how to build a dynamic website using **EJS (Embedded JavaScript)** template engine with Express, Bootstrap 5, and custom styling.

---

## 🎯 What is EJS?

**EJS** is a simple templating language that lets you generate HTML markup with plain JavaScript. It allows you to:
1.  **Create Modular Views (Partials):** Share common components like headers, navigation bars, and footers across different pages.
2.  **Render Dynamic Data:** Inject backend JavaScript variables, arrays, and objects directly into the HTML using specific tags (`<%= %>` for output, `<% %>` for control flow like loops and conditionals).
3.  **Perform Control Flow:** Loop through collections and render list items or tables dynamically on the server side.

---

## 🛠️ Tech Stack & Badges

| Category | Technology | Badge | Purpose |
| :--- | :--- | :--- | :--- |
| **Backend Runtime** | **Node.js** | ![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white) | JavaScript execution environment |
| **Framework** | **Express.js** | ![Express.js](https://img.shields.io/badge/Express.js-000000?style=flat-square&logo=express&logoColor=white) | Routing and middleware core |
| **Template Engine** | **EJS** | ![EJS](https://img.shields.io/badge/EJS-B83B2E?style=flat-square) | Dynamic server-side rendering |
| **Styling** | **Bootstrap 5** | ![Bootstrap](https://img.shields.io/badge/Bootstrap-7952B3?style=flat-square&logo=bootstrap&logoColor=white) | Front-end CSS styling framework |
| **Dev Tool** | **Nodemon** | ![Nodemon](https://img.shields.io/badge/Nodemon-76D04B?style=flat-square&logo=nodemon&logoColor=white) | Auto-restarting development server |

---

## 📁 Directory Structure

```text
ejs-project/
├── public/
│   └── style.css       # Custom stylesheets served static by Express
├── views/
│   ├── about.ejs       # About page displaying dynamic user array in a table
│   ├── footer.ejs      # Reusable partial: Footer section
│   ├── form.ejs        # Input form page and submit feedback section
│   ├── header.ejs      # Reusable partial: Header tag, meta info, and CDN links
│   └── profile.ejs     # Plain HTML-based secondary profile view page
├── index.js           # Server initializer, urlencoded middleware, and routing
├── package.json       # App scripts and dependencies
└── README.md          # Documentation (this file)
```

---

## 📋 API Route Table

The app configures these core routes in `index.js`:

| HTTP Method | Route URL | View Rendered | Action Description |
| :--- | :--- | :--- | :--- |
| **GET** | `/` | *None (res.send)* | Serves basic text: `"Home Page"` |
| **GET** | `/about` | `about.ejs` | Renders a table of users passed dynamically from a backend array. |
| **GET** | `/form` | `form.ejs` | Renders an input form. |
| **POST** | `/submit` | `form.ejs` | Processes submitted text and renders a customized greeting. |

---

## 🧠 EJS Tag Cheat Sheet Used in This Project

*   `%- include('filename') %>`
    Imports a partial file (like a header or footer) into the current template.
*   `%= variable %>`
    Escapes and outputs the value of a variable into the HTML page.
*   `% control_flow { %>` ... `<% } %>`
    Runs control-flow code (like `forEach` loops or `if` statements) without outputting any text to the browser.
*   `%= item.name _%>`
    The underscore suffix (`_%>`) strips trailing whitespaces/newlines for clean HTML output formatting.

---

## 🚀 Setup & Installation Guide

Follow these steps to run the project locally:

### 1. Prerequisites
Ensure you have [Node.js](https://nodejs.org/) installed (v16.0.0 or higher).

### 2. Clone and Navigate
```bash
git clone https://github.com/moosarehan/nodejs-learning-journey.git
cd nodejs-learning-journey/ejs-project
```

### 3. Install Dependencies
```bash
npm install
```

### 4. Run the Project
*   **Development Mode (Auto-reloads on file changes):**
    ```bash
    npm start
    ```
*   **Standard Mode:**
    ```bash
    node index.js
    ```

You should see:
```text
Server started successfully on port : 3000
```

### 5. Access the App
Open your browser and navigate to:
👉 **[http://localhost:3000/about](http://localhost:3000/about)** or **[http://localhost:3000/form](http://localhost:3000/form)**

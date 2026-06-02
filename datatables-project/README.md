# 📊 DataTables Project

> A full-stack Node.js application that demonstrates how to display MongoDB data in beautiful, interactive data grids using **jQuery DataTables** and **Tabulator** — two of the most popular JavaScript table libraries.

---

## 🎯 What Does This Project Do?

This project is a **beginner-friendly** example of building a backend API with **Express.js** and **MongoDB**, and then rendering the data on the frontend using two different data table libraries:

| View | Library | Features |
| :--- | :--- | :--- |
| `index.html` | **jQuery DataTables** | Sorting, searching, pagination, export to Excel/PDF/CSV/Copy |
| `tabulator.html` | **Tabulator** | Sorting, inline header filtering, pagination, advanced column filtering, export to CSV/JSON/XLSX/PDF/HTML, print support |

Both views fetch user data from the same REST API endpoint (`/api/users`) and display it in a rich, interactive table with action buttons (View, Update, Delete).

---

## 🛠️ Tech Stack

| Layer | Technology |
| :--- | :--- |
| **Runtime** | ![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=node.js&logoColor=white) |
| **Framework** | ![Express.js](https://img.shields.io/badge/Express.js-000000?style=flat-square&logo=express&logoColor=white) |
| **Database** | ![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white) |
| **ODM** | ![Mongoose](https://img.shields.io/badge/Mongoose-880000?style=flat-square&logoColor=white) |
| **Frontend Tables** | ![jQuery DataTables](https://img.shields.io/badge/DataTables-336791?style=flat-square) · ![Tabulator](https://img.shields.io/badge/Tabulator-3FB449?style=flat-square) |
| **Other** | CORS enabled for cross-origin requests |

---

## 📁 Folder Structure

```
datatables-project/
├── index.js                  # Express server entry point & API route
├── package.json              # Project metadata and dependencies
├── package-lock.json         # Locked dependency versions
│
├── models/
│   └── users.model.js        # Mongoose User schema (name, email, age)
│
└── public/                   # Static frontend files served by Express
    ├── index.html            # DataTables view (jQuery DataTables)
    ├── script.js             # Client-side logic for DataTables
    ├── tabulator.html        # Tabulator view (alternative grid)
    └── tabulator.js          # Client-side logic for Tabulator
```

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
cd nodejs-learning-journey/datatables-project
```

### 3. Install Dependencies

```bash
npm install
```

This will install the following packages:
| Package | Purpose |
| :--- | :--- |
| `express` | Web framework for building the API |
| `mongoose` | MongoDB object modeling for Node.js |
| `cors` | Enable Cross-Origin Resource Sharing |
| `nodemon` | Auto-restart server on file changes (dev) |

### 4. Start MongoDB

Make sure your local MongoDB server is running:

```bash
mongod
```

> 💡 **Tip:** If you're using **MongoDB Compass**, just open it — it usually starts the server automatically.

### 5. Seed Sample Data (Optional)

The project connects to a database called `users_demo`. If you don't have any data yet, you can insert some sample users via **MongoDB Compass** or the **Mongo Shell**:

```js
// In Mongo Shell or Compass
use users_demo

db.users.insertMany([
  { name: "Ali Khan", email: "ali@example.com", age: 22 },
  { name: "Sara Ahmed", email: "sara@example.com", age: 25 },
  { name: "Usman Raza", email: "usman@example.com", age: 30 },
  { name: "Fatima Noor", email: "fatima@example.com", age: 19 },
  { name: "Hassan Ali", email: "hassan@example.com", age: 28 }
])
```

### 6. Run the Server

```bash
npm start
```

You should see:

```
Database Connected!
Server started
```

### 7. Open in Browser

| View | URL |
| :--- | :--- |
| **DataTables View** | [http://localhost:3000](http://localhost:3000) |
| **Tabulator View** | [http://localhost:3000/tabulator.html](http://localhost:3000/tabulator.html) |

---

## 📡 API Endpoint

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/api/users` | Returns all users from the `users_demo` database |

**Example Response:**
```json
{
  "data": [
    {
      "_id": "664abc123def456789012345",
      "name": "Ali Khan",
      "email": "ali@example.com",
      "age": 22
    }
  ]
}
```

---

## ✨ Key Features

### jQuery DataTables (`index.html`)
- ✅ Auto-pagination & search
- ✅ Column sorting
- ✅ Export buttons: **Excel**, **PDF**, **CSV**, **Copy**
- ✅ Action buttons per row (View, Update, Delete)

### Tabulator (`tabulator.html`)
- ✅ Auto-pagination with configurable page sizes (10, 25, 50, 100)
- ✅ Per-column header filtering (search within Name/Email columns)
- ✅ Advanced filter bar (field, operator, value)
- ✅ Export buttons: **CSV**, **JSON**, **XLSX**, **PDF**, **HTML**
- ✅ Print table support
- ✅ Action buttons per row (View, Update, Delete)

---

## 🧠 What You'll Learn

If you're a beginner, this project teaches you:

1. **How to build a REST API** with Express.js
2. **How to connect to MongoDB** using Mongoose
3. **How to serve static files** from Express
4. **How to use jQuery DataTables** to render API data in a rich table
5. **How to use Tabulator** as a modern, framework-free alternative
6. **How to add export functionality** (PDF, Excel, CSV) to data tables
7. **How to enable CORS** for API access from different origins

---

## 📝 License

This project is open source and available for learning purposes.

---

<p align="center">
  Made with ❤️ while learning Node.js
</p>

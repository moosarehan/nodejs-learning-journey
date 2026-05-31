# Contact App

## Overview

This project is a beginner-friendly contact management app built with Node.js, Express, EJS, and MongoDB. It allows users to create, view, update, and delete contact entries using a simple web interface.

The app demonstrates how to build a full CRUD application with:
- MongoDB data storage with Mongoose
- Pagination for contact lists
- Clean EJS views
- Route-based controllers
- Environment-based configuration

## What this project does

The Contact App lets users:
- View all saved contacts
- Add a new contact
- Edit an existing contact
- Delete a contact
- View a contact's details

The app uses server-side rendering, so each page is generated with data from the database and rendered in the browser using EJS.

## Tech stack

- Node.js
- Express
- MongoDB
- Mongoose
- mongoose-paginate-v2
- EJS
- Nodemon (development)

## Prerequisites

Be sure you have installed:
- Node.js
- npm
- MongoDB running locally or a MongoDB URI

## Setup and run

1. Change into the contact-app folder:

```bash
cd e:\NODEJS\nodejs-learning-journey\contact-app
```

2. Install dependencies:

```bash
npm install
```

3. Create or update the `.env` file if needed:

```env
PORT=3000
MONGO_URL=mongodb://127.0.0.1:27017/contacts-crud  # replace with your own MongoDB URL if needed
```

4. Start the server:

```bash
npm start
```

5. Open your browser to:

```text
http://localhost:3000
```

## Project structure

- `index.js` — application entry point and Express setup
- `config/database.js` — MongoDB connection logic
- `routes/contacts.routes.js` — route definitions
- `controller/contacts.controller.js` — contact CRUD controller actions
- `models/contacts.models.js` — Mongoose contact schema and pagination plugin
- `views/` — EJS templates for pages
- `public/` — static assets

## Key app features

- Paginated contact list with next/previous page support
- Detail view for a single contact
- Add contact form to save new entries
- Update form for editing contact information
- Delete route for removing contacts
- Error handling with user-friendly pages

## Notes

- The app is configured for local MongoDB by default.
- The `MONGO_URL` environment variable should point to your MongoDB instance.
- The app uses `mongoose-paginate-v2` to keep paging easy and efficient.

## Next improvements

You can extend this app by:
- Adding search/filter capabilities
- Adding form validation
- Adding user authentication
- Saving contact profile photos
- Adding sorting by name or date

Happy building! This project is a great way to learn contact CRUD with Express and MongoDB.
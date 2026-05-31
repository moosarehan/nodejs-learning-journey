# File Upload Project

## Overview

This project demonstrates a beginner-friendly Node.js file upload app using Express, Multer, and EJS. It allows users to upload one image file and multiple document files through a web form, then returns metadata about the uploaded files.

The project is ideal for learning how to:
- Build a simple upload form with EJS
- Handle multipart form submissions in Express
- Validate uploaded files by type and size
- Store uploads locally with Multer
- Report upload errors clearly

## What this project does

When the user visits the homepage, the app renders a form where they can:
- Enter a username
- Upload one image file (`userfile`)
- Upload up to three document files (`userdocuments`)

The server accepts:
- `image/jpeg` and `image/png` for the image field
- `application/pdf` for document uploads

After a successful upload, the server responds with details about the saved files.

## Tech stack

- Node.js
- Express
- Multer
- EJS
- Nodemon (development)

## Prerequisites

Make sure you have the following installed:
- Node.js
- npm

## Setup and run

1. Open a terminal and navigate to the project folder:

```bash
cd e:\NODEJS\nodejs-learning-journey\file-upload
```

2. Install dependencies:

```bash
npm install
```

3. Start the server:

```bash
npm start
```

4. Open your browser and go to:

```text
http://localhost:3000
```

## Project structure

- `index.js` — Express server and Multer file upload handling
- `package.json` — project metadata and dependencies
- `views/myform.ejs` — upload form template
- `uploads/` — local upload destination created automatically by Multer

## How the upload works

- The homepage renders an HTML form with `enctype="multipart/form-data"`.
- The server uses Multer middleware to store files in the `uploads` directory.
- The upload route accepts two fields:
  - `userfile` (single file)
  - `userdocuments` (multiple files)
- The upload logic checks file MIME types and rejects invalid formats.
- Errors from Multer are handled and returned with meaningful messages.

## Supported file rules

- `userfile`: only `jpeg` or `png` images
- `userdocuments`: only `pdf` documents
- Maximum file size: 3 MB per file

## Notes

- If no files are selected, the server responds with a `400` error.
- If too many files are sent or a wrong field name is used, the app returns a Multer error.
- The app is a simple learning example and does not implement user authentication.

## Next steps

You can extend this app by:
- Saving file metadata to a database
- Creating a user authentication flow
- Adding frontend validation before submission
- Serving uploaded files from a secure endpoint

Happy learning! This project is a great way to start with file uploads in Node.js.
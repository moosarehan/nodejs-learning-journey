# 🔐 Google OAuth 2.0 Authentication (OAuth Project)

> A hands-on **Google OAuth 2.0** implementation using **Node.js, Express, and Passport.js** — allowing users to log in securely with their Google account without ever handling passwords.

---

## 🤔 What is OAuth?

**OAuth (Open Authorization)** is an open-standard **authorization framework** that allows a third-party application to gain limited access to a user's account on another service — without exposing the user's password.

Think of it like a **hotel key card** 🏨:
- The hotel (Google) gives you a temporary key card (access token)
- You can use the key card to access certain rooms (your profile, email)
- You never hand your master key (password) to anyone else

### 🔄 OAuth 2.0 Flow (How it Works)

```text
  User                   Your App                  Google
   |                         |                         |
   |  1. Click "Login        |                         |
   |     with Google" ──────►|                         |
   |                         |  2. Redirect to Google  |
   |                         |────────────────────────►|
   |                         |                         |
   |◄────────────────────────────────────────────────── 3. Google shows
   |                         |                         |    consent screen
   |  4. User grants         |                         |
   |     permission ────────────────────────────────── ►|
   |                         |                         |
   |                         |◄──────────────────────── 5. Google returns
   |                         |                         |    auth code
   |                         |                         |
   |                         |  6. Exchange code for   |
   |                         |     access token ──────►|
   |                         |                         |
   |                         |◄──────────────────────── 7. Access token
   |                         |                         |    returned
   |                         |                         |
   |                         |  8. Fetch user profile  |
   |                         |────────────────────────►|
   |                         |                         |
   |◄──────────── 9. User    |◄──────────────────────── 8. Profile data
   |   logged in!            |                         |
```

---

## 💡 Why Use OAuth Instead of Traditional Auth?

| Feature | OAuth (Social Login) | Traditional (Username/Password) |
| :--- | :---: | :---: |
| **Password storage** | ❌ Not needed | ✅ Must hash & store securely |
| **Security burden** | Low — Google handles it | High — you manage breaches |
| **User experience** | ⚡ One click | 📝 Fill forms, verify email |
| **Email verification** | ✅ Already verified | Must implement yourself |
| **Forgotten passwords** | ❌ Not a problem | Needs reset flow |
| **Implementation time** | ⚡ Fast | Much longer |

**In short:** OAuth lets you delegate authentication to a trusted provider (Google, GitHub, Facebook), so you don't need to handle sensitive credentials at all.

---

## 🛠️ Tech Stack & Badges

| Category | Technology | Purpose |
| :--- | :--- | :--- |
| **Runtime** | ![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white) | JavaScript server-side execution |
| **Framework** | ![Express.js](https://img.shields.io/badge/Express.js-000000?style=flat-square&logo=express&logoColor=white) | HTTP routing and middleware pipeline |
| **Auth Middleware** | ![Passport.js](https://img.shields.io/badge/Passport.js-34E27A?style=flat-square&logo=passport&logoColor=white) | Pluggable authentication strategies |
| **OAuth Strategy** | ![Google](https://img.shields.io/badge/passport--google--oauth20-4285F4?style=flat-square&logo=google&logoColor=white) | Google OAuth 2.0 strategy for Passport |
| **Sessions** | ![Session](https://img.shields.io/badge/express--session-FF6C37?style=flat-square&logo=express&logoColor=white) | Persistent login session management |
| **Environment** | ![dotenv](https://img.shields.io/badge/dotenv-ECD53F?style=flat-square&logo=dotenv&logoColor=black) | Secure environment variable management |
| **Dev Server** | ![Nodemon](https://img.shields.io/badge/Nodemon-76D04B?style=flat-square&logo=nodemon&logoColor=white) | Auto-restart on file changes |

---

## 📁 Project Structure

```text
oauth-project/
├── auth/
│   └── google.js        # Passport Google OAuth2.0 strategy + serialize/deserialize
├── .env                 # 🔒 Secret credentials (never commit this!)
├── .env.example         # Template showing required environment variables
├── index.js             # Express app — routes, session config, middleware
├── package.json         # Dependencies and npm scripts
└── README.md            # Documentation (this file)
```

---

## 🔑 Getting Google OAuth Credentials (Step-by-Step)

You need **3 values** from Google: `Client ID`, `Client Secret`, and a `Callback URL`.
Here's exactly how to get them:

### Step 1 — Go to Google Cloud Console

Open 👉 [https://console.cloud.google.com/](https://console.cloud.google.com/) and sign in with your Google account.

---

### Step 2 — Create a New Project

1. Click the **project dropdown** at the top of the page (next to the Google Cloud logo)
2. Click **"New Project"**
3. Give it a name (e.g., `oauth-learning`) and click **"Create"**
4. Make sure the new project is **selected** in the dropdown

---

### Step 3 — Enable the Google+ / People API

1. In the left sidebar, go to **"APIs & Services"** → **"Library"**
2. Search for **"Google People API"** (or `Google+ API`)
3. Click on it and press **"Enable"**

---

### Step 4 — Configure the OAuth Consent Screen

1. Go to **"APIs & Services"** → **"OAuth consent screen"**
2. Select **"External"** (for testing with any Google account) → Click **"Create"**
3. Fill in the required fields:
   - **App name**: `OAuth Learning App` (or any name)
   - **User support email**: your Google email
   - **Developer contact email**: your Google email
4. Click **"Save and Continue"** through the rest of the steps (Scopes → Test users → Summary)
5. On the **"Test users"** step, click **"+ Add Users"** and add your own Google email
6. Click **"Save and Continue"** until done

> ⚠️ **Important:** While your app is in "Testing" mode, only added test users can log in.

---

### Step 5 — Create OAuth 2.0 Credentials

1. Go to **"APIs & Services"** → **"Credentials"**
2. Click **"+ Create Credentials"** → **"OAuth client ID"**
3. Set **Application type** to **"Web application"**
4. Give it a name (e.g., `oauth-web-client`)
5. Under **"Authorized redirect URIs"**, click **"+ Add URI"** and enter:
   ```
   http://localhost:3000/auth/google/callback
   ```
6. Click **"Create"**

---

### Step 6 — Copy Your Credentials

A dialog will appear showing:

```
✅ Your Client ID:      123456789-abcdefghijklmnop.apps.googleusercontent.com
✅ Your Client Secret:  GOCSPX-xxxxxxxxxxxxxxxxxxxx
```

**Copy both values** — you'll need them in the next step.

---

## ⚙️ Environment Variables Setup

### Create a `.env` File

In the root of the `oauth-project/` folder, create a file named **`.env`**:

```bash
# .env — Never commit this file to Git!

# Google OAuth Credentials (from Google Cloud Console)
GOOGLE_CLIENT_ID=your_client_id_here.apps.googleusercontent.com
GOOGLE_CLIENT_SECRET=GOCSPX-your_client_secret_here

# Callback URL — must match what you set in Google Console exactly
CALLBACK_URL=http://localhost:3000/auth/google/callback
```

### Create a `.env.example` File

This is a **safe template** you commit to Git so other developers know what variables they need:

```bash
# .env.example — Commit this file (no real secrets here)

GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
CALLBACK_URL=http://localhost:3000/auth/google/callback
```

### How the `.env` Variables Are Used

In `auth/google.js`, the credentials are loaded via `dotenv` and injected into the Passport strategy:

```javascript
require('dotenv').config()

passport.use(new GoogleStrategy({
    clientID:     process.env.GOOGLE_CLIENT_ID,      // ← from .env
    clientSecret: process.env.GOOGLE_CLIENT_SECRET,  // ← from .env
    callbackURL:  process.env.CALLBACK_URL           // ← from .env
  },
  function(accessToken, refreshToken, profile, cb) {
    return cb(null, profile);
  }
));
```

> 🔒 **Security Note:** The `.gitignore` already excludes `.env` files. Your secrets will never be pushed to GitHub.

---

## 🗺️ Route Reference

| Method | Route | Description |
| :--- | :--- | :--- |
| `GET` | `/` | Home page with "Login with Google" link |
| `GET` | `/auth/google` | Redirects user to Google's OAuth consent screen |
| `GET` | `/auth/google/callback` | Google redirects back here with the auth code |
| `GET` | `/profile` | 🔒 Protected — shows user's name & avatar (requires login) |
| `GET` | `/logout` | Destroys session and redirects to home page |

---

## 🚀 Setup & Installation Guide

### 1. Prerequisites

Ensure you have the following installed:
- [Node.js](https://nodejs.org/) (v16 or higher)
- A Google account to create OAuth credentials

### 2. Clone and Navigate

```bash
git clone https://github.com/moosarehan/nodejs-learning-journey.git
cd nodejs-learning-journey/oauth-project
```

### 3. Install Dependencies

```bash
npm install
```

### 4. Set Up Environment Variables

```bash
# Create your .env file
cp .env.example .env
```

Then open `.env` and fill in your `GOOGLE_CLIENT_ID` and `GOOGLE_CLIENT_SECRET` from the steps above.

### 5. Run the Application

```bash
npm start
```

You should see:
```text
Server is running at http://localhost:3000
```

### 6. Test the Login Flow

1. Open 👉 **[http://localhost:3000](http://localhost:3000)**
2. Click **"Login with Google"**
3. Select your Google account (must be a test user if app is in Testing mode)
4. You'll be redirected to `/profile` showing your name and Google avatar
5. Click **"Logout"** to end the session

---

## 🧱 Key Concepts Explained

### `passport.serializeUser` and `passport.deserializeUser`

```javascript
// Serialize: What to store in the session (just the user object)
passport.serializeUser(function(user, done) {
  done(null, user);
});

// Deserialize: How to retrieve the user from session on each request
passport.deserializeUser(function(user, done) {
  done(null, user);
});
```

- **Serialize** runs once after login — saves the user to the session
- **Deserialize** runs on every request — reconstructs `req.user` from the session

### The `authCheck` Middleware

```javascript
function authCheck(req, res, next) {
  if (req.isAuthenticated()) {
    return next()  // User is logged in — allow access
  }
  res.redirect('/')  // Not logged in — kick back to home
}
```

This protects the `/profile` route from unauthenticated access. Any route wrapped with `authCheck` requires a valid login session.

---

## 🧠 What You'll Learn from This Project

1. **OAuth 2.0 Authorization Code Flow** — Understand how the token exchange works end-to-end
2. **Passport.js Strategy Pattern** — How pluggable auth strategies simplify social login
3. **Session-Based Authentication** — How `express-session` persists login state across requests
4. **Environment Variable Best Practices** — Keeping secrets out of source code using `.env` and `.env.example`
5. **Route Protection Middleware** — How to guard private pages with a simple auth check function
6. **Separation of Concerns** — Why the Passport config lives in `auth/google.js` instead of `index.js`

---

## ⚠️ Common Gotchas

| Problem | Cause | Fix |
| :--- | :--- | :--- |
| `redirect_uri_mismatch` error | Callback URL in `.env` doesn't match Google Console | Make sure both are exactly `http://localhost:3000/auth/google/callback` |
| `Access blocked: app not verified` | App is in Testing mode | Add your email as a test user in the OAuth consent screen |
| `Cannot read property 'displayName'` | User not authenticated, `req.user` is `undefined` | Ensure `authCheck` middleware is applied to the `/profile` route |
| `.env` variables are `undefined` | `require('dotenv').config()` not called before use | Call it at the top of the file that uses `process.env` |
| Session not persisting | `express-session` middleware order is wrong | Make sure session middleware is registered **before** `passport.initialize()` |

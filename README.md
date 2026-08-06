# AI-Powered Career Prep & Resume Engineering Engine 🚀

A production-ready, full-stack web application designed to help job seekers accelerate their interview preparation and build ATS-optimized resumes using Google Gemini AI. Built with a modular 4-tier architecture (UI, API, State, and Custom Hooks), the platform automates skill gap analysis, generates tailored technical/behavioral interview roadmaps, and dynamically compiles server-side PDFs.

---

## ✨ Features

* **AI-Powered Gap Analysis & Mock Interviews:** Analyzes candidate resumes against job descriptions (JDs) to identify skill mismatches and generate custom technical and behavioral interview questions.
* **Strict Schema Type-Safety:** Uses **Zod** to enforce strict structured JSON output from Gemini AI, eliminating runtime parsing errors across complex prompt chains.
* **Production-Grade Security:**
  * **JWT Authentication** stored in secure `HttpOnly`, `SameSite` cookies to prevent client-side XSS access.
  * **Token Blacklisting** mechanism stored in database/cache for immediate session revocation upon logout.
* **Server-Side ATS Resume Generation:** Utilizes headless **Puppeteer** on the backend to render clean, ATS-compliant PDF resumes, keeping client bundle sizes lightweight and preventing browser DOM freezing.
* **Modular 4-Tier Architecture:** Clear separation between Presentation Layer (React), Custom Hooks (`useAuth`, `useInterview`), Centralized State Layer, and Backend API Controllers.

---

## 🏗 Architecture & Tech Stack

```


# 🏗️ Simple Architecture

┌─────────────────┐
│ Presentation UI │  ---> What the user sees (Pages & Buttons)
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Custom Hooks   │  ---> Business logic & API triggers (useAuth, useInterview)
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   State Store   │  ---> App memory (User data & Interview status)
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   Backend API   │  ---> Heavy lifting (Gemini AI, Puppeteer PDFs, MongoDB)
└─────────────────┘

```

* **Frontend:** React.js, SCSS (Sassy CSS)
* **Backend:** Node.js, Express.js
* **Database:** MongoDB Atlas
* **AI Engine:** Google Gemini AI API + Zod Schemas
* **PDF Rendering Engine:** Puppeteer (Headless Chromium)
* **Authentication:** JSON Web Tokens (JWT), HttpOnly Cookies

---

## 🚀 Getting Started

### Prerequisites

Ensure you have the following installed locally:
* [Node.js](https://nodejs.org/) (v18.x or higher)
* [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)
* [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) account (or a local MongoDB instance)
* [Google Gemini AI API Key](https://aistudio.google.com/)

---

### Installation & Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/ai-career-prep-engine.git
   cd ai-career-prep-engine
   ```

2. **Backend Setup:**
   ```bash
   cd backend
   npm install
   ```

   Create a `.env` file in the `backend/` root directory:
   ```env
   PORT=5000
   MONGO_URI=your_mongodb_connection_string
   JWT_SECRET=your_jwt_secret_key
   GEMINI_API_KEY=your_gemini_api_key
   CLIENT_URL=http://localhost:3000
   NODE_ENV=development
   ```

3. **Frontend Setup:**
   ```bash
   cd ../frontend
   npm install
   ```

   Create a `.env` file in the `frontend/` root directory:
   ```env
   REACT_APP_API_BASE_URL=http://localhost:5173/api
   ```

---

## 🏃 Running the Application

1. **Start the Express Server:**
   ```bash
   cd backend
   npm run dev
   ```

2. **Start the React Frontend:**
   ```bash
   cd frontend
   npm start
   ```

3. Open your browser and navigate to `http://localhost:5173`.

---

## 🛡 Security Highlights

* **Token Revocation:** Logout invalidates JWT tokens server-side using a database token blacklist check within the auth middleware.
* **XSS Neutralization:** Authentication tokens are kept completely out of `localStorage` / `sessionStorage`.
* **Input Validation:** Zod schemas validate both incoming API requests and outgoing LLM responses to prevent corrupted data propagation.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

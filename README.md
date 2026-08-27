# TaskFlow Hub 🚀
> A high-performance, full-stack collaborative project management platform built to optimize team workflows, task distribution, and productivity metrics.

TaskFlow Hub is an end-to-end, production-ready web application featuring robust authentication, secure route-level role management, data persistence, client/server validation, and fluid responsive views.

---

## 📑 Table of Contents
- [Project Links](#-project-links)
- [Project Overview](#-project-overview)
- [Tech Stack](#-tech-stack)
- [Key Features & MVP Requirements](#-key-features--mvp-requirements)
- [System Architecture](#%EF%B8%8F-system-architecture)
- [Case Study](#-case-study)
  - [The Problem](#1-the-problem)
  - [Technical Strategy](#2-technical-strategy)
  - [Engineering Challenge & Solution](#3-engineering-challenge--solution)
- [Local Installation & Setup](#-local-installation--setup)
- [Testing Suite](#-testing-suite)
- [Deployment](#-deployment)

---

## 🔗 Project Links

* **Live Demo Deployment:** 

---

## 💻 Project Overview
TaskFlow Hub solves the operational challenges teams face when organizing cross-functional projects. It offers an intuitive user interface structured across an isolated backend API layer and dynamic stateful interfaces.

---

## 🛠 Tech Stack

| Layer | Technologies Used |
| :--- | :--- |
| **Frontend** | React.js, Tailwind CSS, Axios, React Router v6 |
| **Backend** | Node.js, Express.js, JWT (JsonWebTokens), Bcrypt.js |
| **Database** | MongoDB (via Mongoose ODM) |
| **Deployment** | Vercel Serverless (Backend & Frontend Architecture) |
| **Testing** | Jest, Supertest, React Testing Library |

---

## ✨ Key Features & MVP Requirements

### 🛡️ 1. Authentication & Role-Based Permissions
* Secure sign-up/login processes fortified with client-side and server-side password checks.
* State retention via signed HTTP JSON Web Tokens (JWT).
* Tiered RBAC system (`Admin` can delete projects/reassign tasks, `Member` can update statuses and view assigned project scopes).

### 🗂️ 2. Core Full CRUD Resources
* **Projects Model:** Users can create, view list/detail modules, update titles/deadlines, and completely destroy project boards.
* **Tasks Model:** Granular sub-resource items mapped with status hooks (`Todo`, `In-Progress`, `Done`), assignment fields, and description updates.

### 🎨 3. UX UI System Requirements
* Form inputs validate live (e.g., matching emails, strong password check) before triggering server workloads.
* Explicit UI feedback configurations handling loading indicators, generic error notifications, and structured "Empty Slate" view helpers.

---

## ⚙️ System Architecture

The application separates concerns cleanly via modular architecture profiles:

```text
taskFlowBackend/
├── config/              # Database connection environments
├── middleware/          # JWT validation and RBAC checks
├── models/              # Mongoose DB structural schemas (User, Project, Task)
├── routes/              # Express isolated API routers
│   ├── authRoutes.js    # /api/auth endpoints (Login, Signup)
│   ├── projectRoutes.js # /api/projects endpoints (CRUD)
│   └── taskRoutes.js    # /api/tasks endpoints (Granular CRUD)
├── server.js            # Main Express server configuration
├── .gitignore           # Excludes local environments and node dependencies
├── vercel.json          # Deployment routing logic for serverless execution
└── package.json         # Server dependency graph
```

---

## 📝 Case Study

### 1. The Problem
Modern development teams frequently use disconnected tools that result in fragmented tracking. Light alternatives often omit role enforcement, allowing anyone to delete critical project foundations accidentally. TaskFlow Hub was conceived to combine absolute workflow tracking with granular access controls within a fast, zero-bloat platform.

### 2. Technical Strategy
* **Express & Node.js:** Selected due to non-blocking I/O properties, providing lightning-fast response times for multiple concurrent operational users.
* **MongoDB:** Document-store flexibility allows project components to store dynamic metadata without strict, expensive database migrations.
* **Tailwind CSS:** Provided utility-first layouts, keeping the build production sheet lightweight while achieving a high-end UI aesthetic.

### 3. Engineering Challenge & Solution
* **Challenge:** During initial testing, serverless functions on Vercel lost database connectivity state over multiple execution cycles, or crashed when initializing new database pooling handshakes per API call.
* **Solution:** A singleton connection lifecycle model was written into our database initialization layer. Instead of creating global client initializers everywhere, the database utility caches the active connection reference across lambdas, reusing it if open, or generating a single pipeline if closed.

---

## 🚀 Local Installation & Setup

### 1. Prerequisites
Make sure you have [Node.js](https://nodejs.org) (v16+ or higher) and [Git](https://git-scm.com) installed on your local computer.

### 2. Clone the Repository
```bash
git clone https://github.com.git
cd taskFlowBackend
```

### 3. Install Server Dependencies
```bash
npm install
```

### 4. Setup Environment Variables
Create a `.env` file in the root folder (mirroring the project view structural setup):
```env
PORT=5000
MONGODB_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/taskflow
JWT_SECRET=your_super_secure_jwt_random_secret_string
NODE_ENV=development
```

### 5. Start Application Locally
```bash
npm run dev
```
The gateway server starts running on [http://localhost:5000](http://localhost:5000).

---

## 🧪 Testing Suite
This system implements rigorous test coverage profiles checking end-to-end user lifecycles, unauthorized routing rejections, and correct CRUD transaction outputs.

To launch automated tests across the server suite:
```bash
# Execute full system suite
npm run test

# Run tests in observation/watch mode
npm run test:watch
```

---

## 📦 Deployment

### Backend Serverless Routing (`vercel.json`)
The application is configured to run smoothly as a standalone microservice collection via Vercel:
```json
{
  "version": 2,
  "builds": [
    {
      "src": "server.js",
      "use": "@vercel/node"
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "dest": "server.js"
    }
  ]
}
```

To run updates manually inside the production environment, log in to the Vercel CLI and execute:
```bash
vercel --prod
```

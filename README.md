# Full-Stack Multi Code IDE

A full-stack web-based multi-language code editor where users can sign up, log in, create projects, write and run code, and manage projects with a clean UI.

---

## Features

- **Authentication** – Signup / Login with JWT; protected routes for app and API
- **Projects** – Create, edit, delete, and list projects per user
- **Editor** – Monaco-based editor with language support, save (Ctrl+S), and run via Piston API
- **Languages** – Python, JavaScript, C, C++, Java, Bash (and Go in schema)
- **UI** – Tailwind CSS, modals, toasts, loading and error states

---

## Tech Stack

| Layer      | Technologies                          |
|-----------|----------------------------------------|
| Frontend  | React 18, Vite, React Router, Monaco Editor, Tailwind, React Toastify |
| Backend   | Node.js, Express, MongoDB, Mongoose, JWT, bcrypt |
| Run code  | External Piston API (emkc.org)         |

---

## Setup

### Prerequisites

- Node.js 18+
- MongoDB running locally (or set `MONGODB_URI`)

### Backend

```bash
cd backend
npm install
# Optional: copy .env.example to .env and set JWT_SECRET, MONGODB_URI for production
npm start
```

Runs at `http://localhost:3000` by default. Uses `config/env.js` for env vars; development has safe defaults.

### Frontend

```bash
cd frontend
npm install
# Optional: create .env with VITE_API_BASE_URL=http://localhost:3000 if backend is elsewhere
npm run dev
```

Runs at `http://localhost:5173` and talks to the backend API.

---

## Environment

- **Backend** – See `backend/.env.example`. Important: `JWT_SECRET` and `MONGODB_URI` in production.
- **Frontend** – See `frontend/.env.example`. `VITE_API_BASE_URL` must point to the backend (e.g. `http://localhost:3000`).

---

## Folder Structure

```
├── backend/
│   ├── config/          # env, db
│   ├── controllers/     # authController, projectController
│   ├── middleware/      # auth (JWT)
│   ├── models/         # User, Project
│   ├── routes/         # index, auth, projects
│   ├── utils/          # startupCode
│   └── app.js
├── frontend/
│   └── src/
│       ├── components/ # Navbar
│       ├── config/     # constants (API_BASE_URL)
│       ├── pages/      # Home, Editor, Login, SignUp, NoPage
│       ├── services/   # api (auth + projects client)
│       └── utils/      # language, projectImages
└── README.md
```

See [ARCHITECTURE.md](./ARCHITECTURE.md) for design and security notes.

---

## API Overview

| Method | Path               | Auth | Description        |
|--------|--------------------|------|--------------------|
| POST   | /api/auth/signup   | No   | Register           |
| POST   | /api/auth/login    | No   | Login, returns JWT |
| GET    | /api/projects      | Yes  | List my projects   |
| POST   | /api/projects      | Yes  | Create project     |
| GET    | /api/projects/:id  | Yes  | Get one project    |
| PUT    | /api/projects/:id  | Yes  | Save code          |
| PATCH  | /api/projects/:id  | Yes  | Rename project     |
| DELETE | /api/projects/:id  | Yes  | Delete project     |

Token can be sent in body (`token`), query (`?token=...`), or `Authorization: Bearer <token>`.

---

## License

MIT.

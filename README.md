Scalable Auth Dashboard (MERN)
A full‑stack web application built as part of the Frontend Developer Intern assignment. The project implements a scalable authentication system with JWT, a responsive dashboard, and a basic backend using Node.js and MongoDB.​

Features
User registration and login with JWT‑based authentication and hashed passwords (bcrypt).​

Protected routes on the frontend – dashboard and profile are accessible only when logged in.​

User profile fetching and updating via secure API endpoints.​

CRUD operations on a sample entity (Tasks) including create, list, search/filter, update, and delete.​

Responsive UI built with React, designed to work well on desktop and mobile screens.​

Clean project structure prepared for future scaling (modular routes, controllers, models, and context‑based state management).​

Tech Stack
Frontend

React (Vite)

React Router

Axios for API calls

CSS / utility classes for responsive layout (can be extended with Tailwind or Material UI)​

Backend

Node.js + Express

Project Structure

scalable-auth-dashboard-mern/
  backend/
    src/
      config/
      controllers/
      middlewares/
      models/
      routes/
      server.js
  frontend/
    src/
      pages/
      components/
      context/
      routes/
      services/
      main.jsx
      App.jsx

This separation makes it easy to extend either the frontend or backend independently while keeping responsibilities clear.​

Getting Started
Prerequisites
Node.js (LTS) and npm installed

MongoDB connection string (local or cloud, e.g. MongoDB Atlas)​

1. Backend setup

cd backend
npm install
Create a .env file inside backend/:

PORT=5000
MONGO_URI=your_mongo_connection_string
JWT_SECRET=super_strong_secret_here
CLIENT_URL=http://localhost:3000
Start the backend:

npm run dev
The API will be available at http://localhost:5000.​

2. Frontend setup
   
cd ../frontend
npm install
npm run dev
By default the frontend runs on http://localhost:3000.​

Update frontend/src/services/apiClient.js if you change the backend URL.

Usage
Open http://localhost:3000.

Register a new account on the Register page.

After successful registration/login, you are redirected to the Dashboard (JWT stored on the client).

On the Dashboard:

Create new tasks with title and description.

View your tasks list, search by keyword, and delete tasks.

Open the Profile page to view and update your user name.

Use the Logout button to clear the token and return to the login page.​

API Overview
Base URL: http://localhost:5000

Auth
POST /api/auth/register – Register new user; returns user info + JWT.​

POST /api/auth/login – Login existing user; returns user info + JWT.​

GET /api/auth/me – Get current user profile (requires Authorization: Bearer <token>).​

Profile
GET /api/profile – Fetch profile of logged‑in user.

PUT /api/profile – Update profile fields (currently name).​

Tasks
All task routes require a valid JWT and are scoped to the authenticated user.​

POST /api/tasks – Create a new task.

GET /api/tasks?search=&status= – List tasks, with optional search and status filter.

PUT /api/tasks/:id – Update a task owned by the user.

DELETE /api/tasks/:id – Delete a task owned by the user.

Postman Collection
A Postman collection is included in the repository under postman/ (if you export one, name it clearly, for example ScalableAuthDashboard.postman_collection.json). Import it into Postman to test all endpoints with the correct headers and example bodies.​

Scaling & Production Considerations
The assignment asks for a note on how this system would be scaled for production. Key improvements:​

Stronger auth flow

Use HttpOnly cookies for access/refresh tokens instead of localStorage, reducing XSS risk.​

Add refresh tokens with short‑lived access tokens and logout/blacklist mechanism.

Security hardening

Enable CORS only for trusted frontend domains.

Add rate limiting, request size limits, and production logging.​

Architecture & performance

Split backend into service and repository layers so business logic is not tied to controllers, making it easier to add new modules like analytics or roles.​

Containerize services with Docker and deploy using a process manager or orchestrator (e.g., PM2 + Nginx, or Kubernetes) for horizontal scaling.​

Use environment‑specific configs (dev/stage/prod) and managed MongoDB (Atlas) with proper indexing on user and task queries.

Frontend scalability

Introduce UI component library and design system to keep consistent UX as the app grows.

Use a dedicated state management (Context is already used; can scale to Zustand/Redux for more complex dashboards).

dotenv, cors, morgan for configuration and logging​


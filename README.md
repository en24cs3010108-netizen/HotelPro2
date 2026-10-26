# HotelPro — Hotel Management System

A full-stack hotel booking and management application built with React + Vite, Express, MongoDB, Mongoose, and JWT authentication. The project includes customer registration/login, room browsing, booking creation and cancellation, and an admin dashboard for bookings, rooms, and users.

## Project structure

```text
HotelPro/
├── client/                 # React + Vite frontend
│   ├── src/
│   │   ├── App.jsx         # Pages, routing, customer/admin interfaces
│   │   ├── api.js          # Axios client and JWT header
│   │   └── styles.css      # Responsive styling
│   ├── .env.example
│   └── package.json
└── server/                 # Express + MongoDB backend
    ├── models/             # User, Room, Booking schemas
    ├── routes/             # Auth, room, booking, admin API routes
    ├── middleware.js       # JWT authentication and admin authorization
    ├── index.js
    ├── .env.example
    └── package.json
```

## Requirements

- Node.js 18 or later
- MongoDB running locally, or a MongoDB connection string

## Run the backend

Open a terminal:

```bash
cd server
npm install
```

Copy `.env.example` to `.env` and set your environment variables:

```env
PORT=8001
MONGO_URI=mongodb://localhost:27017/hotel
JWT_SECRET=replace_this_with_a_long_random_secret
```

Start the backend:

```bash
npm run dev
```

Backend URL: `http://localhost:8001`
Health check: `http://localhost:8001/api/health`

## Run the frontend

Open a second terminal:

```bash
cd client
npm install
```

Optionally copy `.env.example` to `.env`:

```env
VITE_API_URL=http://localhost:8001/api
```

Start Vite:

```bash
npm run dev
```

Frontend URL: `http://localhost:5173`

## Main routes

- `/` — Home page and room browsing
- `/signup` — Create a customer or admin account
- `/login` — Login
- `/bookings` — Customer booking and cancellation page (login required)
- `/admin` — Admin dashboard (admin login required)

## API routes

- `POST /api/auth/signup`
- `POST /api/auth/login`
- `GET /api/auth/me`
- `GET /api/rooms`
- `POST /api/rooms` (admin)
- `DELETE /api/rooms/:id` (admin)
- `POST /api/bookings` (login required)
- `GET /api/bookings/mine` (login required)
- `PATCH /api/bookings/:id/cancel` (booking owner)
- `GET /api/bookings` (admin)
- `GET /api/admin/users` (admin)

## Important setup notes

- The database name in the project execution instructions is `hotel`; it is the default used by this implementation.
- The frontend supports the documented Ordinary/Customer and Admin roles. For a public deployment, restrict admin account creation to trusted operators rather than exposing admin self-registration.
- Booking payment is currently a **demo flow**, not a real payment integration. Connect a PCI-compliant payment provider before accepting real card payments. Do not store raw card numbers or CVV values in your own database.
- Use a strong, private `JWT_SECRET` in `.env`; do not commit `.env` to source control.
- Room photos can be entered as image URLs by an admin. The home page includes fallback imagery until rooms are added to MongoDB.

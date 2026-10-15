# CraveLoop

> A reels-based food discovery platform. Scroll through short food videos, like and save dishes you love, and explore restaurant storefronts from food partners.

![React](https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-7-646CFF?logo=vite&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-Express_5-339933?logo=node.js&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-Mongoose-47A248?logo=mongodb&logoColor=white)
![ImageKit](https://img.shields.io/badge/ImageKit-Video_Storage-0E7CF4)

---

## ✨ Features

- **Reels feed**: a vertical, swipeable video feed. Each video autoplays when it's on screen and pauses when you scroll away.
- **Two user roles**: separate sign-up and login for **Users** and **Food Partners** (restaurants).
- **Food partner storefronts**: each partner has a profile page with their details and all their food videos.
- **Video uploads**: food partners upload dish videos with a name and description. Videos are stored on ImageKit.
- **Likes and saves**: like or bookmark dishes, and view everything you've saved on one page.
- **Authentication**: JWT in HTTP-only cookies, with passwords hashed using bcrypt.

## 🛠 Tech Stack

| Layer    | Tech |
|----------|------|
| Frontend | React 19, Vite, React Router 7, Axios |
| Backend  | Node.js, Express 5, Multer |
| Database | MongoDB + Mongoose |
| Storage  | ImageKit (video hosting) |
| Auth     | JWT, bcryptjs, cookie-parser |

## 📁 Project Structure

```
.
├── backend/
│   ├── server.js                  # Entry point (port 3000)
│   └── src/
│       ├── app.js                 # Express app, CORS, routes
│       ├── db/db.js               # MongoDB connection
│       ├── controllers/           # auth, food, food-partner
│       ├── middlewares/           # JWT auth for users and food partners
│       ├── models/                # User, FoodPartner, Food, Like, Save
│       ├── routes/                # /api/auth, /api/food, /api/food-partner
│       └── services/              # ImageKit upload service
└── frontend/
    └── src/
        ├── components/            # ReelFeed, BottomNav
        ├── pages/auth/            # User and food partner login/register
        ├── pages/general/         # Home feed, Saved
        ├── pages/food-partner/    # Profile, Create food
        └── routes/                # App routes
```

## 🚀 Getting Started

### Prerequisites

- Node.js 18+
- A MongoDB database (local or [MongoDB Atlas](https://www.mongodb.com/atlas))
- A free [ImageKit](https://imagekit.io/) account for video storage

### 1. Clone the repo

```bash
git clone https://github.com/<your-username>/craveloop.git
cd craveloop
```

### 2. Backend

```bash
cd backend
npm install
cp .env.example .env   # then fill in your values
node server.js
```

The API runs at `http://localhost:3000`.

### 3. Frontend

```bash
cd frontend
npm install
npm run dev
```

The app runs at `http://localhost:5173`.

## 🔐 Environment Variables (`backend/.env`)

| Variable                | Description |
|-------------------------|-------------|
| `MONGODB_URI`           | MongoDB connection string |
| `JWT_SECRET`            | Any long random string, used to sign JWTs |
| `IMAGEKIT_PUBLIC_KEY`   | ImageKit public key |
| `IMAGEKIT_PRIVATE_KEY`  | ImageKit private key |
| `IMAGEKIT_URL_ENDPOINT` | ImageKit URL endpoint |

## 📡 API Reference

### Auth: `/api/auth`

| Method | Endpoint                   | Description |
|--------|----------------------------|-------------|
| POST   | `/user/register`           | Register a user |
| POST   | `/user/login`              | Log in a user |
| GET    | `/user/logout`             | Log out a user |
| POST   | `/food-partner/register`   | Register a food partner |
| POST   | `/food-partner/login`      | Log in a food partner |
| GET    | `/food-partner/logout`     | Log out a food partner |

### Food: `/api/food`

| Method | Endpoint | Access       | Description |
|--------|----------|--------------|-------------|
| POST   | `/`      | Food partner | Upload a food video (multipart) |
| GET    | `/`      | User         | Get the reels feed |
| POST   | `/like`  | User         | Like or unlike a food item |
| POST   | `/save`  | User         | Save or unsave a food item |
| GET    | `/save`  | User         | Get the user's saved items |

### Food Partner: `/api/food-partner`

| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| GET    | `/:id`   | User   | Get a partner's profile and videos |

## 🗺 Roadmap

- [ ] Infinite scroll with cursor-based pagination
- [ ] Comments on reels
- [ ] Unique indexes to prevent duplicate likes and saves, plus a "liked by me" state
- [ ] Request validation, upload size/type limits and rate limiting
- [ ] Nearby restaurants using geospatial search
- [ ] Partner analytics dashboard
- [ ] Deploy with a live demo

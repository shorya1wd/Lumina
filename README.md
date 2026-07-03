# Lumina 🎥

Welcome to the Lumina workspace. This project is divided into a separate frontend and backend to ensure clean architecture and independent deployment pipelines.

👉 **[View Frontend Repository](https://github.com/shorya1wd/lumina-fronted)** (React 19, Vite, Tailwind CSS)
👉 **[View Backend Repository](https://github.com/shorya1wd/lumina-backend)** (Node.js, Express, MongoDB)

Lumina is a full-stack, modern video-sharing application inspired by YouTube. It empowers users to upload videos, create playlists, subscribe to channels, like and comment on videos, and securely manage their own content. 

This repository is organized as a monorepo consisting of two primary components:
- **Lumina-backend**: A robust Node.js/Express REST API serving as the backbone.
- **Lumina-frontend**: A sleek, dynamic React single-page application built with Vite and Tailwind CSS.

## 🚀 Features

- **User Authentication**: Secure JWT-based authentication (Access & Refresh tokens) using HTTP-only cookies.
- **Video Management**: Users can upload, publish, and manage videos, along with custom thumbnails.
- **Social Interactions**: Users can subscribe to channels, like videos, and leave comments on videos or tweets.
- **Playlists**: Organize videos into custom playlists.
- **Watch History**: Keep track of recently watched videos.
- **Cloud Storage**: Seamless integration with Cloudinary for scalable image and video storage.
- **Optimized Data Retrieval**: Advanced MongoDB aggregation pipelines for performant querying of videos, subscriptions, and watch history.

## 🛠 Tech Stack

### Backend (`Lumina-backend`)
- **Runtime**: Node.js
- **Framework**: Express.js (v5)
- **Database**: MongoDB with Mongoose ODM
- **Authentication**: JWT & bcrypt for password hashing
- **File Uploads**: Multer & Cloudinary
- **Logging**: Winston & Morgan

### Frontend (`Lumina-frontend`)
- **Framework**: React.js with Vite
- **Routing**: React Router DOM
- **Styling**: Tailwind CSS
- **API Client**: Axios (with centralized interceptors for automatic token refresh)

## 📁 Project Structure

```text
Lumina-Workspace/
├── Lumina-backend/         # Express server & API routes
│   ├── src/
│   │   ├── controllers/    # Request handlers (user, video, likes, etc.)
│   │   ├── models/         # Mongoose schemas
│   │   ├── routes/         # Express route definitions
│   │   ├── middlewares/    # Custom middlewares (auth, multer, errors)
│   │   └── utils/          # Cloudinary config, API Error/Response handlers
│   └── .env                # Backend environment variables
│
└── Lumina-frontend/        # React Application
    ├── src/
    │   ├── api/            # Axios instance and API integrations
    │   ├── components/     # Reusable UI components (Player, Modals, Layout)
    │   ├── context/        # React Context (AuthContext)
    │   ├── pages/          # Top-level route components (Home, Login, Channel)
    │   └── utils/          # Helper functions
    └── vite.config.js      # Vite build configuration (Production optimized)
```

## ⚙️ Getting Started

### Prerequisites
- Node.js (v18+)
- MongoDB connection string
- Cloudinary Account (for image/video hosting)

### 1. Setup Backend
```bash
cd Lumina-backend
npm install
```
Create a `.env` file in the backend directory:
```env
PORT=3000
MONGODB_URI=your_mongodb_connection_string
CORS_ORIGIN=http://localhost:5173

ACCESS_TOKEN_SECRET=your_access_secret
ACCESS_TOKEN_EXPIRY=1d
REFRESH_TOKEN_SECRET=your_refresh_secret
REFRESH_TOKEN_EXPIRY=10d

CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
NODE_ENV=development
```
Run the development server:
```bash
npm run dev
```

### 2. Setup Frontend
```bash
cd ../Lumina-frontend
npm install
```
Create a `.env` file in the frontend directory:
```env
VITE_API_BASE_URL=http://localhost:3000/api/v1
```
Start the Vite development server:
```bash
npm run dev
```

## 🔐 Production Notes
- **Console Logs**: The Vite frontend is configured via `esbuild` in `vite.config.js` to automatically drop all `console.log` and `debugger` statements during the production build (`npm run build`). You do not need to manually remove logs before deploying.
- **Cookies**: Cross-origin cookies are properly configured for production (`secure: true` and `SameSite='none'`). Ensure your production backend is served over HTTPS to allow successful token exchanges.

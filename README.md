# TalentBridge 💼

**Full-Stack Job Portal**

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat&logo=react&logoColor=black)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat&logo=tailwindcss&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=node.js&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat&logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat&logo=mongodb&logoColor=white)
![Clerk](https://img.shields.io/badge/Clerk-6C47FF?style=flat&logo=clerk&logoColor=white)
![Cloudinary](https://img.shields.io/badge/Cloudinary-3448C5?style=flat&logo=cloudinary&logoColor=white)

TalentBridge is a full-stack recruitment platform that connects job seekers and recruiters through a streamlined hiring experience. Candidates can discover opportunities, apply for jobs, and track their applications, while recruiters manage job postings and review applicants from a centralized dashboard — with role-based, end-to-end workflows for both sides of the hiring process.

## 🚀 Live Demo

- **App:** https://talent-bridge-portal.vercel.app
- **Repository:** https://github.com/ashoksamota0/TalentBridge

> The backend is deployed on Render, so the first request after inactivity may take a few seconds while the server wakes up.

## ✨ Key Features

### 👤 Candidate Features
- Secure authentication with Clerk
- Browse and search job listings with filtering
- Apply for jobs directly through the platform
- Upload resumes and supporting documents (stored via Cloudinary)
- Track real-time application status

### 🧑‍💼 Recruiter Features
- Dedicated recruiter dashboard
- Create, edit, and manage job postings
- View and review candidate applications and profiles
- Manage the hiring workflow end-to-end
- Company/media asset uploads via Cloudinary

## 🛠️ Tech Stack

**Frontend:** React.js · Tailwind CSS

**Backend:** Node.js · Express.js

**Database:** MongoDB

**Authentication & Cloud Services:** Clerk · Cloudinary

**Deployment:** Vercel (frontend) · Render (backend)

## 🏗️ Architecture

```
Browser (React + Tailwind CSS)
   │
   ▼
Express Backend ──► Clerk Auth (role-based: candidate / recruiter)
   │
   ├──► MongoDB (jobs, applications, users)
   └──► Cloudinary (resumes & company assets)
```

- RESTful APIs covering job management, applications, status tracking, search, filtering, and pagination
- Role-based access control — separate candidate and recruiter permissions
- Secure authentication and authorization via Clerk
- Cloud-based file storage for resumes and company assets via Cloudinary

## ⚙️ Getting Started

### Prerequisites
- Node.js & npm
- A MongoDB database (e.g. [MongoDB Atlas](https://www.mongodb.com/atlas))
- A Clerk account (for auth keys)
- A Cloudinary account (for file storage keys)

### 1. Clone the repo
```bash
git clone https://github.com/ashoksamota0/TalentBridge.git
cd TalentBridge
```

### 2. Start the backend server (do this first)
```bash
cd server
npm install
```
Create a `.env` file in `server/`:
```
PORT=5000
MONGODB_URI=your_mongodb_connection_string
CLERK_SECRET_KEY=your_clerk_secret_key
CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret
```
Start it:
```bash
npm start
```
> **Keep this terminal running** — the frontend needs the backend API to be live.

### 3. Start the frontend (in a new terminal)
From the project root:
```bash
cd client
npm install
```
Create a `.env` file in `client/`:
```
VITE_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
VITE_API_URL=your_backend_url
```
Start it:
```bash
npm run dev
```

App will be live at `http://localhost:5173`.

*(Match the `.env` keys above to whatever's actually in your `server`/`client` config if they differ.)*

## 📁 Project Structure

```
TalentBridge/
├── client/     # React + Tailwind CSS frontend
└── server/     # Node.js + Express backend
```

## 👤 Author

**Ashok Kumar** — Full-Stack Web Developer

- GitHub: [@ashoksamota0](https://github.com/ashoksamota0)
- LinkedIn: [ashok~kumar](https://www.linkedin.com/in/ashok~kumar/)

## 📄 License

This project is intended for portfolio and educational purposes.

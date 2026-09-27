# NeuralForge AI 🤖

**Full-Stack AI SaaS Platform**

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat&logo=react&logoColor=black)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat&logo=tailwindcss&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=node.js&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat&logo=express&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat&logo=postgresql&logoColor=white)
![Clerk](https://img.shields.io/badge/Clerk-6C47FF?style=flat&logo=clerk&logoColor=white)
![Google Gemini](https://img.shields.io/badge/Google_Gemini-886FBF?style=flat&logo=googlegemini&logoColor=white)
![Cloudinary](https://img.shields.io/badge/Cloudinary-3448C5?style=flat&logo=cloudinary&logoColor=white)
[![ClipDrop](https://img.shields.io/badge/Clipdrop-000000?style=flat&logoColor=white)](https://clipdrop.co/)

NeuralForge AI is a full-stack AI-powered creative platform that brings six AI tools — article writing, blog titles, image generation, background/object removal, and resume review — together behind secure authentication, a Free/Premium SaaS model, and a community feed for sharing AI-generated content.

## 🚀 Live Demo

- **Live App:** https://neuralforge-ai-web.vercel.app
- **Backend API:** https://neuralforge-ai-saas.onrender.com

## ✨ Key Features

### 🤖 AI-Powered Tools

| Tool | What it does | Powered by |
|---|---|---|
| 📝 AI Article Writer | Generates complete articles from a topic/prompt | Google Gemini |
| #️⃣ Blog Title Generator | Generates creative blog title ideas | Google Gemini |
| 🎨 AI Image Generator | Creates images from text prompts | ClipDrop + Cloudinary |
| 🖼️ Background Removal | Removes the background from an uploaded image | Cloudinary AI |
| ✂️ Object Removal | Removes unwanted objects from an image | Cloudinary Generative AI |
| 📄 Resume Reviewer | Analyzes a resume and gives improvement suggestions | Google Gemini |

### 💎 Free & Premium Plans

| Feature | Free | Premium |
|---|---|---|
| Price | ₹0 / forever | ₹499 (one-time) |
| AI Article Writer | Limited | Unlimited |
| Blog Title Generator | — | Unlimited |
| AI Image Generation | Limited | Unlimited |
| Background Removal | Limited | Unlimited |
| Object Removal | Limited | Unlimited |
| Resume Reviewer | Limited | Unlimited |
| Community Access | ✓ | ✓ |

### 🔍 More Under the Hood

> 👉 **Each category below is expandable — click on one to see its full feature list.**

<details>
<summary><strong>🔐 Authentication & Access Control</strong> &nbsp;<kbd>View details</kbd></summary>

- User registration and login handled by Clerk
- Secure session management
- Protected application routes and API endpoints
- Authentication middleware guards every protected API
- Authenticated user's identity and plan available on the backend
- Server-side Premium validation — the backend checks the user's subscription plan before allowing premium operations, so frontend restrictions can't be bypassed

</details>

<details>
<summary><strong>👥 Community</strong> &nbsp;<kbd>View details</kbd></summary>

- Publish AI-generated content to a shared community feed
- View and interact with other users' published content
- PostgreSQL-backed community data
- Authenticated, user-associated community interactions

</details>

<details>
<summary><strong>🎨 UI & User Experience</strong> &nbsp;<kbd>View details</kbd></summary>

- Modern responsive landing page — hero section, AI tool showcase, testimonials, pricing, CTAs
- Responsive navigation with a mobile menu
- Dedicated About, Contact, Privacy Policy, and FAQ pages
- FAQ uses an interactive accordion interface
- Pricing page with Free/Premium comparison and upgrade flow
- Premium-feature indicators throughout the UI
- Toast notifications and loading states for async actions (AI generation, image processing, etc.)
- Responsive layouts for desktop, tablet, and mobile

</details>

<details>
<summary><strong>🗄️ Backend, Database & Security</strong> &nbsp;<kbd>View details</kbd></summary>

- React frontend talks to the Node.js/Express backend over REST APIs (Axios)
- PostgreSQL (hosted on Neon) stores users, generated content, and community data
- CORS configuration and environment-variable-based secrets
- API keys for Gemini, ClipDrop, Cloudinary, and Clerk are kept backend-only, never exposed to the frontend
- Clear separation between frontend and backend responsibilities

</details>

## 🛠️ Tech Stack

**Frontend:** React · Vite · Tailwind CSS · React Router · Axios · Clerk React · Lucide React · React Hot Toast

**Backend:** Node.js · Express.js · Clerk Express · PostgreSQL · CORS · dotenv

**AI & Cloud Services:** Google Gemini AI · ClipDrop API · Cloudinary

**Database:** PostgreSQL (Neon)

**Deployment:** Vercel (frontend) · Render (backend) · Neon (database) · Cloudinary (media) · Clerk (auth)

## 🏗️ Architecture

```
Browser (React + Vite)
   │
   ▼
Express Backend ──► Clerk Auth
   │
   ├──► PostgreSQL (Neon)
   └──► AI / Cloud APIs (Gemini · ClipDrop · Cloudinary)
```

## ⚙️ Getting Started

### Prerequisites
- Node.js & npm
- A PostgreSQL database (e.g. [Neon](https://neon.tech))
- Clerk account (auth keys)
- Google Gemini API key
- Cloudinary account (cloud name, API key, API secret)
- ClipDrop API key

### 1. Clone the repo
```bash
git clone https://github.com/ashoksamota0/NeuralForge-AI-SaaS.git
cd NeuralForge-AI-SaaS
```

### 2. Start the backend server (do this first)
```bash
cd server
npm install
```
Create a `.env` file in `server/`:
```
PORT=3000
DATABASE_URL=your_neon_postgresql_url
CLERK_SECRET_KEY=your_clerk_secret_key
GEMINI_API_KEY=your_gemini_api_key
CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret
CLIPDROP_API_KEY=your_clipdrop_api_key
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

## 📁 Project Structure

```
NeuralForge-AI-SaaS/
├── client/
│   ├── components/
│   ├── pages/
│   ├── assets/
│   ├── App.jsx
│   └── main.jsx
└── server/
    ├── configs/
    ├── controllers/
    ├── middlewares/
    ├── routes/
    └── server.js
```

## 👤 Author

**Ashok Kumar** — Full-Stack Web Developer

- GitHub: [@ashoksamota0](https://github.com/ashoksamota0)
- LinkedIn: [ashok~kumar](https://www.linkedin.com/in/ashok~kumar/)

## 📄 License

This project is intended for portfolio and educational purposes.

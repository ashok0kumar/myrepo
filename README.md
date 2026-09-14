# VoxMeet

### Real-Time Video Calling Platform

VoxMeet is a full-stack real-time video conferencing platform that enables users to create and join online meetings with live video/audio communication, screen sharing, real-time chat, participant management, and meeting history.

The application is built using **React, Node.js, Express, PostgreSQL, WebRTC, Socket.io, Clerk, and Razorpay**, with a production-style client/server architecture and cloud deployment.

---

## 🚀 Live Demo

**Live Application:**  
https://voxmeet-video.vercel.app

**Backend API:**  
https://voxmeet-j3xe.onrender.com

> Note: The backend is deployed on Render's free tier, so the first request after inactivity may take some time while the server wakes up.

---

## 📌 Project Overview

VoxMeet is designed as a modern browser-based video meeting platform.

Users can:

- Create instant video meetings
- Join meetings using a unique meeting ID
- Communicate through real-time video and audio
- Share their screen
- Send messages through real-time meeting chat
- View participants currently in a meeting
- Manage microphone and camera state
- View previous meeting sessions
- Review participant information and chat history
- Authenticate securely using Clerk
- Upgrade from the Free plan to Premium using Razorpay
- Access increased meeting limits with Premium

The project focuses on implementing the core functionality behind a real-time communication application rather than simply building a static video meeting UI.

---

# ✨ Key Features

## 🎥 Real-Time Video & Audio

VoxMeet uses **WebRTC** to establish peer-to-peer media connections between participants.

Users can:

- Enable/disable microphone
- Enable/disable camera
- See their own video stream
- See remote participants
- Join and leave meetings in real time

The application dynamically manages WebRTC peer connections as participants enter or leave a meeting.

---

## 🖥️ Screen Sharing

VoxMeet supports browser-based screen sharing using the **MediaDevices Screen Capture API**.

Users can share:

- Entire screen
- Application window
- Browser tab

The implementation replaces the current video track in the existing WebRTC connection instead of creating a completely separate meeting connection.

When screen sharing stops, the application automatically restores the user's camera stream.

### Screen Sharing Flow

```text
User clicks "Share Screen"
          ↓
getDisplayMedia()
          ↓
Screen video track created
          ↓
Existing WebRTC video sender found
          ↓
replaceTrack(screenTrack)
          ↓
Remote participants receive screen
          ↓
User stops sharing
          ↓
Camera track restored

The application also handles the browser's native "Stop Sharing" action.

💬 Real-Time Meeting Chat

VoxMeet includes real-time meeting chat powered by Socket.io.

Users can:

Send messages during meetings
Receive messages instantly
See sender information
See message timestamps
Track unread messages
Open/close the chat panel

The chat state is synchronized through the Socket.io server.

👥 Participant Management

Participants are displayed dynamically inside the meeting room.

The participant panel provides information such as:

Participant name
Microphone status
Camera status
Meeting host
Current participant count

Participant state changes are propagated through Socket.io events.

🎛️ Meeting Controls

The meeting control bar provides:

🎤 Microphone toggle
📹 Camera toggle
🖥️ Screen sharing
💬 Chat
👥 Participant list
🔗 Meeting ID copy
📞 Leave meeting
🛑 End meeting for everyone

The controls are designed to remain accessible across desktop and smaller screen sizes.

🔐 Authentication

Authentication is implemented using Clerk.

VoxMeet supports:

Email-based authentication
Google authentication
Secure authenticated sessions
Protected meeting routes
User profile information
User account controls

The frontend obtains an authentication token from Clerk and sends it to protected backend APIs using the Authorization header.

Authentication Flow
User
 ↓
Clerk Authentication
 ↓
Authenticated Session
 ↓
Clerk Access Token
 ↓
React Frontend
 ↓
Authorization: Bearer <token>
 ↓
Express Authentication Middleware
 ↓
Authenticated API Request

The backend verifies the authenticated user before allowing access to protected resources.

💳 Premium Plan & Razorpay

VoxMeet includes a Free and Premium plan.

Free Plan
₹0 / forever
150 meetings per month
Up to 10 participants per meeting
Real-time video & audio
Real-time chat
Screen sharing
Meeting history
Premium Plan
₹499 / forever
Unlimited meetings
Up to 100 participants per meeting
Real-time video & audio
Real-time chat
Screen sharing
Meeting history
Priority access to new features
Payment Implementation

Premium payments are integrated using Razorpay.

The current implementation uses a one-time payment model rather than a recurring subscription.

Payment Flow
User clicks "Upgrade to Premium"
             ↓
Frontend requests order from backend
             ↓
Express creates Razorpay order
             ↓
Razorpay Checkout opens
             ↓
User completes payment
             ↓
Razorpay returns payment details
             ↓
Frontend sends payment details to backend
             ↓
Backend verifies Razorpay signature
             ↓
Backend validates order ownership/details
             ↓
User plan updated to "premium"
             ↓
Premium features unlocked

The Razorpay secret key is kept exclusively on the backend and is never exposed to the frontend.

The deployed demo uses Razorpay Test Mode for demonstration purposes.

📊 Usage Limits

The application implements plan-based meeting limits.

Free Users
Maximum meetings/month: 150
Maximum participants/meeting: 10
Premium Users
Meetings/month: Unlimited
Maximum participants/meeting: 100

Meeting usage is calculated on the backend rather than relying only on frontend checks.

This prevents users from bypassing the usage restriction simply by modifying client-side code.

🗄️ Database Architecture

VoxMeet uses PostgreSQL hosted on Neon.

The database contains the following core entities:

Users

Stores application user information and plan status.

users
├── id
├── name
├── email
├── image
├── plan
├── created_at
└── updated_at
Meetings

Stores meeting information.

meetings
├── id
├── meeting_id
├── title
├── host_id
├── status
├── ended_at
├── created_at
└── updated_at
Meeting Participants

Stores participant activity for each meeting.

meeting_participants
├── id
├── meeting_id
├── user_id
├── name
├── joined_at
└── left_at
Meeting Messages

Stores meeting chat history.

meeting_messages
├── id
├── meeting_id
├── sender_id
├── sender_name
├── text
└── timestamp
Relationships
users
  │
  ├───────────────┐
  │               │
  ▼               ▼
meetings     meeting_participants
  │
  ▼
meeting_messages

Foreign keys are used to maintain relationships between users, meetings, participants, and messages.

Meeting-related records are configured with cascading behavior where appropriate so that dependent records can be cleaned up when a meeting is removed.

⚡ Real-Time Architecture

VoxMeet uses WebRTC + Socket.io together, with each technology responsible for a different part of the system.

WebRTC

WebRTC handles the actual real-time media communication:

Camera
Microphone
Screen sharing
Peer-to-peer media streams
Socket.io

Socket.io handles signaling and real-time application events:

Joining a room
New participant notifications
WebRTC offers
WebRTC answers
ICE candidates
Audio state changes
Video state changes
Screen sharing state
Real-time chat
Participant updates
Meeting termination
Overall Communication Architecture
                    VoxMeet Client
                         │
              ┌──────────┴──────────┐
              │                     │
              ▼                     ▼
          REST APIs             Socket.io
              │                     │
              ▼                     ▼
       Express Backend       Signaling Server
              │
              ▼
         PostgreSQL
           (Neon)

              WebRTC
                 │
        ┌────────┼────────┐
        ▼        ▼        ▼
   Participant Participant Participant
        A          B          C

The backend does not carry the actual video stream. WebRTC handles media communication between participants, while Socket.io is responsible for coordination and signaling.

🔄 WebRTC Connection Flow

When a participant enters a meeting:

1. User opens meeting URL
              ↓
2. Backend validates meeting
              ↓
3. Local camera/microphone initialized
              ↓
4. Socket connects to meeting room
              ↓
5. Existing participants are received
              ↓
6. WebRTC peer connections are created
              ↓
7. SDP Offer generated
              ↓
8. Offer sent through Socket.io
              ↓
9. Remote participant creates SDP Answer
              ↓
10. ICE candidates exchanged
              ↓
11. Peer-to-peer connection established
              ↓
12. Remote video/audio displayed

This architecture separates:

Signaling
Media transport
Application data
Persistent database data

which makes the system easier to reason about and extend.

🧠 Application Architecture

The project follows a separate frontend/backend structure.

VoxMeet
│
├── client/
│   ├── public/
│   └── src/
│       ├── assets/
│       ├── components/
│       │   ├── meeting/
│       │   └── sessions/
│       ├── config/
│       ├── hooks/
│       ├── pages/
│       ├── App.jsx
│       ├── index.css
│       └── main.jsx
│
└── server/
    ├── config/
    ├── controllers/
    ├── middleware/
    ├── routes/
    ├── server.js
    └── socket.js
🎨 Frontend

The frontend is built using:

React
Vite
Tailwind CSS
React Router
Clerk React
Axios
Socket.io Client
Lucide React
React Hot Toast
Main Pages
/login
/register
/dashboard
/sessions
/features
/pricing
/about
/contact
/privacy
/meeting/:meetingId
Important Frontend Components
components/
│
├── Navbar
├── Footer
├── Loader
├── ProtectedRoute
├── Protectedlayout
│
├── meeting/
│   ├── ChatPanel
│   ├── ControlBar
│   ├── ParticipantList
│   ├── VideoGrid
│   └── VideoTile
│
└── sessions/
    ├── EmptySessions
    ├── SessionCard
    ├── SessionChatTab
    ├── SessionDetailModal
    └── SessionParticipantsTab
🧩 Custom React Hooks

The project uses custom hooks to keep complex real-time logic separate from UI components.

useWebRTC

Responsible for:

Local media stream
Remote participants
Peer connections
WebRTC signaling
Microphone state
Camera state
Screen sharing
Connection cleanup

This prevents the meeting UI from becoming tightly coupled with WebRTC implementation details.

useChat

Responsible for:

Receiving chat messages
Sending messages
Chat open/close state
Unread message count
Socket event listeners
Message cleanup

This keeps chat functionality isolated from the meeting layout.

🔌 Backend API

The backend is built using:

Node.js
Express
PostgreSQL
Neon
Clerk Express
Socket.io
Razorpay
CORS
Cookie Parser
dotenv
Meeting APIs
Method	Endpoint	Purpose
POST	/api/meetings	Create a meeting
GET	/api/meetings/stats	Get meeting usage and plan statistics
GET	/api/meetings/sessions	Get user's meeting history
GET	/api/meetings/sessions/:id	Get meeting session details
GET	/api/meetings/:meetingId	Get meeting information
Payment APIs
Method	Endpoint	Purpose
POST	/api/payments/create-order	Create Razorpay Premium order
POST	/api/payments/verify	Verify payment and activate Premium

Protected endpoints require an authenticated Clerk user.

🔐 Backend Security

Several security practices are implemented in the backend.

Authentication Middleware

Protected routes use authentication middleware before accessing user-specific data.

Server-Side Authorization

Important operations are validated on the backend.

For example:

Meeting creation limits are checked server-side.
Premium status is retrieved from PostgreSQL.
Meeting host permissions are checked server-side.
Payment signatures are verified on the server.
Razorpay secret keys are never exposed to the frontend.
Environment Variables

Sensitive configuration is stored in environment variables.

Example:

DATABASE_URL=your_database_url

CLERK_PUBLISHABLE_KEY=your_publishable_key
CLERK_SECRET_KEY=your_secret_key
CLERK_WEBHOOK_SIGNING_SECRET=your_webhook_secret

RAZORPAY_KEY_ID=your_razorpay_key
RAZORPAY_KEY_SECRET=your_razorpay_secret

ORIGINS=http://localhost:5173

Never commit .env files or API secrets to GitHub.

🔔 Clerk Webhooks

VoxMeet uses Clerk webhooks to synchronize authenticated users with the PostgreSQL database.

Relevant user events include:

user.created
user.updated

The webhook endpoint is:

POST /api/clerk

When a user is created or updated in Clerk, the backend synchronizes the relevant user information with the users table.

This allows the application to maintain its own application-level user record while Clerk remains responsible for authentication.

🌐 Deployment

VoxMeet is deployed using separate frontend and backend services.

Frontend

Platform: Vercel

React + Vite
       ↓
Vercel
       ↓
https://voxmeet-video.vercel.app

The Vercel deployment is configured to support React Router's client-side routes using a SPA rewrite.

Backend

Platform: Render

Node.js + Express
       ↓
Render
       ↓
https://voxmeet-j3xe.onrender.com
Database

Platform: Neon

PostgreSQL
    ↓
Neon
    ↓
VoxMeet database
Authentication

Platform: Clerk

Clerk
 ↓
Authentication
 ↓
User identity
 ↓
VoxMeet backend
Payments

Platform: Razorpay

The deployed demo uses Razorpay Test Mode.

🛠️ Local Development Setup
1. Clone the Repository
git clone <your-github-repository-url>
cd VoxMeet
2. Install Frontend Dependencies
cd client
npm install
3. Install Backend Dependencies

Open another terminal:

cd server
npm install
🔑 Environment Variables
Client

Create:

client/.env

Example:

VITE_BASE_URL=http://localhost:3000
VITE_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
Server

Create:

server/.env

Example:

PORT=3000

ORIGINS=http://localhost:5173

DATABASE_URL=your_neon_database_url

CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
CLERK_SECRET_KEY=your_clerk_secret_key
CLERK_WEBHOOK_SIGNING_SECRET=your_clerk_webhook_signing_secret

RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret

Do not commit these files to GitHub.

▶️ Run the Application
Start Backend

From the server directory:

npm run dev

Backend:

http://localhost:3000
Start Frontend

From the client directory:

npm run dev

Frontend:

http://localhost:5173
🧪 Testing the Application

After starting both services:

Authentication
Open the frontend.
Sign up or log in.
Test Google authentication if configured.
Verify that the user appears correctly in the dashboard.
Meeting
Create a new meeting.
Copy the generated meeting ID.
Open the meeting in another browser/device.
Join using the meeting ID.
Test:
Camera
Microphone
Video
Screen sharing
Chat
Participant list
Leave meeting
End meeting
Meeting History

After a meeting:

Open Sessions.
Select a meeting.
Review participant information.
Review chat history.
Premium

In Razorpay Test Mode:

Open Pricing.
Select Upgrade to Premium.
Complete the test payment.
Verify Premium activation.
Return to Dashboard.
Confirm unlimited meeting status.
📁 Important Files
File	Responsibility
client/src/App.jsx	Application routing
client/src/pages/Dashboard.jsx	Main dashboard
client/src/pages/MeetingRoom.jsx	Meeting room UI
client/src/pages/Pricing.jsx	Pricing and Razorpay checkout
client/src/pages/Sessions.jsx	Meeting history
client/src/hooks/useWebRTC.js	WebRTC and screen sharing logic
client/src/hooks/useChat.js	Real-time chat
client/src/components/meeting/VideoGrid.jsx	Video layout
client/src/components/meeting/VideoTile.jsx	Individual video tile
client/src/components/meeting/ControlBar.jsx	Meeting controls
server/server.js	Express and Socket.io server
server/socket.js	Real-time signaling/events
server/controllers/meetingController.js	Meeting business logic
server/controllers/paymentController.js	Razorpay payment logic
server/middleware/auth.js	Authentication middleware
server/config/db.js	PostgreSQL connection and schema initialization
server/routes/meetingRoutes.js	Meeting API routes
server/routes/paymentRoutes.js	Payment API routes
📈 Key Engineering Highlights
1. Real-Time Communication

Implemented a browser-based real-time communication system using WebRTC rather than relying on a third-party video calling SDK.

This required handling:

Peer connection creation
SDP offer/answer exchange
ICE candidate exchange
Media stream management
Participant synchronization
Connection cleanup
2. WebRTC + Socket.io Architecture

Instead of using Socket.io to transport video data, Socket.io is used for signaling while WebRTC handles the actual media communication.

This separation provides a cleaner real-time architecture.

3. Dynamic Screen Sharing

Screen sharing dynamically replaces the existing WebRTC video track using:

sender.replaceTrack(screenTrack);

When sharing stops, the original camera track is restored.

This avoids creating an entirely separate peer connection for screen sharing.

4. Server-Side Plan Enforcement

Free/Premium restrictions are not handled only through the frontend.

The backend determines:

Current Plan
       ↓
Meeting Usage
       ↓
Allowed Limit
       ↓
Request Accepted / Rejected

This makes the application more resistant to client-side manipulation.

5. Persistent Meeting History

Meetings, participants, and chat messages are stored in PostgreSQL.

This allows users to revisit completed sessions instead of losing all meeting information after leaving the room.

6. Secure Payment Verification

The backend verifies the Razorpay payment signature using the Razorpay secret key before activating Premium.

The secret remains server-side and is never exposed to the browser.

7. Authentication + Application User Data

Clerk handles authentication while PostgreSQL stores application-specific user information such as:

Name
Email
Profile image
Subscription plan
Timestamps

This separates authentication concerns from application data.

🧩 Challenges Solved
WebRTC Signaling

Managing multiple participants required implementing signaling events for offers, answers, and ICE candidates.

Dynamic Participant State

Participant audio, video, and screen-sharing states need to remain synchronized across clients.

Screen Share Track Replacement

Screen sharing required dynamically replacing the existing video track while preserving microphone audio.

Authentication Synchronization

Clerk authentication and PostgreSQL application users need to remain synchronized through authenticated APIs and webhooks.

Plan Persistence

Premium status is stored in PostgreSQL so that it persists across sessions and devices.

SPA Deployment

Because the frontend uses React Router, Vercel requires SPA route handling so client-side routes such as /dashboard, /pricing, and /meeting/:meetingId resolve correctly after deployment.

🎯 Future Improvements

Possible future improvements include:

SFU-based media architecture for larger meetings
TURN server support for more reliable connections across restrictive networks
Meeting recording
Virtual backgrounds
Noise suppression
Host-controlled participant removal
Meeting invitations
Email notifications
Recurring meetings
Advanced meeting analytics
Production payment reconciliation
Automated payment/order status validation
Rate limiting and additional API hardening
Automated testing and CI/CD
Redis-based Socket.io scaling for multiple backend instances
📚 Tech Stack
Frontend
React
Vite
Tailwind CSS
React Router
Axios
Socket.io Client
Clerk React
Lucide React
React Hot Toast
Backend
Node.js
Express
Socket.io
Clerk Express
PostgreSQL
Neon
Razorpay
CORS
Cookie Parser
dotenv
Real-Time Technologies
WebRTC
Socket.io
MediaDevices API
Screen Capture API
Deployment
Vercel — Frontend
Render — Backend
Neon — PostgreSQL
Clerk — Authentication
Razorpay — Payments
🏗️ System Architecture
                         ┌──────────────────────┐
                         │       User           │
                         │   Browser / Client   │
                         └──────────┬───────────┘
                                    │
                         ┌──────────▼───────────┐
                         │     React + Vite     │
                         │     Frontend         │
                         └──────┬───────┬───────┘
                                │       │
                     REST API   │       │ Socket.io
                                │       │
                                ▼       ▼
                      ┌────────────────────────┐
                      │     Node + Express      │
                      │      Backend            │
                      └──────┬─────────┬────────┘
                             │         │
                     ┌───────▼───┐   ┌─▼────────────┐
                     │ PostgreSQL│   │ Socket.io    │
                     │   Neon    │   │ Signaling    │
                     └───────────┘   └──────┬───────┘
                                            │
                                      WebRTC Signaling
                                            │
                         ┌──────────────────┼──────────────────┐
                         ▼                  ▼                  ▼
                    Participant A      Participant B      Participant C
                         │                  │                  │
                         └─────────── WebRTC Media ────────────┘
📌 Project Highlights

VoxMeet demonstrates full-stack development combined with real-time communication and third-party service integration.

Highlights
Full-stack React + Node.js application
Real-time peer-to-peer video/audio using WebRTC
Socket.io-based signaling and real-time chat
Browser screen sharing
Secure Clerk authentication
PostgreSQL persistence using Neon
Meeting and participant history
Free/Premium plan architecture
Razorpay payment integration
Server-side authentication and authorization
Responsive UI
Production deployment using Vercel and Render
Environment-based configuration
REST API architecture
Modular React component structure
Custom hooks for complex real-time logic
👨‍💻 Author

Ashok

Full-Stack Web Developer

Built as a portfolio project to demonstrate practical experience with:

React • Node.js • Express • PostgreSQL • WebRTC • Socket.io • Authentication • REST APIs • Payments • Cloud Deployment

📄 License

This project is intended for portfolio and educational purposes.


### Ek important recommendation 👇

README ko aur **recruiter-level** banane ke liye sabse upar ek **hero section + screenshots** add karna bahut useful rahega. Abhi README technically strong hai, lekin recruiter GitHub kholkar pehle 10–15 seconds me visual impression leta hai.

Main structure ye rakhunga:

```text
VoxMeet
Real-Time Video Calling Platform

[Live Demo] [GitHub]

Short 2-line description

[Screenshot of Dashboard]
[Screenshot of Meeting Room]
[Screenshot of Screen Sharing]

Key Features
Tech Stack
Architecture
...

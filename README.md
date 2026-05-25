# 🪄 Sorcerer's Saga

**Sorcerer's Saga** is a gamified wellness web application that transforms daily healthy habits into an RPG-style adventure. Users join as "Apprentices" and complete real-world wellness challenges to earn points, unlock quests, and rise through the ranks of the Grand Wizards on the global leaderboard.

This project is a full-stack solution built with **Node.js**, **Express**, and **MySQL**, featuring a custom-built frontend with a responsive, immersive medieval-fantasy theme.

---

## ✨ Features

### 🎮 Gamification Logic
* **Challenges:** Small, independent tasks (e.g., "Meditate under the stars") that award instant points.
* **Quests:** Epic collections of challenges. Users must complete all linked challenges to finish a quest and earn bonus rewards (Points + Badges).
* **Progression Tracking:** The system tracks which quests a user has started, their completion status, and whether rewards have been claimed.
* **Leaderboard:** A dynamic, real-time ranking system displaying the top sorcerers based on total experience points.

### 🛡️ Security & Authentication
* **Secure Registration:** New accounts are created with **Bcrypt** password hashing to ensure database security.
* **Stateless Authentication:** Uses **JSON Web Tokens (JWT)** for secure, efficient session management.
* **Role-Based Access Control (RBAC):** Distinct middleware ensures that only Admins can access sensitive endpoints (like creating quests or banning users), while standard users can only manage their own progress.

### 🧙‍♂️ "Grand Wizard" (Admin) Controls
Admins have access to a hidden control panel within the application to manage the realm:
* **User Management:** View all registered users ("Souls"), rename users, or "exile" (delete) them permanently.
* **Score Manipulation:** Manually adjust a user's points for special events or corrections.
* **Content Creation:** Create new Quests and Challenges directly from the UI without touching the database.

### 🎨 Frontend Experience
* **Immersive Theme:** A custom "Arcane & Ancient" design system using CSS variables for consistent dark-mode colors (`--bg-void`, `--text-gold`).
* **Responsive Design:** Fully fluid layout that adapts to desktops, tablets, and mobile devices.
* **Zero Frameworks:** Built entirely with **Vanilla JavaScript** and the **Fetch API**, ensuring lightweight performance and full control over the DOM.

---

## 🛠️ Tech Stack

* **Runtime Environment:** Node.js
* **Backend Framework:** Express.js
* **Database:** MySQL (Relational Data Model)
* **Frontend:** HTML5, CSS3, Vanilla JavaScript (ES6+)
* **Security:** `bcrypt` (Hashing), `jsonwebtoken` (Auth)

---

## 🚀 Getting Started

Follow these instructions to set up the project on your local machine.

### 1. Prerequisites
Ensure you have the following installed:
* **Node.js** (v14.0.0 or higher)
* **MySQL Server**

### 2. Installation
Clone the repository and install the necessary dependencies:
```bash
# Clone the repository
git clone <repository-url>
cd sorcerers-saga

# Install dependencies (express, mysql2, dotenv, bcrypt, jsonwebtoken)
npm install
```

### 3. Environment Configuration
Create a file named `.env` in the root directory. Add your local database credentials and a secret key for JWT:

```env
# Database Configuration
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=your_mysql_password
DB_DATABASE=sorcerers_saga_db

# Security Configuration
JWT_SECRET_KEY=your_super_secret_key_here
JWT_EXPIRES_IN=1h
JWT_ALGORITHM=HS256
```

### 4. Database Initialization
This project includes scripts to automatically set up your database schema and seed it with starter data (Lore, Quests, Badges, and Default Users).

Run the following commands in order:

```bash
# Step 1: Create the Database Schema
node src/configs/createSchema.js

# Step 2: Create Tables and Seed Initial Data
node src/configs/initTables.js
```

### 5. Running the Application
Start the server:

```bash
npm start
```
* The server will start on port **3000** by default.
* Open your web browser and navigate to: `http://localhost:3000`

---

## 📂 Project Structure

The project follows a modular **MVC (Model-View-Controller)** architecture to ensure code maintainability and separation of concerns.

```text
sorcerers-saga/
│
├── public/                     # CLIENT-SIDE (Frontend)
│   ├── css/                    # Stylesheets
│   │   ├── colors.css          # CSS Variables (Color Palette)
│   │   └── styles.css          # Core Application Styles
│   ├── index.html              # Main Dashboard (Leaderboard, Quests, Profile)
│   ├── login.html              # Login Page
│   ├── register.html           # Registration Page
│   └── script.js               # Main Logic (Fetch API, DOM Manipulation)
│
├── src/                        # SERVER-SIDE (Backend)
│   ├── configs/                # Configuration & Setup Scripts
│   │   ├── createSchema.js     # DB Creation Script
│   │   └── initTables.js       # Table Setup & Seeding Script
│   │
│   ├── controllers/            # Request Handling Logic
│   │   ├── authController.js   # Login/Register Logic
│   │   ├── questController.js  # Quest Logic
│   │   ├── userController.js   # User Profile Logic
│   │   └── ...                 # (Other controllers)
│   │
│   ├── middlewares/            # Request Processing & Security
│   │   ├── bcryptMiddleware.js # Password Hashing
│   │   └── jwtMiddleware.js    # Token Verification & Admin Checks
│   │
│   ├── models/                 # Database Interaction (SQL Queries)
│   │   ├── userModel.js        # User CRUD Operations
│   │   ├── questModel.js       # Quest Data Operations
│   │   └── ...                 # (Other models)
│   │
│   ├── routes/                 # API Endpoint Definitions
│   │   ├── authRoutes.js       # /auth endpoints
│   │   ├── mainRoutes.js       # Main router hub
│   │   └── ...                 # (Other routes)
│   │
│   ├── services/               # Shared Services
│   │   └── db.js               # MySQL Connection Pool
│   │
│   └── app.js                  # Express App Entry Point
│
├── .env                        # Environment Variables (Ignored by Git)
├── package.json                # Project Metadata & Scripts
└── README.md                   # Project Documentation
```

---

## 🔮 API Documentation

### **Authentication**
* `POST /auth/register` - Create a new user account.
* `POST /auth/login` - Authenticate user and receive a JWT.

### **Users**
* `GET /users` - Retrieve all users (Admin only).
* `GET /users/:id` - Get details of a specific user.
* `PUT /users/:id` - Update username or points (Admin/Self).
* `DELETE /users/:id` - Permanently delete a user (Admin/Self).

### **Gameplay (Quests & Challenges)**
* `GET /quests` - List all available quests.
* `POST /quests/:id/start` - Mark a quest as "Started" for the user.
* `POST /quests/:id/claim` - Claim rewards for a completed quest.
* `GET /challenges` - List all active wellness challenges.
* `POST /challenges/:id` - Record a challenge completion.
* `GET /leaderboard` - Retrieve the global ranking of users.

---

### 👨‍💻 Author
**Student ID:** p2510880  
**Class:** DAAA/FT/1B/04  
**School of Computing, Singapore Polytechnic**
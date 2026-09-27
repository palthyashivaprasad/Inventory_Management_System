<div align="center">
  <h1>📦 Inventory Management System</h1>
  <p><strong>A Full-Stack Enterprise-grade Inventory Management System built with the MERN Stack.</strong></p>

  [![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](https://reactjs.org/)
  [![Vite](https://img.shields.io/badge/Vite-B73BFE?style=for-the-badge&logo=vite&logoColor=FFD62E)](https://vitejs.dev/)
  [![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)](https://nodejs.org/)
  [![Express.js](https://img.shields.io/badge/Express.js-000000?style=for-the-badge&logo=express&logoColor=white)](https://expressjs.com/)
  [![MongoDB](https://img.shields.io/badge/MongoDB-4EA94B?style=for-the-badge&logo=mongodb&logoColor=white)](https://www.mongodb.com/)
  [![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
</div>

---

## 📖 Table of Contents
- [About the Project](#about-the-project)
- [System Architecture](#system-architecture)
- [Key Features](#key-features)
- [Role-Based Access Control (RBAC)](#role-based-access-control-rbac)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [API Reference](#api-reference)
- [Getting Started](#getting-started)
- [Security](#security)
- [Future Enhancements](#future-enhancements)
- [Author](#author)

---

## 🚀 About the Project
This project is a comprehensive **Inventory Management System** designed to handle complex supply chain operations. It seamlessly integrates warehouse tracking, supplier relations, product cataloging, and staff management under a single unified dashboard. The system guarantees secure data handling through JWT-based authentication and a rigorous Role-Based Access Control (RBAC) mechanism.

---

## 🏗️ System Architecture

The application is built on a scalable **Client-Server Architecture** employing the MERN stack.

```mermaid
architecture-diagram
flowchart TD
    subgraph Frontend [Client Side - React/Vite]
        UI[User Interface]
        Ctx[State Management / Context API]
        Router[React Router DOM]
        Axios[Axios HTTP Client]
        
        UI --> Ctx
        UI --> Router
        Router --> Axios
    end

    subgraph Backend [Server Side - Node.js/Express]
        API[Express Routes]
        Auth[JWT & RBAC Middleware]
        Ctrl[Controllers]
        Mongoose[Mongoose Models]
        Services[Services - Multer/Nodemailer]

        Axios -->|HTTP/REST| API
        API --> Auth
        Auth -->|Validated| Ctrl
        Ctrl --> Services
        Ctrl --> Mongoose
    end

    subgraph Database [Database]
        MongoDB[(MongoDB Atlas / Local)]
        Mongoose -->|CRUD Operations| MongoDB
    end
```

### Architecture Highlights
- **Frontend Layer**: React-based Single Page Application (SPA) utilizing Vite for fast builds. Manages routing, state, and visual charting (Recharts/ApexCharts).
- **API Gateway/Routing**: Express.js router acts as the entry point for all client requests.
- **Security Middleware**: Intercepts requests to validate JWT tokens and enforce role permissions before forwarding to controllers.
- **Controller Layer**: Contains the core business logic (Inventory handling, Staff management, Order processing).
- **Data Access Layer**: Mongoose ORM models define the schema structure and interact directly with the MongoDB database.

---

## ✨ Key Features

- **🔐 Robust Authentication**: Secure login, registration, and password recovery via JWT and bcrypt.
- **📊 Real-time Dashboard**: Visual metrics utilizing charting libraries for tracking orders, revenue, and stock levels.
- **🏢 Warehouse Management**: Assign and track stock levels across multiple physical warehouse locations.
- **📦 Product & Category Catalog**: Full CRUD capabilities for products, complete with Cloudinary image uploads and barcode generation.
- **🚚 Supplier & Order Tracking**: Manage vendor details, upload documents, and track order fulfillment statuses.
- **👥 Staff Administration**: Comprehensive staff profile management with hierarchical role distribution.

---

## 🛡️ Role-Based Access Control (RBAC)

The system restricts functionality based on four distinct user roles:

| Role | Permissions & Access Level |
|------|---------------------------|
| **👑 Master Admin** | Absolute control. Can manage all users, assign roles, create warehouses, and access all system data. (Created via backend script only). |
| **👔 Manager** | Can view inventory, access the dashboard, and manage orders. Cannot administer staff roles. |
| **🏬 Warehouse Admin**| Confined to a specific warehouse. Can only view and update stock/operations within their assigned location. |
| **👷 Staff** | Basic read-only access to the dashboard and general inventory lists. |

---

## 💻 Tech Stack

### 🎨 Frontend
- **Framework**: React.js 19 with Vite
- **Routing**: React Router DOM v7
- **Styling**: Tailwind CSS v4
- **State/HTTP**: React Context API, Axios
- **UI Components**: Framer Motion, Lucide React, React Icons
- **Data Visualization**: Recharts, ApexCharts
- **Utilities**: JsBarcode

### ⚙️ Backend
- **Runtime Environment**: Node.js
- **Framework**: Express.js 5
- **Database**: MongoDB with Mongoose ODM
- **Authentication**: JSON Web Tokens (JWT), bcryptjs
- **File Uploads**: Multer
- **Email Services**: Nodemailer

---

## 📁 Project Structure

```text
Inventory_management_system_mohit.ISM/
├── backend/
│   ├── controllers/      # Business logic and request handling
│   ├── db/               # Database connection setup
│   ├── middleware/       # JWT auth and RBAC role validation
│   ├── models/           # Mongoose schemas (User, Product, Order, etc.)
│   ├── routes/           # Express API route definitions
│   ├── scripts/          # Admin provisioning scripts
│   ├── uploads/          # Local storage for Multer uploads
│   ├── utils/            # Helper functions (Mailers, formatters)
│   ├── index.js          # Main server entry point
│   ├── seed.js           # Database seeding script
│   └── package.json
│
├── frontend/
│   ├── public/           # Static assets
│   ├── src/
│   │   ├── assets/       # Images and global styles
│   │   ├── components/   # Reusable UI components (Charts, Forms, Cards)
│   │   ├── context/      # React Context providers (Auth, Theme)
│   │   ├── layout/       # Shared structural layouts (Navbars, Sidebars)
│   │   ├── pages/        # Main application views
│   │   ├── routes/       # Protected and public route definitions
│   │   ├── Staff/        # Staff-specific views
│   │   ├── Warehouse/    # Warehouse-specific views
│   │   ├── App.jsx       # Root component
│   │   └── main.jsx      # React DOM entry
│   ├── vite.config.js
│   └── package.json
└── README.md
```

---

## 🔌 API Reference

The backend exposes a RESTful API. Below are the core endpoints:

**Authentication** (`/api/auth`)
- `POST /register` - Register a new account
- `POST /login` - Authenticate and receive JWT
- `POST /forgot-password` - Request a password reset link
- `POST /reset-password/:token` - Reset account password

**Core Entities** (Standard CRUD: `GET`, `POST`, `PUT`, `DELETE`)
- `/api/products` - Manage products and retrieve trend analysis (`/analysis/trends`)
- `/api/categories` - Manage product categories
- `/api/orders` - Order processing and status updates (`PATCH /status/:id`)
- `/api/suppliers` - Manage suppliers
- `/api/warehouse` - Warehouse administration
- `/api/staffs` - Manage staff and individual profiles (`GET /profile`, `PUT /update-profile`)

**System**
- `GET /health` - API health check

---

## 🛠️ Getting Started

Follow these steps to run the project locally.

### 1. Clone the Repository
```bash
git clone https://github.com/Mohitkumar2217/Inventory_management_system_mohit.ISM.git
cd Inventory_management_system_mohit.ISM
```

### 2. Backend Setup
Navigate to the backend directory, install dependencies, and configure your environment.

```bash
cd backend
npm install
```

Create a `.env` file in the `backend` folder:
```env
PORT=4000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_super_secret_jwt_key
EMAIL_USER=your_smtp_email
EMAIL_PASS=your_smtp_app_password
MASTER_ADMIN_NAME=Master Admin
MASTER_ADMIN_EMAIL=admin@example.com
MASTER_ADMIN_PASSWORD=secure_password_123
```

**Initialize Admin and Start Server:**
```bash
# Creates the Master Admin based on .env variables
npm run admin:create

# Start the development server
npm run start
```
*(Optional)* Populate the database with sample data: `npm run seed`

### 3. Frontend Setup
Open a new terminal, navigate to the frontend directory, and start the Vite dev server.

```bash
cd frontend
npm install
```

Create a `.env` file in the `frontend` folder:
```env
VITE_API_URL=http://localhost:4000
```

**Start the Client:**
```bash
npm run dev
```

---

## 🔒 Security Measures
- **Password Protection**: Passwords are mathematically hashed using `bcrypt` before storage.
- **Stateless Authentication**: Sessions are managed via short-lived JSON Web Tokens (JWT).
- **Endpoint Protection**: API routes are secured by middleware verifying both token validity and user roles.
- **Time-bound Operations**: Password reset tokens expire automatically after 15 minutes to prevent replay attacks.
- **File Upload Validation**: Multer is configured to validate file types and sizes for supplier documents and product images.

---

## 🔮 Future Enhancements
- [ ] Transition demo dashboard analytics to consume live database metrics.
- [ ] Implement automated real-time low-stock email notifications.
- [ ] Add comprehensive PDF and Excel reporting exports (CSV currently supported).
- [ ] Containerize the application using Docker and Docker Compose.
- [ ] Integrate a Swagger UI for interactive API documentation.
- [ ] Implement Unit (Jest) and E2E (Cypress) testing suites.

---

## ✍️ Author
**Mohit Kumawat**

If you found this project helpful or inspiring, please consider giving it a ⭐ on GitHub!
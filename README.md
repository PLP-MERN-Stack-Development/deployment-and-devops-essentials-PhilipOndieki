# MERN Bug Tracker

A production-ready, full-stack bug tracking application built with the MERN stack (MongoDB, Express.js, React, Node.js). Features a modern Kanban-style interface with drag-and-drop functionality, comprehensive authentication, and extensive test coverage.

![bug-tracker dashboard](image-2.png)

## 📋 Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [API Documentation](#api-documentation)
- [Authentication](#authentication)
- [Deployment](#deployment)
- [Environment Variables](#environment-variables)
- [Contributing](#contributing)
- [License](#license)

## ✨ Features

### Core Functionality
- **Complete CRUD Operations** - Create, read, update, and delete bugs
- **User Authentication** - JWT-based authentication with secure password hashing
- **Kanban Board** - Visual bug tracking with drag-and-drop status changes
- **Advanced Filtering** - Filter by status, priority, severity, and search by keywords
- **Real-time Updates** - Optimistic UI updates with state synchronization
- **Responsive Design** - Mobile-first design that works on all devices

### User Experience
- **Drag-and-Drop Interface** - Intuitive bug status management (desktop)
- **Mobile Status Selector** - Touch-friendly status changes on mobile devices
- **Toast Notifications** - Real-time feedback for user actions
- **Loading States** - Skeleton screens and loading indicators
- **Error Boundaries** - Graceful error handling with recovery options
- **Dark Theme** - Modern, eye-friendly dark color scheme

### Developer Features
- **90%+ Test Coverage** - Comprehensive unit and integration tests
- **Type Safety** - Zod schema validation on both frontend and backend
- **Error Logging** - Winston logger with multiple transports
- **API Documentation** - Well-documented REST API endpoints
- **Code Quality** - ESLint, Prettier, and consistent code structure
- **Production Ready** - Deployed on Vercel (frontend) and Render (backend)

## 🚀 Tech Stack

### Frontend
- **React 18.2** - UI library with hooks and modern features
- **React Router v6** - Client-side routing
- **TailwindCSS** - Utility-first CSS framework
- **@dnd-kit** - Drag-and-drop library for React
- **React Hook Form + Zod** - Form management and validation
- **Axios** - HTTP client with interceptors
- **React Hot Toast** - Toast notifications
- **Lucide React** - Icon library
- **Vite** - Fast build tool and dev server

### Backend
- **Node.js & Express** - Server framework
- **MongoDB & Mongoose** - Database and ODM
- **JWT** - JSON Web Tokens for authentication
- **bcryptjs** - Password hashing
- **Express Validator** - Request validation
- **Winston** - Logging framework
- **Helmet** - Security middleware
- **CORS** - Cross-origin resource sharing
- **Express Rate Limit** - API rate limiting

### DevOps
- **Vercel** - Frontend deployment
- **Render** - Backend deployment
- **MongoDB Atlas** - Cloud database
- **GitHub** - Version control

## 🏗️ Architecture

### Application Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                         Client Side                          │
│  ┌────────────┐  ┌────────────┐  ┌──────────────────────┐  │
│  │   React    │─→│   Router   │─→│  Context Providers   │  │
│  │ Components │  │  (Routes)  │  │  (Auth, Bug State)   │  │
│  └────────────┘  └────────────┘  └──────────────────────┘  │
│         │                │                    │              │
│         └────────────────┴────────────────────┘              │
│                          │                                   │
│                  ┌───────▼────────┐                         │
│                  │  Axios Client  │                         │
│                  │ (API Requests) │                         │
│                  └───────┬────────┘                         │
└──────────────────────────┼──────────────────────────────────┘
                           │
                    HTTPS/REST API
                           │
┌──────────────────────────▼──────────────────────────────────┐
│                        Server Side                           │
│  ┌────────────┐  ┌────────────┐  ┌──────────────────────┐  │
│  │  Express   │→ │ Middleware │→ │    Controllers       │  │
│  │   Router   │  │ (Auth/Val) │  │ (Business Logic)     │  │
│  └────────────┘  └────────────┘  └──────────────────────┘  │
│         │                │                    │              │
│         └────────────────┴────────────────────┘              │
│                          │                                   │
│                  ┌───────▼────────┐                         │
│                  │    Mongoose    │                         │
│                  │   (ODM/Models) │                         │
│                  └───────┬────────┘                         │
└──────────────────────────┼──────────────────────────────────┘
                           │
                    MongoDB Protocol
                           │
┌──────────────────────────▼──────────────────────────────────┐
│                      MongoDB Atlas                           │
│  ┌────────────────────────────────────────────────────┐    │
│  │              Bug Tracker Database                  │    │
│  │  ┌──────────────┐  ┌──────────────────────────┐   │    │
│  │  │ Users Coll.  │  │  Bugs Collection        │   │    │
│  │  └──────────────┘  └──────────────────────────┘   │    │
│  └────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────┘
```

### Data Flow

1. **User Authentication Flow**
   ```
   User → Login Form → Auth Context → API Request → JWT Token → 
   Local Storage → Protected Routes Access
   ```

2. **Bug Management Flow**
   ```
   User Action → Component → Bug Context → API Request → 
   MongoDB → Response → State Update → UI Update
   ```

3. **Drag-and-Drop Flow**
   ```
   User Drags Bug → DnD Kit → Optimistic Update → 
   API PATCH Request → Server Validation → Database Update → 
   Success/Rollback → Toast Notification
   ```

## 🎯 Getting Started

### Prerequisites

- **Node.js** >= 18.0.0
- **npm** or **yarn**
- **MongoDB** (local or MongoDB Atlas account)
- **Git**

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/mern-bug-tracker.git
   cd mern-bug-tracker
   ```

2. **Install dependencies**

   **Backend:**
   ```bash
   cd server
   npm install
   ```

   **Frontend:**
   ```bash
   cd ../client
   npm install
   ```

3. **Set up environment variables**

   **Backend (.env):**
   ```bash
   cd server
   cp .env.example .env
   ```
   
   Edit `.env` with your configuration:
   ```env
   NODE_ENV=development
   PORT=5000
   MONGODB_URI=mongodb://localhost:27017/bug-tracker
   JWT_SECRET=your-super-secret-jwt-key-change-in-production
   JWT_EXPIRE=7d
   CORS_ORIGIN=http://localhost:3000
   LOG_LEVEL=info
   ```

   **Frontend (.env):**
   ```bash
   cd ../client
   cp .env.example .env
   ```
   
   Edit `.env`:
   ```env
   VITE_API_URL=http://localhost:5000/api
   VITE_NODE_ENV=development
   ```

4. **Start MongoDB** (if running locally)
   ```bash
   mongod
   ```

5. **Run the application**

   **Terminal 1 - Backend:**
   ```bash
   cd server
   npm run dev
   ```

   **Terminal 2 - Frontend:**
   ```bash
   cd client
   npm run dev
   ```

6. **Access the application**
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:5000/api
   - Health Check: http://localhost:5000/health

## 📁 Project Structure

### Backend Structure

```
server/
├── src/
│   ├── config/
│   │   ├── database.js          # MongoDB connection
│   │   ├── logger.js            # Winston logger setup
│   │   └── constants.js         # App constants
│   ├── controllers/
│   │   ├── authController.js    # Auth business logic
│   │   └── bugController.js     # Bug business logic
│   ├── middleware/
│   │   ├── authMiddleware.js    # JWT verification
│   │   ├── errorHandler.js      # Global error handling
│   │   ├── requestLogger.js     # Request logging
│   │   └── validator.js         # Input validation
│   ├── models/
│   │   ├── Bug.js               # Bug schema
│   │   └── User.js              # User schema
│   ├── routes/
│   │   ├── authRoutes.js        # Auth endpoints
│   │   └── bugRoutes.js         # Bug endpoints
│   ├── utils/
│   │   ├── apiResponse.js       # Response formatters
│   │   └── validateBug.js       # Validation utilities
│   ├── app.js                   # Express app setup
│   └── server.js                # Server entry point
├── logs/                        # Application logs
├── .env.example                 # Environment template
├── package.json                 # Dependencies
└── README.md                    # Documentation
```

### Frontend Structure

```
client/
├── src/
│   ├── components/
│   │   ├── auth/
│   │   │   ├── LoginForm.jsx
│   │   │   ├── SignupForm.jsx
│   │   │   └── ProtectedRoute.jsx
│   │   ├── bugs/
│   │   │   ├── BugBoard.jsx         # Main Kanban board
│   │   │   ├── BugCard.jsx          # Individual bug card
│   │   │   ├── BugColumn.jsx        # Status column
│   │   │   ├── BugModal.jsx         # Create/Edit modal
│   │   │   ├── BugFilters.jsx       # Filtering controls
│   │   │   ├── DeleteConfirm.jsx    # Delete confirmation
│   │   │   └── MobileStatusSelector.jsx
│   │   ├── common/
│   │   │   ├── Button.jsx
│   │   │   ├── Input.jsx
│   │   │   ├── Badge.jsx
│   │   │   ├── Modal.jsx
│   │   │   ├── Loading.jsx
│   │   │   └── ...
│   │   ├── error/
│   │   │   ├── ErrorBoundary.jsx
│   │   │   └── ErrorFallback.jsx
│   │   └── layout/
│   │       ├── Header.jsx
│   │       ├── Sidebar.jsx
│   │       ├── Layout.jsx
│   │       └── MobileMenu.jsx
│   ├── context/
│   │   ├── AuthContext.jsx      # Auth state management
│   │   ├── BugContext.jsx       # Bug state management
│   │   └── bugReducer.js        # Bug state reducer
│   ├── hooks/
│   │   ├── useBugs.js           # Bug operations hook
│   │   ├── useDebounce.js       # Debounce hook
│   │   └── ...
│   ├── services/
│   │   ├── api.js               # Axios configuration
│   │   ├── authService.js       # Auth API calls
│   │   └── bugService.js        # Bug API calls
│   ├── utils/
│   │   ├── constants.js         # App constants
│   │   ├── helpers.js           # Helper functions
│   │   ├── formatters.js        # Data formatters
│   │   └── validators.js        # Zod schemas
│   ├── styles/
│   │   └── index.css            # Global styles
│   ├── App.jsx                  # Root component
│   └── main.jsx                 # App entry point
├── public/
│   └── favicon.ico
├── index.html
├── vite.config.js
├── tailwind.config.js
├── package.json
└── README.md
```

## 📚 API Documentation

### Base URL
```
Production: https://bugtracker-api.onrender.com/api
Development: http://localhost:5000/api
```

### Authentication Endpoints

#### Register User
```http
POST /auth/signup
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "password123"
}
```

**Response (201 Created):**
```json
{
  "success": true,
  "message": "User registered successfully",
  "data": {
    "user": {
      "id": "...",
      "name": "John Doe",
      "email": "john@example.com",
      "role": "user"
    },
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
}
```

#### Login
```http
POST /auth/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "password123"
}
```

#### Get Current User
```http
GET /auth/me
Authorization: Bearer <token>
```

#### Logout
```http
POST /auth/logout
Authorization: Bearer <token>
```

### Bug Endpoints

#### Create Bug
```http
POST /bugs
Authorization: Bearer <token>
Content-Type: application/json

{
  "title": "Button not responding on mobile",
  "description": "The submit button doesn't work on iOS Safari",
  "priority": "high",
  "severity": "major",
  "createdBy": "John Doe"
}
```

**Response (201 Created):**
```json
{
  "success": true,
  "message": "Bug created successfully",
  "data": {
    "id": "...",
    "title": "Button not responding on mobile",
    "description": "The submit button doesn't work on iOS Safari",
    "status": "open",
    "priority": "high",
    "severity": "major",
    "createdBy": "John Doe",
    "createdAt": "2024-01-15T10:30:00.000Z",
    "updatedAt": "2024-01-15T10:30:00.000Z"
  }
}
```

#### Get All Bugs (with filters)
```http
GET /bugs?status=open&priority=high&page=1&limit=10&sortBy=createdAt&order=desc
```

**Query Parameters:**
- `status` - Filter by status (open, in-progress, resolved, closed)
- `priority` - Filter by priority (low, medium, high, critical)
- `severity` - Filter by severity (minor, major, critical)
- `createdBy` - Filter by creator name (partial match)
- `page` - Page number (default: 1)
- `limit` - Items per page (default: 10, max: 100)
- `sortBy` - Sort field (createdAt, updatedAt, priority, severity, status)
- `order` - Sort order (asc, desc)

**Response (200 OK):**
```json
{
  "success": true,
  "message": "Bugs retrieved successfully",
  "data": [
    {
      "id": "...",
      "title": "Bug title",
      "description": "Bug description",
      "status": "open",
      "priority": "high",
      "severity": "major",
      "createdBy": "John Doe",
      "createdAt": "2024-01-15T10:30:00.000Z",
      "updatedAt": "2024-01-15T10:30:00.000Z"
    }
  ],
  "pagination": {
    "currentPage": 1,
    "itemsPerPage": 10,
    "totalItems": 50,
    "totalPages": 5,
    "hasNextPage": true,
    "hasPreviousPage": false
  }
}
```

#### Get Bug by ID
```http
GET /bugs/:id
```

#### Update Bug (Full Update)
```http
PUT /bugs/:id
Authorization: Bearer <token>
Content-Type: application/json

{
  "title": "Updated title",
  "description": "Updated description",
  "status": "in-progress",
  "priority": "critical",
  "severity": "critical",
  "createdBy": "John Doe"
}
```

#### Partial Update (Status Change)
```http
PATCH /bugs/:id
Authorization: Bearer <token>
Content-Type: application/json

{
  "status": "resolved"
}
```

#### Delete Bug
```http
DELETE /bugs/:id
Authorization: Bearer <token>
```

**Response (200 OK):**
```json
{
  "success": true,
  "message": "Bug deleted successfully",
  "data": {
    "id": "..."
  }
}
```

#### Get Bug Statistics
```http
GET /bugs/stats
```

**Response (200 OK):**
```json
{
  "success": true,
  "message": "Statistics retrieved successfully",
  "data": {
    "total": 100,
    "byStatus": {
      "open": 45,
      "in-progress": 30,
      "resolved": 20,
      "closed": 5
    },
    "byPriority": {
      "low": 20,
      "medium": 40,
      "high": 30,
      "critical": 10
    },
    "bySeverity": {
      "minor": 30,
      "major": 50,
      "critical": 20
    }
  }
}
```

### Error Responses

All errors follow this format:

```json
{
  "success": false,
  "message": "Error message",
  "errors": [
    {
      "field": "title",
      "message": "Title is required"
    }
  ]
}
```

**HTTP Status Codes:**
- `200` - Success
- `201` - Created
- `400` - Bad Request (validation errors)
- `401` - Unauthorized (authentication required)
- `403` - Forbidden (insufficient permissions)
- `404` - Not Found
- `409` - Conflict (duplicate resource)
- `500` - Internal Server Error

## 🔐 Authentication

### JWT Token Flow

1. **User Registration/Login**
   - User submits credentials
   - Server validates credentials
   - Server generates JWT token with user info
   - Token sent to client and stored in localStorage

2. **Authenticated Requests**
   - Client includes token in Authorization header: `Bearer <token>`
   - Server middleware verifies token
   - User info attached to request object
   - Protected route access granted

3. **Token Structure**
   ```javascript
   {
     "id": "user-id",
     "email": "user@example.com",
     "role": "user",
     "iat": 1516239022,
     "exp": 1517448622
   }
   ```

4. **Token Expiration**
   - Default: 7 days
   - Configurable via JWT_EXPIRE environment variable
   - Client must re-authenticate after expiration

### Protected Routes

**Backend:**
- `POST /api/bugs` - Create bug (requires authentication)
- `PUT /api/bugs/:id` - Update bug (requires authentication)
- `PATCH /api/bugs/:id` - Patch bug (requires authentication)
- `DELETE /api/bugs/:id` - Delete bug (requires authentication)
- `GET /api/auth/me` - Get current user (requires authentication)
- `POST /api/auth/logout` - Logout (requires authentication)

**Frontend:**
- `/` - Bug Board (protected)
- `/stats` - Statistics (protected)

### Role-Based Access Control (RBAC)

The application supports two user roles:
- **user** - Standard user (default)
- **admin** - Administrator (future feature)

Currently, all authenticated users can:
- Create bugs
- Update their own bugs
- Delete their own bugs
- View all bugs


## 🚢 Deployment

### Production Deployment

**Frontend (Vercel):**
- Repository: Connected to GitHub
- Framework: Vite
- Build Command: `cd client && npm install && npm run build`
- Output Directory: `client/dist`
- Environment Variables: Set in Vercel dashboard
- URL: https://bug-tracker-zeta-pied.vercel.app

**Backend (Render):**
- Service Type: Web Service
- Build Command: `cd server && npm install`
- Start Command: `cd server && npm start`
- Environment Variables: Set in Render dashboard
- Health Check: `/health`
- URL: https://bugtracker-api.onrender.com

**CI-CD screenshots**
- Frontend
![frontend](image-4.png)

- Backend 
![backend screeenshot](image-3.png)
**Database (MongoDB Atlas):**
- Cluster: Cloud-hosted MongoDB
- Connection: Via MONGODB_URI environment variable
- Network Access: Configured for deployment platforms

### Deployment Checklist

**Backend:**
- [ ] Set `NODE_ENV=production`
- [ ] Configure production MongoDB URI
- [ ] Set strong JWT_SECRET
- [ ] Configure CORS_ORIGIN to frontend URL
- [ ] Set appropriate rate limits
- [ ] Configure log levels
- [ ] Enable health checks
- [ ] Set up monitoring

**Frontend:**
- [ ] Set `VITE_NODE_ENV=production`
- [ ] Configure production API URL
- [ ] Optimize build settings
- [ ] Enable caching headers
- [ ] Configure error tracking
- [ ] Test on multiple devices

### Environment Variables

**Backend Production (.env):**
```env
NODE_ENV=production
PORT=10000
MONGODB_URI=mongodb+srv://user:pass@cluster.mongodb.net/bugtracker
JWT_SECRET=your-super-secret-production-key-min-32-chars
JWT_EXPIRE=7d
CORS_ORIGIN=https://bug-tracker-zeta-pied.vercel.app
LOG_LEVEL=info
API_PREFIX=/api
RATE_LIMIT_WINDOW_MS=900000
RATE_LIMIT_MAX_REQUESTS=100
```

**Frontend Production (.env):**
```env
VITE_API_URL=https://bugtracker-api.onrender.com/api
VITE_NODE_ENV=production
VITE_APP_NAME=Bug Tracker
VITE_APP_VERSION=1.0.0
```

### Deployment Commands

**Build for Production:**

Backend:
```bash
cd server
npm install --production
```

Frontend:
```bash
cd client
npm run build
```

**Preview Production Build:**
```bash
cd client
npm run preview
```

## 🔧 Configuration

### Backend Configuration Files

**database.js** - MongoDB connection settings
```javascript
{
  useNewUrlParser: true,
  useUnifiedTopology: true,
  maxPoolSize: 10,
  serverSelectionTimeoutMS: 5000,
  socketTimeoutMS: 45000
}
```

**logger.js** - Winston logging configuration
```javascript
{
  level: 'info',
  format: 'timestamp + level + message',
  transports: [
    'console',
    'error.log',
    'combined.log'
  ]
}
```

### Frontend Configuration Files

**vite.config.js** - Vite build configuration
```javascript
{
  server: {
    port: 3000,
    proxy: {
      '/api': 'http://localhost:5000'
    }
  },
  build: {
    sourcemap: true,
    chunkSizeWarningLimit: 1000
  }
}
```

**tailwind.config.js** - Tailwind CSS configuration
```javascript
{
  theme: {
    extend: {
      colors: {
        primary: '#0A0A0A',
        secondary: '#141414',
        accent: '#3B82F6'
      }
    }
  }
}
```

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Commit your changes**
   ```bash
   git commit -m 'Add amazing feature'
   ```
4. **Push to the branch**
   ```bash
   git push origin feature/amazing-feature
   ```
5. **Open a Pull Request**

### Coding Standards

- Follow ESLint and Prettier configurations
- Write tests for new features
- Maintain 90%+ test coverage
- Update documentation
- Use meaningful commit messages
- Follow existing code structure

### Pull Request Process

1. Update README.md with details of changes
2. Update API documentation if needed
3. Ensure all tests pass
4. Request review from maintainers
5. Address review comments
6. Squash commits before merging

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👨‍💻 Author

**Philip Ondieki**
- Full-stack Developer specializing in MERN stack
- 2+ years of experience
- Expert in TDD and production-ready applications
- Based in Nairobi, Kenya

## 🙏 Acknowledgments

- React Testing Library documentation
- MongoDB Mongoose documentation
- Express.js best practices
- TailwindCSS community
- DnD Kit library
- Open source community

## 📞 Support

For issues, questions, or contributions:
- Open an issue on GitHub
- Check existing documentation
- Review closed issues for solutions

## 🗺️ Roadmap

### Version 1.1 (Planned)
- [ ] File attachments for bugs
- [ ] Comment system
- [ ] Email notifications
- [ ] Real-time collaboration (Socket.io)
- [ ] Advanced search with ElasticSearch
- [ ] Bulk operations
- [ ] Export to CSV/PDF

### Version 2.0 (Future)
- [ ] Project management features
- [ ] Team collaboration tools
- [ ] Time tracking
- [ ] Sprint planning
- [ ] Integration with GitHub/Jira
- [ ] Custom fields
- [ ] Advanced analytics dashboard

## 📊 Performance Metrics

- **Frontend Build Size:** ~300KB (gzipped)
- **Backend Response Time:** <100ms average
- **Database Query Time:** <50ms average
- **Test Execution Time:** <30 seconds
- **Lighthouse Score:** 95+ (Performance, Accessibility, Best Practices, SEO)

## 🔍 Troubleshooting

### Common Issues

**MongoDB Connection Error:**
```bash
# Check MongoDB is running
mongod --version

# Test connection string
mongo <your-connection-string>
```

**Port Already in Use:**
```bash
# Find process using port
lsof -i :5000

# Kill process
kill -9 <PID>
```

**Build Errors:**
```bash
# Clear node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
```

---

**Built with by Philip Ondieki**

**Live Application:** https://bug-tracker-zeta-pied.vercel.app

**API Endpoint:** https://bugtracker-api.onrender.com
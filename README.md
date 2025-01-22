# Online Learning Platform Backend

This is the backend API for an Online Learning Platform. It provides the necessary functionalities for handling user authentication, course management, and chapter uploads. The backend is built with Node.js, Express, and MongoDB.

## Features

- **User Authentication (Signup & Login)**
- **Role-Based Authorization (Admin, Instructor, Student)**
- **Course Management (Create, Fetch by Instructor)**
- **Chapter Management (Add Chapters with Attachments)**

## Tech Stack

- **Node.js**: JavaScript runtime used for building the server.
- **Express**: Web framework for Node.js.
- **MongoDB**: NoSQL database to store user and course data.
- **JWT (JSON Web Token)**: For user authentication.
- **Mongoose**: MongoDB object modeling tool.

## API Endpoints

### Authentication Routes

1. **POST /api/auth/signup**
   - Registers a new user.
   - **Body**: 
     ```json
     {
       "username": "user1",
       "email": "user1@example.com",
       "password": "password123",
       "role": "admin"  // can be 'admin', 'instructor', or 'student'
     }
     ```
   - **Response**: Success message with token on successful registration.

2. **POST /api/auth/login**
   - Authenticates a user.
   - **Body**:
     ```json
     {
       "email": "user1@example.com",
       "password": "password123"
     }
     ```
   - **Response**: JWT token on successful login.

### User Routes

1. **GET /api/users**
   - Fetch all users (Admin only).
   - **Response**: List of all users.
   
2. **GET /api/users/:id**
   - Fetch user details by user ID (Admin or the user themselves).
   - **Response**: User details.

### Course Routes

1. **POST /api/courses**
   - Create a new course (Admin or Instructor).
   - **Body**:
     ```json
     {
       "title": "Introduction to Node.js",
       "description": "Learn the basics of Node.js.",
       "instructor": "instructorId"  // ID of the instructor
     }
     ```
   - **Response**: Created course details.

2. **GET /api/courses**
   - Fetch all courses.
   - **Response**: List of all courses.

3. **GET /api/courses/:instructorId**
   - Fetch courses by instructor ID (Admin or Instructor).
   - **Response**: List of courses for the given instructor.

### Chapter Routes

1. **POST /api/courses/chapter**
   - Add a new chapter to a course (Admin or Instructor).
   - **Body** (Form data):
     ```json
     {
       "title": "Node.js Basics",
       "description": "This chapter introduces Node.js.",
       "courseId": "courseId",  // ID of the course to which chapter is being added
       "attachments": [
         {
           "fileName": "chapter1.pdf",
           "fileUrl": "https://example.com/chapter1.pdf"
         },
         {
           "fileName": "chapter1_video.mp4",
           "fileUrl": "https://example.com/chapter1_video.mp4"
         }
       ]
     }
     ```
   - **Response**: Created chapter details.

### Middleware

1. **Protect Middleware** (`protect.js`)
   - Ensures that only authenticated users can access certain routes.
   
2. **Authorize Middleware** (`authorize.js`)
   - Role-based authorization, allowing only admins, instructors, or students to access specific resources.

## Setup and Installation

Follow these steps to set up the backend on your local machine:

### Prerequisites

- **Node.js** (version 14 or above)
- **MongoDB** (either locally or a cloud instance like MongoDB Atlas)

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/your-username/online-learning-platform-backend.git
   cd online-learning-platform-backend

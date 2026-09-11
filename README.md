#  Spotify Clone Backend

This is a backend project inspired by Spotify. It provides APIs for user authentication, artist management, music uploads, albums, and role-based access.

The project is built using Node.js, Express.js, MongoDB, Mongoose, JWT, Cookies, and ImageKit.

There are two types of users in the application:

* Normal User
* Artist

Artists can upload music and manage their content, while normal users can access and browse the available music and albums.

## 🚀 Features

### Authentication

* User registration
* User login
* Password hashing
* JWT based authentication
* Authentication using cookies
* Protected routes
* Role based authorization

### Normal User

A normal user can:

* Register and login
* Access authenticated routes
* View albums
* Access available music
* Browse the content available on the platform

### Artist

An artist can:

* Register and login as an artist
* Upload music
* Create albums
* Manage music
* Associate music with albums

### Music and Albums

* Upload music files
* Store music files using ImageKit
* Store music details in MongoDB
* Create and retrieve albums
* Connect songs with their respective artists and albums
* Use Mongoose `populate()` to retrieve related data

## 🛠️ Technologies Used

* **Node.js** for running the backend
* **Express.js** for creating the REST APIs
* **MongoDB** for storing application data
* **Mongoose** for working with MongoDB
* **JWT** for authentication
* **Cookie Parser** for handling authentication cookies
* **ImageKit** for cloud storage
* **Postman** for testing APIs

## 📁 Project Structure

```text
spotify-clone-backend/
│
├── src/
│   ├── controllers/
│   │   ├── auth.controller.js
│   │   ├── music.controller.js
│   │   └── album.controller.js
│   │
│   ├── middleware/
│   │   └── auth.middleware.js
│   │
│   ├── models/
│   │   ├── user.model.js
│   │   ├── music.model.js
│   │   └── album.model.js
│   │
│   ├── routes/
│   │   ├── auth.routes.js
│   │   ├── music.routes.js
│   │   └── album.routes.js
│   │
│   ├── services/
│   │   └── storage.service.js
│   │
│   └── app.js
│
├── .env
├── package.json
└── README.md
```

## 🔐 How Authentication Works

The project uses JWT for authentication.

When a user registers, their details are stored in MongoDB. The password is hashed before storing it in the database.

When the user logs in successfully, the backend creates a JWT containing information about the user, including their role.

The token is then stored in a cookie.

For protected routes, the authentication middleware checks the cookie and verifies the JWT.

The basic flow is:

```text
Login
  ↓
Check user credentials
  ↓
Generate JWT
  ↓
Store token in cookie
  ↓
Access protected routes
  ↓
Verify JWT
  ↓
Check user role
  ↓
Allow or reject request
```

If there is no valid token, the user receives a `401 Unauthorized` response.

If the user is authenticated but does not have the required role, the backend returns `403 Forbidden`.

## 👥 Role Based Authorization

The application has two roles:

```text
user
artist
```

The role is stored with the user's information and is also included in the JWT.

For example, artist specific routes check whether:

```text
role === "artist"
```

Only then is the artist allowed to perform operations such as uploading music.

This prevents a normal user from accessing artist specific functionality.

## ☁️ Music File Storage

The actual music files are stored using ImageKit.

MongoDB is used to store information about the music, while ImageKit is used to store the actual file.

The process looks like this:

```text
Artist uploads music
        ↓
Backend receives the file
        ↓
File is uploaded to ImageKit
        ↓
ImageKit returns the file URL
        ↓
Music details and URL are stored in MongoDB
```

This way, large music files do not need to be stored directly inside MongoDB.

## 🗄️ Database

MongoDB is used as the main database and Mongoose is used to interact with it.

### User

A user contains information such as:

```text
_id
username
email
password
role
```

The `role` determines whether the user is a normal user or an artist.

### Music

Music contains information such as:

```text
title
artist
music URL
album
```

### Album

An album contains information such as:

```text
title
artist
musics
```

The relationships between artists, albums, and music are handled using MongoDB references and Mongoose.

## 📡 API Overview

### Authentication

| Method | Endpoint         | Description         |
| ------ | ---------------- | ------------------- |
| POST   | `/auth/register` | Register a new user |
| POST   | `/auth/login`    | Login a user        |

### Music

| Method | Endpoint        | Description  |
| ------ | --------------- | ------------ |
| POST   | `/music/upload` | Upload music |
| GET    | `/music/...`    | Get music    |

### Albums

| Method | Endpoint           | Description          |
| ------ | ------------------ | -------------------- |
| POST   | `/albums`          | Create an album      |
| GET    | `/albums`          | Get all albums       |
| GET    | `/albums/:albumId` | Get a specific album |

> The exact endpoints may vary depending on the current implementation.

## ⚙️ Getting Started

### 1. Clone the repository

```bash
git clone <your-repository-url>
cd spotify-clone-backend
```

### 2. Install dependencies

```bash
npm install
```

### 3. Create a `.env` file

Add the required environment variables:

```env
PORT=3000

MONGODB_URI=your_mongodb_connection_string

JWT_SECRET=your_jwt_secret

IMAGEKIT_PRIVATE_KEY=your_imagekit_private_key
IMAGEKIT_PUBLIC_KEY=your_imagekit_public_key
IMAGEKIT_URL_ENDPOINT=your_imagekit_url_endpoint
```

### 4. Start the server

For development:

```bash
npm run dev
```

Or:

```bash
npm start
```

The server will run on:

```text
http://localhost:3000
```

## 🧪 Testing With Postman

The APIs were tested using Postman.

A typical flow is:

```text
Register User
      ↓
Login
      ↓
JWT Token
      ↓
Access Protected Routes
      ↓
Login as Artist
      ↓
Upload Music
      ↓
Create Album
      ↓
Add Music to Album
      ↓
Fetch Album
```

## 🔒 Security

Some of the security features implemented in this project are:

* Password hashing
* JWT authentication
* Cookie based authentication
* Protected routes
* Role based authorization
* Environment variables for sensitive information

The `.env` file should not be pushed to GitHub.

Add this to `.gitignore`:

```gitignore
node_modules/
.env
```

## 📚 What I Learned

While working on this project, I got practical experience with:

* Building REST APIs with Express.js
* Working with Node.js
* MongoDB and Mongoose
* User registration and login
* JWT authentication
* Cookies
* Middleware
* Role based authorization
* Password hashing
* File uploads
* Cloud storage with ImageKit
* API testing with Postman
* Structuring a backend project

## 🔮 Future Improvements

Some features I would like to add in the future:

* Music streaming
* Playlists
* Like and favorite songs
* Search for songs and artists
* Recently played songs
* Artist dashboard
* Music recommendations
* Album cover uploads
* Refresh token system
* Better validation and error handling

## 👨‍💻 Author

**Mayank Soni**

B.Tech Computer Science Engineering
VIT Bhopal University

# WOC 6.0: IRCTC Clone

> A train-ticket search and booking app modelled on IRCTC, built with React, Express and MongoDB for the WOC 2024 programme run by MSTC, DA-IICT.

![React](https://img.shields.io/badge/React-61DAFB?logo=react&logoColor=black)
![Node.js](https://img.shields.io/badge/Node.js-339933?logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?logo=mongodb&logoColor=white)
![Material UI](https://img.shields.io/badge/MUI-007FFF?logo=mui&logoColor=white)

## What it does

Users sign up, log in, enter a *from* station, a *to* station, a journey date and a class, and get a list of trains between those stations with their timings, classes and fares. They can then continue to a booking page and manage their account details.

The train and fare data is modelled on the response format of the [IRCTC RapidAPI](https://rapidapi.com/) (`irctc1.p.rapidapi.com`: `trainBetweenStations` and `getFare`). In the current code the live API calls are commented out and the pages render **bundled sample responses** instead, so search results are static.

## Features

- Sign up and log in (users stored in MongoDB).
- Protected pages: the `/private/*` routes redirect to login unless an `email` cookie is set.
- Train search between stations with a station-code picker, date and class filter.
- Train cards with timings, runs-on days and class types, and a fare lookup that leads to the booking page.
- Account page to view and update your profile, and log out.
- Backend `/booking` endpoint that stores a booking and rejects a duplicate for the same user, train and date.

## Tech stack

| Part | Tech |
| --- | --- |
| Frontend | React 18 (Create React App), React Router 6, Axios, Material UI, MDB React UI Kit, react-toastify, js-cookie |
| Backend | Node.js, Express 4, Mongoose 8, cors, dotenv |
| Database | MongoDB |
| Fonts | Poppins, Smooch Sans (bundled) |

## Project layout

```
backend/
  index.js          Express server and routes
  UsersModel.js     Mongoose user schema
  BookingModel.js   Mongoose booking schema
frontend/
  src/
    App.js          routes
    config.js       backend base URL
    pages/          Login, Signup, Home (search), Card, Booking, Account, Navbar, Footer, ...
```

## API (backend)

| Method | Route | Purpose |
| --- | --- | --- |
| GET | `/` | Health check |
| POST | `/login` | Check email and password |
| POST | `/Signup` | Register a user |
| POST | `/booking` | Store a booking |
| GET | `/user/:email` | Fetch a user's profile |
| POST | `/update_profile` | Update profile details |

## Getting started

Requirements: Node.js and a MongoDB database (local or hosted).

**Backend**

```bash
cd backend
npm install
```

Create `backend/.env` with your own values:

```
PORT=3001
MONGO_URL=<your MongoDB connection string>
FRONTEND_URL=http://localhost:3000
```

Then start it with `node index.js` (there is no `start` script).

**Frontend**

`frontend/src/config.js` points `BACKEND_API` at a hosted backend. To use your local server, set it to `null` (the pages then fall back to `http://localhost:3001`), then:

```bash
cd frontend
npm install
npm start
```

The app opens at http://localhost:3000.

## Status

A learning project from a college programme, not a production system. Known limitations: passwords are stored and compared in plain text, login state is a plain `email` cookie, and the train search uses sample data as described above. A real deployment would need hashed passwords, proper sessions or tokens, and rotated credentials.

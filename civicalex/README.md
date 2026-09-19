# CivicaLex

CivicaLex is a digital civic-legal assistance platform for Indian citizens. It combines a Node.js/Express web application with MongoDB storage and an AI-powered legal assistant powered by a Python FastAPI WebSocket backend.

## Key Features

- User registration, login, and session-based authentication
- Dashboard for managing legal cases, petitions, documents, and profiles
- Document upload and secure user document storage
- AI chatbot integration for legal research and assistance
- Browsing of Indian laws, acts, services, and legal resources
- CSRF protection, rate limiting, and secure HTTP headers via Helmet
- MongoDB data persistence with Mongoose models

## Architecture

- `server.js` – Express server and route configuration
- `routes/` – Application routes for auth, dashboard, law, acts, services, documents, petitions, search, and AI
- `models/` – Mongoose schemas for users, cases, documents, and petitions
- `views/` – Pug templates for rendered pages
- `public/` – Static assets served by Express
- `civicalexai.py` – Python FastAPI WebSocket backend that connects to the AI model

## Tech Stack

- Node.js + Express
- Pug view engine
- MongoDB + Mongoose
- Python + FastAPI
- WebSocket integration between Node and Python
- Google Gemini / Google ADK connection in Python

## Prerequisites

- Node.js installed
- Python installed
- MongoDB instance available
- Google Gemini API key for AI integration

## Environment Variables

Create a `.env` file in the project root with:

```env
SESSION_SECRET=your_session_secret
MONGODB_URI=mongodb://localhost:27017/civicalex
GOOGLE_API_KEY=your_google_gemini_api_key
NODE_ENV=development
PORT=3000
```

## Setup

1. Install Node dependencies:

```bash
npm install
```

2. Install Python dependencies in a virtual environment. The repository does not include a Python requirements file, so install the packages used by `civicalexai.py` manually, for example:

```bash
python -m venv venv
venv\Scripts\activate
pip install fastapi uvicorn google-genai google-adk
```

> If the `npm start` or `npm run dev` commands fail because `concurrently` is not installed, install it with:

```bash
npm install concurrently --save
```

## Running the Application

### Start the AI backend

```bash
python civicalexai.py
```

### Start the Node server

```bash
npm run dev
```

Alternatively, run each server separately:

```bash
node server.js
```

Then open:

```text
http://localhost:3000
```

## Project Structure

- `server.js` – application entry point
- `civicalexai.py` – AI assistant backend using FastAPI and WebSockets
- `routes/` – Express route handlers
- `models/` – Mongoose data models
- `views/` – Pug templates
- `public/` – static files
- `data/` – project data assets
- `private_uploads/` – upload storage (access blocked by middleware)

## Notes

- The Node app connects to the Python AI service at `ws://127.0.0.1:8000/ws`.
- CSRF is enabled for page routes; JSON API and dashboard routes are excluded by design.
- The AI backend expects `GOOGLE_API_KEY` to be available in the environment.

## License

This repository is licensed under ISC.

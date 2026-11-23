# FactoryHub - Backend

Backend API for FactoryHub, a factory management system that handles stock, products, invoices, customer accounts, and returns.

## Features

- Factory stock and inventory management
- Product management
- Invoices and billing
- Customer accounts
- Returns handling
- OTP-based password reset
- Bilingual interface support (Arabic/English)

## Tech Stack

- Node.js + Express
- MongoDB (Mongoose)
- JWT authentication

## Project Structure

- `config` - configuration files
- `controllers` - request handlers
- `middleware` - auth and validation middleware
- `models` - Mongoose schemas
- `routes` - API routes
- `services` - business logic
- `scripts` - utility scripts
- `uploads` - file uploads
- `server.js` - entry point

## Getting Started

1. Install dependencies: `npm install`
2. Create a `.env` file with your variables (database URI, JWT secret, port)
3. Start the server: `npm start`

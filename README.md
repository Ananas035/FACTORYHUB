# FactoryHub

FactoryHub is a full-stack garment factory management project with an Angular frontend and a Node.js/Express API backed by MongoDB.

## Features

- Products and inventory transactions
- Invoices, payments, checks and returns
- Customer accounts and account statements
- Email-verified signup/login and password reset
- JWT authentication and role-based API access
- Factory profile and logo upload
- Arabic/English interface

This repository is a development project. A feature list is not a claim of production readiness. Use synthetic data when demonstrating it.

## Stack

Angular, TypeScript, Tailwind CSS, Node.js, Express, MongoDB/Mongoose, Nodemailer and JWT.

## Repository layout

```text
Backend/                 Express API, models, services and routes
  README.md              Backend overview, preserved separately
  .env.example           Environment variable template, no credentials
  server.js              API entry point
Frontend/                Angular application
  src/app/               Pages, components, services and guards
  angular.json           Build configuration and budgets
README.md                Setup and project overview
```

## Prerequisites

- Node.js 22.23.5 and npm 11.6.2 were used for the checks described below. The frontend declares npm 11.6.2. Other versions have not been verified here.
- MongoDB, either local or an account/cluster you control
- An SMTP service/account for signup, login and password-reset emails

Use the same npm version when installing dependencies. npm 10 failed to install the frontend lockfile during review; npm 11.6.2 succeeded. Check versions with `node --version` and `npm --version`.

## Run locally

### 1. Clone the project

```bash
git clone https://github.com/Ananas035/FACTORYHUB.git
cd FACTORYHUB
```

### 2. Set up the backend

```bash
cd Backend
npm ci
```

Copy `.env.example` to `.env` in this folder. On macOS/Linux/Git Bash:

```bash
cp .env.example .env
```

On Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

Edit `.env` locally. Never commit actual credentials. Set:

- `MONGODB_URI` and `DB_NAME` for your database
- `JWT_SECRET` to a strong unique secret generated using a trusted password manager
- `OTP_HASH_SECRET` to a separate strong unique secret, recommended; the code falls back to `JWT_SECRET` if omitted
- `SMTP_HOST`, `SMTP_PORT`, `SMTP_SECURE`, `SMTP_USER`, `SMTP_PASS` and `SMTP_FROM` for your mail service
- `PORT` to `5000` for the current local frontend configuration

`SMTP_SECURE=true` is for implicit TLS, commonly port 465. Port 587 commonly uses `SMTP_SECURE=false` with STARTTLS. Follow your provider's requirements. Use a sender your provider allows. Do not use production customer addresses during development.

The template lists optional timeout/attempt/rate-limit overrides, left blank to use the code's defaults. Changing them is not necessary for basic local setup.

```bash
npm start
```

For development with file watching:

```bash
npm run dev
```

The API defaults to `http://localhost:5000`. A running process alone does not prove the database or email service works. Check startup logs and test the relevant flows. Without working SMTP configuration, OTP-based authentication cannot be completed.

### 3. Set up the frontend

In a second terminal, from the repository root:

```bash
cd Frontend
npm ci
npm start
```

Open `http://localhost:4200`.

## Checks

From `Frontend/`:

```bash
npm test -- --watch=false
npm run build
```

The frontend review ran 69 tests across 21 files successfully. Some component smoke tests made requests to an unavailable local backend, so this does not establish end-to-end behavior. Rerun checks after making changes.

The original production build failed on stylesheet size budgets. The accompanying configuration patch sets a 12 kB warning and 16 kB error threshold per component stylesheet. This changes the acceptance thresholds, not CSS size or runtime performance. The initial bundle warning remains at 500 kB; its 1 MB error threshold is unchanged. Consolidating repeated styles and reducing initial loading size remain useful follow-up work.

Backend automated test files are not included in the current repository. Broken scripts referring to missing files have been removed in the accompanying patch. No passing backend test suite is claimed. Restore real test files and scripts before claiming backend test coverage.

## Before a hosted demo

- Configure the frontend API URL and backend CORS for the actual deployment origins. Current source defaults point to `http://localhost:5000/api` and `http://localhost:4200`.
- Use HTTPS and private environment variables on the host.
- Review dependency security advisories and test any updates. Do not assume a successful build is a security review.
- Verify database, email, authentication, role restrictions and business flows with synthetic data.
- Confirm a supported way to create the demo administrator; do not publish real account credentials.
- Check desktop/mobile layouts and both languages.

Do not publish customer data, private factory records or credentials in screenshots or demo data.

## Portfolio presentation

Add real screenshots of the dashboard, products/inventory, invoices and customer statements, including mobile views. State your own contribution and distinguish training/personal work from client work. Confirm rights to any branding, uploaded images and data before sharing. A short walkthrough can demonstrate flows without exposing credentials.

## Documentation

See `Backend/README.md` for the existing backend overview. This root guide supplies the shared setup instructions. The frontend README also contains Angular CLI reference material.

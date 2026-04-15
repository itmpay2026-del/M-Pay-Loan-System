# 🚀 M-PAY LOAN SYSTEM

A polished Node.js system for a user-to-user lending platform with staff support, loan management, automatic repayment handling, and M-Pay Helper chatbot.

---

## ✨ What makes this special

- Fast, synchronous SQLite backend with `better-sqlite3`
- Auto repayment and overdue detection logic
- Staff dashboards via secure header access
- Support ticket integration for customer service workflows
- Lightweight scheduler for recurring loan checks
- Docker-ready deployment with a dedicated `Dockerfile` and `docker-compose.yml`

---

## ⚙️ Quick Start

```bash
npm install
npm start
```

Then open:

```bash
http://localhost:3000
```

> Default port: `3000`

---

## 🚀 Deployment

### Local container deployment

Build the Docker image:

```bash
docker build -t peer-to-peer-loans .
```

Run the app:

```bash
docker run -p 3000:3000 peer-to-peer-loans
```

### Docker Compose (recommended)

```bash
docker compose up -d
```

This uses:

- `Dockerfile` for the app image
- `docker-compose.yml` for port mapping and volume persistence

### Persistent database storage

Keep `loans.db` outside the container so data survives restarts:

```bash
docker run -p 3000:3000 -v "%cd%/loans.db:/app/loans.db" peer-to-peer-loans
```

---

## 🧪 API Overview

### Users

- `POST /users` — create a user
- `GET /users/search?query=` — search by ID, username, phone, or SIM
- `GET /users/:userId/loans` — borrower/lender loans
- `GET /users/:userId/balance` — wallet balance
- `GET /users/:userId/transactions` — transaction history
- `POST /users/:userId/deposit` — deposit funds and trigger auto repayment

### Loans

- `POST /loans/request` — request a loan
- `POST /loans/:loanId/accept` — lender accepts a loan
- `POST /loans/:loanId/repay` — record repayment
- `POST /loans/:loanId/incoming-payment` — auto deduction from incoming funds
- `GET /loans/:loanId/repayments` — repayment history
- `GET /loans/:loanId/support` — support tickets for loan

### Support

- `POST /support/ticket` — create a support ticket
- `POST /support/ticket/:ticketId/resolve` — resolve a ticket

### Staff endpoints

- `GET /staff/loans` — view all loans
- `GET /staff/reminders` — upcoming loan reminders
- `POST /staff/scheduler/run` — manually run scheduler
- `GET /staff/tickets` — view open support tickets

> All staff routes require the `x-staff-key` header.

---

## 🔔 Notes

- Loans can auto-deduct from incoming payments or use scheduled installments
- Overdue loans are tracked and escalate with support workflow
- M-Pay Helper chatbot provides 24/7 assistance for loan-related queries
- This repo is a prototype; add authentication, validation, and security before live use

---

## 🌐 Environment Variables

- `PORT` — server port (default: `3000`)

---

## 📌 Recommended next steps

- Add user authentication and role-based access control
- Store data in a managed database for production
- M-Pay Helper is functional; enhance with AI for better responses if needed
- Add frontend UI for better borrower/lender experience

---

> Ready to deploy with Docker? Use `docker compose up -d` and your special prototype is live in seconds.

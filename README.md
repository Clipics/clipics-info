# 📸 Clipics

> A two-sided marketplace connecting clients with freelance photographers and videographers.  
> Think Airbnb for creative talent — creators list their services, clients browse and book.

**Status:** Early-stage · Active development  
**This repo is private.** Happy to walk through the code or architecture — [get in touch](#contact).

---

## 🧱 Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python · Django · Django REST Framework |
| Frontend | React · TypeScript |
| Database | MySQL |
| Media Storage | Cloudflare R2 |
| CDN | Cloudflare CDN |
| Background Tasks | Redis · Celery |
| Web Server | Gunicorn · Nginx |
| Hosting | Render |

---

## 🏗️ Architecture

```
User → Cloudflare CDN → Render (Django API + React) → MySQL

Media uploads  →  Cloudflare R2  →  served via Cloudflare CDN
Heavy tasks    →  Redis queue    →  Celery workers
```

- The Django backend exposes a **REST API** via Django REST Framework
- The React (TypeScript) frontend is served within the Django project
- Media files are stored in **Cloudflare R2** and referenced by URL in MySQL — binary data is never stored in the database
- Background jobs (e.g. notifications, processing) run asynchronously via **Celery** with Redis as the broker
- Three environments: local dev, staging (Render + managed services), and production

---

## 🗂️ Domain Models

| Model | Description |
|---|---|
| `User` | Can be a creator, a client, or both |
| `CreatorProfile` | Portfolio, availability, rates, service types |
| `Booking` | Connects a client to a creator for a specific job |
| `Review` | Left by clients after a completed booking |
| `Message` | In-platform messaging between users |
| `MediaFile` | References to files in Cloudflare R2 |
| `PaymentMetadata` | Payment records (processing handled externally) |

---

## 📁 Backend Structure

Django apps are kept small and domain-focused:

```
bookings/      # Booking lifecycle and management
creators/      # Creator profiles and availability
messaging/     # In-platform messaging
payments/      # Payment metadata and records
```

Each app follows DRF conventions — serializers and viewsets for API endpoints, `tasks.py` for Celery jobs.

---

## ⚙️ Key Conventions

- All credentials and external config via **environment variables** — nothing hardcoded
- **TypeScript strict mode** on the frontend
- Migrations written manually when auto-generated output needs clarification
- Destructive or irreversible database changes are always flagged before running

---

## 👩‍💻 My Role

Co-founder and junior developer. My contributions include:

- Designing and building the REST API (serializers, viewsets, URL routing)
- Modelling the core domain and database schema
- Integrating Cloudflare R2 for media uploads and CDN delivery
- Setting up async task processing with Redis and Celery
- Collaborating on product, technical, and business decisions

---

## 📩 Contact

This repo is private, but I'm happy to share code samples or do a technical walkthrough.

[![Email](https://img.shields.io/badge/Email-silvia.scivales%40gmail.com-blue?style=flat&logo=gmail)](mailto:silvia.scivales@gmail.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Silvia%20Scivales-blue?style=flat&logo=linkedin)](https://www.linkedin.com/in/silviascivales/)

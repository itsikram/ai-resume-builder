# ChakriCV — AI Resume Builder SaaS for Bangladesh

Production-ready MERN stack SaaS platform for building ATS-optimized resumes, cover letters, and career documents. Powered by **Google Gemini 2.5 Flash**.

![Stack](https://img.shields.io/badge/Stack-MERN-blue)
![TypeScript](https://img.shields.io/badge/TypeScript-5.7-blue)
![License](https://img.shields.io/badge/License-MIT-green)

## Features

- **AI Resume Generator** — Professional summaries, bullet points, skills (Gemini 2.5 Flash)
- **AI Resume Improver** — Keyword optimization from job descriptions + ATS score
- **ATS Score Checker** — Detailed compatibility analysis
- **Cover Letter Generator** — Personalized letters with PDF export
- **Resume Templates** — ATS, Bangladeshi CV, international formats
- **Drag-and-drop section ordering** — Reorder resume sections
- **Real-time preview** — Live resume preview while editing
- **PDF Export** — Free plan includes watermark; Premium removes it
- **Public resume sharing** — Share via public link
- **Bilingual** — English + Bangla (বাংলা)
- **Dark/Light mode**
- **Authentication** — JWT + Google OAuth + email verification + password reset
- **Payments** — SSLCommerz, bKash, Nagad (integration-ready)
- **Subscription plans** — Free (2 resumes) & Premium (unlimited)
- **Referral & coupon system**
- **Admin panel** — Users, revenue, coupons, templates, blogs
- **Blog & SEO** — Sitemap, OpenGraph, schema markup

## Tech Stack

| Layer | Technology |
|-------|------------|
| Frontend | React 19, Vite, TypeScript, TailwindCSS, shadcn/ui, Zustand, TanStack Query, Framer Motion |
| Backend | Node.js, Express, TypeScript, MVC architecture |
| Database | MongoDB (Mongoose) |
| Cache | Redis (ioredis) |
| AI | Google Gemini 2.5 Flash |
| Auth | JWT + Google OAuth |
| Payments | SSLCommerz, bKash, Nagad |
| Email | Nodemailer |
| Files | Cloudinary |
| PDF | PDFKit |
| Security | Helmet, rate limiting, mongo-sanitize, Zod validation |

## Project Structure

```
chakricv/
├── client/                 # React frontend (Vite)
│   ├── src/
│   │   ├── components/     # UI, layout, resume, auth
│   │   ├── pages/          # Landing, dashboard, admin
│   │   ├── store/          # Zustand stores
│   │   ├── i18n/           # en + bn translations
│   │   └── lib/            # API client, utils
│   └── Dockerfile
├── server/                 # Express API
│   ├── src/
│   │   ├── config/         # DB, Redis, env
│   │   ├── controllers/    # MVC controllers
│   │   ├── middleware/     # Auth, validation, rate limit
│   │   ├── models/         # Mongoose schemas
│   │   ├── routes/         # API routes
│   │   ├── services/       # AI, PDF, payment, email
│   │   └── scripts/        # Seed data
│   └── Dockerfile
├── docker-compose.yml
└── README.md
```

## Quick Start

### Prerequisites

- Node.js 20+
- MongoDB (local or Atlas)
- Redis (optional, recommended)
- Gemini API key

### 1. Clone & install

```bash
git clone <repo-url>
cd Ai-resume-builder
npm install
cd server && npm install
cd ../client && npm install
```

### 2. Environment setup

```bash
cp server/.env.example server/.env
cp client/.env.example client/.env
```

Edit `server/.env` with your credentials (minimum):

```env
MONGODB_URI=mongodb://localhost:27017/chakricv
JWT_SECRET=your-32-char-minimum-secret-key-here
JWT_REFRESH_SECRET=your-32-char-refresh-secret-key
GEMINI_API_KEY=your-gemini-api-key
CLIENT_URL=http://localhost:5173
```

### 3. Seed database

```bash
cd server
npm run seed
```

Default admin: `admin@chakricv.com` / `Admin@123456`

### 4. Run development

```bash
# From root — runs API + frontend concurrently
npm run dev
```

- Frontend: http://localhost:5173
- API: http://localhost:5000/api/v1/health

### Docker

```bash
docker-compose up -d
npm run seed --prefix server
```

## API Documentation

Base URL: `http://localhost:5000/api/v1`

See [docs/API.md](docs/API.md) for full endpoint reference.

### Key endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/auth/register` | Register user |
| POST | `/auth/login` | Login |
| POST | `/auth/google` | Google OAuth |
| GET | `/resumes` | List resumes |
| POST | `/resumes` | Create resume |
| POST | `/resumes/ai/generate` | AI generate content |
| POST | `/resumes/ai/ats-check` | ATS analysis |
| POST | `/cover-letters/generate` | AI cover letter |
| GET | `/payments/plans` | Subscription plans |
| POST | `/payments/sslcommerz` | Initiate payment |
| GET | `/admin/dashboard` | Admin stats |

## Deployment

### Frontend (Vercel)

1. Set root directory to `client`
2. Build command: `npm run build`
3. Output: `dist`
4. Env: `VITE_API_URL=https://your-api.com/api/v1`

### Backend (Railway / Render)

1. Set root directory to `server`
2. Build: `npm run build`
3. Start: `npm start`
4. Add MongoDB Atlas + Redis URLs to env

### MongoDB Atlas

Use connection string in `MONGODB_URI`:
```
mongodb+srv://user:pass@cluster.mongodb.net/chakricv
```

## Subscription Plans

| Feature | Free | Premium |
|---------|------|---------|
| Resumes | 2 | Unlimited |
| AI requests/month | 5 | 100 |
| PDF watermark | Yes | No |
| Premium templates | No | Yes |
| ATS checker | No | Yes |
| Cover letters | No | Yes |
| AI optimization | No | Yes |
| Price | ৳0 | ৳499/mo |

Coupon code `CHAKRI20` — 20% off Premium (seeded).

## Payment Setup

### SSLCommerz
Set `SSL_STORE_ID`, `SSL_STORE_PASS`, callback URLs in `.env`.

### bKash / Nagad
Structure is ready; configure sandbox credentials and complete token APIs in `payment.service.ts`.

## License

MIT — Built for the Bangladesh job market 🇧🇩

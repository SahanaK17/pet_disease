# PetCare AI — AI-Powered Pet Disease Detection

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white)
![React](https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![Google Gemini](https://img.shields.io/badge/Google%20Gemini-8E75B2?logo=google&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-646CFF?logo=vite&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/Tailwind%20CSS-4-06B6D4?logo=tailwindcss&logoColor=white)

An AI-assisted pet health screening application that uses **Google Gemini** vision models to analyze pet images, detect potential diseases, highlight affected areas, and provide informational care guidance — all through a modern, responsive web interface.

> **Disclaimer:** This tool is for **informational and educational purposes only**. AI-generated findings may be inaccurate or incomplete and **do not constitute a veterinary diagnosis**. Always consult a qualified veterinarian for medical concerns about your pet.

---

## Table of Contents

- [Screenshots](#screenshots--application-preview)
- [Overview](#overview)
- [Key Features](#key-features)
- [Application Workflow](#application-workflow)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation & Setup](#installation--setup)
- [Environment Variables](#environment-variables)
- [Running the Application](#running-the-application)
- [API Documentation](#api-documentation)
- [API Endpoints](#api-endpoints)
- [Database](#database)
- [Security & Privacy](#security--privacy)
- [Known Limitations](#known-limitations)
- [Future Improvements](#future-improvements)
- [Disclaimer](#disclaimer)

---

## Screenshots / Application Preview

### Dashboard

The main dashboard provides a real-time overview of all scan activity — total scans, healthy vs. unhealthy counts, weekly scan trends, and a breakdown of the most frequently detected diseases.

<p align="center">
  <img src="docs/images/dashboard.png" alt="PetCare AI Dashboard" width="800" />
</p>

### AI Disease Scan — Workflow

The scan page guides users through a multi-step AI analysis pipeline. Each stage — image upload, pet validation, disease detection, diagnosis generation, and result preparation — updates in real time with progress indicators.

<p align="center">
  <img src="docs/images/scan-workflow.png" alt="AI Scan Workflow Progress" width="800" />
</p>

### Scan Results & Diagnosis

Completed scans display the uploaded image with AI-generated bounding boxes highlighting affected regions, alongside a structured diagnosis panel covering the disease overview, common symptoms, and veterinary treatment options.

<p align="center">
  <img src="docs/images/scan-results.png" alt="Scan Results with Bounding Boxes and Diagnosis" width="800" />
</p>

### Knowledge Base

A searchable encyclopedia of 60+ pet diseases organized by category (skin diseases, eye infections, parasites, wounds, and treatments). Each entry includes the affected animal type and expandable treatment details.

<p align="center">
  <img src="docs/images/knowledge-base.png" alt="Disease Knowledge Base" width="800" />
</p>

### API Documentation (Swagger UI)

All backend endpoints are documented via auto-generated Swagger UI, enabling interactive exploration and testing of every API route.

<p align="center">
  <img src="docs/images/swagger-api.png" alt="Swagger API Documentation" width="800" />
</p>

---

## Overview

PetCare AI is a full-stack web application that combines a **FastAPI** backend with a **React + TypeScript** frontend to deliver AI-powered pet health screening. Users upload a photo of their pet, and the system uses Google Gemini's multimodal capabilities to:

1. **Validate** that the image contains a recognizable pet
2. **Analyze** the image for visible signs of disease or abnormalities
3. **Generate bounding boxes** around affected areas for spatial visualization
4. **Produce a structured diagnosis** with disease details, symptoms, severity, and care recommendations
5. **Cross-reference** results against a built-in knowledge base of common pet diseases and treatments

All scan results are persisted in a PostgreSQL database, enabling users to review their scan history, view detailed reports, and track pet health over time through an interactive dashboard.

---

## Key Features

| Feature | Description |
|---|---|
| **AI Image Analysis** | Upload pet photos for automated health screening via Google Gemini vision models |
| **Bounding Box Detection** | Affected areas are visually highlighted with AI-generated bounding boxes |
| **Structured Diagnosis** | Detailed disease information including symptoms, severity, pathogen type, and transmission mode |
| **Care Recommendations** | Home care tips, veterinary treatment guidance, and emergency triage |
| **Disease Knowledge Base** | Searchable database of common pet diseases with curated treatment information |
| **Pet Profiles** | Register and manage individual pet profiles (name, type, age, gender) |
| **Scan History** | Browse and review all previous scan records with timestamps |
| **Dashboard & Statistics** | Visual overview of scan counts, health/unhealthy ratios, and top detected diseases |
| **Printable Reports** | Generate detailed scan reports for sharing or veterinary reference |
| **Interactive API Docs** | Auto-generated Swagger UI for all backend endpoints |
| **Optional S3 Storage** | Configurable AWS S3 integration for image and bounding-box data persistence |

---

## Application Workflow

```
 Upload Image ──> Pet Validation ──> Disease Analysis ──> Bounding Box Detection
                       |                    |                       |
                       v                    v                       v
               Is it a pet?        QA + Diagnostic         Affected area coords
                   |                   prompts                     |
                   v                    |                          v
             [Reject if not]           v                   Spatial overlay
                              Combine Results ──> Save to PostgreSQL
                                      |
                                      v
                          Results Page / Report / Dashboard
                                      |
                                      v
                     KB Lookup + AI Diagnosis + Recommendations
```

1. **Upload** — The user submits a pet image through the scan page
2. **Validation** — Gemini verifies the image contains a recognizable pet
3. **QA Analysis** — A quick health check identifies the pet type and any suspected condition
4. **Bounding Boxes** — Affected areas are localized with coordinate-based bounding boxes
5. **Persistence** — Combined results are stored as a scan record in PostgreSQL
6. **Diagnosis** — A detailed diagnosis is generated with disease overview, symptoms, and care guidance
7. **Knowledge Base** — The system cross-references detected conditions against the curated KB
8. **Recommendations** — Home care and emergency triage guidance is provided based on severity

---

## Technology Stack

| Layer | Technologies |
|---|---|
| **Frontend** | React 19, TypeScript, Vite, Tailwind CSS 4, Framer Motion |
| **UI Libraries** | Lucide React, Recharts, React Dropzone, React Hot Toast, Sonner |
| **State Management** | Zustand |
| **Routing** | React Router DOM v7 |
| **HTTP Client** | Axios |
| **Backend** | Python, FastAPI, Uvicorn |
| **AI / Vision** | Google Gemini API (`google-genai` SDK) |
| **Database** | PostgreSQL, SQLAlchemy (async), asyncpg |
| **Migrations** | Alembic |
| **Data Processing** | Pandas (knowledge base CSV loading) |
| **Optional Storage** | AWS S3 (Boto3) |
| **Validation** | Pydantic, Pydantic Settings |

---

## Project Structure

```
pet_disease/
├── app/
│   ├── config/
│   │   └── settings.py            # Pydantic-based app configuration
│   ├── models/
│   │   ├── pet.py                 # Pet profile model
│   │   ├── pet_kb.py              # Knowledge base model
│   │   └── pet_scan.py            # Scan record model + SQLAlchemy Base
│   ├── routers/
│   │   └── v1/
│   │       ├── diagnosis.py       # Combined diagnosis endpoint
│   │       ├── health.py          # Health check endpoint
│   │       ├── kb.py              # Knowledge base CRUD
│   │       ├── pets.py            # Pet scan (upload + analyze)
│   │       ├── pets_entity.py     # Pet profile CRUD
│   │       ├── recommendations.py # Home care & emergency triage
│   │       ├── scans.py           # Scan history & management
│   │       ├── stats.py           # Dashboard statistics
│   │       └── vision.py          # Standalone vision endpoints
│   ├── schemas/
│   │   └── pets.py                # Pydantic request/response schemas
│   ├── services/
│   │   ├── gemini.py              # Google Gemini AI service
│   │   ├── knowledge.py           # CSV-based knowledge base service
│   │   ├── retry.py               # Async retry utility
│   │   └── s3.py                  # AWS S3 upload service
│   └── utils/
│       └── db_init.py             # Async SQLAlchemy engine & session
├── frontend/
│   ├── src/
│   │   ├── api/                   # Axios API client modules
│   │   ├── assets/                # Static images and icons
│   │   ├── components/
│   │   │   ├── common/            # Navbar, Sidebar
│   │   │   ├── diagnosis/         # DiagnosisCard, SeverityBadge
│   │   │   └── scan/              # BoundingBoxViewer, ScanProgress
│   │   ├── layouts/               # AppLayout wrapper
│   │   ├── pages/                 # All page components
│   │   ├── routes/                # ProtectedRoute guard
│   │   ├── store/                 # Zustand stores (auth, scan, ui)
│   │   └── types/                 # TypeScript type definitions
│   ├── index.html
│   ├── package.json
│   ├── vite.config.ts
│   └── tsconfig.json
├── knowledge_base/
│   └── pet_kb.csv                 # Curated disease-treatment data
├── migrations/
│   └── env.py                     # Alembic migration environment
├── .env.example                   # Environment variable template
├── .gitignore
├── alembic.ini                    # Alembic configuration
├── main.py                        # Application entry point
└── requirements.txt               # Python dependencies
```

---

## Prerequisites

Before setting up the project, ensure you have the following installed:

- **Python 3.10** or later
- **Node.js 18+** and **npm**
- **PostgreSQL** (running locally or accessible remotely)
- A **Google Gemini API key** — obtain one from [Google AI Studio](https://aistudio.google.com/apikey)

> **Note:** AWS credentials are optional. S3 integration is not required for local development and will gracefully degrade if unconfigured.

---

## Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/SahanaK17/pet_disease.git
cd pet_disease
```

### 2. Create a Python Virtual Environment

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

### 3. Install Backend Dependencies

```powershell
pip install -r requirements.txt
```

### 4. Create the PostgreSQL Database

Create a database named `pet_disease` in your local PostgreSQL instance:

```sql
CREATE DATABASE pet_disease;
```

Ensure the username, password, host, port, and database name match the `DATABASE_URL` you will configure in the next step.

### 5. Configure Environment Variables

Copy the example template and fill in your credentials:

**Windows PowerShell:**
```powershell
Copy-Item .env.example .env
```

**macOS / Linux:**
```bash
cp .env.example .env
```

Edit `.env` with your values (see [Environment Variables](#environment-variables) below).

> **Important:** Never commit your `.env` file. It is excluded by `.gitignore`.

### 6. Install Frontend Dependencies

```powershell
cd frontend
npm install
cd ..
```

---

## Environment Variables

Create a `.env` file in the project root using `.env.example` as a template:

```dotenv
# Required: Google Gemini API key
GEMINI_API_KEY=your_gemini_api_key_here

# Gemini model configuration
GEMINI_MODEL_PRIMARY=gemini-2.0-flash
GEMINI_MODEL_FALLBACK=gemini-2.0-flash

# Required: PostgreSQL connection string (async driver)
DATABASE_URL=postgresql+asyncpg://your_username:your_password@localhost:5432/pet_disease

# Optional: AWS S3 configuration (leave empty for local-only mode)
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_REGION=us-east-1
S3_BUCKET_IMAGES=
S3_BUCKET_BBOX=
```

| Variable | Required | Description |
|---|---|---|
| `GEMINI_API_KEY` | **Yes** | Google Gemini API key for AI vision analysis |
| `GEMINI_MODEL_PRIMARY` | No | Primary Gemini model (default: `gemini-2.0-flash`) |
| `GEMINI_MODEL_FALLBACK` | No | Fallback model used on primary failure (default: `gemini-2.0-flash`) |
| `DATABASE_URL` | **Yes** | PostgreSQL async connection string |
| `AWS_ACCESS_KEY_ID` | No | AWS access key for S3 uploads |
| `AWS_SECRET_ACCESS_KEY` | No | AWS secret key for S3 uploads |
| `AWS_REGION` | No | AWS region (default: `us-east-1`) |
| `S3_BUCKET_IMAGES` | No | S3 bucket name for original images |
| `S3_BUCKET_BBOX` | No | S3 bucket name for bounding-box JSON |

---

## Running the Application

### Start the Backend

From the project root (with your virtual environment activated):

```powershell
python main.py
```

The FastAPI server starts on **http://localhost:8001**. Database tables are automatically created on startup if they do not already exist.

### Start the Frontend

In a separate terminal:

```powershell
cd frontend
npm run dev
```

The Vite development server starts on **http://localhost:5173**. API requests to `/api/*` are automatically proxied to the backend.

### Access the Application

| URL | Description |
|---|---|
| http://localhost:5173 | Frontend application |
| http://localhost:8001/docs | Swagger UI — interactive API documentation |
| http://localhost:8001/api/v1/health | Backend health check |

---

## API Documentation

FastAPI auto-generates interactive API documentation via **Swagger UI**, available at:

**http://localhost:8001/docs**

All endpoints are versioned under the `/api/v1` prefix. Use the Swagger interface to explore request/response schemas, test endpoints, and review available parameters.



---

## API Endpoints

| Method | Endpoint | Tag | Description |
|---|---|---|---|
| `GET` | `/api/v1/health` | Health | Backend health check |
| `POST` | `/api/v1/pets/scan` | Scan | Upload image for full AI analysis |
| `GET` | `/api/v1/scans/` | Scans | List all scans (paginated) |
| `GET` | `/api/v1/scans/{scan_id}` | Scans | Get scan details by ID |
| `GET` | `/api/v1/scans/{scan_id}/summary` | Scans | Get brief health summary |
| `GET` | `/api/v1/scans/{scan_id}/diagnosis` | Scans | Combined diagnosis with KB + AI |
| `DELETE` | `/api/v1/scans/{scan_id}` | Scans | Delete a scan record |
| `POST` | `/api/v1/vision/validate` | Vision | Validate if image contains a pet |
| `POST` | `/api/v1/vision/bboxes` | Vision | Generate bounding boxes for affected areas |
| `GET` | `/api/v1/kb/` | Knowledge Base | List KB entries (filterable) |
| `GET` | `/api/v1/kb/treatment` | Knowledge Base | Look up treatment by pet + disease |
| `GET` | `/api/v1/kb/diseases` | Knowledge Base | List distinct diseases in KB |
| `POST` | `/api/v1/kb/` | Knowledge Base | Add a new KB entry |
| `PUT` | `/api/v1/kb/{id}` | Knowledge Base | Update a KB entry |
| `DELETE` | `/api/v1/kb/{id}` | Knowledge Base | Delete a KB entry |
| `POST` | `/api/v1/pets/` | Pets | Create a pet profile |
| `GET` | `/api/v1/pets/` | Pets | List all pet profiles |
| `GET` | `/api/v1/pets/{pet_id}` | Pets | Get pet profile by ID |
| `POST` | `/api/v1/recommendations/home-care` | Recommendations | Get home care guidance |
| `POST` | `/api/v1/recommendations/emergency` | Recommendations | Emergency triage check |
| `GET` | `/api/v1/stats/scans` | Stats | Scan count statistics |
| `GET` | `/api/v1/stats/diseases` | Stats | Top detected diseases |

---

## Database

### Schema

The application uses three PostgreSQL tables, managed via SQLAlchemy ORM:

| Table | Description | Key Columns |
|---|---|---|
| `pet_scans` | Stores scan results | `id`, `is_valid_pet`, `is_healthy`, `result` (JSON), `created_at` |
| `pets` | Pet profile records | `id`, `pet_name`, `pet_type`, `age`, `gender`, `created_at` |
| `pet_kb` | Knowledge base entries | `id`, `pet_name`, `disease_name`, `treatment` |

### Auto-Creation

Tables are **automatically created** on application startup via `Base.metadata.create_all()`. No manual migration is required for initial setup.

### Alembic Migrations

Alembic is configured for schema migrations. The `migrations/` directory and `alembic.ini` are present, but **no migration versions have been generated yet**. To use Alembic for future schema changes:

```powershell
# Generate a new migration after modifying models
alembic revision --autogenerate -m "description"

# Apply migrations
alembic upgrade head
```

> **Note:** Update the `sqlalchemy.url` in `alembic.ini` to match your database credentials before running migrations.

---

## Security & Privacy

- **Keep `.env` files private.** The `.gitignore` is configured to exclude `.env` and all `.env.*` variants (except `.env.example`).
- **Use `.env.example` only as a template** with placeholder values — never include real credentials.
- **Do not commit** virtual environments, `node_modules/`, local databases, logs, or build artifacts.
- **Review uploaded images** and scan data before sharing or publishing. Uploaded images are processed in-memory and are not persistently stored locally unless S3 is configured.
- **API keys** (Gemini, AWS) should be rotated periodically and restricted to the minimum required permissions.

---

## Known Limitations

- **AI accuracy is not guaranteed.** Gemini-generated findings may be inaccurate, incomplete, or misleading. No clinical accuracy benchmarks or diagnostic performance metrics are claimed.
- **No persistent local image storage.** Uploaded images are analyzed in-memory and discarded after processing. Re-analysis of past scans is not available without S3 configuration.
- **Knowledge base scope is limited.** The built-in KB (`pet_kb.csv`) contains a curated but small set of common dog and cat diseases. It is not comprehensive.
- **Authentication is client-side only.** The `ProtectedRoute` guard and auth store provide UI-level route protection but do not enforce server-side authentication or authorization.
- **No automated test suite.** The project does not currently include backend or frontend tests.
- **Single-user design.** There is no multi-tenancy, user accounts, or role-based access control on the backend.
- **Gemini API rate limits** may affect availability during heavy usage. The service includes retry logic with fallback model support.

---

## Future Improvements

- [ ] Add comprehensive backend and frontend test suites
- [ ] Implement server-side authentication and authorization (JWT / OAuth)
- [ ] Expand the knowledge base with additional species, diseases, and treatments
- [ ] Support persistent local image storage as an alternative to S3
- [ ] Enable scan re-analysis from stored images
- [ ] Add multi-language support for diagnosis output
- [ ] Implement user accounts with scan history per user
- [ ] Add input validation and file-type restrictions on the backend
- [ ] Evaluate and document model performance on a representative dataset
- [ ] Add deployment guides for cloud platforms
- [ ] Implement data retention policies and privacy controls

---

## Disclaimer

**PetCare AI is not a substitute for professional veterinary care.**

This application provides AI-generated health screening information for educational and informational purposes only. The analysis is based on visual assessment by Google Gemini and may contain errors, false positives, or false negatives.

- AI-generated findings **do not constitute a medical or veterinary diagnosis**.
- Results should **never** be used as the sole basis for treatment decisions.
- If your pet is unwell or showing concerning symptoms, **consult a qualified veterinarian immediately**.

The developers make no warranties regarding the accuracy, reliability, or completeness of the AI-generated analysis.

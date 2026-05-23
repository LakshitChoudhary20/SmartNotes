<div align="center">

<h1>📝 SmartNotes</h1>

<p><strong>A full-stack note-taking application built and deployed with a complete DevOps pipeline</strong></p>

<p>
  <a href="http://65.2.129.28:3000" target="_blank">
    <img src="https://img.shields.io/badge/🌐%20Live%20Demo-AWS%20EC2-orange?style=for-the-badge" alt="Live Demo"/>
  </a>
  <img src="https://img.shields.io/badge/Spring%20Boot-3.x-6DB33F?style=for-the-badge&logo=springboot&logoColor=white" alt="Spring Boot"/>
  <img src="https://img.shields.io/badge/PostgreSQL-17-4169E1?style=for-the-badge&logo=postgresql&logoColor=white" alt="PostgreSQL"/>
  <img src="https://img.shields.io/badge/Docker-Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker"/>
  <img src="https://img.shields.io/badge/Jenkins-CI%2FCD-D24939?style=for-the-badge&logo=jenkins&logoColor=white" alt="Jenkins"/>
  <img src="https://img.shields.io/badge/AWS-EC2-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white" alt="AWS EC2"/>
</p>

<p>
  <a href="https://github.com/lakshitchoudhary20/smartnotes/actions">
    <img src="https://img.shields.io/github/actions/workflow/status/lakshitchoudhary20/smartnotes/ci.yml?branch=main&label=CI%20Build&style=flat-square&logo=github" alt="CI Status"/>
  </a>
  <img src="https://img.shields.io/github/last-commit/lakshitchoudhary20/smartnotes?style=flat-square" alt="Last Commit"/>
  <img src="https://img.shields.io/github/license/lakshitchoudhary20/smartnotes?style=flat-square" alt="License"/>
</p>

</div>

---

## 🚀 Live Application

> **The application is deployed on AWS EC2 and accessible at:**
>
> ### 🌐 [http://65.2.129.28:3000](http://65.2.129.28:3000)
>
> | Service  | URL |
> |----------|-----|
> | Frontend | [http://65.2.129.28:3000](http://65.2.129.28:3000) |
> | Backend API | [http://65.2.129.28:8081/notes](http://65.2.129.28:8081/notes) |

---

## 📸 Screenshots

> **📌 Screenshots are placed in the `/screenshots` folder. Capture and add them as described below.**

### Application UI — Home Page
![SmartNotes Home Page](screenshots/01_app_home.png)
> *The SmartNotes main interface with input fields for Title and Content, and the notes list below.*

### Adding a New Note
![Adding a New Note](screenshots/02_add_note.png)
> *Filling in the title and content fields and clicking "Add Note".*

### Notes List — After Adding Notes
![Notes List](screenshots/03_notes_list.png)
> *Multiple notes displayed on the page fetched from the PostgreSQL database via the Spring Boot API.*

### Backend REST API — `/notes` Endpoint
![Backend API Response](screenshots/05_api_response.png)
> *Raw JSON response from `http://65.2.129.28:8081/notes` showing all stored notes.*

### GitHub Actions CI Pipeline — Build Success
![GitHub Actions CI](screenshots/06_github_actions_ci.png)
> *GitHub Actions workflow triggered on push to `main` — builds the Spring Boot backend using Maven.*

### Jenkins CD Pipeline — Deployment to AWS EC2
![Jenkins Pipeline](screenshots/07_jenkins_pipeline.png)
> *Jenkins pipeline with Checkout and Deploy stages, showing successful deployment to the EC2 instance.*

### Docker Containers Running on EC2
![Docker Containers on EC2](screenshots/08_docker_ps.png)
> *Output of `docker ps` on the EC2 instance, showing frontend, backend, and postgres containers running.*

---

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                        Developer (Local)                         │
│                     git push → main branch                       │
└────────────────────────────┬────────────────────────────────────┘
                             │
              ┌──────────────▼──────────────┐
              │       GitHub Repository      │
              │  github.com/abhinavshiv7/    │
              │    smartnotes-project        │
              └──────┬───────────┬──────────┘
                     │           │
          ┌──────────▼──┐   ┌───▼────────────┐
          │ GitHub Actions│   │    Jenkins      │
          │  CI Pipeline  │   │  CD Pipeline   │
          │ (Build & Test)│   │ (SSH → EC2)    │
          └──────────────┘   └───────┬────────┘
                                     │  SSH Deploy
                          ┌──────────▼──────────────┐
                          │       AWS EC2 Instance   │
                          │      (Ubuntu, t2.micro)  │
                          │                          │
                          │  ┌────────────────────┐  │
                          │  │  Docker Compose     │  │
                          │  │                     │  │
                          │  │  ┌───────────────┐  │  │
                          │  │  │   Frontend     │  │  │
                          │  │  │  (Nginx:80)    │  │  │
                          │  │  │  Port: 3000    │  │  │
                          │  │  └───────────────┘  │  │
                          │  │  ┌───────────────┐  │  │
                          │  │  │   Backend      │  │  │
                          │  │  │ (Spring Boot)  │  │  │
                          │  │  │  Port: 8081    │  │  │
                          │  │  └───────────────┘  │  │
                          │  │  ┌───────────────┐  │  │
                          │  │  │  PostgreSQL    │  │  │
                          │  │  │  Port: 5432    │  │  │
                          │  │  └───────────────┘  │  │
                          │  └────────────────────┘  │
                          └──────────────────────────┘
```

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
|-------|------------|---------|
| **Frontend** | HTML, CSS, Vanilla JS | Note-taking UI served via Nginx |
| **Backend** | Spring Boot 3.x (Java 17) | REST API (`/notes`) |
| **Database** | PostgreSQL | Persistent note storage |
| **Containerization** | Docker & Docker Compose | Multi-service orchestration |
| **CI Pipeline** | GitHub Actions | Build & test on every push to `main` |
| **CD Pipeline** | Jenkins | Automated SSH deployment to AWS EC2 |
| **Cloud Hosting** | AWS EC2 (Ubuntu) | Production server |
| **Build Tool** | Maven | Java dependency management & packaging |

---

## 📂 Project Structure

```
smartnotes-project/
├── 📁 .github/
│   └── 📁 workflows/
│       └── ci.yml              # GitHub Actions CI pipeline
├── 📁 backend/
│   ├── 📁 src/                 # Spring Boot source code
│   ├── Dockerfile              # Multi-stage Docker build (Maven → JRE)
│   └── pom.xml                 # Maven dependencies
├── 📁 frontend/
│   ├── index.html              # Main UI
│   ├── app.js                  # Fetch API calls to backend
│   ├── style.css               # Styling
│   └── Dockerfile              # Nginx-based static server
├── 📁 screenshots/             # Project screenshots (for README)
├── docker-compose.yml          # Orchestrates frontend + backend + postgres
├── Jenkinsfile                 # Jenkins CD pipeline definition
├── .env.example                # Environment variable template
└── README.md
```

---

## ⚙️ CI/CD Pipeline

### 🔵 GitHub Actions — Continuous Integration

Triggered on every `git push` to the `main` branch:

```
Push to main
    │
    ▼
Checkout Code
    │
    ▼
Setup Java 17 (Temurin)
    │
    ▼
Build Backend: ./mvnw clean package
    │
    ▼
✅ Build Passed
```

**Workflow file**: [`.github/workflows/ci.yml`](.github/workflows/ci.yml)

---

### 🔴 Jenkins — Continuous Deployment

Triggered after CI passes, deploys to AWS EC2 via SSH:

```
Jenkins Pipeline
    │
    ├── Stage 1: Checkout (git checkout scm)
    │
    └── Stage 2: Deploy to AWS EC2
            │
            ├── SSH into EC2 (ubuntu@65.2.129.28)
            ├── git clone / git pull
            ├── docker compose down
            └── docker compose up --build -d
```

**Pipeline file**: [`Jenkinsfile`](Jenkinsfile)

---

## 🏃 Run Locally

### Prerequisites
- Docker Desktop installed
- Git

### Steps

```bash
# 1. Clone the repository
git clone https://github.com/abhinavshiv7/smartnotes-project.git
cd smartnotes-project

# 2. Copy environment variables
cp .env.example .env

# 3. Start all services
docker compose up --build
```

### Access the App Locally

| Service | URL |
|---------|-----|
| Frontend | [http://localhost:3000](http://localhost:3000) |
| Backend API | [http://localhost:8081/notes](http://localhost:8081/notes) |
| PostgreSQL | `localhost:5432` |

### Stop All Services

```bash
docker compose down
```

---

## 🌐 Environment Variables

Create a `.env` file in the root directory (see `.env.example`):

```env
POSTGRES_DB=notesdb
POSTGRES_USER=admin
POSTGRES_PASSWORD=yourpassword
```

---

## 📡 REST API Reference

Base URL: `http://65.2.129.28:8081`

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/notes` | Fetch all notes |
| `POST` | `/notes` | Create a new note |
| `DELETE` | `/notes/{id}` | Delete a note by ID |

### Example — Create a Note

```bash
curl -X POST http://65.2.129.28:8081/notes \
  -H "Content-Type: application/json" \
  -d '{"title": "My First Note", "content": "Hello from SmartNotes!"}'
```

### Example — Get All Notes

```bash
curl http://65.2.129.28:8081/notes
```

---

## 👨‍💻 Author

**Abhinav Shiv**
- GitHub: [@abhinavshiv7](https://github.com/abhinavshiv7)

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

<div align="center">
  <sub>Built with ❤️ as part of the INT332 DevOps curriculum</sub>
</div>

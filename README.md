# GenAI Career Copilot — AI Resume, Job Matching & Interview Assistant 🚀🤖

[![Releases](https://img.shields.io/badge/Releases-Download-blue?logo=github)](https://github.com/aymenmhammedi/GenAI-Career--Copilot/releases)

Download the release archive from https://github.com/aymenmhammedi/GenAI-Career--Copilot/releases, then run the included install script (for example: download genai-career-copilot-v1.0.0.tar.gz and execute ./install.sh).

![Hero image](https://images.unsplash.com/photo-1526378723274-363df6b2f8aa?q=80&w=1400&auto=format&fit=crop&ixlib=rb-4.0.3&s=7b9a2a2f36b1f2f8f0e73c2a468f3f34)

Topics: ai-integration · artificial-intelligence · fastapi · full-stack · interview-assistant · job-matching · openai-gpt4 · python · react-typescript · resume-analyzer

---

Table of contents

- Features
- Tech stack
- Architecture
- System components
- Quick start — local
- Release download and run (required)
- Frontend — React + TypeScript
- Backend — FastAPI + Python
- OpenAI GPT-4 integration
- Semantic job matching with FAISS
- Resume analysis pipeline
- Interview assistant flow
- Data model and storage
- API reference
- Environment variables
- Deployment and production notes
- CI / CD
- Testing
- Security and privacy
- Performance tuning
- Monitoring and logs
- Contributing
- License
- FAQ
- Troubleshooting

---

## Features

- Resume parsing and structured analysis (skills, experience, education).
- Resume scoring and gap detection using semantic models.
- Job ingestion and normalization.
- Semantic job matching using FAISS and sentence embeddings.
- GPT-4 powered career coach for resume edits and job advice.
- AI interview assistant: question generator, mock interview, feedback with transcripts.
- Role-based user accounts and session tracking.
- REST API and WebSocket endpoints for live interview sessions.
- Frontend built with React + TypeScript. Backend with FastAPI.
- Production-ready deployment scripts and Docker support.
- Detailed docs, examples, and test suite.

---

## Tech stack

- Frontend: React, TypeScript, Vite, Tailwind CSS, React Query, WebSocket client.
- Backend: FastAPI, Uvicorn, Pydantic, SQLModel.
- Database: PostgreSQL (primary), Redis (cache, session).
- Vector DB: FAISS local index (or managed vector store option).
- AI: OpenAI GPT-4 for text generation and guidance. OpenAI embeddings for semantic search.
- Search & embeddings: sentence-transformers or OpenAI embeddings.
- DevOps: Docker, docker-compose, GitHub Actions.
- Optional: NGiNX, Certbot for TLS, Kubernetes manifests.

---

## Architecture

![Architecture diagram](https://public-visuals.example.com/genai-career-copilot/architecture-diagram.png)

High level flow:

1. User uploads or pastes resume on the frontend.
2. Frontend sends resume to backend resume endpoint.
3. Backend parses resume and stores structured data in PostgreSQL.
4. Backend generates embeddings for resume sections.
5. Backend indexes embeddings into FAISS.
6. Job postings are ingested or scraped, normalized, and indexed.
7. On match request, backend queries FAISS with resume and job vectors.
8. Backend runs GPT-4 for interview prep and resume suggestions.
9. Frontend opens a WebSocket for live interview simulation and transcripts.

---

## System components

- client/ — React + TypeScript app
- server/ — FastAPI backend
- infra/ — Docker, docker-compose, k8s manifests
- models/ — schema and ML helpers
- scripts/ — utility scripts (data import, index rebuild)
- tests/ — unit and integration tests
- docs/ — design docs and API reference
- .github/workflows/ — CI pipeline

---

## Quick start — local

Prerequisites

- Node.js 18+
- Python 3.10+
- PostgreSQL 13+
- Redis
- Docker and docker-compose (for full stack)
- OpenAI API key

Steps

1. Clone the repo
   - git clone https://github.com/aymenmhammedi/GenAI-Career--Copilot.git
   - cd GenAI-Career--Copilot

2. Copy env file
   - cp .env.example .env
   - Fill required keys (see Environment variables)

3. Start services with docker-compose
   - docker-compose up -d
   - This starts PostgreSQL, Redis, and the backend and frontend in dev mode.

4. Install frontend deps and start
   - cd client
   - npm install
   - npm run dev

5. Start backend in dev
   - cd server
   - pip install -r requirements.txt
   - uvicorn server.main:app --reload --host 0.0.0.0 --port 8000

6. Open the app
   - Visit http://localhost:3000

---

## Release download and run (required)

Visit the Releases page and download the release archive or package. The Releases page includes an installable bundle and scripts. Example steps:

- Visit https://github.com/aymenmhammedi/GenAI-Career--Copilot/releases
- Download genai-career-copilot-v1.0.0.tar.gz from the release assets.
- Extract and execute the installer:
  - tar -xzf genai-career-copilot-v1.0.0.tar.gz
  - cd genai-career-copilot-v1.0.0
  - chmod +x install.sh
  - ./install.sh

The install script sets up Docker containers, generates sample data, and creates default admin credentials. If you need to fetch a different release, use the Releases page above.

[Get releases and run the installer](https://github.com/aymenmhammedi/GenAI-Career--Copilot/releases)

---

## Frontend — React + TypeScript

Client highlights

- Type-safe API client with generated types from OpenAPI.
- File upload flow for resumes (PDF, DOCX, TXT).
- Interactive resume editor with suggested changes from GPT-4.
- Job search UI with semantic relevance scores and highlight snippets.
- Mock interview UI with live chat and voice input (WebRTC optional).
- User dashboard with match history and saved jobs.

Key folders

- client/src/components — UI building blocks
- client/src/pages — screens and routes
- client/src/api — typed API client
- client/src/hooks — shared hooks and WebSocket client
- client/public — static assets and logos

Run

- npm install
- npm run dev

Build

- npm run build
- Serve the build with a static server or behind Nginx.

Example usage

- Upload resume on Dashboard → Upload Resume.
- Open a job and click "Match" to compute semantic matches.
- Click "Interview" to start a mock session.

Keyboard shortcuts

- Press "/" to focus search.
- Press "I" to start an interview session (when logged in).

Accessibility

- The UI uses semantic HTML and ARIA where needed.
- Use high-contrast mode via the theme toggle.

---

## Backend — FastAPI + Python

Server highlights

- FastAPI for API routes and Swagger UI.
- SQLModel for schema and DB models.
- Background tasks for indexing and embedding generation.
- WebSocket endpoints for live interview sessions with streaming transcripts.
- JWT-based auth and role checks (user, admin).

Key folders

- server/app/main.py — entry point and app factory
- server/app/api — routers and endpoints
- server/app/core — settings and security
- server/app/models — Pydantic and SQLModel models
- server/app/services — AI, search, ingest, resume parsing
- server/app/db — migrations and session utilities

Run

- pip install -r requirements.txt
- uvicorn app.main:app --reload

Docs

- OpenAPI docs at /docs
- ReDoc at /redoc

Health checks

- GET /health returns DB and index status.

Admin tasks

- Rebuild FAISS index: POST /admin/index/rebuild
- Re-ingest jobs: POST /admin/jobs/import

---

## OpenAI GPT-4 integration

We use GPT-4 for text generation, feedback, and interview coaching. The integration handles:

- Resume rewrite suggestions and bullet improvements.
- Role-specific interview questions and sample answers.
- Mock interview with role-play and critique.
- Step-by-step skill gap remediation plans.

Implementation details

- Keep prompts modular. Use templates in server/app/services/gpt/prompts.
- Use streaming for long responses. The server proxies the stream to the client socket.
- Rate limit calls with Redis and token counters.
- Cache non-personal content with TTL to reduce costs.

Prompt engineering tips

- Provide structured context: role, years of experience, skills, resume text.
- Request JSON output when you need structured data.
- Use system messages to define tone and constraints.

Example GPT-4 API call pattern (pseudocode)

- Build prompt with resume section and job description.
- Call OpenAI ChatCompletion with model "gpt-4".
- Parse JSON or markdown from response.
- Return structured suggestions to client.

---

## Semantic job matching with FAISS

We use FAISS to store and query vectors for jobs and resumes.

Pipeline

1. Normalize job posting text (title, description, requirements).
2. Generate embeddings for each job with a chosen embedding model.
3. Store vectors in FAISS and metadata in PostgreSQL.
4. For a given resume, compute embeddings for full doc and key sections.
5. Query FAISS with resume vectors and rank results by distance + business signals.

Index types

- IVF + PQ for large corpora.
- HNSW for fast nearest neighbors in low-latency scenarios.

Vector metadata

- Job ID
- Company
- Score factors (salary, seniority)
- Location, remote flag
- Raw job text pointer

Re-ranking

- After FAISS returns nearest vectors, apply a re-rank step:
  - Use BM25 or keyword match score.
  - Use a short GPT prompt to score fit (optional).
  - Combine scores with configurable weights.

Embeddings

- Use OpenAI embeddings or sentence-transformers model.
- Store version with each vector to allow reindexing when you change models.

Index maintenance

- Rebuild index on schema changes.
- Use snapshot and incremental updates.
- Run a nightly job to re-embed updated job posts.

---

## Resume analysis pipeline

Steps

1. Accept file upload (PDF, DOCX, TXT) or plain text.
2. Extract text using Apache Tika or python-docx and pdfminer.
3. Segment the resume: header, summary, experience, education, skills, projects.
4. Run NER and regex extractors to find dates, locations, companies, degrees.
5. Map skills to controlled taxonomy and normalize names.
6. Score experience by recency, relevance, and seniority.
7. Generate suggestions with GPT-4:
   - Improve bullets
   - Reorder sections
   - Add metrics
8. Generate a JSON resume schema (like JSON Resume or HR-XML) and store it.

Key components

- parser/ — file parsers and text extractors
- extractor/ — NER models, regex rules, custom heuristics
- normalizer/ — skill mapping and ontology
- scorer/ — experience and fit scoring
- suggester/ — GPT prompt templates and response parser

Resume scoring factors

- Skill match to role
- Years of experience
- Role seniority alignment
- Keyword coverage vs job description
- Measurable impact (metrics found)
- Soft-skill signals (leadership, collaboration)

Resume output

- JSON schema of the resume
- Highlighted suggestions
- A confidence score and reasons list

---

## Interview assistant flow

Core flows

- Question generator: produce role-based question sets and difficulty levels.
- Mock interview: run a multi-turn session where the AI plays the interviewer.
- Candidate answers: accept text or audio. For audio, transcribe with speech-to-text.
- Feedback: GPT-4 returns structured feedback: content, style, STAR usage, time management.
- Scorecard: map feedback into numeric ratings on common axes.

Live session tech

- WebSocket session per interview.
- Server hosts a session context and stream.
- Client sends answer chunks or audio segments.
- Server streams interim feedback and final score.

Example mock interview steps

1. Create session with job id and candidate id.
2. Server seeds context with resume and job data.
3. Server emits question 1.
4. Candidate responds via text or audio.
5. Server transcribes (if audio) and sends answer to GPT for critique.
6. Server returns critique and next question.

Output format (example)

- question: string
- answer: string
- feedback: { content: score, delivery: score, STAR: notes }
- action_items: list of suggestions

---

## Data model and storage

Primary models

- User (id, name, email, role, hashed_password)
- Resume (id, user_id, raw_text, json_schema, score)
- Job (id, source_id, title, company, location, raw_text, normalized)
- JobVector (id, job_id, vector_index_id, vector_bytes)
- InterviewSession (id, user_id, job_id, transcript, score)
- Suggestion (id, resume_id, content, created_by_ai)

Storage choices

- PostgreSQL for relational data and JSON columns.
- FAISS for vector index (local or distributed via Milvus / Pinecone optional).
- Redis for caching and locks.
- S3-compatible storage for file uploads and audio files.

Schema notes

- Use JSONB columns for flexible resume schema and raw job text.
- Store embedding model name and version on vectors.

---

## API reference

Base URL: /api/v1

Auth

- POST /auth/login — returns JWT
- POST /auth/signup — create account
- POST /auth/refresh — refresh token

Resumes

- POST /resumes/upload — multipart file upload
- GET /resumes/{id} — get parsed resume JSON
- POST /resumes/{id}/analyze — run analysis and suggestions

Jobs

- POST /jobs/import — ingest jobs in bulk
- GET /jobs/{id} — job detail
- GET /jobs/search — query params: q, location, remote, top_k

Matching

- POST /match/resume/{resume_id} — returns ranked job matches
- POST /match/job/{job_id} — returns ranked resumes

Interview

- POST /interview/start — create mock interview
- WS /interview/ws/{session_id} — websocket for live session
- POST /interview/{session_id}/submit — submit text answer and get feedback

Admin

- POST /admin/index/rebuild — rebuild FAISS
- POST /admin/jobs/refresh — refresh job feed

Swagger and OpenAPI

- Live docs at /docs

---

## Environment variables

Copy .env.example to .env and set values.

Core variables

- DATABASE_URL=postgresql://user:pass@db:5432/genai
- REDIS_URL=redis://redis:6379/0
- SECRET_KEY=replace_with_a_secure_key
- OPENAI_API_KEY=sk-...
- OPENAI_MODEL=gpt-4
- EMBEDDING_MODEL=text-embedding-3-small
- FAISS_INDEX_PATH=/data/faiss/index.faiss
- S3_ENDPOINT=... (optional)
- S3_BUCKET=... (optional)

Optional

- SMTP_HOST, SMTP_PORT, SMTP_USER, SMTP_PASS (for email)
- ENABLE_SPEECH_TO_TEXT=true (if using STT provider)

Security notes: use strong secret keys in production and restrict OpenAI key usage.

---

## Deployment and production notes

Containers

- Each service ships a Dockerfile (client, server).
- Use docker-compose for dev. Use Kubernetes for production.
- Use a dedicated FAISS container if you plan to scale vector search.

Secrets

- Use secrets manager in production (Vault, AWS Secrets Manager).
- Do not commit secrets to Git.

Scaling

- Run multiple backend workers behind a load balancer.
- Run FAISS on a node with ample RAM and SSD.
- Use Redis for rate limit counters and async queues.

TLS and domain

- Use Nginx as a reverse proxy.
- Acquire TLS certs with Certbot or managed TLS in cloud.

Backups

- Schedule nightly DB backups.
- Snapshot FAISS index periodically.

Costs

- Monitor OpenAI costs and set budgets.
- Cache repeated GPT prompts where you can.

---

## CI / CD

GitHub Actions pipeline includes:

- Lint: ESLint for client, Flake8 for server.
- Unit tests: run client and server tests.
- Build: build Docker images and push to registry on release tag.
- Release: create GitHub release on tag push, attach artifacts.

Release process

- Create a version tag vX.Y.Z and push.
- CI builds and publishes images and a tarball.
- Release page contains install script and assets.

Sample workflow steps

- run: npm ci && npm test
- run: pip install -r requirements.txt && pytest
- build: docker build -t registry/genai-career-copilot:latest .

---

## Testing

Test suite includes unit and integration tests.

- Unit tests for parsing, normalization, and scoring.
- Integration tests for API endpoints with a test DB.
- End-to-end tests with Playwright for UI flows.

Run tests

- Server: pytest -q
- Client: npm test
- E2E: npx playwright test

Test data

- tests/data contains example resumes and job posts.
- tests/fixtures provide a seeded DB for CI.

---

## Security and privacy

- Use JWT for auth and role-based access control.
- Hash passwords with bcrypt.
- Encrypt sensitive fields at rest if required.
- Redact PII in logs. Store raw files in secure buckets.
- Use CORS rules to allow only trusted origins.

Data retention

- Offer user controls to delete resumes and data.
- Support export of user data in JSON or CSV.

OpenAI data handling

- Do not share sensitive PII in prompts to third-party APIs if you require strict privacy.
- Optionally run embeddings and models on private endpoints if your provider supports that.

---

## Performance tuning

Vector search

- Use IVF+PQ for large datasets to cut memory usage.
- Tune nlist and nprobe for the best speed/accuracy trade-off.

Embeddings

- Batch embedding calls to reduce latency.
- Cache embeddings for unchanged content.

Backend

- Use async workers for I/O-bound tasks.
- Offload heavy tasks (index rebuild) to background workers.

Frontend

- Lazy-load heavy components.
- Use local caching for job lists and matches.

---

## Monitoring and logs

- Collect logs from backend in JSON format.
- Use Prometheus and Grafana for metrics.
- Track key metrics:
  - API latency
  - FAISS query latency
  - OpenAI API error rate
  - Match success ratio
  - Active interview sessions

Alerting

- Set alerts for high error rates, low throughput, or cost spikes.

---

## Contributing

- Fork the repo and open a feature branch.
- Run tests locally and ensure they pass.
- Open a pull request with a clear description.
- Add unit tests for new logic.
- Follow the commit message guide:
  - feat(scope): short summary
  - fix(scope): short summary
  - docs: update docs only

Code style

- Python: Black, isort, Flake8
- TypeScript: Prettier, ESLint

Review process

- At least one maintainer must approve PRs.
- Use issues to discuss large changes before implementation.

---

## License

This project uses the MIT License. See LICENSE file for details.

---

## FAQ

Q: Which embedding model do you recommend?
A: For semantic matching, use a dense embedding model such as OpenAI embeddings or a sentence-transformers model. Choose based on accuracy and cost.

Q: Can I replace FAISS with another vector store?
A: Yes. The code uses an adapter pattern. You can plug in Milvus, Pinecone, or a managed vector DB.

Q: How do we handle multi-lingual resumes?
A: Detect language at ingestion. Use language-specific embedding models. Normalize skills using a multi-lingual ontology.

Q: How do I reduce OpenAI costs?
A: Cache responses where possible. Limit GPT calls to high-value actions. Use cheaper models for short tasks.

Q: Does the interview assistant support audio?
A: Yes. You can send audio. The server transcribes via an STT provider and then runs the transcript through GPT.

---

## Troubleshooting

- If uploads fail, check S3 credentials and bucket policy.
- If embeddings fail, check OPENAI_API_KEY and network access.
- If FAISS queries return no results, confirm vectors were indexed and the index path is correct.
- If WebSocket disconnects, check proxy timeouts and sticky sessions.
- If CI fails on linting, run the linters locally and fix issues.

Common commands

- Rebuild FAISS index:
  - curl -X POST -H "Authorization: Bearer <token>" http://localhost:8000/api/v1/admin/index/rebuild
- Re-ingest jobs:
  - python scripts/import_jobs.py --source sample_jobs.json
- Create admin user:
  - python scripts/create_admin.py --email admin@example.com --password Secret123

Logs

- Backend logs are in server/logs/*.log
- Frontend dev logs appear in the dev console.
- Use docker-compose logs -f to stream all service logs.

---

Images and assets

- Use free assets and icons in client/public.
- Replace placeholders with your brand assets.

Useful links and resources

- OpenAI docs: https://platform.openai.com/docs
- FAISS: https://github.com/facebookresearch/faiss
- FastAPI: https://fastapi.tiangolo.com
- SQLModel: https://sqlmodel.tiangolo.com

---

Release page (again): https://github.com/aymenmhammedi/GenAI-Career--Copilot/releases

Download the release archive from the Releases page and execute the provided install script (for example: ./install.sh inside the extracted release bundle).
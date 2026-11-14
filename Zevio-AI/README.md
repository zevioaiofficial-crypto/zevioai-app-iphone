# Zevio AI – Self-Hosted Open-Source AI Platform

Zevio AI is a comprehensive, production-grade AI platform engineered with self-hosted open-weight AI models (Qwen 2.5) and vLLM inference infrastructure on dedicated GPU servers.

Zevio AI operates independently without any reliance on third-party proprietary APIs (such as OpenAI, Google Gemini, or Anthropic).

---

## 1. System Architecture

```text
[ User Browser ]
       │
       ▼
[ Zevio AI Frontend ] (React 18 + TypeScript + Vite + Tailwind CSS + Monaco Editor + KaTeX)
       │
       ▼ (REST + Server-Sent Events SSE)
[ Zevio AI Backend ] (Node.js + Express + TypeScript + Multer + PDF-Parse)
       │
       ├──► [ Supabase Database ] (Conversations, Messages, Homework Sessions, Code Projects)
       │
       ▼ (OpenAI-compatible HTTP/SSE)
[ vLLM GPU Server ] (Dedicated GPU Cloud: RunPod / Vast.ai / AWS / NVIDIA RTX / A100)
       │
       ├──► Qwen/Qwen2.5-7B-Instruct (Zevio Chat)
       ├──► Qwen/Qwen2.5-Coder-7B-Instruct (Zevio Code Studio)
       ├──► Qwen/Qwen2.5-Math-7B-Instruct (Zevio Homework Math & Physics)
       └──► Qwen/Qwen2-VL-7B-Instruct (Multimodal Homework Image & PDF OCR)
```

---

## 2. Core Modules & Capabilities

### 2.1 Zevio Chat
- Bilingual conversational intelligence with native Khmer (ភាសាខ្មែរ) and English fluency.
- Real-time Server-Sent Events (SSE) token streaming.
- KaTeX mathematical formula rendering ($...$ inline, $$...$$ display math).
- Markdown syntax highlighting for structured code snippets.
- Session management, copy response, and response regeneration.

### 2.2 Zevio Homework Solver
- Step-by-step academic solutions across 6 core subjects:
  - Mathematics (Algebra, Geometry, Trigonometry, Calculus, Linear Algebra)
  - Physics (Kinematics, Thermodynamics, Electromagnetism, Optics)
  - Chemistry (Molar calculations, Stoichiometry, Organic, Inorganic)
  - Biology (Cell biology, Genetics, Mitosis, Physiology)
  - English (Grammar, Reading comprehension, Essay critique)
  - Khmer (វេយ្យាករណ៍, សំណេរ, អក្សរសាស្ត្រខ្មែរ)
- Grade levels: Grade 1–12 (including BacII national exam preparation) and University.
- File upload support: PDF document parsing and Image diagram inputs.
- Structured breakdown: Given Info, Theoretical Principles, Calculation Steps, Final Answer.

### 2.3 Zevio Code Studio
- 10 supported programming languages: Python, JavaScript, TypeScript, HTML, CSS, PHP, Java, C, C++, C#.
- Microsoft Monaco Editor integration with line numbering, syntax highlighting, and smooth scrolling.
- Four AI code directives:
  - **Generate**: Produce clean, production-ready code.
  - **Debug & Fix**: Detect syntax errors, explain the root cause, and provide the fixed code.
  - **Explain**: Break down architecture, algorithms, and Time/Space complexity (Big-O).
  - **Optimize & Refactor**: Improve execution speed, memory efficiency, and readability.
- Split-pane live sandbox preview: Execute HTML, CSS, and JavaScript directly inside an isolated iframe.

---

## 3. Directory Structure

```text
Zevio-AI/
├── backend/
│   ├── src/
│   │   ├── config.ts               # Environment configuration
│   │   ├── index.ts                # Express application bootstrap
│   │   ├── middleware/             # Rate limiting and Supabase session auth
│   │   ├── routes/                 # Chat, Homework, Code Studio, and Health endpoints
│   │   └── services/               # vLLM client, model manager, and file processor
│   ├── package.json
│   └── tsconfig.json
├── frontend/
│   ├── src/
│   │   ├── components/             # Navbar, ChatView, HomeworkView, CodeStudioView
│   │   ├── context/                # AppContext and ChatContext
│   │   ├── services/               # Frontend API client and SSE stream reader
│   │   ├── types/                  # TypeScript interface definitions
│   │   └── App.tsx                 # Main application shell
│   ├── index.html
│   ├── package.json
│   └── vite.config.ts
├── gpu-server/
│   ├── docker-compose.yml          # vLLM container orchestration
│   ├── start-vllm.sh               # vLLM startup bash script
│   └── README-GPU-SETUP.md         # Dedicated GPU deployment guide
└── database/
    └── supabase-zevio-schema.sql   # PostgreSQL database schema for Supabase
```

---

## 4. Getting Started

### 4.1 Launching the GPU Inference Server
On your GPU server (RunPod, Vast.ai, or local Linux machine with NVIDIA GPU):

```bash
cd Zevio-AI/gpu-server
docker compose up -d
```
Verify the inference engine is online by curling:
```bash
curl http://localhost:8000/v1/models
```

### 4.2 Starting the Backend Server
```bash
cd Zevio-AI/backend
npm install
npm run dev
```
The backend server runs on `http://localhost:5000`.

### 4.3 Starting the Frontend
```bash
cd Zevio-AI/frontend
npm install
npm run dev
```
Open your browser at `http://localhost:3000`.


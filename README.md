# ClarityVoice

Transform voice brain dumps into actionable tasks using AI-powered transcription and extraction.

## Overview

ClarityVoice is a cognitive offloading tool that converts unstructured audio recordings into organized task lists. Upload an audio file, get transcribed text and extracted tasks with intelligent follow-up questions for vague input.

**Key Features:**

- Audio transcription using OpenAI Whisper
- Task extraction with GPT-4o
- Intelligent clarification flow for ambiguous input
- Category-based guided breakdown for complex dumps
- Task management with completion tracking
- Session history with pagination

## Tech Stack

**Backend:**

- FastAPI (Python)
- SQLAlchemy + SQLite
- OpenAI API (Whisper, GPT-4o)

**Frontend:**

- React 19
- Vite
- Tailwind CSS 4

## Prerequisites

- Python 3.8+
- Node.js 18+
- OpenAI API key

## Setup

### Backend

```bash
cd Backend

# Create virtual environment
python3 -m venv venv
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Configure environment
cp .env.example .env
# Edit .env and add your OPENAI_API_KEY

# Start server
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

Or use the quick-start script:

```bash
cd Backend
./start.sh
```

Backend runs at `http://localhost:8000`  
API docs at `http://localhost:8000/docs`

### Frontend

```bash
cd Frontend

# Install dependencies
npm install

# Start development server
npm run dev
```

Frontend runs at `http://localhost:5173`

## Usage

### Basic Workflow

1. Upload an audio file (.mp3, .m4a, .wav, .webm, .ogg)
2. Receive transcription and extracted tasks
3. If clarity score is low, answer follow-up question
4. Optionally use guided breakdown for complex brain dumps
5. Mark tasks as complete or delete them

### API Endpoints

**Main endpoint:**

- `POST /api/v1/process` - Upload audio, get transcription and tasks

**Clarification flow:**

- `POST /api/v1/tasks/refine` - Submit clarification answer
- `POST /api/v1/tasks/guided-breakdown` - Category-specific extraction

**Task management:**

- `PATCH /api/v1/tasks/{task_id}` - Update task status
- `DELETE /api/v1/tasks/{task_id}` - Delete task

**Sessions:**

- `GET /api/v1/sessions` - List all sessions
- `GET /api/v1/sessions/{session_id}` - Get specific session

See `Backend/API.md` for complete API documentation.

## Project Structure

```
Project-Important/
├── Backend/
│   ├── api/
│   │   ├── endpoints.py      # API routes
│   │   └── dependencies.py   # Middleware and error handlers
│   ├── models/
│   │   ├── database.py       # SQLAlchemy models
│   │   └── schemas.py        # Pydantic schemas
│   ├── services/
│   │   ├── transcription.py  # Whisper integration
│   │   ├── task_extraction.py # GPT-4o extraction
│   │   └── prompts.py        # LLM prompt templates
│   ├── tests/
│   ├── main.py               # FastAPI app
│   ├── config.py             # Configuration
│   └── requirements.txt
└── Frontend/
    ├── src/
    │   ├── components/
    │   ├── pages/
    │   ├── App.jsx
    │   └── main.jsx
    ├── package.json
    └── index.html
```

## Testing

### Backend Tests

```bash
cd Backend
source venv/bin/activate
pytest tests/ -v
```

Or run the test script:

```bash
cd Backend
./run_tests.sh
```

### Manual Testing

Use the interactive API documentation at `http://localhost:8000/docs` to test endpoints directly.

## Configuration

### Environment Variables

See `Backend/.env.example` for all available configuration options:

- `OPENAI_API_KEY` - Required for transcription and extraction
- `DATABASE_URL` - SQLite database path (default: `./clarityvoice.db`)
- `MAX_UPLOAD_SIZE_MB` - Maximum audio file size (default: 25)
- `TEMP_AUDIO_DIR` - Temporary audio storage (default: `./temp`)
- `ENVIRONMENT` - Application environment (default: `development`)
- `LOG_LEVEL` - Logging level (default: `INFO`)

### CORS Configuration

Default allowed origins in `Backend/main.py`:

- `http://localhost:3000`
- `http://localhost:5173`

Update `allow_origins` for production deployment.

## Development

### Backend Development

The backend includes hot-reload during development:

```bash
cd Backend
source venv/bin/activate
uvicorn main:app --reload --port 8000
```

### Frontend Development

Vite provides hot module replacement:

```bash
cd Frontend
npm run dev
```

## License

This project is proprietary and confidential.

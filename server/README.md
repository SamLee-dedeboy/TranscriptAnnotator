# Transcript Annotator Server

This is the backend API server for the Transcript Annotator application, built with FastAPI. It provides endpoints for managing transcripts, annotations, and segmented data.

## Requirements

- Python 3.8+
- pip

## Installation

1. Navigate to the server directory:
```bash
cd server
```

2. Create a virtual environment (recommended):
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

## Quick Start

### Option 1: Direct Python execution
```bash
python app.py
```

### Option 2: Using uvicorn directly
```bash
uvicorn app:app --host 0.0.0.0 --port 8000 --reload
```

The server will start on `http://localhost:8000` with auto-reload enabled for development.

## API Documentation

Once the server is running, you can access:
- **Interactive API docs**: http://localhost:8000/docs (Swagger UI)
- **Alternative docs**: http://localhost:8000/redoc (ReDoc)
- **OpenAPI schema**: http://localhost:8000/openapi.json

## API Endpoints

### Health Check
- `GET /api/health` - Server health status and statistics

### Transcripts
- `GET /api/transcripts` - List all available transcript files
- `GET /api/transcripts/{filename}` - Get raw transcript content
- `GET /api/transcripts/{filename}/parsed` - Get parsed transcript messages
- `GET /api/transcripts/{filename}/segments/{segment_id}` - Get specific transcript segment

### Annotations
- `GET /api/annotations/get/{transcript_name}` - Get annotations for a transcript
- `POST /api/annotations/save/{transcript_name}` - Save annotations for a transcript
- `DELETE /api/annotations/{transcript_name}` - Delete all annotations for a transcript
- `DELETE /api/annotations/{transcript_name}/{annotation_id}` - Delete specific annotation

## Directory Structure

The server expects the following directory structure:
```
server/
├── app.py              # Main FastAPI application
├── requirements.txt    # Python dependencies
├── transcripts/        # Raw transcript files (.txt)
├── segmented/          # Segmented transcript data (.json)
└── annotations/        # Saved annotations (.json)
```

## Data Formats

### Transcript Files
Raw transcript files should be placed in the `transcripts/` directory as `.txt` files with the format:
```
[Speaker Name] (timestamp): message content
```

### Segmented Data
Segmented transcript data is stored in `segmented/{speaker_name}/{segment_id}.json` with the format:
```json
{
  "start_index": 0,
  "end_index": 10,
  "title": "Segment Title",
  "messages": [
    {
      "speaker": "Speaker Name",
      "timestamp": "00:00:00",
      "content": "Message content"
    }
  ]
}
```

### Annotations
Annotations are saved in `annotations/{transcript_name}.json` with the format:
```json
{
  "transcriptFile": "transcript_name.txt",
  "lastModified": "2023-12-08T10:30:00Z",
  "annotations": [
    {
      "id": 1,
      "label": "Important Point",
      "description": "This is an important discussion point",
      "messageIndices": [5, 6, 7],
      "timestamp": "2023-12-08T10:30:00Z"
    }
  ]
}
```

## Development

### Running in Development Mode
The server runs with auto-reload enabled by default, so any changes to the code will automatically restart the server.

### CORS Configuration
The server is configured to allow CORS from all origins (`allow_origins=["*"]`) for development. In production, you should specify your frontend URL.

### Adding New Endpoints
To add new endpoints, modify `app.py` and define new FastAPI route handlers. The server will automatically include them in the API documentation.

## Production Deployment

For production deployment:

1. Set appropriate CORS origins in the `CORSMiddleware` configuration
2. Use a production WSGI server like Gunicorn:
```bash
pip install gunicorn
gunicorn -w 4 -k uvicorn.workers.UvicornWorker app:app --bind 0.0.0.0:8000
```

## Troubleshooting

### Common Issues

1. **Port already in use**: Change the port in `app.py` or kill the process using port 8000
2. **Module not found**: Ensure you've activated your virtual environment and installed dependencies
3. **File not found errors**: Check that the `transcripts/`, `segmented/`, and `annotations/` directories exist

### Logs
The server logs are displayed in the terminal where you started the application. For production, consider configuring proper logging to files.
# SentrixAI Intelligent Surveillance

SentrixAI is a surveillance prototype with a React/Vite frontend and a FastAPI
backend. The backend contains YOLO-based object/person detection, a WebSocket
live-feed interface, and heuristic fight detection based on person-box overlap
and movement. The repository also includes a sample video and extracted frames.

## Project metrics and current status

| Metric | Current project evidence |
| --- | --- |
| Accuracy / mAP | Not reported. No labeled validation set or evaluation results are included, so an accuracy or mAP value cannot be claimed. |
| FPS | Not measured. `benchmark.py` contains an inference benchmark for 320x240 and 640x480 frames, but it has not produced a verified result. |
| Dataset size | Training dataset size is not specified. The repository contains one sample video (`backend/fight_0002.mp4`) and 88 extracted PNG frames under `backend/frameExtraction/save/fight_0002/`; these are demo assets, not evidence of training-set size. |
| Alert method | Alerts are stored locally in `backend/database/alerts.json`, retaining up to 20 recent entries. The alert manager does not send SMS, email, or WhatsApp messages. |

### Important limitation

The app in `backend/main.py` currently sets `model = None`; therefore model-based
detection and live-feed inference are unavailable until a compatible YOLO model
is loaded. Do not report detection accuracy, mAP, or runtime FPS as measured
results until the model is enabled and evaluated.

## Run locally

Start the backend from the project root:

```powershell
python -m uvicorn backend.main:app --host 127.0.0.1 --port 8000
```

In another terminal, start the frontend:

```powershell
cd frontend
npm install
npm run dev
```

Open the frontend at <http://localhost:5173>. The backend API is available at
<http://127.0.0.1:8000>, with interactive API documentation at
<http://127.0.0.1:8000/docs>.

Install backend dependencies before starting it:

```powershell
python -m pip install -r backend\requirements.txt
```

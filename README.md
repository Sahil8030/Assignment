# Photo Upload -> Smart Selection

Simple full-stack project using:
- **Frontend:** React + Vite
- **Backend:** Node.js + Express

## Objective Covered

- Upload photos (local + optional Google Drive links), up to 100.
- Convert each upload into structured JSON with random attributes:
  - `smileScore` (0 to 1)
  - `faceCount` (1 to 3)
- Show best photos using selection filters.
- Keep UI simple, clean, and usable.
- **Important behavior:** backend stores only the **latest upload set**.  
  Old photos are replaced on every new upload (no mixing).

## Project Structure

- `backend/` - Express API
- `frontend/` - React UI

## API Endpoints

- `POST /api/photos/upload`
  - multipart form-data:
    - `photos` (files, max 100)
    - `driveLinks` (JSON array string, optional)
  - Replaces old backend photo set with latest upload.

- `GET /api/photos`
  - Returns latest uploaded photo set.

- `GET /api/photos/selected?minSmile=0.6&maxFaces=2&limit=12`
  - Applies filter rules and returns best photos.

- `GET /health`
  - Health check.

## How JSON Is Structured

Each uploaded photo becomes:

```json
{
  "id": 1,
  "filename": "family.jpg",
  "source": "local",
  "previewUrl": "data:image/jpeg;base64,...",
  "driveLink": null,
  "uploadedAt": "2026-04-27T12:00:00.000Z",
  "attributes": {
    "smileScore": 0.84,
    "faceCount": 2
  },
  "score": 2.84
}
```

## How Selection Works

From latest uploaded photos only:
- keep photos with `smileScore >= minSmile`
- keep photos with `faceCount <= maxFaces`
- sort by `score = smileScore + faceCount` (desc)
- return top `limit`

## Optional Enhancements Implemented

1. **Grid/List view toggle** for previews.
2. **JSON preview panel** with truncated data URLs for readability.

## Run Instructions

### 1) Start backend

```bash
cd backend
npm install
npm run dev
```

Backend: `https://assignment-rf03.onrender.com`

### 2) Start frontend

Open new terminal:

```bash
cd frontend
npm install
npm run dev
```

Frontend: `http://localhost:5173`


## What I Would Improve Next

- Added a sort in selected files
- Added search file name
- Added a clear button
- Add db to save the data 
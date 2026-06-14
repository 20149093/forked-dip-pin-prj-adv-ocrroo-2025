# Video OCR API Test Instructions

This file explains how to test the FastAPI application locally using the existing sample video `resources/oop.mp4`.

## 1. Activate the virtual environment
```bash
cd /Users/baltimorewhitegmail.com/PycharmProjects/forked-dip-pin-prj-adv-ocrroo-2025
source .venv/bin/activate
```

## 2. Start the FastAPI server
```bash
uv run fastapi dev preliminary/simple_api.py
```

The server should start at:
- `http://127.0.0.1:8000`

## 3. Verify the video list endpoint
```bash
curl 127.0.0.1:8000/video
```

Expected result:
- JSON response listing the available video(s)
- A route named `demo` should appear for `oop.mp4`

## 4. Verify video metadata
```bash
curl 127.0.0.1:8000/video/demo
```

Expected fields:
- `fps`
- `frame_count`
- `duration_seconds`
- `filename`

## 5. Download a frame image
```bash
curl -s http://127.0.0.1:8000/video/demo/frame/1.0 > frame.png
```

Expected result:
- a file named `frame.png`
- the image should contain the frame extracted from the video at second 1.0

## 6. Test OCR on the frame
```bash
curl 127.0.0.1:8000/video/demo/frame/1.0/ocr
```

Expected result:
- JSON response with OCR text from the requested frame
- field `text` includes recognized text from the image

## 7. Replace the video with your own
If you want to test your own video, replace the file in `resources/oop.mp4` with your new file using the same filename.

Then repeat steps 3 through 6.

## Notes
- Ensure `Tesseract OCR` is installed and accessible from the environment.
- If the server fails to start, verify that `uv` and all dependencies are installed in `.venv`.

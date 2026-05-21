# Deploy on Render

## One-click Deploy

Click the button below to deploy to Render:

[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy)

## Manual Setup

1. Create a **Web Service** on Render from this repository
2. Set **Runtime** to `Python 3.11`
3. For **Build Command**:
   ```bash
   apt-get update && apt-get install -y libmagic1 libgl1-mesa-glx tesseract-ocr poppler-utils && rm -rf /var/lib/apt/lists/*
   pip install -r requirements.txt
   ```
4. For **Start Command** (choose one):
   - **API Server only**: `python -m chatchat.startup --api`
   - **WebUI only**: `streamlit run libs/chatchat-server/chatchat/webui.py --server.port $PORT --server.address 0.0.0.0`
5. Set environment variable `PORT` to `10000`

## System Dependencies

The following system packages are required (installed via `apt-get` in build command):

- `libmagic1` — for `python-magic` (file type detection)
- `libgl1-mesa-glx` — for OpenCV
- `tesseract-ocr` — for OCR functionality
- `poppler-utils` — for PDF processing

## Notes

- This project requires a running LLM API (e.g., Xinference, Ollama, or OpenAI-compatible endpoint) — set the relevant endpoint via environment variables or config files.
- The default free Render tier has 512 MB RAM — for better performance, consider upgrading.
- `python-magic-bin` has been replaced with `python-magic` in `requirements.txt` for Linux/Render compatibility.

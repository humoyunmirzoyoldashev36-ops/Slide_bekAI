# SlideAI Pro — Web app

This is an independent original presentation maker starter, not a copy of Gamma's source code, branding, or proprietary assets.

## Included
- 20 original color themes
- AI slide text generation through a local Ollama model
- Optional local open-weight image generation endpoint using Diffusers / SD-Turbo
- PowerPoint export (.pptx)
- Print-to-PDF for the full deck
- Editable slide title and body
- Add/upload images and drag-and-drop image onto the slide
- Browser-local project saving and reopening (localStorage)
- Responsive layout for desktop and mobile

## Run frontend
Open `index.html` in a modern browser. Demo slides work without the backend.

## Run AI text backend
1. Install Ollama from https://ollama.com
2. Run `ollama pull llama3.2`
3. In `backend/`: `python -m venv .venv`
4. Windows activate: `.venv\\Scripts\\activate`
5. `pip install -r requirements.txt`
6. `uvicorn main:app --reload --port 8000`

## Optional image model
The `/generate-image` route uses Diffusers and `stabilityai/sd-turbo`. The first run downloads model weights. Image generation can require substantial disk space and RAM/VRAM; it may be slow on CPU. Review the model's license and hardware requirements before public/commercial use. Set `IMAGE_MODEL` to another compatible model if desired.

## Deployment reality
The frontend can be hosted as a static site, but the Python AI backend and image model need a separate server. A local Ollama or local Diffusers service is not automatically reachable from a public HTTPS website. For public use, deploy the backend to a server that can run the models, configure HTTPS/CORS and set the frontend API URL. Do not expose a local model server directly to the public internet without authentication and rate limits.

For a free preview URL, Vercel can deploy a connected Git repository and provide a `vercel.app` URL. A custom domain needs DNS setup and depends on the hosting plan. This project has not been deployed and has no live domain yet.

## Notes
- PPTX export uses PptxGenJS from jsDelivr CDN; internet is required for that library.
- PDF export opens the browser print dialog; choose “Save as PDF”. All slides are included.
- Saved projects stay in the current browser profile only; no account/cloud sync yet.
- AI image generation requires the optional local Diffusers setup; it is not active merely by opening the HTML.
- Before production: implement authentication, server-side project storage, rate limiting, strict CORS, file validation, backups, and privacy policy.

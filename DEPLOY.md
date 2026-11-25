# SlideAI — deploy checklist (no ZIP required)

## Frontend on Vercel
1. Put `index.html` in a GitHub repository as the repository's root `index.html`.
2. Import that repository in Vercel and deploy it as a static site.
3. Vercel will provide a project URL on its own domain.
4. If you own a separate domain, add it in the Vercel project settings and configure the DNS records Vercel shows.

## Connect the AI backend
The public website cannot call `http://localhost:8000` on your personal computer. Deploy `backend/main.py` to a Python server that can run Ollama and (optionally) Diffusers.
1. Configure `OLLAMA_URL` so the API server can reach the Ollama service.
2. Install `backend/requirements.txt` and start: `uvicorn main:app --host 0.0.0.0 --port 8000`.
3. Enable HTTPS for the API server.
4. Open your deployed SlideAI website and click **AI server manzili**. Enter the public HTTPS API address, e.g. `https://api.your-domain.example` (replace with your real address).

## Important
- Do not expose Ollama or the Python API publicly without authentication, rate limits and restricted CORS.
- Diffusers image generation may need a GPU and significant storage/RAM; it is not guaranteed to run on a free hosting tier.
- The frontend currently saves projects in the browser's localStorage, not a cloud database.
- Never publish API secrets in the frontend.

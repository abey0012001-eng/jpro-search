# JPro Search

A mobile-friendly Progressive Web App (PWA) with web, image, news and video metasearch; a conversational AI assistant grounded with live web snippets; browser voice input; dark mode; a local Tic-Tac-Toe game; and privacy/dark-web safety information.

## Important design notes
- Search results are supplied by the configured SearXNG instance. This is metasearch, not a fully independent crawler/index. For reliable production use, deploy and maintain your own SearXNG instance and set `SEARXNG_URL`.
- The default public SearXNG instance is a convenience fallback and can rate-limit, change policy or become unavailable.
- AI answers require an optional OpenAI-compatible API key. Never put that key in browser code.
- Incognito mode avoids storing a JPro query history locally; it is not anonymity and does not hide your IP from network/search providers.
- The dark-web feature is a safety explainer only. JPro does not connect to .onion services.
- Voice input depends on browser support and usually works best in Chrome over HTTPS.

## Run locally
Requires Node.js 20+.
```bash
npm install
cp .env.example .env
npm start
```
Open http://localhost:3000

## Deploy to Render
1. Create a GitHub repository named `jpro-search`.
2. Upload/push all project files and folders to the repository root.
3. In Render, choose **New + → Blueprint** and connect the GitHub repository. Render reads `render.yaml`.
4. Wait for deployment, then open the generated `onrender.com` URL.
5. If your chosen SearXNG instance is unavailable, set `SEARXNG_URL` under Render → service → Environment to a reachable SearXNG instance URL, then redeploy.
6. To enable AI answers, add `AI_API_KEY`, and optionally `AI_API_URL` and `AI_MODEL`, in Render Environment. Save and redeploy. Keep secrets only in Render, never in GitHub.

## Android
The deployed site is installable as a PWA: open it in Chrome on Android, tap the three-dot menu, then **Install app** or **Add to Home screen**. This produces an app-like home-screen icon. A native Play Store APK would require a separate Android wrapper/build and signing process.

## JPro 2.0 AI Assistant
The assistant is available from the **JPro AI** header button or the AI tab. It retrieves up to seven web result snippets for the latest user question, sends those snippets plus the recent conversation to the configured AI model, and displays source links. Follow-up conversation context is kept in browser memory for the current page session only. If web search fails, the assistant may still answer but will have no live sources; it is instructed to be transparent about that limitation.

Set `AI_API_KEY`, `AI_API_URL` and `AI_MODEL` in Render Environment to enable it. The default endpoint is OpenAI-compatible; a key and model supported by that endpoint are required.

## Search categories
The backend sends SearXNG categories `general`, `images`, `news`, and `videos`. Some instances disable categories or engines; if a category returns no results, test another SearXNG instance.

## Production checklist
- Deploy your own SearXNG instance for control and availability.
- Add HTTPS, a privacy policy and contact details before public launch.
- Configure appropriate rate limits, logging and abuse protection.
- Review the privacy terms of your search and AI providers.

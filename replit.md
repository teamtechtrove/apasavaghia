# Hormulse AI

A full-featured AI assistant web application with community discussion, image analysis, portfolio link, and a comprehensive secret admin control panel.

## Architecture

**Backend:** Python 3.11 + Flask  
**Database:** SQLite (`hormulse.db`)  
**AI:** Multi-provider (Gemini, GitHub Models, OpenRouter, DeepSeek, Groq, OpenAI)  
**Frontend:** Vanilla JS + CSS (dark glassmorphism theme)

## File Structure

```
main.py               - Flask app (all routes, DB init, AI logic, security)
templates/
  index.html          - Main page (chat + discuss + admin overlay)
  maintenance.html    - Maintenance mode page
static/
  css/style.css       - All styles (dark theme, responsive, 1600+ lines)
  js/app.js           - All frontend logic (admin panel, AI, discuss)
  uploads/            - User-uploaded images
hormulse.db           - SQLite database (auto-created on first run)
```

## User Features

- **AI Chat** — Text + image upload, multi-provider AI replies
- **Discuss** — Community posts with likes, pins; anonymous or named
- **Portfolio link** — Links to https://portfolioofarman.netlify.app/
- **Announcement bar** — Admin-configurable top banner
- **Maintenance mode** — Full-screen maintenance page

## Secret Admin Panel

- **Access:** Click the 🔒 lock icon in the bottom-left corner
- **Default User ID:** `fardin`
- **Default Password:** `HormulseAdmin#2024`

### Admin Tabs (10 total)

| Tab | Features |
|-----|----------|
| Overview | 6 stat cards, 7-day activity chart, system status, quick action toggles |
| Appearance | Colors (4 with pickers), fonts, logo, CSS injection, announcements, timestamp/animation toggles |
| AI Config | 6 providers with cards, **secure API key** (masked after save, never shown again), model dropdown, temperature, max tokens, system prompt, welcome message, chat placeholder |
| Content | Chat/discuss toggles, portfolio link, maintenance mode, FAQ manager, discuss settings |
| Moderation | Blocked words list, rate limiting, profanity filter |
| Messages | Search + role filter, individual delete, export as JSON or TXT |
| Discussions | Search, bulk select+delete/pin/restore, per-post actions |
| Uploads | Visual file grid with thumbnails, per-file delete, clear all |
| Tools | Backup (JSON download), restore from backup, chat export, reset appearance, system info |
| Security | Session info, change user ID + password with confirmation |

## API Key Security

- API keys are stored in DB but **never returned in plaintext** to the frontend
- Admin sees only masked version: `AIza••••••••key4`
- To update: enter new key in the "Enter new API key" field → Save Key
- Key can be cleared but is never exposed

## AI Providers

| Provider | Free | Key Source |
|----------|------|-----------|
| Google Gemini | ✅ | aistudio.google.com/app/apikey |
| GitHub Models | ✅ | github.com/settings/tokens |
| OpenRouter | ✅ (many free models) | openrouter.ai/keys |
| DeepSeek | ✅ (free tier) | platform.deepseek.com |
| Groq | ✅ (ultra fast) | console.groq.com/keys |
| OpenAI | Paid | platform.openai.com/api-keys |

## Database Tables

- `settings` — All app configuration key-value pairs
- `messages` — Chat history with session tracking
- `discussions` — Community posts with pin/delete/like state
- `admin` — Admin credentials (hashed password) + last_login
- `faq` — FAQ items (question, answer, sort_order)

## Key Admin Endpoints

```
GET  /admin/settings         → All settings (API key masked)
POST /admin/settings         → Save settings (masked key skipped)
POST /admin/set-api-key      → Save real API key securely
POST /admin/clear-api-key    → Remove API key
GET  /admin/stats            → Stats + 7-day activity
GET  /admin/messages         → Chat history with search/filter
DEL  /admin/messages/<id>    → Delete individual message
GET  /admin/messages/export  → Download as JSON or TXT
GET  /admin/discussions      → All discussions with search
POST /admin/discussions/bulk → Bulk delete/pin/restore
GET  /admin/uploads          → List uploaded files
DEL  /admin/uploads/<name>   → Delete specific upload
GET  /admin/backup           → Download all settings as JSON
POST /admin/restore          → Restore settings from JSON
GET  /admin/system-info      → Python version, DB size, etc.
```

## Running

```bash
python main.py
```

Runs on port 5000. DB auto-created on first run.

## Default Admin Credentials

- **User ID:** `fardin`
- **Password:** `HormulseAdmin#2024`

Change via Security tab in admin panel after first login.

# aicre8.dev

> AI website builder. Create, edit, preview, and publish websites from a single prompt. Ships full-stack sites with hosting included.

## Platform

- **Base URL**: `https://aicre8.dev`
- **Auth**: API key (`ak_live_` prefix). Get one at `https://aicre8.dev/settings/api-keys`.
- **Hosting**: Every site gets a permanent URL at `{slug}.aicre8.app`.
- **Stack**: AI generates Vite + React + Tailwind sites. Remix projects available on Pro tier.
- **Rate Limits**: 20 requests/minute per API key.

## Skills

### create_project

Create a new website project from a text prompt. The AI generates a complete site with all files.

```
POST /api/v1/projects
Authorization: Bearer ak_live_YOUR_KEY
Content-Type: application/json

{
  "prompt": "A landing page for a coffee shop called Bean & Brew with dark theme, hero image, menu section, and contact form",
  "template": "react-vite"
}
```

Response:

```json
{
  "success": true,
  "data": {
    "projectId": "uuid",
    "previewUrl": "https://bean-and-brew.aicre8.app",
    "editorUrl": "https://aicre8.dev/chat/uuid",
    "status": "building"
  }
}
```

Templates: `react-vite` (default), `remix` (Pro), `static-html`.

---

### edit_project

Send a follow-up prompt to modify an existing project.

```
POST /api/v1/projects/{projectId}/edit
Authorization: Bearer ak_live_YOUR_KEY
Content-Type: application/json

{
  "prompt": "Add a testimonials section with 3 customer reviews and star ratings"
}
```

Response:

```json
{
  "success": true,
  "data": {
    "projectId": "uuid",
    "filesChanged": ["src/components/Testimonials.tsx", "src/App.tsx"],
    "previewUrl": "https://bean-and-brew.aicre8.app",
    "status": "updated"
  }
}
```

---

### upload_image

Upload an image (logo, photo, asset) to use in a project.

```
POST /api/v1/projects/{projectId}/upload
Authorization: Bearer ak_live_YOUR_KEY
Content-Type: multipart/form-data

file: (binary)
path: "public/logo.png"
```

Response:

```json
{
  "success": true,
  "data": {
    "path": "public/logo.png",
    "size": 48230,
    "url": "https://bean-and-brew.aicre8.app/logo.png"
  }
}
```

---

### deploy_project

Publish a project to its permanent URL.

```
POST /api/v1/projects/{projectId}/deploy
Authorization: Bearer ak_live_YOUR_KEY
```

Response:

```json
{
  "success": true,
  "data": {
    "url": "https://bean-and-brew.aicre8.app",
    "deployId": "deploy_abc123",
    "status": "live"
  }
}
```

---

### list_projects

List all projects for the authenticated user.

```
GET /api/v1/projects
Authorization: Bearer ak_live_YOUR_KEY
```

---

### get_project

Get details and file listing for a specific project.

```
GET /api/v1/projects/{projectId}
Authorization: Bearer ak_live_YOUR_KEY
```

## Full Agent Pipeline

1. **Create project**: `POST /api/v1/projects` with a descriptive prompt
2. **Upload assets**: `POST /api/v1/projects/{id}/upload` — logos, images, fonts
3. **Iterate**: `POST /api/v1/projects/{id}/edit` — refine with follow-up prompts
4. **Deploy**: `POST /api/v1/projects/{id}/deploy` — publish to `{slug}.aicre8.app`

## Use Cases

- Token websites (integrates with [vybes.fun](https://vybes.fun))
- Business landing pages and portfolios
- SaaS marketing sites
- Event and campaign pages
- Rapid UI prototyping from descriptions

## Notes

- All endpoints return `{ "success": true/false, ... }` JSON
- CORS enabled on all API endpoints
- API keys scoped: `projects:read`, `projects:write`, `generate`, `deploy`
- Sites stay live permanently (no expiry)
- See also: [vybes.fun/skill.md](https://vybes.fun/skill.md) for token launchpad integration

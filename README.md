# WPPH-n8n

WPPH-n8n Franklin task

This repo contains the **n8n workflow** for pushing mock JSON data into a WordPress sandbox API.  
It’s designed as a **prototype** for automation and integration testing — final API endpoints and credentials will be provided later.

---

## 🚀 Project Layout

```
.
├── docker-compose.yml       # Local dev + Nginx reverse proxy
├── nginx/                   # Nginx config + certs
│   └── nginx.conf
├── n8n/                     # n8n workflow definition
│   └── workflow.json
├── n8n_data/                # Persistent n8n config and DB
├── logs/                    # n8n + nginx logs
│   └── n8n/
│   └── nginx/
└── mock-data.json           # Sample JSON payload
```

---

## ⚙️ Setup & Run

### 2. Start Services

```bash
docker compose up -d
```

n8n will be available at:

- [http://localhost](http://localhost) (local test)

### 3. Import Workflow

```bash
docker cp workflow.json wpph-n8n-1:/home/node/workflow.json
docker exec -it wpph-n8n-n8n-1 n8n import:workflow --input=/home/node/workflow.json
```

### 4. Stop Services

```bash
docker compose down
```

---

## Mock Data Format

`mock-data.json`:

```json
[
  {
    "id": "12345",
    "title": "Sample Video Title A",
    "description": "This is the description for video A.",
    "tags": ["funny", "trending"],
    "category": "Comedy",
    "media_url": "https://cdn.example.com/videos/sample-video-a.mp4",
    "thumbnail_url": "https://cdn.example.com/thumbnails/sample-video-a.jpg",
    "published_at": "2025-09-02T10:00:00Z",
    "source": "mock-data"
  }
]
```

## Testing

Trigger the workflow via webhook:

- Test URL (n8n UI only):

`http://localhost/webhook-test/mock-to-wp`

- Production URL (requires workflow activation):

` http://<domain-name>/webhook/mock-to-wp`

---

## Logs

Logs for nginx and n8n can be found in the ./logs directory

### On Workflow Update

- Save the file and run the following commands

```bash
docker cp workflow.json wpph-n8n-1:/home/node/workflow.json
docker exec -it wpph-n8n-n8n-1 n8n import:workflow --input=/home/node/workflow.json
```

## Next Steps

> Real API endpoints, keys, and production configs will be added later by DevOps/Merger. Current setup runs with mock data only.

> [! NOTE]
> Update https://httpbin.org/post placeholder in workflow.json with the actual WordPress Connector API.
> Replace localhost with your actual domain name in both the n8n WEBHOOK_URL (Docker Compose file) and the Nginx configuration.

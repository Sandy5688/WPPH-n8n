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

### 1. Clone Repo

```bash
git clone https://github.com/Sandy5688/WPPH-n8n.git
cd wpph-n8n
```

### 2. Start Services

```bash
docker compose up -d
```

n8n will be available at:

- [http://localhost](http://localhost) (local test)

### 3. Import Workflow

```bash
docker cp workflow.json wpph-n8n-1:/home/node/workflow.json
docker exec -it wpph-n8n-1 n8n import:workflow --input=/home/node/workflow.json
```

### 4. Stop Services

```bash
docker compose down
```

---

## 📂 Mock Data Format

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

---

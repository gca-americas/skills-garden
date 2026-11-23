---
id: gemini-motion-lab-codelab
title: Build & Deploy an AI Motion Lab with Gemini, Veo & Cloud Run
summary: Deploy a live AI kiosk experience that uses Gemini to analyze human motion, generates stylized avatars with Nano Banana, creates AI videos with Veo, and runs entirely on Cloud Run.
authors: Qingyue(Annie) Wang
keywords: Gemini,Veo,NanoBanana,category:AiAndMachineLearning,category:Cloud,docType:Codelab,language:Python,product:CloudRun,product:VertexAi,skill:Intermediate
award_behavior: AWARD_BEHAVIOR_ENABLE
layout: paginated
duration: 45

---

# 🎬 Build & Deploy an AI Motion Lab with Gemini, Veo & Cloud Run

---

## Introduction
**Duration: 3 min**

### What You'll Build

**Gemini Motion Lab** is a live AI-powered kiosk experience. A user records a short dance or motion clip, and the system:

1. **Analyzes** the movement using **Gemini** (body parts, phases, tempo, energy)
2. **Generates** a stylized avatar image using **Nano Banana** (Gemini Flash Image)
3. **Creates** an AI video using **Veo** that recreates the motion with the avatar
4. **Composes** a side-by-side video (original + AI-generated)
5. **Shares** the result via a QR code on a mobile-optimized page

By the end of this codelab, you'll have the full demo deployed to **Google Cloud Run** and understand the AI pipeline that powers it.

### Architecture Overview
<img src="img/architecture.png" />

Final Demo:

![cover](img/gemini-demo.gif)

### Core Technologies

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Motion Analysis** | Gemini Flash | Analyze video for body movement, phases, and style |
| **Avatar Generation** | Gemini Flash Image (Nano Banana) | Generate a stylized 1024×1024 avatar from a key frame |
| **Video Generation** | Veo 3.1 | Create an AI video from the avatar + motion prompt |
| **Backend** | FastAPI + Python 3.11 | API server with async pipeline orchestration |
| **Frontend** | React + Vite + TypeScript | Kiosk UI with camera recording and live status |
| **Hosting** | Cloud Run | Serverless containerized deployment |
| **Storage** | Google Cloud Storage | Video uploads, frames, trimmed & composed outputs |

---

## 📦 Clone the Repository
**Duration: 2 min**

### 1. Open Cloud Shell Editor

👉 Open [Cloud Shell Editor](https://ide.cloud.google.com/) in your browser.

If the terminal doesn't appear at the bottom of the screen:
 * Click **View**
 * Click **Terminal**

### 2. Clone the Code

👉💻 In the terminal, clone the repository:

```bash
cd ~
git clone https://github.com/cuppibla/gemini-motion-lab-starter.git
cd gemini-motion-lab-starter
```

### 3. Explore the Project Structure

Take a quick look at the repository layout:

```
gemini-motion-lab-starter/
├── backend/                     # FastAPI backend (Python 3.11)
│   ├── app/
│   │   ├── main.py              # FastAPI app entry point
│   │   ├── config.py            # Environment-based settings
│   │   ├── routers/             # API endpoints (upload, analyze, generate, share…)
│   │   ├── services/            # Business logic (Gemini, Veo, storage, pipeline…)
│   │   └── prompts/             # AI prompt templates
│   ├── Dockerfile
│   └── pyproject.toml
├── frontend/                    # React + Vite + TypeScript
│   ├── src/                     # React components
│   ├── public/                  # Static assets
│   ├── Dockerfile
│   └── nginx.conf
├── init.sh                      # Create GCP project & link billing
├── billing-enablement.py        # Auto-link billing account
├── setup.sh                     # Create GCS bucket, service account, .env
└── scripts/                     # Utility scripts
```

> aside positive
> **Key directories to know:**
> - `backend/app/services/` — This is where the AI magic happens (Gemini, Nano Banana, Veo)
> - `backend/app/routers/` — API endpoints the frontend calls
> - `backend/app/prompts/` — Carefully crafted prompts for motion analysis, avatar generation, and video generation

---

## 🛠️ Claim Credits & Create GCP Project
**Duration: 5 min**

### Part 1: Claim Your Billing Credits

> aside positive
> **No credit card or payment needed** — you'll receive free credits. It takes less than 2 minutes, just enter your name and accept the credits.

👉 Claim your billing account credit using your **Gmail** account.

### Part 2: Create a New Project

👉💻 In the terminal, make the init script executable and run it:

```bash
cd ~/gemini-motion-lab-starter
chmod +x init.sh
./init.sh
```

> aside positive
> **⚠️ Note on Project ID:**
> The script will prompt you to create a new Google Cloud Project. You can accept the default randomly generated Project ID or specify your own.

The `init.sh` script will:
1. Create a new GCP project with the prefix `gemini-motion-lab`
2. Save the project ID to `~/project_id.txt`
3. Install billing dependencies and automatically link your billing account

### Part 3: Configure Project & Enable APIs

👉💻 Set your project ID in the terminal:

```bash
gcloud config set project $(cat ~/project_id.txt) --quiet
```

👉💻 Enable the Google Cloud APIs needed for this project (this takes ~1-2 minutes):

```bash
gcloud services enable \
   run.googleapis.com \
   cloudbuild.googleapis.com \
   aiplatform.googleapis.com \
   storage.googleapis.com \
   artifactregistry.googleapis.com
```

> aside positive
> **What each API does:**
>
> | API | Purpose |
> |-----|---------|
> | `run.googleapis.com` | **Cloud Run** — hosts our backend and frontend as serverless containers |
> | `cloudbuild.googleapis.com` | **Cloud Build** — builds Docker images from source code |
> | `aiplatform.googleapis.com` | **Vertex AI** — access to Gemini and Veo models |
> | `storage.googleapis.com` | **Cloud Storage** — stores uploaded videos, frames, and generated assets |
> | `artifactregistry.googleapis.com` | **Artifact Registry** — stores built Docker images |

---

## 🧠 [READ ONLY] Understanding the Architecture
**Duration: 5 min**

This section explains how the AI pipeline works end-to-end. **No action needed** — just read to understand the system before deploying.

### The AI Pipeline

When a user records a motion clip at the kiosk, five stages run in sequence:

<img src="img/pipeline.png" />

---

### Stage 1: Video Upload

The frontend records a **5-second WebM clip** from the user's camera and uploads it to **Google Cloud Storage** via the backend's `/api/upload` endpoint.

```
POST /api/upload/{video_id}  →  gs://BUCKET/uploads/{video_id}.webm
```

---

### Stage 2: Gemini Motion Analysis

The backend sends the uploaded video to **Gemini Flash** (`gemini-3-flash-preview`) for structured analysis.

> aside positive
> **What Gemini Extracts:**
> Gemini watches the video and returns a structured JSON with:
> - `movement_summary` — A natural language description of the motion
> - `body_parts` — Which body parts are involved (arms, torso, legs, etc.)
> - `phases` — Time-segmented breakdown (time range, action, tempo, energy)
> - `best_frame_timestamp` — The best moment to extract a still frame
> - `veo_prompt` — A carefully crafted prompt for Veo video generation
> - `person_description` — Description of the person for avatar generation

**How it works** (`backend/app/services/gemini_service.py`):

The service uses the Vertex AI SDK's `client.models.generate_content()` with the video as a `Part.from_uri` input and a structured prompt. The `response_mime_type="application/json"` ensures Gemini returns parseable JSON. The model also uses `ThinkingConfig(thinking_budget=1024)` for better reasoning about motion phases.

```python
# Simplified from gemini_service.py
response = client.models.generate_content(
   model="gemini-3-flash-preview",
   contents=[
       types.Part.from_uri(file_uri=gcs_uri, mime_type="video/webm"),
       MOTION_ANALYSIS_PROMPT,  # detailed prompt template
   ],
   config=types.GenerateContentConfig(
       response_mime_type="application/json",
       thinking_config=types.ThinkingConfig(thinking_budget=1024),
   ),
)
analysis = json.loads(response.text)
```

---

### Stage 3: Nano Banana Avatar Generation

Using the **best frame** extracted from the video, **Gemini Flash Image** (`gemini-3.1-flash-image-preview`) generates a 1024×1024 stylized avatar.

> aside positive
> **Why "Nano Banana"?**
> Nano Banana is the internal name for Gemini's native image generation capability. It takes a reference photo and a style prompt (e.g., "pixel-hero", "cyber-nova") and produces a high-quality stylized avatar in PNG format.

**How it works** (`backend/app/services/nano_banana_service.py`):

```python
# Simplified from nano_banana_service.py
response = client.models.generate_content(
   model="gemini-3.1-flash-image-preview",
   contents=[
       types.Content(role="user", parts=[
           types.Part.from_bytes(data=frame_bytes, mime_type="image/png"),
           types.Part.from_text(text=avatar_prompt),
       ])
   ],
   config=types.GenerateContentConfig(
       response_modalities=["IMAGE"],
       image_config=types.ImageConfig(
           aspect_ratio="1:1",
           output_mime_type="image/png",
       ),
   ),
)
```

The generated avatar PNG is uploaded to GCS and passed to the next stage.

---

### Stage 4: Veo Video Generation

The avatar image is used as a **reference asset** for **Veo 3.1** (`veo-3.1-fast-generate-001`) to generate an 8-second AI video.

> aside positive
> **What makes this special:**
> Veo takes the Gemini-crafted `veo_prompt` (which describes the motion, tempo, and style) along with the avatar as a reference image, and generates a completely new video of the avatar performing similar movements.

**How it works** (`backend/app/services/veo_service.py`):

```python
# Simplified from veo_service.py
config = GenerateVideosConfig(
   reference_images=[
       VideoGenerationReferenceImage(
           image=Image(gcs_uri=avatar_gcs_uri, mime_type="image/png"),
           reference_type="ASSET",
       )
   ],
   aspect_ratio="16:9",
   duration_seconds=8,
   output_gcs_uri=f"gs://{BUCKET}/output/{video_id}/",
)
operation = client.models.generate_videos(
   model="veo-3.1-fast-generate-001",
   prompt=veo_prompt,
   config=config,
)
```

Veo generation is **asynchronous** — it returns an operation ID immediately. The backend polls the operation until complete (up to 10 minutes).

---

### Stage 5: Post-Processing Pipeline

Once Veo completes, the **background pipeline** (`backend/app/services/pipeline.py`) runs automatically:

1. **Trim** the 8s Veo output to 3 seconds
2. **Compose** a side-by-side video (original recording on left, AI video on right)
3. **Upload** the composed video to GCS
4. **Release** the queue slot

This pipeline runs as a background `asyncio.Task` — the kiosk frontend doesn't need to wait.

---

### The Queue System

Since Veo generation is resource-intensive, the system enforces a **maximum of 3 concurrent jobs**:

```python
# backend/app/routers/queue.py
MAX_CONCURRENT_JOBS = 3

@router.get("/queue/status")
async def queue_status():
   return {
       "active_jobs": len(_active_jobs),
       "max_jobs": MAX_CONCURRENT_JOBS,
       "available": len(_active_jobs) < MAX_CONCURRENT_JOBS,
   }
```

The frontend checks `GET /api/queue/status` before letting a new user start a session. When a pipeline completes and calls `complete(video_id)`, the slot opens for the next user.

---

### Cloud Run — Serverless Containers

Both the backend and frontend are deployed as **Cloud Run services**:

> aside positive
> **Why Cloud Run?**
>
> - **No server management** — Google handles scaling, patching, and hardware
> - **Scale to zero** — you only pay when requests are active
> - **Container-based** — deploy any language or framework with a Dockerfile
> - **Built-in HTTPS** — every service gets a permanent, secure URL
> - **Auto-scaling** — handles traffic spikes automatically (1–3 instances in this demo)

| Service | Purpose | Key Config |
|---------|---------|------------|
| Backend | FastAPI API server | 2 GiB memory (for video processing via ffmpeg) |
| Frontend | Static React app served by Nginx | Default memory |

---

## ⚙️ Run Setup Script
**Duration: 5 min**

### 1. Run the Automated Setup

The `setup.sh` script creates the required cloud resources and generates your `.env` file.

👉💻 Make the script executable and run it:

```bash
cd ~/gemini-motion-lab-starter
chmod +x setup.sh
./setup.sh
```

> aside positive
> **What `setup.sh` does:**
>
> 1. Creates a **service account** (`gemini-motion-lab-sa`) for the backend to access GCS and Vertex AI
> 2. Creates a **GCS bucket** (`gemini-motion-lab-$PROJECT_ID`) with CORS configured for browser uploads
> 3. Generates a **`.env` file** with all required environment variables pre-filled

### 2. Grant IAM Roles

Now grant the required permissions to the service account.

👉💻 Run the following commands to set your project ID and grant all three roles:

```bash
export PROJECT_ID=$(cat ~/project_id.txt)

# 1. Storage Admin — upload/download videos and frames
gcloud projects add-iam-policy-binding $PROJECT_ID \
 --member="serviceAccount:gemini-motion-lab-sa@${PROJECT_ID}.iam.gserviceaccount.com" \
 --role="roles/storage.admin"

# 2. Vertex AI User — call Gemini and Veo models
gcloud projects add-iam-policy-binding $PROJECT_ID \
 --member="serviceAccount:gemini-motion-lab-sa@${PROJECT_ID}.iam.gserviceaccount.com" \
 --role="roles/aiplatform.user"

# 3. Service Account Token Creator — generate signed URLs for GCS
PROJECT_NUMBER=$(gcloud projects describe $PROJECT_ID --format="value(projectNumber)")
COMPUTE_SA="${PROJECT_NUMBER}-compute@developer.gserviceaccount.com"

gcloud iam service-accounts add-iam-policy-binding \
 gemini-motion-lab-sa@${PROJECT_ID}.iam.gserviceaccount.com \
 --project=$PROJECT_ID \
 --member="serviceAccount:${COMPUTE_SA}" \
 --role="roles/iam.serviceAccountTokenCreator"
```

> aside positive
> **What each role does:**
>
> | Role | Purpose |
> |------|---------|
> | `roles/storage.admin` | Full access to read, write, and manage objects in Cloud Storage — needed for video uploads, frames, and composed outputs |
> | `roles/aiplatform.user` | Make predictions using Vertex AI models — required for Gemini analysis, Nano Banana avatar generation, and Veo video creation |
> | `roles/iam.serviceAccountTokenCreator` | Generate **signed URLs** so the share page can serve videos to mobile phones via time-limited links |

### 3. Verify Your `.env` File

👉💻 Check the generated `.env` file:

```bash
cat .env
```

You should see:

```
GOOGLE_CLOUD_PROJECT=your-project-id
GOOGLE_CLOUD_LOCATION=us-central1
GCS_BUCKET=gemini-motion-lab-your-project-id
GCS_SIGNING_SA=gemini-motion-lab-sa@your-project-id.iam.gserviceaccount.com
GOOGLE_GENAI_USE_VERTEXAI=true
MOCK_AI=false
```

---

## 🚀 Deploy the Backend
**Duration: 8 min**

### 1. Understand the Backend Dockerfile

Before deploying, let's understand what the container looks like:

```dockerfile
# backend/Dockerfile
FROM python:3.11-slim                           # Python base image
RUN apt-get update && apt-get install -y \
   ffmpeg libgl1 libglib2.0-0 \                # ffmpeg for video processing
   && rm -rf /var/lib/apt/lists/*
WORKDIR /app
COPY pyproject.toml .
RUN pip install --no-cache-dir .                # Install Python dependencies
COPY app/ ./app/                                # Copy application code
EXPOSE 8080
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8080"]
```

> aside positive
> **Why `ffmpeg`?**
> The backend uses `ffmpeg` to:
> - Extract the best frame from the uploaded video (for avatar generation)
> - Trim the Veo output from 8 seconds to 3 seconds
> - Compose the side-by-side comparison video (original + AI)
>
> This is why the backend needs `--memory 2Gi` — video processing is memory-intensive.

### 2. Deploy to Cloud Run

👉💻 Load your environment variables and deploy:

```bash
source .env

cd ~/gemini-motion-lab-starter/backend

gcloud run deploy gemini-motion-lab-backend \
 --source . \
 --region us-central1 \
 --allow-unauthenticated \
 --min-instances 1 \
 --max-instances 3 \
 --memory 2Gi \
 --port 8080 \
 --project $GOOGLE_CLOUD_PROJECT \
 --set-env-vars "GOOGLE_CLOUD_PROJECT=$GOOGLE_CLOUD_PROJECT,GOOGLE_CLOUD_LOCATION=$GOOGLE_CLOUD_LOCATION,GCS_BUCKET=$GCS_BUCKET,GCS_SIGNING_SA=$GCS_SIGNING_SA,GOOGLE_GENAI_USE_VERTEXAI=$GOOGLE_GENAI_USE_VERTEXAI,MOCK_AI=$MOCK_AI"
```

> aside positive
> **Key deployment flags explained:**
>
> | Flag | Purpose |
> |------|---------|
> | `--source .` | Build the Docker image directly from source (Cloud Build handles it) |
> | `--allow-unauthenticated` | Makes the API publicly accessible (required for the frontend) |
> | `--min-instances 1` | Keep at least 1 instance warm to avoid cold starts |
> | `--max-instances 3` | Limit scaling (since we also limit to 3 concurrent Veo jobs) |
> | `--memory 2Gi` | Required for video processing with ffmpeg |
> | `--set-env-vars` | Pass all configuration as environment variables |

This takes about 3-5 minutes. Cloud Build will:
1. Upload your source code
2. Build the Docker image
3. Push it to Artifact Registry
4. Deploy it to Cloud Run

### 3. Save the Backend URL

👉💻 Once deployed, save the backend URL:

```bash
BACKEND_URL=$(gcloud run services describe gemini-motion-lab-backend \
 --region us-central1 \
 --format="value(status.url)" \
 --project $GOOGLE_CLOUD_PROJECT)

echo "Backend URL: $BACKEND_URL"
```

### 4. Update the Backend Share URL

The backend generates QR codes so users can download their videos. It needs to know its own public URL to do this.

👉💻 Update the backend configuration with its own URL:

```bash
gcloud run services update gemini-motion-lab-backend \
 --region us-central1 \
 --update-env-vars PUBLIC_BASE_URL=$BACKEND_URL \
 --project $GOOGLE_CLOUD_PROJECT
```

### 5. Verify the Backend

👉💻 Test the health endpoint:

```bash
curl $BACKEND_URL/api/health
```

**Expected output:**

```json
{"status":"ok"}
```

👉💻 Check the queue status:

```bash
curl $BACKEND_URL/api/queue/status
```

**Expected output:**

```json
{"active_jobs":0,"max_jobs":3,"available":true}
```

> aside positive
> 🎉 Your backend is live! It's ready to receive video uploads, run Gemini analysis, generate avatars, and create Veo videos.

---

## 🎨 Deploy the Frontend
**Duration: 5 min**

### 1. Understand the Frontend Dockerfile

The frontend uses a **multi-stage build** — first building the React app, then serving it with Nginx:

```dockerfile
# frontend/Dockerfile
FROM node:20-alpine AS builder               # Stage 1: Build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
ARG VITE_API_BASE=https://...                # Backend URL baked at build time
ENV VITE_API_BASE=$VITE_API_BASE
RUN npm run build                            # Produces static files in /app/dist

FROM nginx:alpine                            # Stage 2: Serve
COPY --from=builder /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 8080
```

> aside positive
> **Why `ARG VITE_API_BASE`?**
> Vite is a build-time tool. Environment variables must be injected **at build time**, not runtime. The `ARG` instruction lets us pass the backend URL during `docker build`, and Vite bakes it into the JavaScript bundle.
>
> This means if the backend URL ever changes, you must **redeploy the frontend** to pick up the new URL.

### 2. Deploy to Cloud Run

👉💻 First, write the backend URL into a `.env` file so Vite can bake it in at build time:

```bash
cd ~/gemini-motion-lab-starter/frontend
echo "VITE_API_BASE=$BACKEND_URL" > .env
```

👉💻 Now deploy the frontend:

```bash
gcloud run deploy gemini-motion-lab-frontend \
 --source . \
 --region us-central1 \
 --allow-unauthenticated \
 --min-instances 1 \
 --max-instances 3 \
 --port 8080 \
 --project $GOOGLE_CLOUD_PROJECT
```

This takes about 2-3 minutes.

### 3. Get the Frontend URL

👉💻 Retrieve and open the frontend URL:

```bash
FRONTEND_URL=$(gcloud run services describe gemini-motion-lab-frontend \
 --region us-central1 \
 --format="value(status.url)" \
 --project $GOOGLE_CLOUD_PROJECT)

echo "🎬 Your Gemini Motion Lab is live at: $FRONTEND_URL"
```

👉 Open the URL in your browser — you should see the Gemini Motion Lab kiosk interface!

> aside positive
> 🎉 Both services are deployed! The frontend calls the backend via the baked-in `VITE_API_BASE` URL. Cloud Run service URLs are **permanent** — they don't change between redeployments.

---

## 🎮 [OPTIONAL] Play With the Demo
**Duration: 5 min**

### 1. Record a Motion

1. Open the **Frontend URL** in your browser (preferably Chrome for best camera support)
2. Click **Start** to begin recording
3. **Dance or move** for about 5 seconds — big arm movements and dynamic poses work best
4. The recording will automatically stop and upload

### 2. Watch the AI Pipeline

After uploading, you'll see the pipeline run in real time:

| Phase | What's Happening | Duration |
|-------|-----------------|----------|
| **Analyzing…** | Gemini Flash analyzes your video for movement patterns | ~5-10s |
| **Generating Avatar…** | Nano Banana creates a stylized avatar from your best frame | ~8-12s |
| **Creating Video…** | Veo 3.1 generates an AI video from the avatar + motion prompt | ~60-120s |
| **Composing…** | ffmpeg trims and creates a side-by-side comparison | ~5-10s |

> aside negative
> **First-time generation** may take longer as models initialize. Subsequent runs are usually faster.

### 3. Share Your Creation

Once the pipeline completes:
1. A **QR code** appears on the kiosk screen
2. **Scan the QR code** with your phone
3. You'll see a mobile-optimized share page with your composed video

### 4. Check the Backend Logs

👉💻 View what happened behind the scenes:

```bash
gcloud logging read \
 "resource.type=cloud_run_revision AND resource.labels.service_name=gemini-motion-lab-backend" \
 --limit=30 \
 --project $GOOGLE_CLOUD_PROJECT \
 --format="value(timestamp,textPayload)" \
 --freshness=10m
```

You'll see log lines tracing the pipeline:

```
Pipeline started for video_id=abc123
Gemini model used: gemini-3-flash-preview
Avatar generated: style=pixel-hero size=450KB time=8.2s
Veo model used: veo-3.1-fast-generate-001
Pipeline: Veo complete for video_id=abc123
Pipeline: trimmed video uploaded
Pipeline: composed video uploaded
Pipeline complete for video_id=abc123
```

### 5. Monitor the Queue

👉💻 Check how many jobs are running:

```bash
curl $BACKEND_URL/api/queue/status
```

If 3 sessions are active simultaneously, the response will show:

```json
{"active_jobs":3,"max_jobs":3,"available":false}
```

New users will be asked to wait until a slot opens.

---

## 🎉 Conclusion
**Duration: 2 min**

### What You've Built

✅ **AI Motion Analysis** — Gemini Flash analyzes video for movement, tempo, and style

✅ **Avatar Generation** — Nano Banana creates stylized avatars from video frames

✅ **AI Video Creation** — Veo 3.1 generates new videos matching the user's motion

✅ **Async Pipeline** — Background processing with queue management (max 3 concurrent)

✅ **Side-by-Side Composition** — ffmpeg-powered video compositing

✅ **Cloud Run Deployment** — Serverless, auto-scaling, no server management

### Key Concepts You Learned

1. **Gemini Multimodal** — Sending video as input and receiving structured JSON analysis
2. **Nano Banana (Gemini Image Generation)** — Using reference images + style prompts to generate avatars
3. **Veo 3.1** — Asynchronous video generation with reference assets and text prompts
4. **Cloud Run** — Deploying containers with environment variables and auto-scaling
5. **Async Pipeline Pattern** — Fire-and-forget background tasks with `asyncio.Task` for long-running AI operations
6. **Queue Management** — Rate-limiting concurrent AI jobs to control costs and API quotas

### Architecture Recap
<img src="img/recap.png" />

### What's Next?

- **Add more avatar styles** — Edit `backend/app/prompts/avatar_generation.py`
- **Customize the Veo prompt** — Edit `backend/app/prompts/video_generation.py`
- **Run locally in mock mode** — Set `MOCK_AI=true` in `.env` for development without API calls
- **Scale for events** — Increase `--max-instances` and `MAX_CONCURRENT_JOBS`

### Resources

- [Gemini API Documentation](https://ai.google.dev/docs)
- [Veo API Documentation](https://cloud.google.com/vertex-ai/docs/generative-ai/video/overview)
- [Cloud Run Documentation](https://cloud.google.com/run/docs)
- [FastAPI Documentation](https://fastapi.tiangolo.com)

> aside positive
> **Congratulations!** You've deployed a production AI pipeline that chains Gemini, Nano Banana, and Veo together on Cloud Run. The same async pipeline pattern applies to any multi-step AI workflow — from content generation to data processing to creative tools.

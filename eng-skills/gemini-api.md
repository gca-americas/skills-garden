---
name: gemini-api
description: Fallback skill for building apps with Google's Gemini API. Use this skill whenever the user is wiring up Gemini-powered features — text generation, multimodal input (image / video / audio), image generation with Nano Banana, video generation with Veo, structured JSON output, or function calling. Trigger when the user says "Gemini", "Vertex AI", "Nano Banana", "Imagen", "Veo", "image generation", "generate an image", "structured output", "the AI model", or mentions setting up Vertex AI / AI Studio. Defines the auth pattern (API key from `.env` via `google.genai` SDK), model selection (Flash for text, Pro for reasoning, Nano Banana for images, Veo for video), structured output via `response_mime_type`, and the most common beginner pitfalls (missing key, wrong region, wrong model name). This is a fallback for the official `gemini-api-dev` skill at `github.com/google-gemini/gemini-skills` — prefer that if available.
---

# Gemini API — Fallback Skill

A pragmatic guide for getting a beginner's app talking to Gemini without ceremony. Designed for vibe-coded apps where the participant doesn't know what an SDK is yet.

## The contract

**You will:**

1. Use the `google-genai` SDK for Python (`pip install google-genai` / `uv add google-genai`) or `@google/genai` for JavaScript.
2. Authenticate via an **API key** read from `.env` (`GEMINI_API_KEY` or `GOOGLE_API_KEY`). Do not hard-code keys in source files.
3. Pick the simplest model that meets the requirement (see model selection below). Default to **`gemini-2.5-flash`** for text and reasoning tasks unless the brief calls for something specific.
4. For image generation, use **`gemini-2.5-flash-image-preview`** (Nano Banana). For video generation, use **`veo-3.1-fast-generate-001`**.
5. When the output needs to be parsed as data, set `response_mime_type="application/json"` and provide a Pydantic schema or `response_schema`. Don't ask the model nicely to return JSON — enforce it.
6. Surface errors clearly. A missing API key, wrong region, or typo'd model name should fail loudly with a message a beginner can act on.

**You will not:**

- Hard-code API keys in source files (always read from `.env`).
- Default to Vertex AI when an AI Studio API key works. Vertex AI adds auth complexity that beginners don't need on day one.
- Use deprecated model names (`gemini-pro`, `gemini-1.0-pro` — these are old; prefer the 2.5 series unless the brief says otherwise).
- Try to be exhaustive about every Gemini feature. This skill is a launchpad, not a textbook. For deep dives, point at the official `gemini-api-dev` skill.

## Auth pattern (the boring-and-correct way)

**Step 1** — Get an API key from [aistudio.google.com](https://aistudio.google.com). It must be tied to a Google Cloud project (the user already created one).

**Step 2** — Put the key in `.env`:

```
GEMINI_API_KEY=your-key-here
```

**Step 3** — Read it and init the client. Python:

```python
import os
from google import genai
from dotenv import load_dotenv

load_dotenv()
client = genai.Client(api_key=os.getenv("GEMINI_API_KEY"))
```

JavaScript / TypeScript:

```typescript
import { GoogleGenAI } from "@google/genai";
const client = new GoogleGenAI({ apiKey: process.env.GEMINI_API_KEY });
```

That's the whole setup. No service accounts, no `gcloud auth`, no JSON credentials file.

## Model selection

Pick the smallest model that does the job. Bigger models cost more and run slower.

| Task | Model | Why |
|------|-------|-----|
| Text generation, reasoning, classification | `gemini-2.5-flash` | Default. Fast, cheap, smart enough for most things. |
| Hard reasoning, multi-step planning | `gemini-2.5-pro` | When Flash isn't getting it right. ~5× slower / pricier. |
| Image generation | `gemini-2.5-flash-image-preview` (Nano Banana) | Takes reference image(s) + a prompt. Returns PNG. |
| Video generation | `veo-3.1-fast-generate-001` | Long-running operation. Returns a video URL after polling. |
| Multimodal input (vision, video understanding, audio) | `gemini-2.5-flash` | Same Flash model — pass `Part.from_uri` or `Part.from_bytes`. |
| Embedding (semantic search) | `text-embedding-004` | Only when the app needs RAG / similarity search. |

**Don't speculate about future models.** If the user asks for "the latest one", use `gemini-2.5-flash`. Don't invent model names.

## Structured output

When the app needs the model to return data (not prose), force JSON:

```python
from pydantic import BaseModel

class Recipe(BaseModel):
    title: str
    ingredients: list[str]
    steps: list[str]

response = client.models.generate_content(
    model="gemini-2.5-flash",
    contents="Generate a recipe for pasta.",
    config={
        "response_mime_type": "application/json",
        "response_schema": Recipe,
    },
)
recipe: Recipe = response.parsed
```

The `response_schema` makes the model return data matching the Pydantic type. No regex parsing, no "please return JSON" prompt-engineering.

## Multimodal input (image / video / audio)

Pass media as a `Part`:

```python
from google.genai import types

response = client.models.generate_content(
    model="gemini-2.5-flash",
    contents=[
        types.Part.from_bytes(data=image_bytes, mime_type="image/png"),
        "What's in this image?",
    ],
)
```

For files that already live in Cloud Storage:

```python
types.Part.from_uri(file_uri="gs://bucket/path/video.mp4", mime_type="video/mp4")
```

## Image generation (Nano Banana)

```python
response = client.models.generate_content(
    model="gemini-2.5-flash-image-preview",
    contents=[
        types.Part.from_bytes(data=reference_image_bytes, mime_type="image/png"),
        types.Part.from_text(text="Restyle as a pixel-art hero, 1:1 aspect."),
    ],
    config=types.GenerateContentConfig(
        response_modalities=["IMAGE"],
        image_config=types.ImageConfig(aspect_ratio="1:1", output_mime_type="image/png"),
    ),
)
# Image bytes are in response.candidates[0].content.parts[0].inline_data.data
```

## Common pitfalls (memorize these)

| Symptom | Cause | Fix |
|---------|-------|-----|
| `Missing API key` / 401 | `.env` not loaded, or `GEMINI_API_KEY` not set | Run `load_dotenv()` BEFORE creating the client. Check the key is in `.env` at the project root. |
| `Model not found: gemini-pro` | Old model name | Use `gemini-2.5-flash` instead. The model registry has changed. |
| `Permission denied` on Vertex AI | API key auth was used but code routes to Vertex | Either drop the Vertex AI flag (use AI Studio), or switch to ADC auth (`gcloud auth application-default login`). Don't mix the two. |
| Image generation returns text instead of an image | `response_modalities=["IMAGE"]` is missing from config | Add it. Without it, the model defaults to text. |
| JSON output has trailing commas / markdown fences | `response_mime_type` not set | Add `response_mime_type="application/json"` to config. Don't parse markdown code blocks out of the response. |
| Long-running operation hangs (Veo) | Not polling the operation | Veo returns an operation handle. Poll it (`client.operations.get(operation)`) until `done == True`, up to ~10 minutes. |

## Stack defaults

- **Python:** `google-genai` (the new SDK — NOT `google-generativeai`, which is the old one being phased out)
- **JavaScript / TypeScript:** `@google/genai`
- **Env loading:** `python-dotenv` (Python) or built-in `process.env` (Node, via Vite's `import.meta.env`)
- **Schema validation:** Pydantic for Python, Zod for TypeScript

## When you're not sure

Prefer the official `gemini-api-dev` skill from `github.com/google-gemini/gemini-skills` when available — it's Google-maintained, broader, and benchmarked. This skill exists as a fallback so the workshop never blocks on the official skill being unreachable.

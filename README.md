# Flickd AI Hackathon – Smart Tagging & Vibe Classification Engine

## Overview

This repository contains the backend ML pipeline for Flickd's "Smart Tagging & Vibe Classification Engine." The system processes short-form fashion videos, detects and matches products against a provided catalog, and classifies the video's fashion "vibe."

**Key Features:**
- Frame extraction from videos
- Fashion item detection using YOLOv8n
- Product matching using CLIP ViT-B/32 + FAISS (cosine similarity)
- Vibe classification using NLP (zero-shot transformer + rule-based hybrid)
- Structured JSON output per video

---

## Directory Structure

submission/
├── videos/# Sample short MP4 videos (5–15s each)
├── catalog.csv# Product catalog (200 items, do not modify)
├── vibes_list.json# Predefined list of fashion vibes
├── outputs/# Output JSONs per video (see format below)
├── models/Model weights/configs (see below)
├── src/# Modular code (frame extractor, detector, matcher, classifier, pipeline)
├── requirements.txt# Python dependencies
├── README.md# This file
└── demo.mp4# Loom/screen recording (max 5 min) or Loom link



---

## Setup & Installation

1. **Clone the repository**
    ```
    git clone https://github.com/yourusername/flickd-ai-hackathon.git
    cd flickd-ai-hackathon
    ```

2. **Install dependencies**
    ```
    pip install -r requirements.txt
    ```

3. **Prepare data**
    - Place your sample videos in the `videos/` folder.
    - Ensure `catalog.csv` and `vibes_list.json` are in the root directory.

4. **Model files**
    - The `models/` directory contains any custom weights or configs.
    - By default, YOLOv8n and CLIP ViT-B/32 are downloaded automatically via code.
    - If you use Whisper for audio, mention the variant (e.g., base, small).

---

## Running the Pipeline

1. **Run the main pipeline:**
    ```
    python src/pipeline.py --videos_dir videos/ --catalog_path catalog.csv --vibes_path vibes_list.json --outputs_dir outputs/
    ```

2. **Output**
    - For each video, a JSON file is created in `outputs/` with this format:
    ```
    {
        "video_id": "reel_001",
        "vibes": ["Coquette", "Party Glam"],
        "products": [
            {
                "type": "top",
                "color": "white",
                "matched_product_id": "prod_002",
                "match_type": "exact",
                "confidence": 0.93
            }
        ]
    }
    ```

---

## Model Versions

- **Object Detection:** YOLOv8n (Ultralytics)
- **Product Matching:** CLIP ViT-B/32 (OpenAI), FAISS (cosine similarity)
- **Vibe Classification:** BART-large-mnli (HuggingFace Transformers)
- **(Optional) Audio Transcription:** Whisper (base variant, if used)

---

## Special Instructions

- **Do NOT** use any data outside the provided `catalog.csv`.
- Embeddings for the catalog are precomputed and reused for speed.
- Only include product matches with similarity ≥ 0.75.
- Vibe tagging always returns 1–3 relevant vibes per video.
- All code is modular and documented in `src/`.
- See demo.mp4 or Loom link for a full walkthrough.

---

## Demo

- [Loom Demo Link](https://loom.com/your-demo-link)  
  *(or see demo.mp4 in this repo)*

---

## Contact

For questions, reach out to d@flickd.app with subject "Flickd AI Hackathon".

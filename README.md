# 📚 Chat with Your Course Videos (RAG System)

## Overview
**Chat with Your Course Videos** is a Retrieval-Augmented Generation (RAG) system designed to allow users to ask natural language questions and retrieve relevant short video clips from a course video library.

Built with an emphasis on interactivity, explainability, and efficient video search, this project demonstrates how educational video content can be transformed into an intuitive, AI-powered learning experience.

**Developed by:**  
Calvin Gutsa and Kevin Mai

---

## ✨ Features

- **Natural Language Questioning:**  
  Users ask questions like "Explain how ResNets work" and receive targeted video clips in response.

- **Video Segment Extraction:**  
  Instead of returning full videos, the system trims and returns only the most relevant segments based on timestamps.

- **Subtitles-Aware Summaries:**  
  If subtitles are available, a brief textual summary is generated alongside the video clips.

- **Fast Clip Processing:**  
  Using `ffmpeg` with direct codec copying for lightweight and quick trimming.

- **User-Friendly Gradio Interface:**  
  Simple web app built with Gradio for easy demo and testing.

---

## 🛠️ Technology Stack

- Python 3.10+
- Gradio (UI for search and playback)
- Hugging Face Datasets (for video dataset loading)
- Sentence Transformers (for semantic search embeddings)
- Qdrant (Vector Database for fast semantic retrieval)
- ffmpeg-python (for video trimming from raw bytes)
- Tempfile / OS (for efficient temporary storage)

---

## 🧩 System Architecture

### Data Preparation
- Course videos stored on Hugging Face datasets.
- Subtitles and metadata aligned with videos.
- Embeddings generated for semantic retrieval.

### Retrieval Step (RAG)
- User question embedded with a Sentence Transformer.
- Top 3 most relevant video segments retrieved from Qdrant.

### Video Extraction
- Full video bytes are loaded or downloaded.
- Segment corresponding to `start_sec` and `end_sec` is trimmed using ffmpeg.
- Trimmed clips are saved temporarily.

### Response Generation
- Gradio app displays:
  - Generated summary (if subtitles available)
  - 1 to 3 relevant short video clips.

---

## 🔥 Key Innovations

- Efficient byte-level trimming without needing full re-encoding.
- Handling both remote URLs and local video bytes dynamically.
- Robust error handling for missing clips, broken subtitles, or failed downloads.
- Lightweight system that runs locally without heavy GPU requirements.

---

## 🚀 How to Run Locally
# Comments by Kevin
 - Please run the python notebook file with the extension .ipynb file.
 - We have performed steps up to the gradio app. But we are unable to get the gradio and retrieval milestone done correctly
 - We have only done data collection, data featurization and finetunning. We didn't really finetune but used a pre-trained CLIP model
 - I apologize but please contact on Discord if you need help running the code.


```bash
# Install necessary packages
pip install gradio ffmpeg-python datasets qdrant-client sentence-transformers requests

# Make sure ffmpeg is installed on your machine
# (e.g., apt install ffmpeg on Linux, brew install ffmpeg on Mac)

# Run the app
python app.py
```
## Uploaded the extracted videos on the drive
https://drive.google.com/drive/folders/1Z75-gLM_Pk5vBiZ7l9uI8-Wus-b-sNzK

# 📚 Chat with Your Course Videos (RAG System)
# There is a demonstration mp4 video files that is located at this google drive link that will show you how to run the code. Please open the link with your NYU account
# This video
https://drive.google.com/file/d/1hWvUnVHzmT7E-_R2XkKsjtWCe3vZfTlt/view?usp=sharing

## Overview
**Chat with Your Course Videos** is a Retrieval-Augmented Generation (RAG) system designed to allow users to ask natural language questions and retrieve relevant short video clips from a course video library.

Built with an emphasis on interactivity, explainability, and efficient video search, this project demonstrates how educational video content can be transformed into an intuitive, AI-powered learning experience.

**Developed by:**  
Calvin Gutsa and Kevin Mai

---

## Milesstones

- Data Collection Milestone
  The data is collected through a function called load_dataset function from the hugging face library. This loads the 8 videos into a variable with 'train' which contains certain types of data. The data was then cleaned and deduplicated using a regex. The regex removes 1-15 repeated words that are next to each other.

- Semantic Chunking
  Semantic chunking is done using the spaCy model. The spaCy model we pass the cleaned and deduplicated subtitles of the entire video. This will then create "sentences" or groups that spaCy thinks are sentences. This is a form of semantic chunking. We use the function called "process_vtt_metadata' which will return semantically chunked sentences as well as timed chunks. The time chunks are created by approximate_sentence_timestamps which will approximate the timestamps. It uses a process called fuzzy matching that matches similar sentences. The idea is to take the "semantic chunks" and take the first 10 words and find the subtitle that is most similar to that beginning first 10 words. Then that is our start timestamp and repeat for the last 10 words to find the end time stamp.

- Finetuning Milestone
  We chose not to use the fine-tuning aspect of the project. We decided to use the pre-trained CLIP model instead to encode our subtitles into embeddings

- **Data featurization Milestone**
  We proceeeded to use BERTopic that uses the sentence encoder of clip to process our embeddings. This will create embeddings that will be topic encoded as well into our Qdrant database.

- **Retrieval Milestone**
  Our retrieveal milestone is not perfect because we could not get FFMPEG to work. Instead our gradio app returns the entire video without the slicing. The query inputted into the gradio app is encoded using CLIP then performs a similarity search on Qdrant. This will then produce the nearest 3 semantic chunks to that query. We could not get FFMPEG to work so instead our gradio app returns the entire video of that related semantic chunk.
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
python rag_chatwithyourvideolibraryaiproject_ctg7987.py
```
## Uploaded the extracted videos on the drive
https://drive.google.com/drive/folders/1Z75-gLM_Pk5vBiZ7l9uI8-Wus-b-sNzK

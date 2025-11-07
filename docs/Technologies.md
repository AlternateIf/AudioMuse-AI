# Technology Stack Overview

AudioMuse AI is built on a curated set of reliable, open‑source technologies that power its web interface, audio analysis, 
background processing and data persistence.

Below is overview of each component and its role in the system.

---

## Web & API Layer

### **Flask**
:link: https://flask.palletsprojects.com/  
Lightweight Python web framework used to expose the UI and REST API endpoints.

### **Supervisord**
:link: https://supervisord.org/  
A Client/Server system that manages and monitors multiple processes (API server, workers, queues) on a UNIX-like operating system.

---

## Background Processing

### **Redis Queue (RQ)**
:link: https://redis.io/glossary/redis-queue/  
Handles asynchronous task execution, allowing processes to be run in the background.

---

## Audio Analysis & Feature Extraction

### **Librosa**  
:link: https://github.com/librosa/librosa  
Used for audio preprocessing, feature extraction, and general DSP operations.

### **MusicNN (TensorFlow Models from Essentia)**  
:link: https://essentia.upf.edu/models.html
Open-source MIR (Music Information Retrieval) framework.  
Used for MusicNN deep learning models prior to ONNX migration.

---

## Machine Learning Inference

### **ONNX + ONNX Runtime**  *(from v0.7.0-beta onward)*  
:link: https://onnx.ai/  
:link: https://onnxruntime.ai/  
Fast, portable cross‑platform model execution engine.  
Replaced TensorFlow for improved performance, lightweight deployment, and broader hardware support.

### **scikit-learn**  
:link: https://scikit-learn.org/  
Used for classical ML algorithms, clustering, and similarity computations.

### **voyager (Spotify)**  *(since v0.6.3-beta)*  
:link: https://github.com/spotify/voyager  
Approximate Nearest Neighbor (ANN) search powering the `/similarity` interface.

---

## LLM Integration

### **Ollama**  
:link: https://ollama.com/  
Enables local/runtime execution of open-source LLMs—for example, to intelligently suggest playlist names.

---

## Data Storage

### **PostgreSQL**
:link: https://www.postgresql.org/  
Primary persistent data store for metadata, analysis results, similarity vectors, and system state.

---

## Deployment & Packaging

### **OCI Containers**
:link: https://www.docker.com/  
:link: https://podman.io/  
:link: https://kubernetes.io/  
The entire backend (API, workers, queue, database) is containerized for consistent, portable deployment.  
Supports Docker, Podman, and any OCI‑compatible runtime.
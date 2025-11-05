AudioMuse AI is built upon a robust stack of open-source technologies:

* [**Flask:**](https://flask.palletsprojects.com/) Provides the lightweight web interface for user interaction and API endpoints.  
* [**Redis Queue (RQ):**](https://redis.io/glossary/redis-queue/) A simple Python library for queueing jobs and processing them in the background with Redis.
* [**Supervisord:**](https://supervisord.org/) Supervisor is a client/server system that allows its users to monitor and control a number of processes on UNIX-like operating systems.
* [**Essentia-tensorflow**](https://essentia.upf.edu/) An open-source library for audio analysis, feature extraction, and music information retrieval. (used only until version v0.5.0-beta)
* [**MusicNN Tensorflow Audio Models from Essentia**](https://essentia.upf.edu/models.html) Leverages pre-trained MusicNN models for feature extraction and prediction. More details and models.
* [**Librosa**](https://github.com/librosa/librosa) Library for audio analysis, feature extraction, and music information retrieval. (used from version v0.6.0-beta)
* [**ONNX**](https://onnx.ai/) Open Neural Network Exchange format and [ONNX Runtime](https://onnxruntime.ai/) for fast, portable, cross-platform model inference. **(Used from v0.7.0-beta, replaces TensorFlow)**
* [**Tensorflow**](https://www.tensorflow.org/) Platform developed by Google for building, training, and deploying machine learning and deep learning models. **(Used only in versions before v0.7.0-beta)**
* [**scikit-learn**](https://scikit-learn.org/) Utilized for machine learning algorithms:
* [**voyager**](https://github.com/spotify/voyager) Approximate Nearest Neighbors used for the /similarity interface. Used from v0.6.3-beta
* [**PostgreSQL:**](https://www.postgresql.org/) A powerful, open-source relational database used for persisting:  
* [**Ollama**](https://ollama.com/) Enables self-hosting of various open-source Large Language Models (LLMs) for tasks like intelligent playlist naming.
* [**Docker / OCI-compatible Containers**](https://www.docker.com/) – The entire application is packaged as a container, ensuring consistent and portable deployment across environments.

![GitHub license](https://img.shields.io/github/license/neptunehub/AudioMuse-AI.svg)
![Latest Tag](https://img.shields.io/github/v/tag/neptunehub/AudioMuse-AI?label=latest-tag)
![Media Server Support: Jellyfin 10.10.7, Navidrome 0.58.0, LMS v3.69.0, Lyrion 9.0.2, Emby 4.9.1.80](https://img.shields.io/badge/Media%20Server-Jellyfin%2010.10.7%2C%20Navidrome%200.58.0%2C%20LMS%20v3.69.0%2C%20Lyrion%209.0.2%2C%20Emby%204.9.1.80-blue?style=flat-square&logo=server&logoColor=white)


<h1 align="center">
AudioMuse-AI - Where Music Takes Shape
</h1>

<p align="center">
    <img src="screenshot/logo.png?raw=true" alt="AudioMuse-AI Logo" width="250">
</p>

AudioMuse-AI is an open-source, Dockerized environment that brings **automatic playlist generation** to your self-hosted music library. 
It features [Jellyfin](https://jellyfin.org), [Navidrome](https://www.navidrome.org/), [LMS](https://github.com/epoupon/lms/tree/master), [Lyrion](https://lyrion.org/), and [Emby](https://emby.media) integrations with more to come. 

Using tools such as [Librosa](https://github.com/librosa/librosa) and [ONNX](https://onnx.ai/), it performs **sonic analysis** on your audio files locally, 
allowing you to curate playlists for any mood or occasion without relying on external APIs.

# Feature Overview

- :link: **Clustering**  
  Automatically group sonically similar songs and create genre-defying playlists based on the music's actual sound. 
  AI Integration (Gemini, Mistral, Ollama) can be used to find nice names for the auto generated playlists. 

- :zap: **Instant Playlists**  
  Tell AudioMuse what you would like to hear and it will instantly generate a playlist for you. (e.g "high-tempo, low-energy music")

- :globe_with_meridians: **Music Map**
    Discover your music collection visually with a vibrant, genre-based 2D map.

- :musical_keyboard: **Playlist from Similar Songs**  
  Pick a track you love, and AudioMuse will find all the songs in your library that share its sonic signature, creating a new discovery playlist.

- :arrow_right: **Song Paths**  
  Create a seamless listening journey between two songs. AudioMuse-AI finds the perfect tracks to bridge the sonic gap.

- :sound: **Sonic Fingerprint**  
  Generates playlists based on your listening habits, finding tracks similar to what you've been playing most often.

- :musical_score: **Song Alchemy**  
  Mix your ideal vibe, mark tracks as "ADD" or "SUBTRACT" to get a curated playlist and a 2D preview. Export the final selection directly to your media server.

# Hardware Requirements

| Component               | Minimum Specification                            | Recommended Specification           |
|-------------------------|--------------------------------------------------|-------------------------------------|
| CPU                     | Quad-Core Intel or ARM CPU (2015 or more recent) | Octa-Core Intel / ARM CPU or higher |
| Memory (RAM)            | 5 GB                                             | 8 GB or higher                      |
| Storage                 | 20 GB SSD                                        | 20 GB NVMe SSD                      |
| OS                      | Windows, macOS, Linux via Docker                 | -                                   |
| Additional Requirements | AVX Support                                      | -                                   |

- It may run on older CPUs (3rd generation and above) and with less RAM (for example, 4 GB), but these configurations are untested.

To check which hardware has already been confirmed working check [Tested Hardware and Configuration](docs/HARDWARE.md). 
If you have tested the software on missing configurations feel free to create an issue, so we can add the configuration to the list.

# Installation

There are 3 ways to spin up your AudioMuse instance. To learn more about them follow the links below
1. [Docker](docs/Docker.md)
2. [Podman](docs/Podman.md)
3. [Kubernetes](docs/Kubernetes.md)

> It is also possible to mix those ways in case you are using the advanced setup. (e.g. docker server [Flask+Postgres+Redis] and Podman Worker [])

Want to learn more about what technologies AudioMuse uses? Check out the [Technologies](docs/Technologies.md)

# Setup

[comment]: <> (todo @AlternateIf finish this section)
Info about setup here (e.g. first run analysis. hwo to access the web interface etc.)

# Misc

- **Frequently Asked Question (FAQ)** can be found [here](docs/FAQ.md).
- The **Image Tagging Strategy** can be found [here](docs/Image-Tagging.md)

# How To Contribute

Contributions, issues, and feature requests are welcome\!  
This is a BETA early release, so expect bugs or functions that are still not implemented.

For more details on how to contribute please follow the [Contributing Guidelines](https://github.com/NeptuneHub/AudioMuse-AI/blob/main/CONTRIBUTING.md)

# AudioMuse-AI related repositories

* [AudioMuse-AI Helm Chart](https://github.com/NeptuneHub/AudioMuse-AI-helm): helm chart for easy installation on Kubernetes;
* [AudioMuse-AI Plugin for Jellyfin](https://github.com/NeptuneHub/audiomuse-ai-plugin): Jellyfin Plugin;
* [AudioMuse-AI MusicServer](https://github.com/NeptuneHub/AudioMuse-AI-MusicServer): **Experimental** Open Subosnic like Music Sever with integrated sonic functionality.

# Disclaimer

Despite the similar name, this project (**AudioMuse-AI**) is an independent, community-driven effort. It has no official connection to the website `audiomuse.ai`.

<p align="center">
  <img src="screenshot/AM-AI-MAP.png?raw=true" alt="AudioMuse-AI Logo" width="480">
</p>

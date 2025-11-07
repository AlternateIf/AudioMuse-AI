# Image Tagging Strategy & Experimental Nvidia Support

## Image Tagging Strategy

Our automated GitHub Actions workflow continuously builds and publishes Docker images.  
Below is the versioning and tagging convention we follow:

| Tag                                              | Source Branch    | Description                                                             | Recommended Use                          |
|:-------------------------------------------------|:-----------------|:------------------------------------------------------------------------|:-----------------------------------------|
| **`:latest`**                                    | `main`           | Latest stable release, fully tested and suitable for production.        | Recommended for most users               |
| **`:devel`**                                     | `devel`          | Development branch containing upcoming features. Not guaranteed stable. | For testing and development only         |
| **`:vX.Y.Z`** (e.g., `:v0.1.4-alpha`, `:v1.0.0`) | Git release tags | Immutable, version-locked builds for reproducible deployments.          | Use when pinning to a specific version   |
> **Experimental NVIDIA images**  
> Tags ending in `-nvidia` (e.g., `:latest-nvidia`) include CUDA support for GPU acceleration, which can speed up processing of tracks  
> These builds are **experimental** though and provided for users who wish to test or contribute to GPU integration.  
> It has been tested with an NVidia RX 3060 running CUDA 12.9 and Driver V575.64.05. During testing, the worker used up to 10GiB of VRAM, 
> but this may vary on your instances

---

## :bulb: Summary

- Use **`:latest`** for stable, general use.  
- Use **`:devel`** only to test upcoming features.  
- Use **`:vX.Y.Z`** for reproducibility.  
- Use **`*-nvidia`** only if you’re actively testing GPU functionality.
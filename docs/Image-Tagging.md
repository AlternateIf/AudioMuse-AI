### (Optional) Experimental Nvidia Support

NVidia GPU support is available for the worker process. This can significantly speed up processing of tracks. 

This has been tested with an NVidia RX 3060 running CUDA 12.9 and Driver V575.64.05. During testing, the worker used up to 10GiB of VRAM but your mileage may vary.

## **Docker Image Tagging Strategy**

Our GitHub Actions workflow automatically builds and pushes Docker images. Here's how our tags work:

* :**latest**  
  * Builds from the **main branch**.  
  * Represents the latest stable release.  
  * **Recommended for most users.**  
* :**devel**  
  * Builds from the **devel branch**.  
  * Contains features still in development, not fully tested, and they could not work.  
  * **Use only for development.**  
* :**vX.Y.Z** (e.g., :v0.1.4-alpha, :v1.0.0)  
  * Immutable tags created from **specific Git releases/tags**.  
  * Ensures you're running a precise, versioned build.  
  * **Use for reproducible deployments or locking to a specific version.**
 
**IMPORTANT:** the `-nvidia` images are experimental. Try them if you want to help us improve the support, but we do not recommend using them for daily production use.
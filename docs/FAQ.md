# AudioMuse-AI FAQ

*A guide for deploying and using AudioMuse-AI. If you have other questions that are not mentioned here check the [README](/README.md)
or create an issue for your question.*

## Deployment

### What are the hardware requirements?

AudioMuse-AI work on both ARM and INTEL architecture and there is an experimental Nvidia image available.


| Component               | Minimum Specification                            | Recommended Specification           |
|-------------------------|--------------------------------------------------|-------------------------------------|
| CPU                     | Quad-Core Intel or ARM CPU (2015 or more recent) | Octa-Core Intel / ARM CPU or higher |
| Memory (RAM)            | 5 GB                                             | 8 GB or higher                      |
| Storage                 | 20 GB SSD                                        | 20 GB NVMe SSD                      |
| OS                      | Windows, macOS, Linux via Docker                 | -                                   |
| Additional Requirements | AVX Support                                      | -                                   |

You might also check [this](/README.md#hardware-requirements).


### How to deploy AudioMuse-AI?

You can run Audiomuse on either Kubernetes, with Docker or Podman. To read more about how to deploy them follow the [README](/README.md#installation).

If you're not able to reach the front-end on **[http://YOUR-IP:8000](http://YOUR-IP:8000)** or the analysis seems to finish without analyzing anything, 
it usually means that some parameters are missing in your `.env`. In this case take a look at the [.env.example](/deployment/.env.example)


### Can AudioMuse-AI support multiple music libraries?

Yes, it can support multiple music libraries within a single media server instance (e.g., two separate music folders in one Jellyfin server). 
However, a single AudioMuse-AI instance cannot connect to multiple different media servers (e.g., one Jellyfin and one Navidrome server) at the same time. 

The ENV variable `MUSIC_LIBRARIES` can be used for match multiple music library on the same music server. 
The variable is a comma-separated list of music libraries/folders for analysis. If empty, all libraries/folders are scanned. 

> For Lyrion: Use folder paths like "/music/myfolder". 

> For Jellyfin/Navidrome: Use library/folder names.

To learn more about the env variables check [Config-Params](/docs/Config-Params.md)

## User Guide

> Most front-end parameters can also be set as environment variables. See [Config-Params](/docs/Config-Params.md)

### How do I start using AudioMuse-AI?

After deployment, the first thing to do is access the AudioMuse-AI frontend, which is available at **[http://YOUR-IP:8000](http://YOUR-IP:8000)** if you haven't changed the default Ports.

From there, run the **Analysis**. This process collects information about your songs and stores it in your local database.

Running the analysis is **mandatory** before you can use any other features.

Make sure to also check the Setup Chapter in the [README](/README.md#setup)

### How long does the analysis take? What if it gets interrupted midway?

The time required for the analysis depends on several factors, such as the number of songs to analyze and the hardware on which AudioMuse-AI is running.

Depending on these factors, it can take anywhere from a few hours to several days. 

Already analyzed songs are stored in the database. If the process is interrupted, you can restart it and only missing songs will be analyzed.

### Clustering returns empty playlist or with only a few songs. How can I fix this?

The default clustering parameters are fine-tuned for music collections of around **50,000–100,000 songs**.
If your clusters are too small or is empty, you can adjust the following values in the **Advanced Parameters** view:

* **`Stratified Sampling Target Percentile`**:
  Defines the percentile of songs sampled per genre for clustering.
  The higher this value, the more songs will be clustered. You can set it to **100** to include more songs.

* **`min clusters` and `max clusters`**:
  By default, AudioMuse-AI creates between **40 and 100 clusters (playlists)**.
  Lowering these numbers will result in fewer clusters, each containing more songs.

You can learn more about the Config Params [here](/docs/Config-Params.md)

### Clustering returns clusters with big number of songs. How can I fix this?

You can raise the `Stratified Sampling Target Percentile`, `min clusters` and `max clusters` values in the advanced parameter view. 
Check the [entry](#clustering-returns-empty-playlist-or-with-only-a-few-songs-how-can-i-fix-this) above.

### Clustering takes a lot of time, how can I make it run faster?

The Clustering algorithm is by default set to do 5000 runs. This means that multiple run are executed and the best is kept. 

You can lower this number in the front-end under `Clustering Runs:` to do less runs. 
For example with it being set to 1000 runs, the result should still be good enough and take a reasonable amount of time.

Another way to make it run faster is to outsource the worker to a stronger / different machine. To read more about this, check the advanced setups in
- [Docker](/docs/Docker.md)
- [Podman](/docs/Podman.md)
- [Kubernetes](/docs/Kubernetes.md)
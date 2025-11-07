# **Deployment with Podman Quadlets**

To learn more about how to deploy with Podman Quadlets check their official [documentation](https://docs.podman.io/en/latest/markdown/podman-systemd.unit.5.html)

This document is separated in two sections:

1. [**All-In-One solution (Basic Setup)**](#all-in-one-solution-basic-setup)
   - Runs all relevant services on the same instance. 
   - Instance must meet the [Hardware Requirements](/README.md#hardware-requirements). 
   - Instance needs to have Podman and systemd installed and working. Check the [official Podman website](https://podman.io/docs/installation) 
   - needs to have an active `Jellyfin`|`Navidrome`|`Lyrion`|`Emby` on the same or a separate instance
2. [**Server + Worker Solution (Advanced Setup)**](#server--worker-solution-advanced-setup)
   - can run each service on a separate instance. (Redis, Postgres, Flask App, Worker). In the advanced example a 2 machine setup is shown that
     features Redis, Postgres and the Flask App one (server) instance and the worker on a separate (worker) instance. 
     This works great if you want to move the resource heavy part of AudioMuse to a separate instance 
   - server instance might work below required [Hardware Requirements](/README.md#hardware-requirements). 
   - worker instance should meet the [Hardware Requirements](/README.md#hardware-requirements)
   - Both instances need to have Podman and systemd installed. Check the [official Podman website](https://podman.io/docs/installation) 
   - needs to have an active `Jellyfin`|`Navidrome`|`Lyrion`|`Emby` on the same or a separate instance

> The **Image Tagging Strategy** can be found [here](docs/Image-Tagging.md)


## All-In-One Solution (Basic Setup)

### Step 1: Download the required files

Download the container config files. Make sure you are using the right container folder in the next commands. You can find more info in the quadlets official [documentation](https://docs.podman.io/en/latest/markdown/podman-systemd.unit.5.html)

```bash
sudo wget -O /etc/containers/systemd/audiomuse.pod https://raw.githubusercontent.com/NeptuneHub/AudioMuse-AI/refs/heads/main/deployment/podman-quadlets/audiomuse.pod
sudo wget -O /etc/containers/systemd/audiomuse-ai-flask.container https://raw.githubusercontent.com/NeptuneHub/AudioMuse-AI/refs/heads/main/deployment/podman-quadlets/audiomuse-ai-flask.container
sudo wget -O /etc/containers/systemd/audiomuse-ai-postgres.container https://raw.githubusercontent.com/NeptuneHub/AudioMuse-AI/refs/heads/main/deployment/podman-quadlets/audiomuse-postgres.container
sudo wget -O /etc/containers/systemd/audiomuse-ai-redis.container https://raw.githubusercontent.com/NeptuneHub/AudioMuse-AI/refs/heads/main/deployment/podman-quadlets/audiomuse-redis.container
sudo wget -O /etc/containers/systemd/audiomuse-ai-worker.container https://raw.githubusercontent.com/NeptuneHub/AudioMuse-AI/refs/heads/main/deployment/podman-quadlets/audiomuse-ai-worker.container
```

### Step 2: Update the container files with your settings

```dotenv
    Environment=SERVICE_TYPE=flask 
    # Jellyfin specific settings (comment these with # if you are using Emby, Navidrome, or Lyrion)
    Environment=MEDIASERVER_TYPE=jellyfin
    Environment=JELLYFIN_USER_ID=JELLYFIN_USER_ID JELLYFIN_TOKEN=JELLYFIN_TOKEN JELLYFIN_URL= JELLYFIN_URL
    # EMBY specific settings (uncomment these if you are using Emby) #
    #Environment=MEDIASERVER_TYPE=emby
    #Environment=EMBY_USER_ID=EMBY_USER_ID EMBY_TOKEN=EMBY_TOKEN EMBY_URL=EMBY_URL
    # LYRION specific settings (uncomment these if you are using Lyrion) #
    #Environment=MEDIASERVER_TYPE=lyrion
    #Environment=LYRION_URL=LYRION_URL
    # NAVIDROME specific settings (uncomment these if you are using Navidrom) #
    #Environment=MEDIASERVER_TYPE=navidrome 
    #Environment=NAVIDROME_URL=YOUR-NAVIDROME-URL NAVIDROME_USER=YOUR-USER NAVIDROME_PASSWORD=YOUR-PASSWORD
    Environment=POSTGRES_USER=audiomuse POSTGRES_PASSWORD=audiomusepassword 
    Environment=POSTGRES_DB=audiomusedb POSTGRES_HOST=localhost POSTGRES_PORT=5432 
    Environment=REDIS_URL=redis://localhost:6379/0 
    Environment=GEMINI_API_KEY=YOUR_GEMINI_API_KEY_HERE
    Environment=GEMINI_MODEL_NAME=gemini-2.5-flash
    Environment=MISTRAL_API_KEY=MISTRAL_API_KEY
    Environment=OLLAMA_SERVER_URL=OLLAMA_SERVER_URL
    Environment=TEMP_DIR=/app/temp_audio
```

Once you have your mediaserver section (`Jellyfin`|`Navidrome`|`Lyrion`|`Emby`) active you will need to set the values for it 
as well as potentially changing the Redis and Postgres settings. If you plan on using AI to name your playlists you will also need to
set the settings of your desired AI Provider  (`Gemini`|`Mistral`|`Ollama`)

If you want to use the nvidia images instead of the ARM/Intel Image you can search the container for nvidia to find instructions.

In case you want to check out other available .env variables check out [Config-Params](/docs/Config-Params.md)

### Step 3: Start the containers

```bash
systemctl --user daemon-reload
systemctl --user start audiomuse-pod
```

Do you want to stop the containers. Just run:

```bash
systemctl --user stop audiomuse-pod
```

### Step 4: Access the Application

Once the container are running you can access the web app at `http://localhost:8000`. Make sure that you are using the
Port that you defined for the Flask App in your pod file. The default is set to 8000

## Server + Worker Solution (Advanced Setup)

### Step 1: Download the required files

Download the container config files. Make sure you are using the right container folder in the next commands. You can find more info in the quadlets official [documentation](https://docs.podman.io/en/latest/markdown/podman-systemd.unit.5.html)

#### Server Instance:

```bash
sudo wget -O /etc/containers/systemd/audiomuse.pod https://raw.githubusercontent.com/NeptuneHub/AudioMuse-AI/refs/heads/main/deployment/podman-quadlets/audiomuse.pod
sudo wget -O /etc/containers/systemd/audiomuse-ai-flask.container https://raw.githubusercontent.com/NeptuneHub/AudioMuse-AI/refs/heads/main/deployment/podman-quadlets/audiomuse-ai-flask.container
sudo wget -O /etc/containers/systemd/audiomuse-ai-postgres.container https://raw.githubusercontent.com/NeptuneHub/AudioMuse-AI/refs/heads/main/deployment/podman-quadlets/audiomuse-postgres.container
sudo wget -O /etc/containers/systemd/audiomuse-ai-redis.container https://raw.githubusercontent.com/NeptuneHub/AudioMuse-AI/refs/heads/main/deployment/podman-quadlets/audiomuse-redis.container
```

#### Worker Instance

```bash
sudo wget -O /etc/containers/systemd/audiomuse.pod https://raw.githubusercontent.com/NeptuneHub/AudioMuse-AI/refs/heads/main/deployment/podman-quadlets/audiomuse-worker.pod
sudo wget -O /etc/containers/systemd/audiomuse-ai-worker.container https://raw.githubusercontent.com/NeptuneHub/AudioMuse-AI/refs/heads/main/deployment/podman-quadlets/audiomuse-ai-worker.container
```

### Step 2: Update the container file with your settings

```dotenv
Environment=SERVICE_TYPE=flask
# Jellyfin specific settings (comment these with # if you are using Emby, Navidrome, or Lyrion)
Environment=MEDIASERVER_TYPE=jellyfin
Environment=JELLYFIN_USER_ID=JELLYFIN_USER_ID JELLYFIN_TOKEN=JELLYFIN_TOKEN JELLYFIN_URL= JELLYFIN_URL
# EMBY specific settings (uncomment these if you are using Emby) #
#Environment=MEDIASERVER_TYPE=emby
#Environment=EMBY_USER_ID=EMBY_USER_ID EMBY_TOKEN=EMBY_TOKEN EMBY_URL=EMBY_URL
# LYRION specific settings (uncomment these if you are using Lyrion) #
#Environment=MEDIASERVER_TYPE=lyrion
#Environment=LYRION_URL=LYRION_URL
# NAVIDROME specific settings (uncomment these if you are using Navidrom) #
#Environment=MEDIASERVER_TYPE=navidrome
#Environment=NAVIDROME_URL=YOUR-NAVIDROME-URL NAVIDROME_USER=YOUR-USER NAVIDROME_PASSWORD=YOUR-PASSWORD
Environment=POSTGRES_USER=audiomuse POSTGRES_PASSWORD=audiomusepassword 
Environment=POSTGRES_DB=audiomusedb POSTGRES_HOST=localhost POSTGRES_PORT=5432 
Environment=REDIS_URL=redis://localhost:6379/0 
Environment=GEMINI_API_KEY=YOUR_GEMINI_API_KEY_HERE
Environment=GEMINI_MODEL_NAME=gemini-2.5-flash
Environment=MISTRAL_API_KEY=MISTRAL_API_KEY
Environment=OLLAMA_SERVER_URL=OLLAMA_SERVER_URL
Environment=TEMP_DIR=/app/temp_audio
```

Once you have your mediaserver section (`Jellyfin`|`Navidrome`|`Lyrion`|`Emby`) active you will need to set the values for it 
as well as potentially changing the Redis and Postgres settings. If you plan on using AI to name your playlists you will also need to
set the settings of your desired AI Provider  (`Gemini`|`Mistral`|`Ollama`)

If you want to use the nvidia images instead of the ARM/Intel Image you can search the container for nvidia to find instructions.

In case you want to check out other available .env variables check out [Config-Params](/docs/Config-Params.md)

Note that for the Server + Worker solution to work you need to set the variables below in your container files.

```dotenv
# Remote worker Variables [Not Required for the All-In-One Solution / Basic Setup]
Environment=WORKER_URL=WORKER_URL
Environment=WORKER_POSTGRES_HOST=WORKER_POSTGRES_HOST WORKER_REDIS_URL=WORKER_REDIS_URL
```

### Step 3: Start the containers

```bash
systemctl --user daemon-reload
systemctl --user start audiomuse-pod
```

Do you want to stop the containers. Just run:

```bash
systemctl --user stop audiomuse-pod
```

### Step 4: Access the Application

Once the container are running you can access the web app at `http://localhost:8000` on your server instance. Make sure that you are using the
Port that you defined for the Flask App in your pod file. The default is set to 8000
# **Deployment with Docker Compose**

This document is separated in two sections:

1. [**All-In-One solution (Basic Setup)**](#all-in-one-solution-basic-setup)
   - Runs all relevant services on the same instance. 
   - Instance must meet the [Hardware Requirements](/README.md#hardware-requirements). 
   - Instance needs to have Docker and Docker compose installed and working. Check the [official Docker website](https://docs.docker.com/compose/install/) 
   - needs to have an active `Jellyfin`|`Navidrome`|`Lyrion`|`Emby`|`AudioMuse-AI-MusicServer` on the same or a separate instance
2. [**Server + Worker Solution (Advanced Setup)**](#server--worker-solution-advanced-setup)
   - runs Redis, Postgres and the Flask App on one (server) instance and the worker on a separate (worker) instance
   - server instance might work below required [Hardware Requirements](/README.md#hardware-requirements). 
   - worker instance should meet the [Hardware Requirements](/README.md#hardware-requirements)
   - Both instances need to have Docker and Docker Compose installed. Check the [official Docker website](https://docs.docker.com/compose/install/) 
   - needs to have an active `Jellyfin`|`Navidrome`|`Lyrion`|`Emby` on the same or a separate instance

## All-In-One Solution (Basic Setup)

### Step 1: Download the required files 

Create a directory to store your docker-compose and .env file for your instance
```
mkdir ./audiomuse-ai
cd ./audiomuse-ai
```

Download the [.env](/deployment/.env.example) file that houses all our environment settings
```
wget -O .env https://github.com/NeptuneHub/AudioMuse-AI/blob/main/deployment/.env.example
```

Download the docker-compose file. 

```
wget -O docker-compose.yml https://github.com/NeptuneHub/AudioMuse-AI/blob/main/deployment/docker-compose.yaml
```

### Step 2: Update the .env file with your settings

If you are using `Navidrome`,`Lyrion` or `Emby` uncomment the respective sections and comment the Jellyfin sections. 
If you have activated Emby it will look like this:

```
      # Jellyfin specific settings (comment these with # if you are using Emby, Navidrome, or Lyrion)
      #MEDIASERVER_TYPE: "jellyfin" # Specify the media server type
      #JELLYFIN_USER_ID: "${JELLYFIN_USER_ID}"
      #JELLYFIN_TOKEN: "${JELLYFIN_TOKEN}"
      #JELLYFIN_URL: "${JELLYFIN_URL}"
      # EMBY specific settings (uncomment these if you are using Emby) #
      MEDIASERVER_TYPE: "emby" # Specify the media server type
      EMBY_USER_ID: "${EMBY_USER_ID}"
      EMBY_TOKEN: "${EMBY_TOKEN}"
      EMBY_URL: "${EMBY_URL}"
      # LYRION specific settings (uncomment these if you are using Lyrion) #
      #MEDIASERVER_TYPE: "lyrion"
      #LYRION_URL: "${LYRION_URL}"
      # NAVIDROME specific settings (uncomment these if you are using Navidrom) #
      #MEDIASERVER_TYPE: "navidrome"
      #NAVIDROME_URL: "${NAVIDROME_URL}"
      #NAVIDROME_USER: "${NAVIDROME_USER}"
      #NAVIDROME_PASSWORD: "${NAVIDROME_PASSWORD}"
```

If you have your mediaserver section (`Jellyfin`|`Navidrome`|`Lyrion`|`Emby`) active you will need to set the values for it 
as well as potentially changing the Redis and Postgres settings. If you plan on using AI to name your playlists you will also need to
set the settings of your desired AI Provider  (`Gemini`|`Mistral`|`Ollama`)

If you want to use the nvidia images instead of the ARM/Intel Image you can search the docker compose for nvidia

[comment]: <> (todo @AlternateIf add url here)
In case you want to check out other available .env variables check out add url here

> If you use LMS instead of the password you need to create and use the Subsonic API token. 
> Additional Subsonic API based Mediaserver could require it in place of the password.

### Step 3: Start the containers

```
docker compose up -d
```

Do you want to stop the containers. Just run:

```
docker compose stop
```

#### Step 4: Access the Application
Once the container are running you can access the web app at `http://localhost:8000`. Make sure that you are using the
Port that you defined for the Flask App in your docker compose file. The default is set to 8000

## Server + Worker Solution (Advanced Setup)

[comment]: <> (todo @AlternateIf finish advanced setup worker + server)
### Step 1: Download the required files 

### Step 2: Update the .env file with your settings

### Step 3: Start the containers


**Remote worker tip:**
If you deploy a worker on different hardware (using `docker-compose-worker.yaml` or `docker-compose-worker-nvidia.yaml`), copy your `.env` to that machine and update `WORKER_POSTGRES_HOST` and `WORKER_REDIS_URL` so the worker can reach the main server.

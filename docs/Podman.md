todo @AlternateIf
# **Deployment with Podman Quadlets**

This document is separated in two sections:

1. [**All-In-One solution (Basic Setup)**](#all-in-one-solution-basic-setup)
   - Runs all relevant services on the same instance. 
   - Instance must meet the [Hardware Requirements](/README.md#hardware-requirements). 
   - Instance needs to have Podman and systemd installed and working. Check the [official Podman website](https://podman.io/docs/installation) 
   - needs to have an active `Jellyfin`|`Navidrome`|`Lyrion`|`Emby`` on the same or a separate instance
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

### Step 2: Update the .env file with your settings

### Step 3: Start the containers

### Step 4: Access the Application

## Server + Worker Solution (Advanced Setup)

### Step 1: Download the required files

### Step 2: Update the .env file with your settings

### Step 3: Start the containers

### Step 4: Access the Application









For an alternative local setup, [Podman Quadlet](https://docs.podman.io/en/latest/markdown/podman-systemd.unit.5.html) files are provided in the `deployment/podman-quadlets` directory for interacting with **Navidrome**. The unit files can  be edited for use with **Jellyfin**. 

These files are configured to automatically update AudioMuse-AI using the [latest](/docs/Image-Tagging.md) stable release and should perform an automatic rollback if the updated image fails to start.

**Steps:**
1.  **Navigate to the `deployment/podman-quadlets` directory:**
    ```bash
    cd deployment/podman-quadlets
    ```
2.  **Review and Customize:**

    The `audiomuse-ai-postgres.container` and `audiomuse-redis.container` files are pre-configured with default credentials and settings suitable for local testing. <BR>
    You will need to edit environment variables within `audiomuse-ai-worker.container` and `audiomuse-ai-flask.container` files to reflect your personal credentials and environment.
    * For **Navidrome**, update `NAVIDROME_URL`, `NAVIDROME_USER` and `NAVIDROME_PASSWORD` with your real credentials.  
    * For **Jellyfin** replace these variables with `JELLYFIN_URL`, `JELLYFIN_USER_ID`, `JELLYFIN_TOKEN`; add your real credentials; and change the `MEDIASERVER_TYPE` to `jellyfin`. 

    Once you've customized the unit files, you will need to copy all of them into a systemd container directory, such as `/etc/containers/systemd/user/`.<BR>

3.  **Start the Services:**
    ```bash
    systemctl --user daemon-reload
    systemctl --user start audiomuse-pod
    ```
    The first command reloads systemd (generating the systemd service files) and the second command starts all AudioMuse services (Flask app, RQ worker, Redis, PostgreSQL).
4.  **Access the Application:**
    Once the containers are up, you can access the web UI at `http://localhost:8000`.
5.  **Stopping the Services:**
    ```bash
    systemctl --user stop audiomuse-pod
    ```
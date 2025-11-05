## **Local Deployment with Docker Compose**

AudioMuse-AI provides Docker Compose files for different media server backends:

- **Jellyfin**: Use `deployment/docker-compose.yaml`
- **Navidrome**: Use `deployment/docker-compose-navidrome.yaml`
- **Lyrion**: Use `deployment/docker-compose-lyrion.yaml`
- **Emby**: Use `deployment/docker-compose-emby.yaml`

Choose the appropriate file based on your media server setup.

**Prerequisites:**
*   Docker and Docker Compose installed.
*   `Jellyfin` or `Navidrome` or `Lyrion` or `Emby` installed.
*   Respect the [hardware requirements](#hardware-requirements)

**Steps:**
1.  **Create your environment file:**
    ```bash
    cp deployment/.env.example deployment/.env
    ```
    you can find the example here: [deployment/.env.example](deployment/.env.example)
    
2.  **Review and Customize:**
    Edit `.env` and provide the media-server credentials (e.g., `JELLYFIN_URL`, `JELLYFIN_USER_ID`, `JELLYFIN_TOKEN` or `NAVIDROME_*`, `EMBY_*`, `LYRION_URL`) along with any API keys (`GEMINI_API_KEY`, `MISTRAL_API_KEY`). The same values are injected into every compose file, so you only need to edit them here.
3.  **Start the Services:**
    ```bash
    docker compose -f deployment/docker-compose.yaml up -d
    ```
    Swap the compose filename if you're targeting Navidrome (`docker-compose-navidrome.yaml`), Lyrion (`docker-compose-lyrion.yaml`) or Emby (`docker-compose-emby.yaml`). This command starts all services (Flask app, RQ workers, Redis, PostgreSQL) in detached mode (`-d`).

    **IMPORTANT:** both `docker-compose.yaml` and `.env` file need to be in the same directory.
5.  **Access the Application:**
    Once the containers are up, you can access the web UI at `http://localhost:8000`.
6.  **Stopping the Services:**
    ```bash
    docker compose -f deployment/docker-compose.yaml down
    ```
    Swap the compose filename here as well if you started a different variant.
**Note:**
  > If you use LMS instead of the password you need to create and use the Subsonic API token. Additional Subsonic API based Mediaserver could require it in place of the password.

**Remote worker tip:**
If you deploy a worker on different hardware (using `docker-compose-worker.yaml` or `docker-compose-worker-nvidia.yaml`), copy your `.env` to that machine and update `WORKER_POSTGRES_HOST` and `WORKER_REDIS_URL` so the worker can reach the main server.

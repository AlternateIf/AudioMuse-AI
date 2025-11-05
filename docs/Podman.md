## **Local Deployment with Podman Quadlets**

For an alternative local setup, [Podman Quadlet](https://docs.podman.io/en/latest/markdown/podman-systemd.unit.5.html) files are provided in the `deployment/podman-quadlets` directory for interacting with **Navidrome**. The unit files can  be edited for use with **Jellyfin**. 

These files are configured to automatically update AudioMuse-AI using the [latest](#docker-image-tagging-strategy) stable release and should perform an automatic rollback if the updated image fails to start.

**Prerequisites:**
*   Podman and systemd.
*   `Jellyfin` or `Navidrome` installed.
*   Respect the [hardware requirements](#hardware-requirements)

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

**IMPORTANT:** From `v0.7.0-beta`, ONNX replaces TensorFlow. As a result, some CPUs previously not supported may now work.
## **Quick Start Deployment on K3S WITH HELM**

The best way to install AudioMuse-AI on K3S (kubernetes) is by [AudioMuse-AI Helm Chart repository](https://github.com/NeptuneHub/AudioMuse-AI-helm)

*  **Prerequisites:**
    *   A running `K3S cluster`.
    *   `kubectl` configured to interact with your cluster.
    *   `helm` installed.
    *   `Jellyfin` or `Navidrome` or `Lyrion` installed.
    *   Respect the HW requirements (look the specific chapter)

You can directly check the Helm Chart repo for more details and deployments examples.

## **Quick Start Deployment on K3S**

This section provides a minimal guide to deploy AudioMuse-AI on a K3S (Kubernetes) cluster by directly using the `deployment` manifests.

* **Prerequisites:**
    *   A running K3S cluster.
    *   `kubectl` configured to interact with your cluster.
    *   `Jellyfin` or `Navidrome` or `Lyrion` installed.
    *   Respect the HW requirements (look the specific chapter)

*  **Jellyfin Configuration:**
    *   Navigate to the `deployment/` directory.
    *   Edit `deployment.yaml` to configure mandatory parameters:
        *   **Secrets:**
            *   `jellyfin-credentials`: Update `api_token` and `user_id`.
            *   `postgres-credentials`: Update `POSTGRES_USER`, `POSTGRES_PASSWORD`, and `POSTGRES_DB`.
            *   `gemini-api-credentials` (if using Gemini for AI Naming): Update `GEMINI_API_KEY`.
            *   `mistral-api-credentials` (if using Mistral for AI Naming): Update `MISTRAL_API_KEY`.
        *   **ConfigMap (`audiomuse-ai-config`):**
            *   Update `JELLYFIN_URL`.
            *   Ensure `POSTGRES_HOST`, `POSTGRES_PORT`, and `REDIS_URL` are correct for your setup (defaults are for in-cluster services).

*  **Navidrome/LMS (Open Subsonic API Music Server) Configuration:**
    *   Navigate to the `deployment/` directory.
    *   Edit `deployment-navidrome.yaml` to configure mandatory parameters:
        *   **Secrets:**
            *   `navidrome-credentials`: Update `NAVIDROME_USER` and `NAVIDROME_PASSWORD`.
            *   `postgres-credentials`: Update `POSTGRES_USER`, `POSTGRES_PASSWORD`, and `POSTGRES_DB`.
            *   `gemini-api-credentials` (if using Gemini for AI Naming): Update `GEMINI_API_KEY`.
            *   `mistral-api-credentials` (if using Mistral for AI Naming): Update `MISTRAL_API_KEY`.
        *   **ConfigMap (`audiomuse-ai-config`):**
            *   Update `NAVIDROME_URL`.
            *   Ensure `POSTGRES_HOST`, `POSTGRES_PORT`, and `REDIS_URL` are correct for your setup (defaults are for in-cluster services).
        *   > The same instruction used for Navidrome could apply to other Mediaserver that support Subsonic API. LMS for example is supported, only remember to user the Subsonic API token instead of the password.

*  **Lyrion Configuration:**
    *   Navigate to the `deployment/` directory.
    *   Edit `deployment-lyrion.yaml` to configure mandatory parameters:
        *   **Secrets:**
            *   `postgres-credentials`: Update `POSTGRES_USER`, `POSTGRES_PASSWORD`, and `POSTGRES_DB`.
            *   `gemini-api-credentials` (if using Gemini for AI Naming): Update `GEMINI_API_KEY`.
        *   **ConfigMap (`audiomuse-ai-config`):**
            *   Update `LYRION_URL`.
            *   Ensure `POSTGRES_HOST`, `POSTGRES_PORT`, and `REDIS_URL` are correct for your setup (defaults are for in-cluster services).
            
*  **Deploy:**
    ```bash
    kubectl apply -f deployment/deployment.yaml
    ```
*  **Access:**
    *   **Main UI:** Access at `http://<EXTERNAL-IP>:8000`
    *   **API Docs (Swagger UI):** Explore the API at `http://<EXTERNAL-IP>:8000/apidocs`
# :computer: Tested Hardware & Configurations

This document lists confirmed working configurations for **AudioMuse-AI**, split by backend version.

> **Note:**  
> Hardware not listed here simply hasn’t been tested yet — it may still work.  
> If you encounter issues with a particular setup, please open a GitHub issue.

---

## With ONNX Backend (from `v0.7.0-beta`)

|                           Issue ID                            | Hardware                                                  | Configuration                                          | Supported | Notes                                   |
|:-------------------------------------------------------------:|-----------------------------------------------------------|--------------------------------------------------------|:---------:|-----------------------------------------|
|                               —                               | **CPU:** Intel i5 6th Gen / i5 8th Gen; **ARM:** Cloud VM | K3S cluster • Docker Image `:0.7.0-beta`               |   ✅ Yes   | —                                       |
|                               —                               | **CPU:** Intel i5-12450H                                  | K3S cluster • Docker Image `:0.7.0-beta`               |   ✅ Yes   | —                                       |
| [#104](https://github.com/NeptuneHub/AudioMuse-AI/issues/104) | **CPU:** Intel i5-12600K                                  | Docker Compose • Jellyfin • Docker Image `:0.7.0-beta` |   ✅ Yes   | Container requires ≥ 4 GB RAM allocation |

---

## With TensorFlow Backend (up to `v0.6.10-beta`)

|                          Issue ID                           | Hardware                                           | Configuration                                                               |   Supported    | Notes                                                                |
|:-----------------------------------------------------------:|----------------------------------------------------|-----------------------------------------------------------------------------|:--------------:|----------------------------------------------------------------------|
| [#14](https://github.com/NeptuneHub/AudioMuse-AI/issues/14) | **CPU:** Ryzen 5600G                               | Docker Compose • Jellyfin                                                   |     ✅ Yes      | —                                                                    |
| [#24](https://github.com/NeptuneHub/AudioMuse-AI/issues/24) | **CPU:** Ryzen 5600G                               | TrueNAS SCALE • Docker Image `v0.6.0-beta` / `v0.6.2-beta`                  |     ✅ Yes      | —                                                                    |
| [#25](https://github.com/NeptuneHub/AudioMuse-AI/issues/25) | **CPU:** Intel i5 6th/8th Gen • ARM Raspberry Pi 5 | K3S cluster • Docker Image `:devel`                                         |     ✅ Yes      | —                                                                    |
| [#39](https://github.com/NeptuneHub/AudioMuse-AI/issues/39) | **CPU:** Ryzen 5 3600                              | Bazzite (Fedora Atomic) • Docker Image `v0.6.4-beta`                        |     ✅ Yes      | —                                                                    |
| [#55](https://github.com/NeptuneHub/AudioMuse-AI/issues/55) | **CPU:** Intel (32 cores) • **GPU:** RTX 3060      | Docker Swarm / Single Docker • Navidrome                                    |     ✅ Yes      | Analysis failed on hi-res FLACs; fixed after full Navidrome rescan   |
| [#62](https://github.com/NeptuneHub/AudioMuse-AI/issues/62) | **CPU:** Intel Xeon W-2125                         | Proxmox VE LXC (Debian) • Docker Image `v0.6.5-beta`                        |     ✅ Yes      | —                                                                    |
| [#66](https://github.com/NeptuneHub/AudioMuse-AI/issues/66) | **CPU:** Intel E5-2697                             | Docker Compose (via Portainer) • Navidrome 0.58.0                           |     ✅ Yes      | —                                                                    |
| [#67](https://github.com/NeptuneHub/AudioMuse-AI/issues/67) | **CPU:** Intel i7-10850H                           | Arch Linux • Docker Image `latest-nvidia`                                   |     ✅ Yes      | —                                                                    |
| [#69](https://github.com/NeptuneHub/AudioMuse-AI/issues/69) | **CPU:** Ryzen 5 PRO 4650G                         | Ubuntu 24.04.3 LTS • Docker Image `v0.6.7-beta`                             |     ✅ Yes      | —                                                                    |
| [#73](https://github.com/NeptuneHub/AudioMuse-AI/issues/73) | **CPU:** Intel i5-1035G1                           | Docker Compose • Jellyfin 10.10.7                                           |     ✅ Yes      | Database empty after analysis → Float precision bug fixed in `:devel` |
| [#74](https://github.com/NeptuneHub/AudioMuse-AI/issues/74) | **CPU:** Ryzen 3600                                | Docker Compose • Navidrome v0.58.0                                          |     ✅ Yes      | —                                                                    |
| [#65](https://github.com/NeptuneHub/AudioMuse-AI/issues/65) | **CPU:** Intel N100                                | Docker Compose • Navidrome                                                  |     ✅ Yes      | —                                                                    |
| [#93](https://github.com/NeptuneHub/AudioMuse-AI/issues/93) | **CPU:** Ryzen AI 9 HX 370 w/ Radeon 890M (64-bit) | Podman + Docker-Compose 5.6.1, Jellyfin 10.10.7, AudioMuse-AI `v0.6.8-beta` | 🚧 In Progress | Fix in `:devel` (`TF_ENABLE_ONEDNN_OPTS=0`) → configurable soon      |
| [#56](https://github.com/NeptuneHub/AudioMuse-AI/issues/56) | **CPU:** Intel Celeron N3160                       | Docker Compose • Unraid 7.1.4                                               |      ❌ No      | `Illegal instruction` → CPU lacks AVX support                        |
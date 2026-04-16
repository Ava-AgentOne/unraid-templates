<div align="center">

# 🖥️ Ava-AgentOne Unraid Templates

**Community Applications templates for Unraid**

[![Unraid](https://img.shields.io/badge/Unraid-Compatible-orange?logo=unraid)](https://unraid.net)

</div>

## 📦 Available Containers

| Container | Version | Description | Repo |
|-----------|---------|-------------|------|
| **ollama-intel** | v1.1 | Ollama with Intel iGPU acceleration via IPEX-LLM. Source-based build with weekly auto-updates. GPU device selection and parallel request control. | [GitHub](https://github.com/Ava-AgentOne/ollama-intel) |
| **ollama-dashboard** | v1.1 | Real-time Ollama monitoring dashboard. Tracks Ollama native + OpenAI /v1/ APIs. Optional Nemo Guardrails, prompt logging, 6 themes. | [GitHub](https://github.com/Ava-AgentOne/ollama-dashboard) |

## 🚀 How to Install

### Method 1: Docker Pull (Quick)

Pull and run any container directly:

```bash
docker pull ghcr.io/ava-agentone/ollama-intel:latest
docker pull ghcr.io/ava-agentone/ollama-dashboard:latest
```

See each container's [GitHub repo](#-available-containers) for full `docker run` commands and configuration options.

### Method 2: Unraid Private Apps (Recommended)

Add all containers to your Unraid **Apps** tab with auto-sync from this repo:

1. Run these commands in your Unraid terminal:
   ```bash
   mkdir -p /boot/config/plugins/community.applications/private/Ava-AgentOne

   curl -o /boot/config/plugins/community.applications/private/Ava-AgentOne/ollama-intel.xml \
     https://raw.githubusercontent.com/Ava-AgentOne/unraid-templates/main/ollama-intel.xml

   curl -o /boot/config/plugins/community.applications/private/Ava-AgentOne/ollama-dashboard.xml \
     https://raw.githubusercontent.com/Ava-AgentOne/unraid-templates/main/ollama-dashboard.xml
   ```
2. Go to **Apps** tab in the Unraid WebUI
3. Look for **Private Apps** in the left sidebar — your containers are there
4. Click **Install**, configure your settings, and click **Apply**

> 💡 **Auto-sync**: To automatically pick up new containers added to this repo, set up the [sync script](https://github.com/Ava-AgentOne/unraid-templates#-auto-sync-optional) below.

### 🔄 Auto-Sync (Optional)

Create a sync script that automatically downloads all templates from this repo:

1. Save this as `/boot/config/plugins/community.applications/private/sync-templates.sh` on your flash drive
2. Add it to the **User Scripts** plugin with schedule "At Array Start" or "Daily"
3. Any new container XML pushed to this repo will appear in Private Apps after the next sync

> **Note**: The "Template Repositories" setting was removed in Unraid 6.10+. Private Apps with a sync script is the recommended replacement.

## 📜 License

[MIT](https://opensource.org/licenses/MIT)

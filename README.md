<div align="center">

# 🖥️ Ava-AgentOne Unraid Templates

**Community Applications templates for Unraid**

[![Unraid](https://img.shields.io/badge/Unraid-Compatible-orange?logo=unraid)](https://unraid.net)

</div>

## 📦 Available Containers

| Container | Version | Description | Repo |
|-----------|---------|-------------|------|
| **ollama-intel** | v1.3 | Ollama with Intel iGPU acceleration via IPEX-LLM (bundled Ollama v0.9.x). Pinned, layered build, so updates only download what changed. GPU device selection and parallel request control. | [GitHub](https://github.com/Ava-AgentOne/ollama-intel) |
| **ollama-intel-vulkan** | v1.3 | *Experimental.* The current official Ollama on Intel iGPUs through Mesa's Vulkan driver. Rebuilt weekly to follow Ollama releases. | [GitHub](https://github.com/Ava-AgentOne/ollama-intel#-vulkan-variant-experimental) |
| **ollama-dashboard** | v1.2.2 | Real-time Ollama monitoring dashboard. Tracks Ollama native + OpenAI /v1/ APIs. Optional Nemo Guardrails, prompt logging, 6 themes. | [GitHub](https://github.com/Ava-AgentOne/ollama-dashboard) |

## 🚀 How to Install

### Method 1: Docker Pull (Quick)

Pull and run any container directly:

```bash
docker pull ghcr.io/ava-agentone/ollama-intel:latest
docker pull ghcr.io/ava-agentone/ollama-intel:vulkan
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

   curl -o /boot/config/plugins/community.applications/private/Ava-AgentOne/ollama-intel-vulkan.xml \
     https://raw.githubusercontent.com/Ava-AgentOne/unraid-templates/main/ollama-intel-vulkan.xml

   curl -o /boot/config/plugins/community.applications/private/Ava-AgentOne/ollama-dashboard.xml \
     https://raw.githubusercontent.com/Ava-AgentOne/unraid-templates/main/ollama-dashboard.xml
   ```
2. Go to **Apps** tab in the Unraid WebUI
3. Look for **Private Apps** in the left sidebar — your containers are there
4. Click **Install**, configure your settings, and click **Apply**

> 💡 **Auto-sync**: To automatically pick up new containers added to this repo, set up the [sync script](https://github.com/Ava-AgentOne/unraid-templates#-auto-sync-optional) below.

### 🔄 Auto-Sync (Optional)

A small script keeps your Private Apps templates up to date and picks up new containers added to this repo:

1. Install the **User Scripts** plugin from the Apps tab if you don't have it.
2. In **Settings → User Scripts**, click **Add New Script**, name it `sync-ava-templates`, then edit the script and replace its contents with:
   ```bash
   #!/bin/bash
   #description=Download the Ava-AgentOne container templates into Private Apps
   DEST=${DEST:-/boot/config/plugins/community.applications/private/Ava-AgentOne}
   REPO=Ava-AgentOne/unraid-templates
   mkdir -p "$DEST"
   files=$(curl -fsSL "https://api.github.com/repos/$REPO/contents" \
     | grep -o '"name": *"[^"]*\.xml"' | sed 's/.*"\([^"]*\)"$/\1/' | grep -vx 'ca_profile.xml')
   if [ -z "$files" ]; then
     echo "Could not list the templates (is GitHub reachable?)"
     exit 1
   fi
   for f in $files; do
     if curl -fsSL -o "$DEST/$f.tmp" "https://raw.githubusercontent.com/$REPO/main/$f"; then
       mv "$DEST/$f.tmp" "$DEST/$f"
       echo "Updated $f"
     else
       rm -f "$DEST/$f.tmp"
       echo "Failed to download $f"
     fi
   done
   ```
3. Set its schedule to **At Startup of Array** or **Scheduled Daily**, click **Apply**, and press **Run Script** once to check it works.

A template is only replaced after a complete download, so a failed sync leaves your current ones untouched. Templates removed from this repo stay in Private Apps until you delete them.

> **Note**: The "Template Repositories" setting was removed in Unraid 6.10+. Private Apps with a sync script is the recommended replacement.

## 📜 License

[MIT](https://opensource.org/licenses/MIT)

# Install on CasaOS via Portainer (portainer.io)

This project includes a ready-to-deploy stack file:

- `portainer-stack.yml`

It runs the browser-based app (`symlink-editor-web`) so no desktop GUI is required.

## Prerequisites

- CasaOS server running
- Portainer available from CasaOS App Store
- A shared data path mounted at `/DATA` on the host (default for CasaOS)

## 1) Put the project on your CasaOS host

From SSH on your CasaOS machine:

```bash
cd /DATA/AppData
mkdir -p symlink-editor
cd symlink-editor
# copy this repository here (git clone or upload files)
```

You should end up with files like:

- `/DATA/AppData/symlink-editor/symlink-editor-web`
- `/DATA/AppData/symlink-editor/portainer-stack.yml`

## 2) Deploy as a Portainer stack

1. Open Portainer in your browser.
2. Go to **Stacks** → **Add stack**.
3. Name it `symlink-editor`.
4. Paste the contents of `portainer-stack.yml` into the editor (or upload it).
5. Click **Deploy the stack**.

## 3) Open the app

- Visit: `http://192.168.1.14:9090`

The web app will browse and manage symlinks under mounted paths (including `/DATA`).

## 4) Optional customization

- Change startup folder by editing env var in stack:
  - `SYMLINK_EDITOR_START_DIR=/DATA`
- Change exposed port by editing:
  - `"192.168.1.14:9090:8080"` (default in this repo)
  - and command `--port 8080`

## Troubleshooting

- If `192.168.1.14:9090` is already in use or unavailable on your host, change the mapping to your host IP/port (for example `192.168.1.14:9091:8080` or `0.0.0.0:9090:8080`).
- If you cannot see files, verify host paths are mounted in the stack volumes.
- If the container fails to start, check **Portainer → Containers → Logs**.

# Install on CasaOS via Portainer (portioner.io/portainer.io)

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
git clone https://github.com/iansutherland74/symlink-editor.git

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

- Visit: `http://<CASAOS_IP>:8080`

The web app will browse and manage symlinks under mounted paths (including `/DATA`).

## 4) Optional customization

- Change startup folder by editing env var in stack:
  - `SYMLINK_EDITOR_START_DIR=/DATA`
- Change exposed port by editing:
  - `"8080:8080"`
  - and command `--port 8080`

## Troubleshooting

- If port 8080 is already in use, switch to another port (for example `8088:8080`).
- If you cannot see files, verify host paths are mounted in the stack volumes.
- If the container fails to start, check **Portainer → Containers → Logs**.

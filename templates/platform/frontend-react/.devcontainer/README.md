# Frontend React Dev Container

A fully-configured development environment running in Docker. This provides a consistent, reproducible setup across all team members with zero local configuration.

## What's Included

| Component           | Description                                                 |
| ------------------- | ----------------------------------------------------------- |
| **Node.js 22**      | Node.js runtime                                             |

## Prerequisites

### Required Software

1. **Docker** (version 4.0+)
   - Linux: Install [Docker Engine](https://docs.docker.com/engine/install/) + [Compose](https://docs.docker.com/compose/install/)

2. **Visual Studio Code** with the [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

## Quick Start

1. Open the project in VSCode
2. When prompted, click **"Reopen in Container"** (or use `Cmd/Ctrl+Shift+P` → "Dev Containers: Reopen in Container")
3. Wait for initialization to complete (first time takes a few minutes)
4. Start developing:
   ```bash
   dotnet new webapi -n MyDotnetBackend
   ```

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    Dev Container (app)                      │
│  Node.js 22                                                 │
│  Workspace mounted at /workspace/application                │
└──────────────────────┬──────────────────────────────────────┘
                       
```

### Service Ports

| Service       | Port | URL                   | Description               |
| ------------- | ---- | --------------------- | ------------------------- |

## File Structure

```
.devcontainer/
├── devcontainer.json      # VSCode configuration (extensions, settings, ports)
├── docker-compose.yml     # Service orchestration (postgres, dynamodb)
├── Dockerfile             # Container image (.NET SDK)
└── README.md              # This file
```

## How It Works

### Service Orchestration (docker-compose.yml)

Three services run together:

1. **node** - Main development container where you work

### VSCode Integration (devcontainer.json)

Configures:

- Automatic port forwarding
- Pre-installed extensions (Github COpilot, Sonarqube)
- Editor settings (format on save, TypeScript SDK)
- Lifecycle commands (postCreate, postStart)


## Service Access

## Troubleshooting

### Container Won't Start

1. Ensure Docker Desktop is running
2. Increase Docker resources (minimum 4GB RAM)
3. Rebuild container: `Cmd/Ctrl+Shift+P` → "Dev Containers: Rebuild Container"

### Port Already in Use

Stop conflicting services on your host machine, or modify port mappings in `docker-compose.yml`.

### Complete Reset

To start fresh, remove all containers and volumes:

```bash
# Run from host machine (not inside container)
docker-compose -f .devcontainer/docker-compose.yml down -v
```

Then reopen the project in the Dev Container.

## Customization

Edit files in `.devcontainer/` to customize the environment:

- `devcontainer.json` - Extensions, settings, port forwarding
- `docker-compose.yml` - Services, ports, volumes
- `Dockerfile` - Tools, certificates, shell configuration

After changes, rebuild: `Cmd/Ctrl+Shift+P` → "Dev Containers: Rebuild Container"

## Resources

- [VSCode Dev Containers Documentation](https://code.visualstudio.com/docs/devcontainers/containers)
- [Docker Compose Documentation](https://docs.docker.com/compose/)
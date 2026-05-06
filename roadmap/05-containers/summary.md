# Module 05: Containers (Docker)

## Why This Module

Diego understands Linux processes, filesystems, and namespaces from his kernel troubleshooting work. Containers are built on these exact primitives. This module connects his deep OS knowledge to modern application packaging and deployment patterns.

## Key Concepts

### Containers Are Linux Features

Diego already knows the building blocks:
- **Namespaces**: Process isolation (pid, net, mnt, uts, ipc, user) — what `unshare` does
- **Cgroups**: Resource limits (CPU, memory, I/O) — what Diego monitors in performance issues
- **Union filesystems**: Layered file systems (OverlayFS) — related to his filesystem troubleshooting
- Docker is an orchestration layer on top of these kernel features

### Docker Architecture

- **Docker daemon** (dockerd): Manages images, containers, networks, volumes
- **Docker CLI**: Client that talks to the daemon via API
- **Images**: Immutable filesystem layers built from Dockerfiles
- **Containers**: Running instances of images (ephemeral by default)
- **Registry**: Image storage and distribution (Docker Hub, ECR, GHCR)

### Dockerfile Best Practices

- Multi-stage builds (separate build dependencies from runtime)
- Layer ordering for cache efficiency
- Minimal base images (Alpine, distroless, scratch)
- Non-root users and security
- `.dockerignore` for build context optimization
- Health checks
- Proper signal handling (PID 1 problem)

### Docker Compose for Local Development

- Multi-container applications
- Service dependencies and health checks
- Volume mounts for development
- Network isolation between services
- Environment variable management

### Container Security

- Image scanning (Trivy, Snyk)
- Read-only filesystems
- Capability dropping
- Secrets management (never bake into images)
- Base image updates and patching strategy

### Production Patterns

- Container logging (stdout/stderr → log driver)
- Container networking (bridge, host, overlay)
- Volume management (bind mounts vs named volumes vs tmpfs)
- Resource limits (--memory, --cpus)
- Restart policies

## Topics

1. Container fundamentals (namespaces, cgroups — review through Diego's kernel lens)
2. Docker CLI essentials (run, build, exec, logs, inspect)
3. Dockerfile writing (best practices, multi-stage, security)
4. Docker Compose (multi-service applications)
5. Networking (bridge, host, custom networks, DNS)
6. Volumes and data persistence
7. Image registries (Docker Hub, GHCR, ECR)
8. Container security (scanning, hardening, least privilege)
9. Docker in CI/CD (building and pushing images in GitHub Actions)
10. Production patterns (logging, monitoring, orchestration intro)

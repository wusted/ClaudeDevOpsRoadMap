# Module 05: Containers — Hands-On Exercises

## Module Repository: `docker-applications`

All deliverables for this module live in `repos/docker-applications/` and on GitHub at `github.com/<username>/docker-applications`. Create it with `/setup-repo` before starting Exercise 5.1.

The repo's README should describe it as a portfolio of Docker projects demonstrating container internals understanding, multi-stage builds, security hardening, multi-service compositions, and CI/CD image pipelines.

Replace earlier paths like `devops-lab/docker/...` with in-repo equivalents (e.g., `01-internals/`, `02-multistage/`, `03-compose/`).

---

## Exercise 5.1: Container Internals

**Objective**: Understand what Docker does at the kernel level using Diego's Linux knowledge.

**Context**: Before using Docker as a black box, understand the primitives.

**Steps**:
1. Run a container: `docker run -d --name demo nginx`
2. Inspect the container's namespaces: `ls -la /proc/$(docker inspect --format '{{.State.Pid}}' demo)/ns/`
3. View the container's cgroups: examine `/sys/fs/cgroup/` entries
4. Inspect the overlay filesystem: `docker inspect demo | jq '.[0].GraphDriver'`
5. Enter the container's namespace manually: `nsenter --target <PID> --mount --uts --ipc --net --pid`
6. Compare `ps aux` inside vs outside the container
7. Document your findings in `devops-lab/docker/01-internals/README.md`

**Validation**: Can explain containers in terms of Linux primitives, not just "lightweight VMs"

---

## Exercise 5.2: Multi-Stage Dockerfile

**Objective**: Build a production-optimized container image.

**Steps**:
1. Create a simple Go or Python application (web server returning JSON)
2. Write a naive Dockerfile (single stage, full OS base)
3. Note the image size: `docker images`
4. Rewrite as multi-stage:
   - Stage 1: Build (install deps, compile)
   - Stage 2: Runtime (minimal base, copy only artifacts)
5. Compare image sizes
6. Add: non-root user, health check, proper signal handling
7. Scan with Trivy: `trivy image <your-image>`
8. Fix any critical/high vulnerabilities

**Validation**: Final image is <100MB (for Go) or <200MB (Python), runs as non-root, passes Trivy scan

---

## Exercise 5.3: Docker Compose Application Stack

**Objective**: Deploy a multi-service application locally.

**Steps**:
1. Create `devops-lab/docker/03-compose/docker-compose.yml`
2. Services:
   - Web app (nginx or custom app from 5.2)
   - API backend (Python Flask or Node)
   - Database (PostgreSQL)
   - Cache (Redis)
3. Configure:
   - Custom network isolating frontend from database
   - Named volumes for database persistence
   - Health checks on all services
   - Dependency ordering (db starts before api)
   - Environment variables via `.env` file
4. Run `docker compose up` and verify all services communicate
5. Simulate a failure: stop the database, observe app behavior
6. Run `docker compose down -v` for clean teardown

**Validation**: All services start and communicate, data persists across restarts, network isolation works

---

## Exercise 5.4: CI/CD for Container Images

**Objective**: Automate image building and publishing with GitHub Actions.

**Steps**:
1. Create `.github/workflows/docker-build.yml`
2. On PR: build image, run Trivy scan, fail on critical vulnerabilities
3. On merge to main: build, tag (semver + sha), push to GitHub Container Registry (GHCR)
4. Use Docker layer caching in CI for faster builds
5. Add image metadata labels (build date, commit SHA, version)
6. Set up Dependabot for Docker base image updates

**Validation**: PR triggers build+scan, merge pushes tagged image to GHCR, caching speeds up subsequent builds

---

## Exercise 5.5: Terraform + Docker Provider

**Objective**: Manage Docker resources with Terraform (bridges Module 02 and 05).

**Steps**:
1. Create `devops-lab/terraform/docker/main.tf`
2. Use the Docker Terraform provider to:
   - Pull an image
   - Create a network
   - Deploy a container with environment variables and port mappings
3. Deploy a complete stack (web + db) using only Terraform
4. Compare this approach vs Docker Compose — when to use which

**Validation**: Docker infrastructure managed by Terraform state, can be destroyed and recreated cleanly

---
name: dockerfile-best-practices
description: Dockerfile best practices, layer optimization, multi-stage builds, security, and image size reduction.
---

# Dockerfile Best Practices

Writing efficient, secure container images.

## Context

You are writing a Dockerfile. Optimize for size, build speed, and security.

## Domain Context

- **Layers**: Each line creates a layer; fat layers are slow to build/push
- **Caching**: Earlier layers cache better; put changeable stuff at end
- **Multi-Stage**: Separate build and runtime images; smaller final image
- **Security**: Don't run as root; minimal base image
- **Size**: Alpine < Ubuntu < Debian; watch for bloat

## Instructions

1. **Choose Base Image**: Alpine (small), Debian (compatible), Ubuntu (big)
2. **Install Essentials**: Only what's needed; remove package caches
3. **Use Multi-Stage**: Build stage, runtime stage; small final image
4. **Order Statements**: Stable first, changeable last (maximize caching)
5. **Run as Non-Root**: Create user, switch with USER
6. **Health Checks**: HEALTHCHECK for container orchestrators
7. **Documentation**: Comments explain why, not what

## Anti-Patterns

- Fat images (>500MB); slow to push/deploy
- Running as root; security risk
- Single huge layer; no caching benefit
- Installing dev tools in production; unnecessary bloat
- Many layers; each adds overhead

## Further Reading

- Docker documentation best practices
- Google Cloud dockerfile best practices
- Container security guidelines

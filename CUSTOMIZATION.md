# Customization Guide

## Adding Custom Tools

To add additional tools to the runner image, modify the `Dockerfile`:

1. Add package installations in the appropriate section
2. Ensure you clean up apt lists to keep image size minimal
3. Test the build locally before pushing

Example:
```dockerfile
RUN apt-get update && apt-get install -y --no-install-recommends \
    your-package-here \
    && rm -rf /var/lib/apt/lists/*
```

## Version Management

All major tool versions are defined as build arguments at the top of the Dockerfile:
- `RUNNER_VERSION` - GitHub Actions Runner version
- `KUBECTL_VERSION` - Kubernetes CLI version
- `HELM_VERSION` - Helm CLI version
- `NODE_VERSION` - Node.js major version

These can be overridden during build:
```bash
docker build --build-arg RUNNER_VERSION=2.318.0 -t custom-runner .
```

## Cloud Provider CLIs

The Dockerfile includes commented examples for installing cloud provider CLIs (AWS, Azure, GCP). Uncomment and modify as needed for your environment.

## Security Scanning

All builds are automatically scanned with Trivy for vulnerabilities. Critical and high-severity issues are reported in GitHub Security.

## Renovate Configuration

The `renovate.json` file tracks:
- Base runner image updates
- Tool version updates (kubectl, helm, node)
- GitHub Actions updates

Renovate runs weekly and creates PRs for available updates.

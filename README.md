# Custom GitHub Actions Runner for ARC

This repository contains a customized GitHub Actions Runner image for use with [Actions Runner Controller (ARC)](https://github.com/actions/actions-runner-controller).

## Overview

This image extends the official GitHub Actions Runner image with additional tools and configurations optimized for our workflows.

## Building the Image

The image is automatically built and pushed to the container registry via GitHub Actions on:
- Push to `main` branch
- Manual workflow dispatch
- Weekly schedule (to incorporate upstream updates)

### Manual Build

```bash
docker build -t custom-actions-runner:latest .
```

## Upstream Tracking

This repository uses Renovate to automatically track updates from the upstream Actions Runner Controller images. Renovate will create PRs when new versions are available.

## Usage with ARC

To use this custom runner image with ARC, reference it in your `RunnerDeployment` or `AutoscalingRunnerSet`:

```yaml
apiVersion: actions.summerwind.dev/v1alpha1
kind: RunnerDeployment
metadata:
  name: custom-runner
spec:
  template:
    spec:
      image: ghcr.io/<your-org>/custom-actions-runner:latest
      # ... other configurations
```

## Customizations

- Pre-installed development tools and dependencies
- Custom configurations for CI/CD workflows
- Optimized for cloud-native environments

## License

MIT

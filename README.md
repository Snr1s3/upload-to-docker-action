# Upload to Docker Action

Builds and uploads a new Docker image to the configured registry.

## Inputs

### `docker_username` (required)
Docker Hub username used to authenticate and push the image.

### `docker_token` (required)
Docker Hub access token used for secure authentication.

### `docker_tags` (required)
Comma-separated image tags to apply when pushing, for example `latest,v1.2.0`.

### `docker_platforms` (required)
Target build platforms, for example `linux/amd64,linux/arm64`.

### `docker_file` (required)
Path to the Dockerfile to build, relative to the repository root (e.g., `./Dockerfile` or `./bot/Dockerfile`).

## Requirements

This action requires the repository to be checked out before running. Make sure to include `actions/checkout@v4` as a step before this action in your workflow.

## Example Usage

```yaml
name: Build and Push Docker Image

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Upload to Docker
        uses: your-username/upload-to-docker-action@v1
        with:
          docker_username: ${{ secrets.DOCKERHUB_USERNAME }}
          docker_token: ${{ secrets.DOCKERHUB_TOKEN }}
          docker_tags: your-username/your-app:latest,your-username/your-app:v1.0.0
          docker_platforms: linux/amd64,linux/arm64
          docker_file: ./Dockerfile
```

## What This Action Does

1. Sets up Docker Buildx for multi-platform builds
2. Authenticates to Docker Hub using provided credentials
3. Builds and pushes the Docker image to your registry with specified tags and platforms

## Secrets

Store your Docker Hub credentials as repository secrets:
- `DOCKERHUB_USERNAME`: Your Docker Hub username
- `DOCKERHUB_TOKEN`: Your Docker Hub personal access token (not your password)

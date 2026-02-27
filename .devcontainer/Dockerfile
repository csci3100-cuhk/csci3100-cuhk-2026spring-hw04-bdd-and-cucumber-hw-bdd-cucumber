# Use Ubuntu base image - Ruby will be installed via devcontainer feature
FROM mcr.microsoft.com/devcontainers/base:ubuntu

# Install system dependencies for building gems and running tests
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
        && apt-get -y install --no-install-recommends \
             build-essential \
             libsqlite3-dev \
             nodejs \
             npm \
             chromium-driver \
        && rm -rf /var/lib/apt/lists/*

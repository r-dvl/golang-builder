FROM golang:1.21

# Install build tools and cross-compilation dependencies
RUN apt-get update && apt-get install -y \
    gcc \
    gcc-aarch64-linux-gnu \
    libc6-dev-arm64-cross

# Go build params
ENV GOOS=linux
ENV GOARCH=arm64
ENV CGO_ENABLED=1
ENV CC=aarch64-linux-gnu-gcc
ENV EXT=
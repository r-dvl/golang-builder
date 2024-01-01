FROM golang:1.21

# Install build tools
RUN apt-get update && apt-get install -y \
    clang

# Go build params
ENV GOOS=darwin
ENV GOARCH=amd64
ENV CGO_ENABLED=1
ENV CC=o64-clang
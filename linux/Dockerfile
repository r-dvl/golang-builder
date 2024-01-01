FROM golang:1.21

# Install build tools
RUN apt-get update && apt-get install -y \
    gcc

# Go build params
ENV GOOS=linux
ENV GOARCH=amd64
ENV CGO_ENABLED=1
ENV CC=x86_64-linux-gnu-gcc
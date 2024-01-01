FROM golang:1.21

# Install build tools
RUN apt-get update && apt-get install -y \
    mingw-w64

# Go build params
ENV GOOS=windows
ENV GOARCH=amd64
ENV CGO_ENABLED=1
ENV CC=x86_64-w64-mingw32-gcc
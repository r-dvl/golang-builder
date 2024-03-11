# Golang Builder
Docker images to build multiplatform golang binaries. These three images are built using `golang:1.21` as the base image since it is based on Debian and already has the golang dependencies installed.


## Contents
1. [Usage](#Usage)
2. [Platforms](#Platforms)


## Usage
This images can be used as a first step builder or just to generate your binaries.


### Example
A real example from [rdvl-cli](https://github.com/r-dvl/rdvl-cli).

#### Dockerfile
```dockerfile
ARG OS
ARG ARCH

FROM ghcr.io/r-dvl/golang-builder:${OS}-${ARCH}

ENV PROJECT_NAME=rdvl-cli
ENV VERSION=x.x.x

WORKDIR /home/app

COPY . .

RUN go mod download && go mod verify

RUN mkdir -p ./bin/${PROJECT_NAME}-${VERSION}.${GOOS}-${GOARCH}

# Compile binaries
CMD ["sh", "-c", "go build -o ./bin/${PROJECT_NAME}-${VERSION}.${GOOS}-${GOARCH}/${PROJECT_NAME}${EXT}"]
```

#### Docker Compose
```yaml
version: '3'

services:
  builder:
    container_name: rdvl-builder
    build:
      context: .
      args:
        OS: windows
        ARCH: amd64
    volumes:
      - ./bin:/home/app/bin
    environment:
      - VERSION=1.0.0
```

## Platforms
### Windows
Windows Dockerfile only installs the `mingw-w64` build tools to perform a cross-compile and configures the environment variables to run a go build.

### Linux
Just as Windows Dockerfile, this one just installs `gcc` build tools and configures the environment variables.

### Darwin
The one that motivated this project, installs `osxcross` and all its dependencies using the `Xcode 15` SDK.

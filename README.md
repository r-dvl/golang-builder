# Golang Builder
Docker images to build multiplatform golang binaries. These three images are built using `golang:1.21` as the base image since it is based on Debian and already has the golang dependencies installed.


## Contents
1. [Windows](#Windows)
2. [Linux](#Linux)
3. [Darwin](#Darwin)


## Windows
Windows Dockerfile only installs the `mingw-w64` build tools to perform a cross-compile and configures the environment variables to run a go build.

## Linux
Just as Windows Dockerfile, this one just installs `gcc` build tools and configures the environment variables.

## Darwin
The one that motivated this project, installs `osxcross` and all its dependencies using the `Xcode 15` SDK.
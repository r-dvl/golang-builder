FROM golang:1.21

# Install build tools and dependencies for osxcross
RUN apt-get update && apt-get install -y \
    cmake \
    patch \
    cpio \
    clang \
    git \
    curl \
    xz-utils \
    libssl-dev \
    libxml2-dev \
    liblzma-dev \
    zlib1g-dev \
    libbz2-dev

# Clone the osxcross repository
RUN git clone https://github.com/tpoechtrager/osxcross /osxcross

# Copy Xcode
COPY ./xcode/ /osxcross/tarballs/

# Generate the SDK package
RUN /osxcross/tools/gen_sdk_package_pbzx.sh /osxcross/tarballs/Xcode_15.1.xip

# Move SDK package to tarball directory
RUN mv /osxcross/MacOSX14.sdk.tar.xz /osxcross/tarballs/

# Build osxcross
RUN UNATTENDED=1 /osxcross/build.sh

# Add osxcross to PATH
ENV PATH="/osxcross/target/bin:${PATH}"

# Go build params
ENV GOOS=darwin
ENV GOARCH=arm64
ENV CGO_ENABLED=1
ENV CC=o64-clang
ENV EXT=
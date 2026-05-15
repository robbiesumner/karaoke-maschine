FROM debian:bookworm-slim

RUN apt-get update && apt-get install -y --no-install-recommends \
        bc \
        binutils \
        bzip2 \
        ca-certificates \
        cpio \
        file \
        g++ \
        git \
        libc6-dev \
        libncurses-dev \
        make \
        patch \
        perl \
        rsync \
        unzip \
        wget \
        which \
        xz-utils \
    && rm -rf /var/lib/apt/lists/*

# Buildroot refuses to run as root, so build under a fixed non-root user.
# UID 1000 is the conventional first user; on macOS hosts the bind-mount
# layer rewrites ownership anyway, and Linux hosts on non-1000 UIDs only
# notice when removing files written into ./run/ from outside the container.
RUN groupadd -g 1000 build \
 && useradd -m -u 1000 -g 1000 -s /bin/bash build

ENV BR2_DL_DIR=/cache/dl

USER build
WORKDIR /output
CMD ["bash"]

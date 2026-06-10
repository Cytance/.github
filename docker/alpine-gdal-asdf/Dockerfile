FROM --platform=$BUILDPLATFORM ghcr.io/osgeo/gdal:alpine-small-latest

ENV NONINTERACTIVE=1
ENV HOMEBREW_NO_AUTO_UPDATE=1

ARG HOMEBREW_PREFIX="/home/linuxbrew/.linuxbrew"
ARG HOMEBREW_CELLAR="/home/linuxbrew/.linuxbrew/Cellar"
ARG HOMEBREW_REPOSITORY="/home/linuxbrew/.linuxbrew/Homebrew"

ENV HOMEBREW_PREFIX=${HOMEBREW_PREFIX}
ENV HOMEBREW_CELLAR=${HOMEBREW_CELLAR}
ENV HOMEBREW_REPOSITORY=${HOMEBREW_REPOSITORY}
ENV PATH=$PATH:${HOMEBREW_PREFIX}/bin:${HOMEBREW_PREFIX}/sbin
ENV MANPATH=$MANPATH:${HOMEBREW_PREFIX}/share/man
ENV INFOPATH=$INFOPATH:${HOMEBREW_PREFIX}/share/info

RUN apk add --no-cache \
    bash \
    build-base \
    coreutils \
    curl \
    gcompat \
    git \
    grep \
    libffi-dev \
    zlib-dev && \
    printf '#!/bin/sh\nwhile test $# -gt 0; do\n    case "$1" in\n        --vers|--versi|--versio|--version)\n            echo "ldd (Alpine MUSL 2.13) 2.13"\n            exit 0\n            ;;\n    esac\ndone\nexec /lib/ld-musl-x86_64.so.1 --list "$@"\n' > /usr/bin/ldd && \
    chmod +x /usr/bin/ldd && \
    adduser -s /bin/bash -D linuxbrew && \
    echo 'linuxbrew ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER linuxbrew
RUN /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" && \
    eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)" && \
    echo "eval \"\$($(brew --prefix)/bin/brew shellenv)\"" >> ~/.bashrc && \
    brew install asdf pipenv && \
    brew cleanup --prune=all && \
    rm -rf /home/linuxbrew/.cache

USER root
CMD ["/bin/bash"]

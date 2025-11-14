FROM --platform=linux/x86_64 ghcr.io/osgeo/gdal:ubuntu-small-latest

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

RUN useradd -m -s /bin/bash linuxbrew && \
    echo 'linuxbrew ALL=(ALL) NOPASSWD:ALL' >>/etc/sudoers

RUN apt update && apt install -y build-essential git libedit-dev zlib1g-dev libffi-dev curl ca-certificates --no-install-recommends && rm -rf /var/lib/apt/lists/*
USER linuxbrew
RUN /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
RUN eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)" && echo "eval \"\$($(brew --prefix)/bin/brew shellenv)\"" >> ~/.bashrc
RUN brew install asdf pipenv

USER root
CMD /bin/bash

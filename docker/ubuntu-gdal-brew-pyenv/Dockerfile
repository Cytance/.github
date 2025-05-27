FROM --platform=linux/x86_64 ghcr.io/osgeo/gdal:ubuntu-small-latest

USER root
ENV NONINTERACTIVE=1

ARG HOMEBREW_PREFIX="/home/linuxbrew/.linuxbrew"
ARG HOMEBREW_CELLAR="/home/linuxbrew/.linuxbrew/Cellar"
ARG HOMEBREW_REPOSITORY="/home/linuxbrew/.linuxbrew/Homebrew"

ENV HOMEBREW_PREFIX=${HOMEBREW_PREFIX}
ENV HOMEBREW_CELLAR=${HOMEBREW_CELLAR}
ENV HOMEBREW_REPOSITORY=${HOMEBREW_REPOSITORY}
ENV PATH=$PATH:${HOMEBREW_PREFIX}/bin:${HOMEBREW_PREFIX}/sbin
ENV MANPATH=$MANPATH:${HOMEBREW_PREFIX}/share/man
ENV INFOPATH=$INFOPATH:${HOMEBREW_PREFIX}/share/info

RUN apt update && apt install -y build-essential git libedit-dev zlib1g-dev libffi-dev --no-install-recommends && rm -rf /var/lib/apt/lists/*
RUN /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
RUN eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)" && echo "eval \"\$($(brew --prefix)/bin/brew shellenv)\"" >> ~/.bashrc && brew install pyenv pipenv

RUN which brew

CMD /bin/bash
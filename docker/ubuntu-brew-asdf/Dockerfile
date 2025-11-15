FROM --platform=linux/x86_64 ubuntu:latest

ENV NONINTERACTIVE=1
ENV HOMEBREW_NO_AUTO_UPDATE=1

RUN useradd -m -s /bin/bash linuxbrew
RUN echo 'linuxbrew ALL=(ALL) NOPASSWD:ALL' >>/etc/sudoers
RUN echo 'ubuntu ALL=(ALL) NOPASSWD:ALL' >>/etc/sudoers

RUN apt update && apt install -y build-essential git curl ca-certificates --no-install-recommends && rm -rf /var/lib/apt/lists/*

USER linuxbrew
ARG HOMEBREW_PREFIX="/home/linuxbrew/.linuxbrew"
ARG HOMEBREW_CELLAR="/home/linuxbrew/.linuxbrew/Cellar"
ARG HOMEBREW_REPOSITORY="/home/linuxbrew/.linuxbrew/Homebrew"
ENV HOMEBREW_PREFIX=${HOMEBREW_PREFIX}
ENV HOMEBREW_CELLAR=${HOMEBREW_CELLAR}
ENV HOMEBREW_REPOSITORY=${HOMEBREW_REPOSITORY}
ENV PATH=$PATH:${HOMEBREW_PREFIX}/bin:${HOMEBREW_PREFIX}/sbin
ENV MANPATH=$MANPATH:${HOMEBREW_PREFIX}/share/man
ENV INFOPATH=$INFOPATH:${HOMEBREW_PREFIX}/share/info

RUN /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

USER root
RUN chown -R ubuntu:ubuntu /home/linuxbrew/.linuxbrew
RUN chmod 755 /home/linuxbrew

USER ubuntu
RUN eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)" && echo "eval \"\$($(brew --prefix)/bin/brew shellenv)\"" >> ~/.bashrc
RUN echo 'export PATH="${ASDF_DATA_DIR:-$HOME/.asdf}/shims:$PATH"' >> ~/.bashrc
RUN echo 'export PATH="${ASDF_DATA_DIR:-$HOME/.asdf}/shims:$PATH"' >> ~/.bash_profile
RUN brew install asdf && brew cleanup
RUN echo "Homebrew version:" && brew --version
RUN echo "asdf version:" && asdf version

CMD /bin/bash

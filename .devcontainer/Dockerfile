FROM debian:trixie

ENV DEBIAN_FRONTEND=noninteractive

# -- Install our core dependencies
RUN apt-get update && \
    apt-get install --assume-yes --no-install-recommends \
    curl=8.5.0-2ubuntu10.15 \
    wget=1.21.4-1ubuntu4.5 \
    git=1:2.43.0-1ubuntu7.3 \
    git-lfs=3.4.1-1ubuntu0.4 \
    zsh=5.9-6ubuntu2 \
    zsh-common=5.9-6ubuntu2 \
    zsh-doc=5.9-6ubuntu2 \
    zsh-syntax-highlighting=0.7.1-2 \
    && \
    rm -rf /var/lib/apt/lists/*

# -- Install Homebrew
# hadolint ignore=SC2016
RUN curl -fsSLo install-brew.sh \
    "https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh" && \
    chmod u+x install-brew.sh && \
    NONINTERACTIVE=1 ./install-brew.sh && \
    rm install-brew.sh && \
    mkdir -p "/etc/zsh/" && \
    if [ -f /etc/bash.bashrc ]; then echo "" >> /etc/bash.bashrc ; fi && \
    echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv bash)"' >> /etc/bash.bashrc && \
    if [ -f /etc/zsh/zprofile ]; then echo "" >> /etc/zsh/zprofile ; fi && \
    echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv zsh)"' >> /etc/zsh/zprofile && \
    rm -rf /var/lib/apt/lists/*

# -- Install Homebrew-based packages
RUN brew install neovim@0.12.6 && \
    brew install tmux@3.8 && \
    brew install lazygit@0.66.1

# -- Install Oh My Zsh as root
RUN curl -fsSLo install-oh-my-zsh.sh \
    "https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh" && \
    chmod u+x install-oh-my-zsh.sh && \
    ./install-oh-my-zsh.sh --unattended && \
    rm install-oh-my-zsh.sh

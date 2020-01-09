FROM debian:experimental
MAINTAINER Bence SZIGETI <bence.szigeti@gohyda.com>

# User
ENV USER root
ENV HOME /root
USER ${USER}
WORKDIR ${HOME}

# General-tools install
RUN apt update && apt install --no-install-recommends --yes \
    ca-certificates \
    curl \
    dnsutils \
    htop \
    iputils-ping \
    less \
    locales \
    locales-all \
    lsof \
    man \
    netcat \
    openssh-client \
    procps \
    traceroute \
    whois

# Console-tools install
RUN apt update && apt install --no-install-recommends --yes \
    git \
    gnupg2 \
    neovim \
    radare2 \
    ranger \
    tig \
    tmux \
    zsh

# GUI-tools install
RUN apt update && apt install --no-install-recommends --yes \
    dmenu \
    feh \
    firefox \
    fonts-hack-ttf \
    gnome-screenshot \
    i3 \
    i3blocks \
    i3lock \
    rxvt-unicode-256color \
    tigervnc-common \
    tigervnc-standalone-server \
    x11-xserver-utils \
    xfonts-base \
    xfonts-100dpi \
    xfonts-75dpi

# Docker install
RUN apt install --no-install-recommends --yes \
    apt-transport-https \
    software-properties-common
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/debian buster test"
RUN apt update && apt install --no-install-recommends --yes docker-ce

# Development-tools install
RUN apt install --no-install-recommends --yes build-essential
RUN curl https://sh.rustup.rs -sSf | sh -s -- --default-toolchain nightly -y
ENV PATH="${HOME}/.cargo/bin:${PATH}"
RUN cargo install rustfmt-nightly --force
RUN echo "$(rustc --print sysroot)/lib" >> /etc/ld.so.conf.d/rust.conf
RUN ldconfig

# General-tools settings
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Console-tools settings
RUN mkdir -p ${HOME}/.config/nvim
COPY res/tmux/.tmux.conf ${HOME}
COPY res/zsh/.zshrc ${HOME}
COPY res/vim/init.vim ${HOME}/.config/nvim
RUN git clone git://github.com/robbyrussell/oh-my-zsh.git ${HOME}/.oh-my-zsh
RUN git clone \
    git://github.com/VundleVim/Vundle.vim.git ${HOME}/.vim/bundle/Vundle.vim
RUN nvim +PluginInstall +qall
RUN git config --global core.editor nvim
RUN git config --global commit.gpgsign true
RUN chsh -s /bin/zsh

# GUI-tools settings
RUN mkdir -p ${HOME}/.config/i3
COPY res/i3/config ${HOME}/.config/i3
COPY res/i3/i3blocks.conf ${HOME}/.config/i3
COPY res/x/.Xresources ${HOME}
COPY res/vnc/xstartup ${HOME}/.vnc/xstartup
COPY res/img/.bg.jpg ${HOME}/.bg.jpg

EXPOSE 5901

# Entrypoint
COPY opt/entrypoint.sh /opt
ENTRYPOINT ["/opt/entrypoint.sh"]

FROM finalduty/archlinux:weekly
# MAINTAINER foo <foo@bar.com>

# Lang
RUN echo "ja_JP.UTF-8 UTF-8" >> /etc/locale.gen && locale-gen

RUN pacman -Syu base-devel man --noconfirm --needed

# Install basic packages
RUN sudo pacman -S --noconfirm --needed \
    vi vim \
    zsh tmux \
    git \
    openssh openssl \
    htop

# add user
RUN useradd -ms /bin/zsh dev \
    && echo "dev ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers \
    && echo "dev:dev" | chpasswd

USER dev
WORKDIR /home/dev

# LANG
ENV LANG ja_JP.UTF-8
ENV LC_ALL ja_JP.UTF-8
ENV LC_CTYPE ja_JP.UTF-8


# Settings
ENV PYTHON_VERSION 3.5.2
ENV PYTHON2_VERSION 2.7.12

RUN sudo pacman -S --noconfirm --needed \
    emacs-nox

RUN git clone https://github.com/1m38/dotfiles /home/dev/dotfiles
RUN zsh /home/dev/dotfiles/init.zsh --change-repo

# pyenv
RUN set -ex \
    && git clone https://github.com/yyuu/pyenv.git /home/dev/.pyenv \
    && git clone https://github.com/yyuu/pyenv-virtualenv.git /home/dev/.pyenv/plugins/pyenv-virtualenv \
    && export PYENV_ROOT="$HOME/.pyenv" \
    && export PATH="$PYENV_ROOT/bin:$PATH" \
    && eval "$(pyenv init -)" \
    && eval "$(pyenv virtualenv-init -)" \
    && pyenv install $PYTHON_VERSION \
    && pyenv install $PYTHON2_VERSION \
    && pyenv global $PYTHON_VERSION $PYTHON2_VERSION \
    && pyenv rehash \
    && pip install -U pip \
    && pip install ipython jupyter numpy requests \
    && pip2 install -U pip \
    && pip2 install ipython jupyter numpy

# node
# haskell

FROM ubuntu:18.04

# General packages
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    fonts-powerline \
    git \
    locales \
    software-properties-common \
    tmux \
    xsel \
    wget \
    && rm -rf /var/lib/apt/lists/*
    
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8

# ccls
RUN apt-get update && apt-get install -y --no-install-recommends \
    libncurses5-dev \
    zlib1g-dev \
    && rm -rf /var/lib/apt/lists/* \
    && mkdir -p /tools && cd /tools \
    # cmake-3.14
    && wget -O - https://github.com/Kitware/CMake/releases/download/v3.14.1/cmake-3.14.1.tar.gz | tar -zxvf - \
    && mv /tools/cmake-3.14.1 /tools/cmake && cd /tools/cmake \
    && ./configure && make -j8 \
    # llvm-7.0.1
    && wget -c -O - http://releases.llvm.org/7.0.1/clang+llvm-7.0.1-x86_64-linux-gnu-ubuntu-16.04.tar.xz | tar -Jxvf - -C /tools \
    # ccls
    && git clone --depth=1 --recursive https://github.com/MaskRay/ccls /tools/ccls && cd /tools/ccls \
    && git submodule update --init \
    && /tools/cmake/bin/cmake -H. -BRelease -DCMAKE_BUILD_TYPE=Release -DCMAKE_PREFIX_PATH=/tools/clang+llvm-7.0.1-x86_64-linux-gnu-ubuntu-16.04 \
    && /tools/cmake/bin/cmake --build Release --target install \
    && rm -rf /tools

# Neovim Install
RUN add-apt-repository ppa:neovim-ppa/unstable -y \
    && apt-get update && apt-get install -y --no-install-recommends \
    neovim \
    && rm -rf /var/lib/apt/lists/*

# pyenv
ENV PYENV_ROOT /root/.pyenv/
ENV PATH $PYENV_ROOT/bin:$PATH
RUN apt-get update && apt-get install -y --no-install-recommends \
    libssl-dev \
    libbz2-dev \
    libffi-dev \
    libreadline-dev \
    libsqlite3-dev \
    python-openssl \
    && rm -rf /var/lib/apt/lists/* \
    && git clone https://github.com/pyenv/pyenv.git /root/.pyenv \
    && git clone https://github.com/pyenv/pyenv-virtualenv.git /root/.pyenv/plugins/pyenv-virtualenv \
    && echo 'eval "$(pyenv init -)"' >> /root/.bashrc \
    && echo 'eval "$(pyenv virtualenv-init -)"' >> /root/.bashrc

# python install
RUN . /root/.bashrc \
    && pyenv install 3.7.0 \
    && pyenv install 2.7.15 \
    && pyenv virtualenv 3.7.0 neovim3 \
    && pyenv virtualenv 2.7.15 neovim2 \
    && pyenv activate neovim3 \
    && pip3 install pynvim flake8 python-language-server \
    && pyenv activate neovim2 \
    && pip2 install pynvim flake8 python-language-server

ENV XDG_CONFIG_HOME /root/.config/
COPY ./.tmux.conf /root/
COPY ./alias.bash /root/

RUN echo "source /root/alias.bash" >> /root/.bashrc \
    && mkdir -p $XDG_CONFIG_HOME \
    && git clone -b ubuntu https://github.com/arwtyxouymz/dotfiles.git \
    && mv /dotfiles/.config/nvim/ $XDG_CONFIG_HOME \
    && rm -rf /dotfiles \
    && nvim +UpdateRemotePlugins +qa

CMD ["/bin/bash"]

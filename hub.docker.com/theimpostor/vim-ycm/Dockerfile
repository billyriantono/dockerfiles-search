FROM buildpack-deps:xenial

# ARG UID
# ARG GID

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        build-essential \
        cmake \
        golang \
        nodejs \
        nodejs-legacy \
        npm \
        python3-dev \
        python-dev \
        silversearcher-ag \
        vim \
    && rm -rf /var/lib/apt/lists/* \
    && npm install -g typescript

#       mono-complete \
#       astyle \
#       libbz2-dev \
#       libffi-dev \
#       libncurses5-dev \
#       libncursesw5-dev \
#       libreadline-dev \
#       libsqlite3-dev \
#       libssl-dev \
#       llvm \
#       ninja-build \

# create user
# RUN \
#     groupadd -g $GID vim && \
#     useradd -ms /bin/bash -l -u $UID -g $GID vim

# RUN useradd -mlU dvim

# USER dvim

# add .vimrc
COPY .vimrc /root/.vimrc

# clone vundle
RUN git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim

# run vim command to install plugins
RUN vim +PluginInstall +qall

# run ycmd build
#   c#: --omnisharp-completer
RUN cd ~/.vim/bundle/YouCompleteMe \
    && ./install.py --clang-completer --gocode-completer --tern-completer

ENTRYPOINT [ "/usr/bin/vim" ]

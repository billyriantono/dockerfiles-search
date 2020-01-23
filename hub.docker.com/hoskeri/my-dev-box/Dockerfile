FROM debian:testing
RUN  apt-get update -y && \
     apt-get install -y cabal-install build-essential zlib1g-dev libncurses5-dev \
     vim-nox vim-doc vim-addon-manager vim-pathogen vim-youcompleteme \
     git wget \
     tmux \
     && apt-get clean \
     && apt-get autoremove --purge

# Elm Language
ENV  PATH /root/go/bin/:/root/go-env/bin:/root/.cabal/bin:$PATH
RUN  cabal update && cabal install cabal-install
RUN  cabal update && cabal install elm-compiler elm-package elm-make elm-repl elm-reactor
RUN  mkdir -p ~/.vim/bundle && cd ~/.vim/bundle && git clone https://github.com/lambdatoast/elm.vim.git

# Go Language
RUN  wget -O /tmp/go.tar.gz https://storage.googleapis.com/golang/go1.4.2.linux-amd64.tar.gz && \
     tar -zxvf /tmp/go.tar.gz -C /root/ && \
     rm -v -f /tmp/go.tar.gz
ENV  GOROOT /root/go
ENV  GOPATH /root/go-env
RUN  go get github.com/nsf/gocode &&  \
     go get golang.org/x/tools/.../ && \
     go get github.com/github/hub && \
     go get github.com/motemen/gore

# dotfiles.
COPY ./vimrc /root/.vimrc
COPY ./bashrc /root/.bashrc

# Runtime stuff.
ENV HOME /root
VOLUME /workspace
WORKDIR /workspace
ENTRYPOINT /bin/bash

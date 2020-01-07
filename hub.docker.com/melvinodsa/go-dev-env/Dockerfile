FROM golang:latest
LABEL maintainer="melvinodsa@gmail.com"

RUN apt-get update && apt-get install -y --no-install-recommends vim \
    vim-gtk \
    && rm -rf /var/lib/apt/lists/*
RUN curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim \
    && curl -fLo ~/.vimrc https://raw.githubusercontent.com/melvinodsa/vim-go-tutorial/master/vimrc \
    && vim +PlugInstall +qall
RUN go get -u github.com/klauspost/asmfmt/cmd/asmfmt \
    github.com/go-delve/delve/cmd/dlv \
    github.com/kisielk/errcheck \
    github.com/davidrjenni/reftools/cmd/fillstruct \
    github.com/mdempsky/gocode \
    github.com/stamblerre/gocode \
    github.com/rogpeppe/godef \
    github.com/zmb3/gogetdoc \
    golang.org/x/tools/cmd/goimports \
    golang.org/x/lint/golint \
    golang.org/x/tools/cmd/gopls \
    github.com/alecthomas/gometalinter \
    github.com/fatih/gomodifytags \
    golang.org/x/tools/cmd/gorename \
    github.com/jstemmer/gotags \
    golang.org/x/tools/cmd/guru \
    github.com/josharian/impl \
    honnef.co/go/tools/cmd/keyify \
    github.com/fatih/motion \
    github.com/koron/iferr \
    github.com/stamblerre/gocode
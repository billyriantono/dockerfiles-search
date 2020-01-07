FROM golang:latest

RUN apt-get update && \
    apt-get remove vim vim-runtime gvim && \
    DEBIAN_FRONTEND=noninteractive apt-get -y install ncurses-dev && \
    git clone https://github.com/gmarik/Vundle.vim ~/.vim/bundle/Vundle.vim && \
    git clone https://github.com/vim/vim /tmp/vim && \
    cd /tmp/vim/src && \
    ./configure --with-features=huge --enable-multibyte && \
    make && \
    make install && \
    cd /tmp && \
    rm -rf /tmp/vim

RUN git clone https://github.com/9fans/go /go/src/9fans.net/go && \
    go get github.com/rogpeppe/godef && \
    go install github.com/rogpeppe/godef

ADD .vimrc /root/.vimrc

RUN vim +PluginInstall +GoInstallBinaries +qall

ENTRYPOINT ["vim"]

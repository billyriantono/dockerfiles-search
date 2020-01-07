FROM golang:wheezy
MAINTAINER Michele Bertasi

ADD fs/ /

# install pagkages
RUN apt-get update                                                      && \
    apt-get install -y ncurses-dev unzip autoconf libtolua-dev exuberant-ctags         && \
    ln -s /usr/include/lua5.2/ /usr/include/lua                         && \
    ln -s /usr/lib/x86_64-linux-gnu/liblua5.2.so /usr/lib/liblua.so
# build and install vim
RUN cd /tmp                                                             && \
    git clone https://github.com/vim/vim.git                            && \
    cd vim                                                              && \
    ./configure --with-features=huge --enable-luainterp                    \
        --enable-gui=no --without-x --prefix=/usr                       && \
    make VIMRUNTIMEDIR=/usr/share/vim/vim74                             && \
    make install
# get go tools
RUN go get golang.org/x/tools/cmd/godoc                                 && \
    go get github.com/nsf/gocode                                        && \
    go get golang.org/x/tools/cmd/goimports                             && \
    go get github.com/rogpeppe/godef                                    && \
    go get golang.org/x/tools/cmd/oracle                                && \
    go get golang.org/x/tools/cmd/gorename                              && \
    go get github.com/golang/lint/golint                                && \
    go get github.com/kisielk/errcheck                                  && \
    go get github.com/jstemmer/gotags                                   && \
    mv /go/bin/* /usr/local/go/bin
#  Install protoc
RUN cd /tmp; wget https://github.com/google/protobuf/archive/v3.0.0-beta-2.tar.gz
RUN cd /tmp; tar -xzf v3.0.0-beta-2.tar.gz
RUN cd /tmp/protobuf-3.0.0-beta-2; ./autogen.sh
RUN cd /tmp/protobuf-3.0.0-beta-2; ./configure
RUN cd /tmp/protobuf-3.0.0-beta-2; make
RUN cd /tmp/protobuf-3.0.0-beta-2; make install
RUN ldconfig
RUN go get -u github.com/golang/protobuf/protoc-gen-go
# cleanup
RUN rm -rf /go/src/* /go/pkg                                            && \
    apt-get remove -y ncurses-dev                                       && \
    apt-get autoremove -y                                               && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*      && \
    echo "set editing-mode vi" > /etc/inputrc                           && \
    echo "set keymap vi-command" >> /etc/inputrc
# add dev user
RUN \
    groupadd -g 1000 dev                                                  && \
    chown -R 1000:1000 /home/dev /go                                      && \
    adduser dev --uid 1000 --gid 1000 --disabled-password --gecos ""

USER dev
ENV HOME /home/dev

# install vim plugins
RUN mkdir -p ~/.vim/bundle                                              && \
    cd  ~/.vim/bundle                                                   && \
    git clone --depth 1 https://github.com/gmarik/Vundle.vim.git        && \
    git clone --depth 1 https://github.com/fatih/vim-go.git             && \
    git clone --depth 1 https://github.com/majutsushi/tagbar.git        && \
    git clone --depth 1 https://github.com/Shougo/neocomplete.vim.git   && \
    git clone --depth 1 https://github.com/scrooloose/nerdtree.git      && \
    git clone --depth 1 https://github.com/bling/vim-airline.git        && \
    git clone --depth 1 https://github.com/tpope/vim-fugitive.git       && \
    git clone --depth 1 https://github.com/jistr/vim-nerdtree-tabs.git  && \
    git clone --depth 1 https://github.com/mbbill/undotree.git          && \
    git clone --depth 1 https://github.com/Lokaltog/vim-easymotion.git  && \
    git clone --depth 1 https://github.com/scrooloose/nerdcommenter.git && \
    vim +PluginInstall +qall                                            && \
# cleanup
    rm -rf Vundle.vim/.git vim-go/.git tagbar/.git neocomplete.vim/.git    \
        nerdtree/.git vim-airline/.git vim-fugitive/.git                   \
        vim-nerdtree-tabs/.git undotree/.git vim-easymotion/.git           \
        nerdcommenter/.git

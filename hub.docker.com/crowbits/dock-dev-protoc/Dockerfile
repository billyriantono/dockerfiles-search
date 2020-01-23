FROM golang:wheezy
MAINTAINER Timothy Woodby

COPY scandir.sh /bin/scandir.sh
#  This is no longer necessary.
## RUN chmod +x /bin/scandir.sh

# install pagkages
RUN apt-get update                                                              && \
    apt-get install -y ncurses-dev unzip autoconf libtolua-dev exuberant-ctags  && \
    ln -s /usr/include/lua5.2/ /usr/include/lua                                 && \
    ln -s /usr/lib/x86_64-linux-gnu/liblua5.2.so /usr/lib/liblua.so

###### get go tools
RUN go get golang.org/x/tools/cmd/godoc                                         && \
    go get github.com/nsf/gocode                                                && \
    go get golang.org/x/tools/cmd/goimports                                     && \
    go get github.com/rogpeppe/godef                                            && \
    go get golang.org/x/tools/cmd/oracle                                        && \
    go get golang.org/x/tools/cmd/gorename                                      && \
    go get github.com/golang/lint/golint                                        && \
    go get github.com/kisielk/errcheck                                          && \
    go get github.com/jstemmer/gotags                                           && \
    mv /go/bin/* /usr/local/go/bin

######  Install protoc
RUN cd /tmp; wget https://github.com/google/protobuf/archive/v3.0.0-beta-2.tar.gz
RUN cd /tmp; tar -xzf v3.0.0-beta-2.tar.gz
RUN cd /tmp/protobuf-3.0.0-beta-2; ./autogen.sh
RUN cd /tmp/protobuf-3.0.0-beta-2; ./configure
RUN cd /tmp/protobuf-3.0.0-beta-2; make
RUN cd /tmp/protobuf-3.0.0-beta-2; make install
RUN ldconfig
RUN go get -u github.com/golang/protobuf/protoc-gen-go

RUN apt-get install -y inotify-tools

######################## cleanup
RUN rm -rf /go/src/* /go/pkg                                                    && \
    apt-get remove -y ncurses-dev                                               && \
    apt-get autoremove -y                                                       && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# cleanup
RUN rm -rf Vundle.vim/.git vim-go/.git tagbar/.git neocomplete.vim/.git    \
        nerdtree/.git vim-airline/.git vim-fugitive/.git                   \
        vim-nerdtree-tabs/.git undotree/.git vim-easymotion/.git           \
        nerdcommenter/.git

CMD ["scandir.sh"]

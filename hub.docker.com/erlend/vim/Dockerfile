FROM ruby:alpine

# Create user
RUN adduser -D vimuser

ENV VIM_VERSION="v8.1.1512"

# Build and install vim
RUN build_deps="build-base ncurses-dev" && \
    vim_dir="vim-`echo $VIM_VERSION | sed s/^v//`" && \
    apk add $build_deps && \
    wget -O- https://github.com/vim/vim/archive/$VIM_VERSION.tar.gz|tar zx && \
    cd $vim_dir && \
    ./configure --enable-rubyinterp && \
    make install && \
    cd / && \
    apk del $build_deps && \
    rm -rf $vim_dir

WORKDIR /home/vimuser
USER vimuser
ENTRYPOINT vim

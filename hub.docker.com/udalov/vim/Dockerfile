FROM debian:buster
MAINTAINER Sergei O. Udalov <sergei.udalov@gmail.com>

ENV AMIX_VIMRC_REVISION=993ed55

RUN apt update && apt install -y neovim git-core
RUN git clone --depth=1 https://github.com/amix/vimrc.git ~/.vim_runtime \
                      && cd ~/.vim_runtime && git checkout $AMIX_VIMRC_REVISION \
                      && sh ~/.vim_runtime/install_awesome_vimrc.sh \
                      && mkdir -p ~/.config \
                      && ln -s ~/.vim_runtime ~/.config/nvim \
                      && ln -s ~/.vimrc ~/.config/nvim/init.vim

RUN cd ~/.vim_runtime && git clone git://github.com/tpope/vim-rails.git my_plugins/vim-rails

COPY my_configs.vim /root/.vim_runtime/

WORKDIR /guest
ENTRYPOINT ["vim"]

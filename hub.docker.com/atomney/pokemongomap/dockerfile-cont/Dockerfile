# Atlas-IT 

FROM debian:jessie

MAINTAINER Jan Hoelscher <jan@atlas-it.de>

ENV DEBIAN_FRONTEND noninteractive

RUN apt update && \
    apt install -y vim git curl

RUN useradd dev && \
    echo "ALL            ALL = (ALL) NOPASSWD: ALL" >> /etc/sudoers

RUN mkdir -p /home/dev/workspace
WORKDIR /home/dev/workspace
ENV HOME /home/dev

RUN chown -R dev:dev $HOME
USER dev

RUN mkdir -p ~/.vim/autoload ~/.vim/bundle && \
    curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim

RUN echo "execute pathogen#infect()\nsyntax on\nfiletype plugin indent on" > ~/.vimrc

RUN cd ~/.vim/bundle && \
    git clone https://github.com/tpope/vim-sensible.git

RUN cd ~/.vim/bundle && \
    git clone https://github.com/itchyny/lightline.vim

RUN cd ~/.vim/bundle && \
    git clone https://github.com/terryma/vim-multiple-cursors

RUN cd ~/.vim/bundle && \
    git clone https://github.com/tpope/vim-surround

RUN cd ~/.vim/bundle && \
    git clone git://github.com/airblade/vim-gitgutter.git

RUN git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf && \
    ~/.fzf/install

RUN cd ~/.vim/bundle && \
    git clone https://github.com/junegunn/fzf.vim

RUN echo "set rtp+=~/.fzf" >> ~/.vimrc

COPY fzf.vimrc /tmp/fzf.vimrc

RUN cat /tmp/fzf.vimrc >> ~/.vimrc

COPY run /usr/local/bin/

ENTRYPOINT ["sh", "/usr/local/bin/run"]

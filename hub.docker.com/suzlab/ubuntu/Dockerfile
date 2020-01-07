FROM ubuntu:trusty

RUN apt-get update
RUN apt-get install -y curl git patch bash-completion npm vim-nox
RUN apt-get clean

RUN npm install -g jsonlint

WORKDIR /root

COPY .bashrc.patch ./
RUN patch .bashrc < .bashrc.patch
RUN rm .bashrc.patch

COPY jsonlint.patch ./
RUN patch /usr/local/lib/node_modules/jsonlint/lib/cli.js < jsonlint.patch
RUN rm jsonlint.patch

RUN curl -sOL https://raw.githubusercontent.com/Shougo/neobundle.vim/master/bin/install.sh
RUN sh ./install.sh
RUN rm install.sh 
COPY .vimrc ./
RUN vim +NeoBundleInstall +qall

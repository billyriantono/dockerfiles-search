FROM python:3.5.0

RUN apt-get update
RUN apt-get install -y vim wget git
RUN apt-get install -y vim vim-nox
RUN git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim

RUN echo """ \
\nset rtp+=~/.vim/bundle/Vundle.vim \
\ncall vundle#begin() \
\nPlugin 'mrtazz/simplenote.vim' \
\ncall vundle#end()            \" required \
\nfiletype plugin indent on    \" required \
\n \
\nlet g:SimplenoteUsername = \"y2971507@mvrht.net\" \
\nlet g:SimplenotePassword = \"test123\" """ >> ~/.vimrc

RUN git clone --recursive https://github.com/mrtazz/simplenote.vim.git ~/.vim/bundle/simplenote.vim

FROM debian

# Update packages & install wget, python, pip and awscli

RUN apt-get update && apt-get install -y curl vim wget python git && wget https://bootstrap.pypa.io/get-pip.py && python get-pip.py && pip install awscli

# Install pathogen & vim packages

RUN mkdir -p ~/.vim/autoload ~/.vim/bundle && curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim && cd ~/.vim/bundle && git clone https://github.com/scrooloose/nerdtree.git && git clone https://github.com/tomtom/tcomment_vim.git && git clone https://github.com/scrooloose/syntastic.git

# Setup .vimrc

RUN echo "execute pathogen#infect()" >> ~/.vimrc && echo "syntax on" >> ~/.vimrc

CMD /bin/bash


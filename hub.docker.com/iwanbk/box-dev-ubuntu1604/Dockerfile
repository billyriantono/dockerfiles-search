FROM ubuntu:16.04
MAINTAINER Iwan Budi Kusnanto <iwanbk@gmail.com>
RUN apt-get update -y	&& \
	apt-get install -y vim build-essential mercurial git cmake ctags pkg-config vim-nox apt-utils autoconf libtool && \
	apt-get install -y wget curl iputils-ping tmux && \
	apt-get upgrade -y && \

	# vim
	cd && \

	# vim bundle & pathogen
	mkdir -p ~/.vim/autoload ~/.vim/bundle && \
	curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim && \
	echo "execute pathogen#infect()" >> ~/.vimrc && \

	# vim neocomplete
	cd ~/.vim/bundle && \
	git clone https://github.com/Shougo/neocomplete.vim.git && \
	echo "let g:neocomplete#enable_at_startup = 1" >> ~/.vimrc


ADD vimrc /etc/vim/


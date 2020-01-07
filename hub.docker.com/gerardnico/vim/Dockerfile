FROM ubuntu:16.04

# Root
RUN \
    echo "==> Add user Vim..."  && \
    useradd -m vim && \
    echo "==> Update"  && \
    apt-get update -y

RUN \
	echo "==> Install Vim and tools"  && \
	apt-get install -y vim wget jq

# Vim
ENV VIM_USER vim
USER $VIM_USER

ENV VIM_CONF_DIR /home/$VIM_USER/.vim
ENV VIM_WORK_DIR /home/$VIM_USER/workdir

RUN \
	echo "==> Creating the dir structure" && \
	mkdir -p $VIM_WORK_DIR && \
	mkdir -p $VIM_CONF_DIR && \
    echo "==> Add user ColorSchem Monokai..."  && \
    wget -O $VIM_CONF_DIR/monokai.vim https://raw.githubusercontent.com/sickill/vim-monokai/master/colors/monokai.vim

COPY .vimrc $HOME/.vimrc

WORKDIR $VIM_WORK_DIR


#
# Run Example: 
#    docker run --rm -it gerardnico/vim:latest bash

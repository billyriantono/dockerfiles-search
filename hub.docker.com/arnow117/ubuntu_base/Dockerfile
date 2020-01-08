FROM ubuntu:16.04

MAINTAINER arnow117 "arnow117@gmail.com"
ENV TOOLS_PATH /root/Tools
ENV WORK_PATH /root/Workspace
RUN mkdir $TOOLS_PATH $WORK_PATH

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils
RUN apt-get install -y git vim curl wget python python3 python-pip python3-pip tmux openssh-server
RUN echo "install essential basic apps"

#Config awesome vim
RUN git clone --depth=1 git://github.com/amix/vimrc.git ~/.vim_runtime
RUN sh ~/.vim_runtime/install_basic_vimrc.sh

#Install&config oh-my-zsh
RUN apt-get install -y zsh
RUN git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
RUN chsh -s /bin/zsh
COPY zshrc /root/.zshrc

#Config PIP for China & install IPython
RUN mkdir -p /root/.config/pip
COPY pip.conf /root/.config/pip/pip.conf
RUN pip3 install ipython

WORKDIR $WORK_PATH


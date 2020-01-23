FROM ubuntu:latest

RUN apt-get clean && apt-get update && apt-get install -y locales
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8
ENV LC_ALL en_US.UTF-8
COPY .vimrc /root/.vimrc
COPY .vim /root/.vim
COPY .bashrc /root/.bashrc
COPY .tmux.conf /root/.tmux.conf

RUN apt-get -y install git vim g++ python
WORKDIR /root

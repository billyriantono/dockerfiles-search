FROM ubuntu:16.04

RUN apt-get update && apt-get install -y \
    git \
    vim

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

COPY ./vim /root/.vim/
COPY ./vimrc /root/.vimrc
COPY ./bashrc /root/.bashrc
COPY ./gitconfig /root/.gitconfig

VOLUME /code
WORKDIR /code

CMD ["/bin/bash"]

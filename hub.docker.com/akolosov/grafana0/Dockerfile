FROM ubuntu:16.04
MAINTAINER akirakudo <aki9do@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

# install sudo
RUN apt-get update && apt-get install -y sudo

# add user
RUN groupadd -g 1000 admin && useradd -g admin -G sudo -m -s /bin/bash akira && echo 'akira:password' | chpasswd
RUN echo 'akira ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

ENV HOME /home/akira
WORKDIR $HOME

USER akira

# install basic package
RUN sudo apt-get install -y git make build-essential curl

# install pyenv
RUN git clone git://github.com/yyuu/pyenv.git ~/.pyenv
RUN git clone https://github.com/yyuu/pyenv-pip-rehash.git ~/.pyenv/plugins/pyenv-pip-rehash

ENV PYENV_ROOT $HOME/.pyenv
ENV PATH $PYENV_ROOT/bin:$PATH

# install anaconda
RUN pyenv install anaconda3-4.4.0
RUN pyenv global anaconda3-4.4.0

ENV PATH $PYENV_ROOT/versions/anaconda3-4.4.0/bin:$PATH
RUN conda update -y conda

CMD /bin/bash

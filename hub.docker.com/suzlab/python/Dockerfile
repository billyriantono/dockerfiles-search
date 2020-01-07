FROM suzlab/ubuntu:latest

RUN apt-get update
RUN apt-get install -y python-pip python-dev
RUN apt-get clean

RUN pip install autopep8
RUN pip install pylint
RUN pip install virtualenv

WORKDIR /root

COPY .bashrc.patch ./
RUN patch .bashrc < .bashrc.patch
RUN rm .bashrc.patch

COPY .vimrc.patch ./
RUN patch .vimrc < .vimrc.patch
RUN rm .vimrc.patch
RUN vim +NeoBundleInstall +qall 

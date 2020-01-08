FROM suzlab/ubuntu:latest

WORKDIR /root

COPY .bashrc.patch ./
RUN patch .bashrc < .bashrc.patch
RUN rm .bashrc.patch

COPY .vimrc.patch ./
RUN patch .vimrc < .vimrc.patch
RUN rm .vimrc.patch
RUN vim +NeoBundleInstall +qall 

RUN git clone https://github.com/suz-lab/docker.git 

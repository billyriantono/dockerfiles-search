FROM ubuntu

ARG latex_user=latex_user
RUN echo ${latex_user}
RUN apt-get update
RUN apt-get install -y xterm wget perl vim
RUN export TERM=xterm
RUN adduser --disabled-password --shell /bin/bash --gecos "User" $latex_user && su $latex_user
# https://wiki.termux.com/wiki/TeX_Live
RUN apt-get install -y texlive

VOLUME ["/documents"]
WORKDIR /documents
CMD ["bash"]



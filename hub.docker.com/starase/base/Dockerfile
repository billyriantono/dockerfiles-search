FROM ubuntu:16.04
MAINTAINER Paolo De Michele <paolo@starase.com>


RUN apt-get update && apt-get upgrade -y
RUN apt-get install vim supervisor git-core zsh curl -y
RUN curl -L http://install.ohmyz.sh | sh || true
RUN chsh -s $(which zsh)
RUN mkdir -p /etc/starase
COPY zsh.sh /etc/starase/zsh.sh
RUN  chmod +x /etc/starase/zsh.sh \
&& /bin/bash /etc/starase/zsh.sh

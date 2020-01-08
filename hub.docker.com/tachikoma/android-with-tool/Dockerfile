FROM tachikoma/android-base:latest

LABEL maintainer="kentrino@h-kento.jp"

# install git-lfs
RUN echo 'deb http://http.debian.net/debian wheezy-backports main' | sudo tee -a /etc/apt/sources.list.d/wheezy-backports-main.list
RUN curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash
RUN sudo apt-get install git-lfs

# install ruby
RUN sudo apt install ruby

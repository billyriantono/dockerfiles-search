FROM debian:jessie
MAINTAINER Samisdat bastian.pertz@gmail.com

RUN apt-get update

RUN apt-get install -y apt-utils
RUN apt-get install -y net-tools
RUN apt-get install -y ca-certificates
RUN apt-get install -y htop
RUN apt-get install -y vim

RUN apt-get install -y wget
RUN apt-get install -y curl
RUN apt-get install -y unzip

## set locale
RUN apt-get install -y locales
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen
RUN echo 'LANG="en_US.UTF-8"' > /etc/default/locale
RUN dpkg-reconfigure --frontend=noninteractive locales
RUN update-locale LANG=en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
ENV LC_ALL C.UTF-8

RUN apt-get install -y git-core
RUN apt-get install -y git-flow

#install node
RUN curl -sL https://deb.nodesource.com/setup_5.x | bash -
RUN apt-get install -y nodejs


#install grunt-cli
RUN npm install -g grunt-cli
RUN npm install -g bower

## install oh-my-zsh
RUN apt-get install -y zsh
RUN curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh | bash -

## install ssh-server
RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN sed -i 's@#PasswordAuthentication yes@PasswordAuthentication no@g' /etc/ssh/sshd_config
RUN mkdir /root/.ssh

# install tig from source while the one from package is not working
RUN mkdir /root/tig
RUN git clone https://github.com/jonas/tig.git /root/tig
RUN apt-get install -y build-essential
RUN apt-get install -y ncurses-dev
WORKDIR /root/tig
RUN make
RUN make install
RUN ln -s /root/bin/tig /bin/tig
RUN apt-get remove -y build-essential
RUN apt-get remove -y ncurses-dev
RUN rm -rf /root/tig
WORKDIR /

EXPOSE 22


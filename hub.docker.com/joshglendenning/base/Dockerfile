FROM debian
MAINTAINER Josh Glendenning <joshglendenning@gmail.com>

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections
RUN apt-get update
RUN apt-get -y install vim zsh wget curl
RUN apt-get -y install python-software-properties
RUN apt-get -y install software-properties-common

CMD /bin/zsh

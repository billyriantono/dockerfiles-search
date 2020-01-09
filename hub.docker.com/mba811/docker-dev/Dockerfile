FROM ubuntu:14.10
MAINTAINER Tsong khapa <ztd811@yahoo.com>
ADD etc /etc
CMD /config/loop
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
	apt-get upgrade -y
# Install Oracle Java7
RUN apt-get install -y software-properties-common && \
    add-apt-repository -y ppa:webupd8team/java && \
    apt-get update && \
    echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
    echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections && \
    apt-get install -y oracle-java7-installer
ENV JAVA_HOME /usr/lib/jvm/java-7-oracle/
# Install languages
RUN apt-get install -y ruby && \
    apt-get install -y python && \
    apt-get install -y erlang && \
    apt-get install -y golang
# Install tools
RUN apt-get install -y git && \
    apt-get install -y mercurial && \
    apt-get install -y diffstat && \
    apt-get install -y maven && \
    apt-get install -y emacs && \
    apt-get install -y vim && \
    apt-get install -y cmake && \
    apt-get install -y build-essential && \
    apt-get install -y tcpdump && \
    apt-get install -y tmux && \
    apt-get install -y curl && \
    apt-get install -y wget && \
    apt-get install -y strace && \
    apt-get install -y gem && \
    apt-get install -y python-pip && \
    apt-get install -y ack-grep && \
    apt-get install -y htop && \
    apt-get install -y unrar && \
    apt-get install -y unzip && \
    apt-get install -y pwgen && \
    apt-get instll -y docker.io && \
	apt-get clean && \
	echo -n > /var/lib/apt/extended_states
RUN mkdir /config /data
RUN useradd -u 500 core
ADD config /config
RUN chmod +x /config/loop
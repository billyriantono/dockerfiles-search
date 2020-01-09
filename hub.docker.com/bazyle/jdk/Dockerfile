FROM library/ubuntu:latest
LABEL maintainer="vasilevici777@gmail.com"

# Setup play-framework user
RUN groupadd -r play -g 1000 && useradd -u 1000 -r -g play -m -d /opt/play -s /bin/nologin -c "Play Framework user" play && chmod 755 /opt/play

# User root user to install software
USER root

# INSTALL OS DEPENDENCIES
RUN apt-get update; apt-get install -y software-properties-common unzip
RUN apt-get install -y apt-transport-https

# Install necessary packages
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
    echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections && \
    add-apt-repository -y ppa:webupd8team/java && \
    apt-get update && \
    apt-get install -y oracle-java8-installer

RUN apt-get clean


# Switch back to our user
USER play

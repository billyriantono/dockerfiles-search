# VERSION 1.0
# DOCKER-VERSION  1.2.0
# AUTHOR:         Richard Lee <lifuzu@gmail.com>
# DESCRIPTION:    Devbase-gvm Image Container - groovy environment manager

FROM dockerbase/devbase-jdk

MAINTAINER Richad Lee "lifuzu@gmail.com"

ENV LC_ALL C
ENV DEBIAN_FRONTEND noninteractive

# Installed Java Jdk/Jre
ENV     JAVA_HOME /usr/local/java
ENV     JRE_HOME /usr/local/java/jre
ENV     PATH $PATH:$JAVA_HOME/bin:$JRE_HOME/bin

USER    root
# Run the build scripts
RUN     apt-get update

RUN     apt-get install -y --no-install-recommends unzip

# Clean up system
RUN     apt-get clean
RUN     rm -rf /tmp/* /var/tmp/*

USER    devbase

# Set environment variables.
ENV     HOME /home/devbase

# Define working directory.
WORKDIR /home/devbase

# Install gvm
RUN     curl -s get.gvmtool.net | bash
RUN     bash $HOME/.gvm/bin/gvm-init.sh

# Define default command.
CMD ["bash"]

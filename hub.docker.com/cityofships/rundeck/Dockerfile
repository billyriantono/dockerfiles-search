FROM ubuntu:14.04
MAINTAINER cityofships
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get install -yq openssh-client openjdk-7-jre

# Add the install commands
ADD ./install.sh /

ADD ./run.sh /

# Change Rundeck admin password from default
ENV RDPASS RDPASS

ENV MYHOST MYHOST

# From address when sending email
ENV MAILFROM MAILFROM

# Download Rundeck
ADD http://dl.bintray.com/rundeck/rundeck-deb/rundeck-2.6.7-1-GA.deb /tmp/rundeck.deb

# Run the installation script
RUN /install.sh
RUN chown rundeck /tmp/rundeck

ENTRYPOINT /run.sh

VOLUME /var/lib/rundeck/data
VOLUME /var/lib/rundeck/var
VOLUME /var/lib/rundeck/logs
VOLUME /var/rundeck/projects

EXPOSE 4440 4443

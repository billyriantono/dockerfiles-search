FROM ubuntu:14.04
MAINTAINER Michaela Böckler 

ENV DEBIAN_FRONTEND noninteractive

#Install VLC 

RUN apt-get update && apt-get install -y  \
	libgl1-mesa-dri \
	libgl1-mesa-glx \
	openssh-client \
	&& rm -rf /var/lib/apt/lists/*

COPY sshclient.sh /opt/
#RUN mkdir /.ssh
#COPY id_rsa /.ssh/

RUN chmod +x /opt/sshclient.sh

ENTRYPOINT ["/opt/sshclient.sh"]

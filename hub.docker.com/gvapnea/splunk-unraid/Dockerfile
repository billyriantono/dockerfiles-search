### Dockerfile for splunk
FROM phusion/baseimage:0.9.16
MAINTAINER gvapnea

ENV SPLUNK_PRODUCT splunk


# 7.3.2
ENV SPLUNK_VERSION 7.3.2
ENV SPLUNK_BUILD c60db69f8e32
ENV SPLUNK_FILENAME splunk-${SPLUNK_VERSION}-${SPLUNK_BUILD}-linux-2.6-amd64.deb
## 8.0.0
#ENV SPLUNK_VERSION 8.0.0
#ENV SPLUNK_BUILD 1357bef0a7f6
#ENV SPLUNK_FILENAME splunk-${SPLUNK_VERSION}-${SPLUNK_BUILD}-linux-2.6-amd64.deb

ENV HOME /root
ENV SPLUNK_HOME=/opt/splunk
ENV DEBIAN_FRONTEND noninteractive
ENV LC_ALL C.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8

CMD ["/sbin/my_init"]

# Configure user nobody to match unRAID's settings
RUN usermod -u 99 nobody && \
    usermod -g 100 nobody && \
    usermod -d /home nobody && \
    chown -R nobody:users /home

# Disable SSH
RUN rm -rf /etc/service/sshd /etc/my_init.d/00_regen_ssh_host_keys.sh

RUN apt-get clean
RUN apt-get update -q && \
	apt-get install -y wget
RUN apt-get install -y dpkg
	
RUN wget -O ${SPLUNK_FILENAME} https://download.splunk.com/products/${SPLUNK_PRODUCT}/releases/${SPLUNK_VERSION}/linux/${SPLUNK_FILENAME}

RUN dpkg -i /${SPLUNK_FILENAME}
RUN rm /${SPLUNK_FILENAME}

### Configure Service Startup
    
RUN echo "#!/bin/sh " > /etc/rc.local
RUN echo "nohup /opt/splunk/bin/splunk start --accept-license --answer-yes --no-prompt &" >> /etc/rc.local
RUN echo "exit 0 " >> /etc/rc.local
RUN chmod a+x /etc/rc.local && \
    chown -R nobody:users /opt/splunk

RUN printf "\nOPTIMISTIC_ABOUT_FILE_LOCKING = 1\n" >> $SPLUNK_HOME/etc/splunk-launch.conf

EXPOSE 8000 8088 8089 9997 514 

VOLUME [ "/opt/splunk/etc", "/opt/splunk/var", "/data", "/license" ]


### END
### To make this a persistent container, you must map /opt/splunk/var and /opt/splunk/etc of this container
### to a folder on your host machine.
###

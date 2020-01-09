FROM phusion/baseimage:0.9.15

#########################################
##        ENVIRONMENTAL CONFIG         ##
#########################################

# Set correct environment variables
ENV DEBIAN_FRONTEND noninteractive
ENV HOME            /root
ENV LC_ALL          C.UTF-8
ENV LANG            en_US.UTF-8
ENV LANGUAGE        en_US.UTF-8
ENV PATH            $PATH
ENV WEBPORT         8765

#########################################
##              Install                ##
#########################################

ADD install.sh /tmp/

# Configure user nobody to match unRAID's settings
RUN usermod -u 99 nobody && usermod -g 100 nobody && usermod -d /home nobody && chown -R nobody:users /home

# Disable SSH
RUN rm -rf /etc/service/sshd /etc/my_init.d/00_regen_ssh_host_keys.sh

RUN mkdir -p /var/run/dbus

# Repositories
RUN add-apt-repository "deb http://us.archive.ubuntu.com/ubuntu/ trusty universe multiverse" && add-apt-repository "deb http://us.archive.ubuntu.com/ubuntu/ trusty-updates universe multiverse"

# Install prerequisites
RUN sudo apt-get update && sudo apt-get install -qy git make gcc g++ && curl -sL https://deb.nodesource.com/setup_6.x | bash - && sudo apt-get install -qy nodejs && sudo apt-get install -qy avahi-daemon avahi-discover libnss-mdns libavahi-compat-libdnssd-dev

# Install homebridge
RUN sudo npm install -g --unsafe-perm homebridge && sudo npm install -g --unsafe-perm homebridge-server 

##################################################
#               Start                            #
##################################################

USER root

EXPOSE 5353 51826 $WEBPORT

ADD run.sh /root/run.sh

VOLUME ["/root/.homebridge"]
CMD ["/root/run.sh"]

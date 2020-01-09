FROM debian:latest

MAINTAINER / Heiko Holzheimer 

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y build-essential python apt-utils curl avahi-daemon git unzip sudo wget nano

#RUN curl -sL https://deb.nodesource.com/setup_8.x | bash
#RUN apt-get install -y nodejs

#RUN sed -i '/^rlimit-nproc/s/^\(.*\)/#\1/g' /etc/avahi/avahi-daemon.conf
#RUN sed -i -e 's/# de_DE.UTF-8 UTF-8/de_DE.UTF-8 UTF-8/' /etc/locale.gen && \dpkg-reconfigure --frontend=noninteractive locales && \update-locale LANG=de_DE.UTF-8
#ENV LANG de_DE.UTF-8 
#RUN cp /usr/share/zoneinfo/Europe/Berlin /etc/localtime
#ENV TZ Europe/Berlin

RUN mkdir -p /opt/hyperion/ && chmod 777 /opt/hyperion/
#RUN mkdir -p /opt/scripts/ && chmod 777 /opt/scripts/

WORKDIR /opt/hyperion/

#ADD scripts/avahi_startup.sh avahi_startup.sh
#RUN chmod +x avahi_startup.sh
#RUN mkdir /var/run/dbus/

#ADD scripts/iobroker_startup.sh iobroker_startup.sh
RUN curl -k -L --output install_hyperion.sh --get https://raw.githubusercontent.com/hyperion-project/hyperion/master/bin/install_hyperion.sh
RUN chmod +x install_hyperion.sh
RUN sudo sh ./install_hyperion.sh

#WORKDIR /opt/iobroker/

#RUN npm install iobroker --unsafe-perm && echo $(hostname) > .install_host
#RUN update-rc.d iobroker.sh remove
#RUN npm install node-gyp -g
#RUN npm install --global speed-test

#CMD ["sh", "/opt/scripts/iobroker_startup.sh"]

ENV DEBIAN_FRONTEND teletype

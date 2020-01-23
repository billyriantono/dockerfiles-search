FROM phusion/baseimage:0.9.16

MAINTAINER giovanni@atende.info

RUN apt-get update -qq && \
    apt-get install -qqy software-properties-common python-software-properties && \
    apt-add-repository ppa:webupd8team/java -y && \
    apt-get update -qq && \
    echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
    apt-get install -y oracle-java7-installer && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install confluence
COPY install-confluence.sh /root/install-confluence.sh
RUN /root/install-confluence.sh

# Launching confluence
# And add start script in my_init.d of Phusion baseimage
WORKDIR /opt/confluence-home
RUN rm -f /opt/confluence-home/.confluence-home.lock && mkdir -p /etc/my_init.d
COPY ./start-confluence.sh /etc/my_init.d/start-confluence.sh

EXPOSE 8090

CMD  ["/sbin/my_init"]

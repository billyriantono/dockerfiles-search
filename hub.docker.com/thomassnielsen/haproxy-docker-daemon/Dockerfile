FROM ubuntu:14.04

RUN apt-get update
RUN apt-get install -y software-properties-common python-software-properties
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1C61B9CD
RUN add-apt-repository ppa:vbernat/haproxy-1.6
RUN apt-get remove -y software-properties-common python-software-properties
RUN apt-get update
RUN apt-get install -y haproxy supervisor
RUN rm -rf /var/lib/apt/lists/*

ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf

CMD ["supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]

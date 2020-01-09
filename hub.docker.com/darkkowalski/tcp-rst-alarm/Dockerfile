FROM ubuntu:18.04
RUN apt-get update \
	&& apt-get upgrade -y \
	&& apt-get install -y tcptraceroute curl ruby build-essential ruby-dev bc \
	&& rm -rf /var/lib/apt/lists/* 

RUN gem install json

RUN curl -o /usr/local/bin/tcpping http://www.vdberg.org/~richard/tcpping \
	&&chmod +x /usr/local/bin/tcpping

COPY run.sh /opt/tcprstalarm/
COPY lib/ /opt/tcprstalarm/lib/
COPY shell/ /opt/tcprstalarm/shell/

RUN mkdir -p /etc/tcprstalarm/

ENTRYPOINT ["/opt/tcprstalarm/run.sh"]
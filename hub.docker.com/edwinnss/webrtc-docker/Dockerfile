# stream oriented kurento VERSION  4.4.3
# Added mongoDB & NodeJS project

FROM      ubuntu:14.04

RUN apt-get update \
  && apt-get -y dist-upgrade \
	&& apt-get install -y wget

RUN	echo "deb http://ubuntu.kurento.org/ trusty kms6" | tee /etc/apt/sources.list.d/kurento.list \
	&& wget -O - http://ubuntu.kurento.org/kurento.gpg.key | apt-key add - \
	&& apt-get update \
	&& apt-get -y install kurento-media-server-6.0 \
	&& apt-get clean \
  && rm -rf /var/lib/apt/lists/*

#git & node
RUN apt-get update \
	&& apt-get -y install git \
	&& apt-get -y install curl && curl -sL https://deb.nodesource.com/setup_6.x | bash - && apt-get install -y nodejs

#other needed
RUN apt-get -y install python \
	&& apt-get -y install make \
	&& apt-get -y install g++ && apt-get -y install build-essential

#mongodb
RUN sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10 \
  && echo "deb http://downloads-distro.mongodb.org/repo/debian-sysvinit dist 10gen" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list \
  && apt-get update && apt-get -y install mongodb-org

# Create the MongoDB data directory
RUN mkdir -p /data/db

WORKDIR "/home"

RUN git clone https://github.com/Ynov-webRTC/ynov_rtc.git

WORKDIR "/home/ynov_rtc"
RUN sudo npm install \
	&& npm install -g bower

WORKDIR "/home/ynov_rtc/public"
RUN bower install --allow-root

WORKDIR "/"

EXPOSE 8888 8443 27017

COPY ./entrypoint.sh /entrypoint.sh

ENV GST_DEBUG=Kurento*:5

RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
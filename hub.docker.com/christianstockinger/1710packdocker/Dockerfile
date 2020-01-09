FROM openjdk:8-jre-alpine

Label maintainer Stockinger Christian <mail@christian-stockinger.de>

RUN apk update \ 
	&& apk add ca-certificates wget \ 
	&&  update-ca-certificates

RUN  	mkdir -p /opt/minecraft \
    &&  cd /opt/minecraft \
    &&  wget -q http://solder.endermedia.com/repository/downloads/the-1710-pack/the-1710-pack_0.9.8b.zip \
	&& unzip the-1710-pack_0.9.8b.zip \
	&& rm the-1710-pack_0.9.8b.zip \
	&& chmod +x LaunchServer.sh

EXPOSE 25565

CMD echo eula=true > /eula.txt && LaunchServer.sh
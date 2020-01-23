FROM maven:3.5.2-jdk-9-slim as defaultjavaapp
MAINTAINER brian.wilkinson@1and1.co.uk
COPY defaultapp /
RUN cd /defaultapp && mvn package

FROM 1and1internet/debian-9
MAINTAINER brian.wilkinson@1and1.co.uk
COPY files/ /
COPY --from=defaultjavaapp /defaultapp/target/defaultapp-1.0-SNAPSHOT-jar-with-dependencies.jar /opt/jarfiles
RUN export DEBIAN_FRONTEND=noninteractive DEBCONF_NONINTERACTIVE_SEEN=true \
	&& echo "deb http://ftp.debian.org/debian stretch-backports main" >> /etc/apt/sources.list \
	&& apt-get update \
	&& apt-get install openjdk-9-jre-headless \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/* \
	&& mkdir -p /var/www/ \
	&& chmod 777 /var/www/ \
	&& chmod +x /usr/local/bin/* \
	&& chmod -R 777 /opt/jarfiles
WORKDIR /var/www

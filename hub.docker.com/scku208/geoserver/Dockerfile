FROM tomcat:9-jre8-alpine
MAINTAINER scku208 <scku208@gmail.com>
RUN apk update \
	&& apk add \
		--no-cache --virtual .get_war_deps \
		openssl \
	&& wget \
		-O geoserver.zip http://sourceforge.net/projects/geoserver/files/GeoServer/2.13.1/geoserver-2.13.1-war.zip \
	&& unzip \
		geoserver.zip geoserver.war \
		-d /usr/local/tomcat/webapps \
	&& rm \
		geoserver.zip \
	&& apk del \
		.get_war_deps
VOLUME /usr/local/tomcat/webapps/

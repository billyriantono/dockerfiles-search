FROM tomcat:7.0.86-jre8

# Version
ENV GEOSERVER_VERSION 2.15.2

# MediaWiki setup
RUN curl -fSL "https://jaist.dl.sourceforge.net/project/geoserver/GeoServer/${GEOSERVER_VERSION}/geoserver-${GEOSERVER_VERSION}-war.zip" -o geoserver-war.zip \
        && unzip geoserver-war.zip -d webapps/

# Open port 8080 so linked containers can see them
EXPOSE 8080
FROM tomcat:9.0-jre8
MAINTAINER Damien PIQUET <dpiquet@teicee.com>

RUN curl https://datapacket.dl.sourceforge.net/project/geonetwork/GeoSource%20-%20french%20only/GeoSource3.0.1/geosource.war --output /usr/local/tomcat/webapps/geosource.war \
    && mkdir /usr/local/tomcat/webapps/geosource \
    && unzip /usr/local/tomcat/webapps/geosource.war -d /usr/local/tomcat/webapps/geosource/ \
    && rm /usr/local/tomcat/webapps/geosource.war

CMD ["catalina.sh", "run"]

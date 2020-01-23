FROM oscarfonts/geoserver:2.11.1

MAINTAINER michimau <mauro.michielon@eea.europa.eu>

RUN wget https://github.com/ngageoint/elasticgeo/releases/download/2.11.1-RC1/elasticgeo-2.11.1.zip
RUN unzip -o elasticgeo-2.11.1.zip -d /usr/local/geoserver/WEB-INF/lib/
#RUN mv elasticgeo-2.11.0.jar /usr/local/geoserver/WEB-INF/lib/

RUN rm /usr/local/geoserver/WEB-INF/lib/postgresql-*.jar

RUN wget https://github.com/locationtech/geogig/releases/download/v1.1.1/geoserver-2.11.x-geogig-plugin.zip
RUN unzip -o geoserver-2.11.x-geogig-plugin.zip -d /usr/local/geoserver/WEB-INF/lib/

EXPOSE 8080

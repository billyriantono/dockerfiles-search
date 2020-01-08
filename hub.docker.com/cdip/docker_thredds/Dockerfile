#
# docker builed -t thredds .
# docker run --name THREDDS -i -t thredds
# docker run --name=sccoos_thredds -m 2048M -d -p 8081:8080 thredds
# docker run --name=thredds -m 2048M -v /data/InSitu/SASS/netcdfs:/mnt -d -p 8081:8080 thredds
#
FROM tomcat:jre8
MAINTAINER darren

#EXPOSE 8080 8443

RUN apt-get update && apt-get install -y \
  libnetcdf-dev \
  vim 

ADD ./data data

#RUN sed -i '$i<role rolename="manager-gui"/>' conf/tomcat-users.xml && \
#    sed -i '$i<user username="sccoos" password="c2Njb29z" roles="manager-gui"/>' conf/tomcat-users.xml

RUN mkdir -p content/thredds && \
    cp -r data/thredds content

RUN chmod 775 data/thredds*.war && \
    chmod 775 data/setenv.sh && \
    mv data/thredds*.war webapps/thredds.war && \
    mv data/setenv.sh bin/setenv.sh

RUN mkdir -p /mnt/archive/100p1 && \
    mv data/*.nc /mnt/archive/100p1
    
COPY docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["catalina.sh", "run"]

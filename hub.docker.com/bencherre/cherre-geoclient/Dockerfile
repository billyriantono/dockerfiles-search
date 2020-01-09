FROM tomcat:8.0.43-jre8

LABEL GEOSUPPORT_RELEASE=18c GEOSUPPORT_VERSION=18.3
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends wget unzip git openjdk-8-jdk maven build-essential jq

RUN mkdir /app/

WORKDIR /app/

# Get the latest Geosupport
RUN wget --progress=dot -e dotbytes=10M http://www1.nyc.gov/assets/planning/download/zip/data-maps/open-data/gdelx_18c.zip \
    && unzip gdelx_18c.zip \
    && rm gdelx_18c.zip

# Set some paths
ENV GEOSUPPORT_HOME=/app/version-18c_18.3 \
    JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/
ENV LD_LIBRARY_PATH=$GEOSUPPORT_HOME/lib/ \
    GEOFILES=$GEOSUPPORT_HOME/fls/ \
    GS_INCLUDE_PATH=$GEOSUPPORT_HOME/include/foruser \
    GS_LIBRARY_PATH=$GEOSUPPORT_HOME/lib

# Install JSONP support
RUN git clone https://github.com/bhagyas/spring-jsonp-support \
    && ( cd spring-jsonp-support \
         && mvn -Dmaven.compiler.source=1.8 -Dmaven.compiler.target=1.8 install ) \
    && rm -rf spring-jsonp-support

# Patch & build the Geoclient from master
RUN (git clone https://github.com/CityOfNewYork/geoclient.git \
    && cd geoclient \
    && ./gradlew clean build)

# this relates to an older version //&& patch -p1 < /app/geoclient-build.patch \

# Cleanup unused files
# RUN DEBIAN_FRONTEND=noninteractive apt-get remove -y unzip wget git openjdk-8-jdk maven build-essential \
#     && DEBIAN_FRONTEND=noninteractive apt-get autoremove -y \
#     && apt-get clean \
#     && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /root/.m2 root/.gradle

# Replace default Tomcat web application with Geoclient
RUN (rm -rfv $CATALINA_HOME/webapps/ROOT && \
    cp -v /app/geoclient/geoclient-service/build/libs/geoclient-service-2.0.0-rc.1.war $CATALINA_HOME/webapps/ROOT.war)

# in order to remove the buid folder which is about 2GB, we will move the required geoclient libraries outside
ENV GEOCLIENT_BUILT_LIBS=/app/geoclient_built_libs
RUN (mv -v /app/geoclient/build/libs/ $GEOCLIENT_BUILT_LIBS \
  && rm -rfv /app/geoclient)

# Setup Tomcat to link to our native library
ENV CATALINA_OPTS=-Djava.library.path=/usr/lib/jni/:$LD_LIBRARY_PATH:$GEOCLIENT_BUILT_LIBS

#setup a HEALTHCHECK for a particular (random) bin.
HEALTHCHECK --interval=5s CMD curl --silent http://localhost:8080/bin.json?bin=1022573 |jq '(.bin.geosupportReturnCode == "00")' ||exit 1

EXPOSE 8080

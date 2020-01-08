FROM neoskop/maven
MAINTAINER Neoskop DevOps "devops@neoskop.de"

ENV TOMCAT_MAJOR_VERSION=8 \
    TOMCAT_VERSION=8.5.24 \
    TOMCAT_USER=tomcat \
    HOME_DIR=/home/tomcat \
    CATALINA_HOME=/home/tomcat/tomcat \
    PATH=/home/tomcat/tomcat/bin:/home/tomcat/bin:$PATH

# Fetch binaries
RUN apk add --no-cache --virtual .fetch-deps ca-certificates tar gnupg && \
    set -ex && \
    for key in \
  		05AB33110949707C93A279E3D3EFE6B686867BA6 \
  		07E48665A34DCAFAE522E5E6266191C37C037D42 \
  		47309207D818FFD8DCD3F83F1931D684307A10A5 \
  		541FBE7D8F78B25E055DDEE13C370389288584E7 \
  		61B832AC2F1C5A90F0F9B00A1C506407564C17A3 \
  		713DA88BE50911535FE716F5208B0AB1D63011C7 \
  		79F7026C690BAA50B92CD8B66A3AD3F4F22C4FED \
  		9BA44C2621385CB966EBA586F72C284D731FABEE \
  		A27677289986DB50844682F8ACB77FC2E86E29AC \
  		A9C5DF4D22E99998D9875A5110C01C5A2F6059E7 \
  		DCFD35E0BF8CA7344752DE8B6FB21E8933C60243 \
  		F3A04C595DB5B6A5F1ECA43E3B7BBB100D811BBE \
  		F7DA48BB64BCB84ECBA7EE6935CD23C10D498E23 \
  	; do \
  		gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key" || \
        gpg --keyserver pgp.mit.edu --recv-keys "$key" || \
        gpg --keyserver keyserver.pgp.com --recv-keys "$key" ; \
  	done && \
    adduser -S $TOMCAT_USER && \
    cd $HOME_DIR && \
    wget -q -O tomcat.tar.gz "http://www.apache.org/dist/tomcat/tomcat-$TOMCAT_MAJOR_VERSION/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz" && \
    wget -q -O tomcat.tar.gz.asc "http://www.apache.org/dist/tomcat/tomcat-$TOMCAT_MAJOR_VERSION/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz.asc" && \
    gpg --batch --verify tomcat.tar.gz.asc tomcat.tar.gz && \
    apk del .fetch-deps

USER $TOMCAT_USER

# Install Tomcat
RUN tar -xvf $HOME_DIR/tomcat.tar.gz -C $HOME_DIR && \
    ln -s $HOME_DIR/apache-tomcat-$TOMCAT_VERSION $CATALINA_HOME && \
    rm -rf $CATALINA_HOME/webapps/*

# Copy custom server.xml to container
COPY server.xml $CATALINA_HOME/conf/

EXPOSE 8080
CMD $CATALINA_HOME/bin/catalina.sh run

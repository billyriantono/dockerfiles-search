FROM vincentvu/oracle-java8

# Default values for build-args
ARG ARG_TOMCAT_MAJOR="8"
ARG ARG_TOMCAT_VERSION="8.5.4"

# Set environment variables
ENV TOMCAT_MAJOR $ARG_TOMCAT_MAJOR
ENV TOMCAT_VERSION $ARG_TOMCAT_VERSION
ENV CATALINA_HOME /usr/local/tomcat
ENV PATH $CATALINA_HOME/bin:$PATH

# Create user tomcat directory
RUN groupadd -r tomcat && \
		useradd -r -g tomcat -m -d $CATALINA_HOME tomcat

USER tomcat
WORKDIR $CATALINA_HOME

ENV TOMCAT_TGZ_URL https://archive.apache.org/dist/tomcat/tomcat-$TOMCAT_MAJOR/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz

RUN set -x \
	&& wget  $TOMCAT_TGZ_URL.sha1 \
	&& wget  $TOMCAT_TGZ_URL \
	&& sha1sum -c apache-tomcat-$TOMCAT_VERSION.tar.gz.sha1 \
	&& tar -xvf apache-tomcat-$TOMCAT_VERSION.tar.gz --strip-components=1 \
	&& rm bin/*.bat \
	&& rm apache-tomcat-$TOMCAT_VERSION.tar.gz*

EXPOSE 8080
CMD ["catalina.sh", "run"]

# link3tecnologia/tomcat:8
FROM link3tecnologia/oraclejava:8
ENV TOMCAT_VERSION=8.5.24
ENV TOMCAT_FILE=apache-tomcat-$TOMCAT_VERSION.tar.gz
ENV CATALINA_HOME=/opt/tomcat
# let "Tomcat Native" live somewhere isolated
ENV TOMCAT_NATIVE_LIBDIR $CATALINA_HOME/native-jni-lib
ENV LD_LIBRARY_PATH ${LD_LIBRARY_PATH:+$LD_LIBRARY_PATH:}$TOMCAT_NATIVE_LIBDIR
WORKDIR  /opt
RUN wget http://mirror.nbtelecom.com.br/apache/tomcat/tomcat-8/v$TOMCAT_VERSION/bin/$TOMCAT_FILE
RUN tar xzf $TOMCAT_FILE
EXPOSE 8080
RUN ln -s /opt/apache-tomcat-$TOMCAT_VERSION /opt/tomcat
RUN ["rm", "-fr", "/opt/tomcat/webapps/ROOT"]
RUN yum -y update
RUN yum -y install apr-devel openssl-devel
CMD ["/opt/tomcat/bin/catalina.sh", "run"]


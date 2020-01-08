FROM parana/centos7-openjdk8
MAINTAINER João Paraná - joao.parana@gmail.com

ENV REFRESHED_AT 2016-07-15

ENV TOMCAT_VERSION 8.0.36
ENV ARCHIVE apache-tomcat-${TOMCAT_VERSION}
ENV INSTALL_DIR /usr/local
ENV SERVER_HOME ${INSTALL_DIR}/${ARCHIVE}
ENV TOMCAT_DOWNLOAD_URL https://archive.apache.org/dist/tomcat/tomcat-8/v${TOMCAT_VERSION}/bin/${ARCHIVE}.zip
# https://archive.apache.org/dist/tomcat/tomcat-8/v8.0.36/bin/apache-tomcat-8.0.36.zip
RUN mkdir -p ${INSTALL_DIR} ; curl -o ${SERVER_HOME}.zip -L ${TOMCAT_DOWNLOAD_URL}
RUN unzip ${SERVER_HOME}.zip -d ${INSTALL_DIR} && mv ${INSTALL_DIR}/${ARCHIVE} ${INSTALL_DIR}/tomcat && rm ${SERVER_HOME}.zip && ls -la ${INSTALL_DIR}
RUN chmod a+x ${INSTALL_DIR}/tomcat/bin/catalina.sh
ENV DEPLOYMENT_DIR ${SERVER_HOME}/webapps/
# ENTRYPOINT ${INSTALL_DIR}/tomcat/bin/catalina.sh run
EXPOSE 8080
CMD ["bash"]

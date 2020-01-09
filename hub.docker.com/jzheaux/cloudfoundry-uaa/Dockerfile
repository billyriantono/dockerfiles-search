FROM tomcat:9-jre8

ENV UAA_VERSION=4.19.0

RUN wget \
      http://central.maven.org/maven2/org/cloudfoundry/identity/cloudfoundry-identity-uaa/$UAA_VERSION/cloudfoundry-identity-uaa-$UAA_VERSION.war \
      -O $CATALINA_HOME/webapps/uaa.war

EXPOSE 8080

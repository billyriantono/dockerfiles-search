FROM jboss/keycloak:2.5.1.Final

ADD activate_ajp.xsl /opt/schlothauer/

RUN java -jar /usr/share/java/saxon.jar -s:/opt/jboss/keycloak/standalone/configuration/standalone.xml -xsl:/opt/schlothauer/activate_ajp.xsl -o:/opt/jboss/keycloak/standalone/configuration/standalone.xml

EXPOSE 8009

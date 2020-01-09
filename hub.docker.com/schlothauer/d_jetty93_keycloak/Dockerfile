FROM jetty:9.4-jre8-alpine

ADD keycloak-jetty94-adapter-dist-3.2.1.Final/lib/keycloak /usr/local/jetty/lib/keycloak/
ADD keycloak-jetty94-adapter-dist-3.2.1.Final/modules/keycloak.mod /usr/local/jetty/modules/

RUN cd /var/lib/jetty && java -jar $JETTY_HOME/start.jar --add-to-start=keycloak,http,http-forwarded,https,ssl
    
EXPOSE 8080
EXPOSE 8443

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["java","-jar","/usr/local/jetty/start.jar"]


FROM limetri/wildfly

WORKDIR /opt/wildfly/standalone/deployments/
ADD client-web/target/ygg.war /opt/wildfly/standalone/deployments/
#RUN mkdir ygg.war

RUN mv ygg.war ygg.war.tmp && unzip -d $JBOSS_HOME/standalone/deployments/ygg.war ygg.war.tmp && touch ygg.war.dodeploy && rm ygg.war.tmp

WORKDIR /opt/wildfly
# custom start script
ADD start-wildfly.sh /opt/wildfly/
# keycloak.json template
ADD keycloak.json.template /opt/wildfly/


# for testing switch to bash
#ENTRYPOINT ["/bin/sh","-c"]
#CMD ["bash"]

ENTRYPOINT ["/opt/wildfly/start-wildfly.sh"]
CMD ["-b", "0.0.0.0","-Djboss.socket.binding.port-offset=$PORT_OFFSET"]


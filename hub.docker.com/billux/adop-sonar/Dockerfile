FROM sonarqube:latest

ENV SONARQUBE_PLUGINS_DIR=/opt/sonarqube/default/extensions/plugins \
    SONARQUBE_SERVER_BASE="http://localhost:9000" \
    SONARQUBE_WEB_CONTEXT="/sonar" \
    SONARQUBE_FORCE_AUTHENTICATION=false \
    ADOP_LDAP_ENABLED=true \
    SONARQUBE_JMX_ENABLED=false 

COPY resources/plugins.txt ${SONARQUBE_PLUGINS_DIR}/
COPY resources/sonar.sh resources/plugins.sh /usr/local/bin/

RUN rm -f ${SONARQUBE_PLUGINS_DIR}/*.jar 

USER root
RUN chmod +x /usr/local/bin/sonar.sh 
RUN chmod +x /usr/local/bin/plugins.sh 

RUN /usr/local/bin/plugins.sh ${SONARQUBE_PLUGINS_DIR}/plugins.txt

RUN chown -R sonarqube:sonarqube /opt/sonarqube/

VOLUME ["/opt/sonarqube/logs/"]

USER sonarqube
ENTRYPOINT ["/usr/local/bin/sonar.sh"]

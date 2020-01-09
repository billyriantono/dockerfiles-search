FROM sonarqube:6.7.5
MAINTAINER Angel Soliño "angel@nuvolar.eu"

# create plugin download location; so we can copy them later when SonarQube is started
ENV PLUGIN_DOWNLOAD_LOCATION /opt/plugins-download
RUN mkdir -p $PLUGIN_DOWNLOAD_LOCATION
WORKDIR ${PLUGIN_DOWNLOAD_LOCATION}

# download plugins from:
# - http://downloads.sonarsource.com/plugins/org/codehaus/sonar-plugins/
# - https://sonarsource.bintray.com/Distribution/
# - https://github.com/SonarQubeCommunity/
#RUN wget https://sonarsource.bintray.com/Distribution/sonar-java-plugin/sonar-java-plugin-4.0.jar
RUN wget https://github.com/SonarSource/sonar-auth-bitbucket/releases/download/1.0/sonar-auth-bitbucket-plugin-1.0.jar
#RUN wget https://github.com/spotbugs/sonar-findbugs/releases/download/3.7.0/sonar-findbugs-plugin-3.7.0.jar
#RUN wget https://github.com/SonarQubeCommunity/sonar-pmd/releases/download/2.6/sonar-pmd-plugin-2.6.jar
#RUN wget https://github.com/checkstyle/sonar-checkstyle/releases/download/4.11/checkstyle-sonar-plugin-4.11.jar
RUN wget https://dl.bintray.com/fundacionjala/enforce/apex-plugin-1.0b219.jar

COPY docker-entrypoint.sh /opt/docker-entrypoint.sh
RUN chmod +x /opt/docker-entrypoint.sh

WORKDIR ${SONARQUBE_HOME}
ENTRYPOINT ["/opt/docker-entrypoint.sh"]
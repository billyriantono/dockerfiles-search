#See https://github.com/mwz/sonar-scala
FROM sonarqube:7.6-community

#note both the sonar-scala-plugin and sonar-scala_2.12-7.4.0-assembly calls themselves the scala plugin but the former cannot process scoverage
RUN rm ${SONARQUBE_HOME}/extensions/plugins/sonar-scala-plugin-*.jar \
    && wget https://dl.bintray.com/mwz/maven/com/github/mwz/sonar-scala_2.12/7.4.0/sonar-scala_2.12-7.4.0-assembly.jar -P ${SONARQUBE_HOME}/extensions/plugins

WORKDIR $SONARQUBE_HOME
USER sonarqube
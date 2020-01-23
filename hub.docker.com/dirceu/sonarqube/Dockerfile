FROM sonarqube:6.2-alpine

ENV BUILD_BREAKER_PLUGIN_VERSION=1.1
ENV AUTH_GITHUB_PLUGIN_VERSION=1.3
ENV JAVA_PLUGIN_VERSION=4.4.0.8066
ENV JPROPERTIES_PLUGIN_VERSION=2.4
ENV PHP_PLUGIN_VERSION=2.9.2.1744

RUN cd /opt/sonarqube/extensions/plugins && \
	curl -sLo sonar-build-breaker-plugin-${BUILD_BREAKER_PLUGIN_VERSION}.jar \
    http://downloads.sonarsource.com/plugins/org/codehaus/sonar-plugins/sonar-build-breaker-plugin/${BUILD_BREAKER_PLUGIN_VERSION}/sonar-build-breaker-plugin-${BUILD_BREAKER_PLUGIN_VERSION}.jar

RUN cd /opt/sonarqube/extensions/plugins && \
    curl -sLo sonar-auth-github-plugin-${AUTH_GITHUB_PLUGIN_VERSION}.jar \
    https://sonarsource.bintray.com/Distribution/sonar-auth-github-plugin/sonar-auth-github-plugin-${AUTH_GITHUB_PLUGIN_VERSION}.jar

RUN cd /opt/sonarqube/extensions/plugins && \
    curl -sLo sonar-java-plugin-${JAVA_PLUGIN_VERSION}.jar \
    https://sonarsource.bintray.com/Distribution/sonar-java-plugin/sonar-java-plugin-${JAVA_PLUGIN_VERSION}.jar

RUN cd /opt/sonarqube/extensions/plugins && \
    curl -sLo sonar-jproperties-plugin-${JPROPERTIES_PLUGIN_VERSION}.jar \
    https://github.com/racodond/sonar-jproperties-plugin/releases/download/${JPROPERTIES_PLUGIN_VERSION}/sonar-jproperties-plugin-${JPROPERTIES_PLUGIN_VERSION}.jar

RUN cd /opt/sonarqube/extensions/plugins && \
    curl -sLo sonar-php-plugin-${PHP_PLUGIN_VERSION}.jar \
    https://sonarsource.bintray.com/Distribution/sonar-php-plugin/sonar-php-plugin-${PHP_PLUGIN_VERSION}.jar


FROM sonarqube:5.1

#################################
# Install Cobertura Plugin
#################################
ENV COBERTURA_VERSION 1.6.3
RUN set -x \
	&& cd /opt \
	&& curl -o sonar-cobertura-plugin-$COBERTURA_VERSION.jar -fSL http://downloads.sonarsource.com/plugins/org/codehaus/sonar-plugins/sonar-cobertura-plugin/$COBERTURA_VERSION/sonar-cobertura-plugin-$COBERTURA_VERSION.jar \
	&& mv sonar-cobertura-plugin-$COBERTURA_VERSION.jar $SONARQUBE_HOME/extensions/plugins 
#################################
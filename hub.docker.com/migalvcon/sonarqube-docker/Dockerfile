FROM sonarqube:lts

MAINTAINER Miguel Angel Alvarez (migalvcon@gmail.com)

# Add some plugins
RUN cd /opt/sonarqube/extensions/plugins && \
	curl -LO https://github.com/checkstyle/sonar-checkstyle/releases/download/4.17/checkstyle-sonar-plugin-4.17.jar && \
	curl -LO https://github.com/galexandre/sonar-cobertura/releases/download/2.0/sonar-cobertura-plugin-2.0.jar && \
	curl -LO https://github.com/QualInsight/qualinsight-plugins-sonarqube-smell/releases/download/qualinsight-plugins-sonarqube-smell-4.0.0/qualinsight-sonarqube-smell-plugin-4.0.0.jar && \
	curl -LO https://github.com/spotbugs/sonar-findbugs/releases/download/3.9.2/sonar-findbugs-plugin-3.9.2.jar && \
	curl -LO https://binaries.sonarsource.com/Distribution/sonar-jacoco-plugin/sonar-jacoco-plugin-1.0.1.143.jar && \
	curl -LO https://github.com/jensgerdes/sonar-pmd/releases/download/3.1.3/sonar-pmd-plugin-3.1.3.jar && \
	curl -LO https://github.com/racodond/sonar-css-plugin/releases/download/4.18/sonar-css-plugin-4.18.jar && \
	curl -LO https://github.com/SonarSource/SonarJS/releases/download/5.0.0.6962/sonar-javascript-plugin-5.0.0.6962.jar && \
	curl -LO https://binaries.sonarsource.com/Distribution/sonar-java-plugin/sonar-java-plugin-5.11.0.17289.jar && \
	curl -LO https://binaries.sonarsource.com/Distribution/sonar-scala-plugin/sonar-scala-plugin-1.4.0.155.jar && \
	curl -LO https://github.com/SonarSource/SonarTS/releases/download/v1.9.0/sonar-typescript-plugin-1.9.0.3766.jar && \
	curl -LO https://binaries.sonarsource.com/Distribution/sonar-xml-plugin/sonar-xml-plugin-2.0.1.2020.jar
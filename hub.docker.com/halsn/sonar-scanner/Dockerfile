FROM openjdk:8-jre-alpine

ENV SONAR_SCANNER_VERSION 2.7

ADD "https://sonarsource.bintray.com/Distribution/sonar-scanner-cli/sonar-scanner-${SONAR_SCANNER_VERSION}.zip" /

RUN unzip "sonar-scanner-${SONAR_SCANNER_VERSION}.zip"

RUN mkdir -p /data
WORKDIR /data

ENV PATH "/sonar-scanner-${SONAR_SCANNER_VERSION}/bin:${PATH}"

# CMD sonar-scanner -Dsonar.host.url=$SONAR_HOST -Dsonar.projectKey=$PROJECT_KEY -Dsonar.projectName=$PROJECT_NAME -Dsonar.projectVersion=$PROJECT_VERSION -Dsonar.sources=$SOURCES -Dsonar.javascript.lcov.reportPaths=$REPORT_PATH
CMD sonar-scanner

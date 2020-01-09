FROM iloveflamingo/buildenv:1.10

RUN apt update && apt install unzip

# install sonarQube client - WONT WORK WITH ALPINE! - this is using a embedded jre!
ADD https://sonarsource.bintray.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-3.2.0.1227-linux.zip /sonar-scanner-cli-3.2.0.1227-linux.zip
RUN cd / && unzip sonar-scanner-cli-3.2.0.1227-linux.zip && mv /sonar-scanner-3.2.0.1227-linux/ /sonar/ && rm sonar-scanner-cli-3.2.0.1227-linux.zip
ENV SONAR_SCANNER_HOME=/sonar

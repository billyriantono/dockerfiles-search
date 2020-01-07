FROM openjdk:8-jre-alpine
MAINTAINER prieux@sierrawireless.com

ADD run.sh /usr/local/bin/run

ENV SONARQUBE_VERSION=5.6.6 \
    SONARQUBE_HOME=/opt/sonarqube

# Install.
RUN \
    set -x && \
    apk add --no-cache gnupg unzip wget && \
    # sonarqube
    gpg --keyserver ha.pool.sks-keyservers.net --recv-keys F1182E81C792928921DBCAB4CFCA4A29D26468DE && \
    mkdir /opt && \
    cd /opt && \
    wget -q -O sonarqube.zip https://sonarsource.bintray.com/Distribution/sonarqube/sonarqube-$SONARQUBE_VERSION.zip && \
    wget -q -O sonarqube.zip.asc https://sonarsource.bintray.com/Distribution/sonarqube/sonarqube-$SONARQUBE_VERSION.zip.asc && \
    gpg --batch --verify sonarqube.zip.asc sonarqube.zip && \
    unzip -q sonarqube.zip && \
    mv sonarqube-$SONARQUBE_VERSION sonarqube && \
    rm sonarqube.zip* && \
    rm -rf $SONARQUBE_HOME/bin/* && \
    cd $SONARQUBE_HOME/extensions/plugins/ && \
    wget -q -O sonar-java-plugin.jar https://github.com/SonarSource/sonar-java/releases/download/4.15-RC1/sonar-java-plugin-4.15.0.12310.jar && \
    wget -q -O sonar-javascript-plugin.jar https://github.com/SonarSource/SonarJS/releases/download/3.2.0.5506/sonar-javascript-plugin-3.2.0.5506.jar && \
    wget -q -O sonar-css-plugin.jar https://github.com/racodond/sonar-css-plugin/releases/download/4.7/sonar-css-plugin-4.7.jar && \
    wget -q -O sonar-findbugs-plugin.jar https://github.com/SonarQubeCommunity/sonar-findbugs/releases/download/3.6.0/sonar-findbugs-plugin-3.6.0.jar && \
    wget -q -O checkstyle-sonar-plugin.jar https://github.com/checkstyle/sonar-checkstyle/releases/download/3.7/checkstyle-sonar-plugin-3.7.jar && \
    wget -q -O sonar-jproperties-plugin.jar https://github.com/racodond/sonar-jproperties-plugin/releases/download/2.5/sonar-jproperties-plugin-2.5.jar && \
    wget -q -O sonar-scm-git-plugin.jar https://sonarsource.bintray.com/Distribution/sonar-scm-git-plugin/sonar-scm-git-plugin-1.2.jar && \
    wget -q -O sonar-github-plugin.jar https://sonarsource.bintray.com/Distribution/sonar-github-plugin/sonar-github-plugin-1.4.2.1027.jar && \
    wget -q -O sonar-auth-github-plugin.jar https://sonarsource.bintray.com/Distribution/sonar-auth-github-plugin/sonar-auth-github-plugin-1.3.jar && \
    addgroup -S sonarqube && \
    adduser -S -g sonarqube sonarqube && \
    chmod +x /usr/local/bin/run && \
    mkdir -p $SONARQUBE_HOME/extconf/ && \
    chown sonarqube.sonarqube /usr/local/bin/run && \
    chown -R sonarqube.sonarqube $SONARQUBE_HOME/
#

ADD sonar_conf/sonar.properties $SONARQUBE_HOME/conf/sonar.properties

USER sonarqube

EXPOSE 9000

ENTRYPOINT ["/usr/local/bin/run"]

FROM sonarqube:7.1-alpine

MAINTAINER Chris Misson

RUN apk add --no-cache curl

RUN mkdir -p $HOME/plugins

ENV GITLAB_PLUGIN_VERSION 3.0.2
RUN set -x && curl -sLo $HOME/plugins/sonar-gitlab-plugin-${GITLAB_PLUGIN_VERSION}.jar \
	https://github.com/gabrie-allaigre/sonar-gitlab-plugin/releases/download/${GITLAB_PLUGIN_VERSION}/sonar-gitlab-plugin-${GITLAB_PLUGIN_VERSION}.jar

ENV SLACK_PLUGIN_VERSION 2.1.2
RUN set -x && curl -sLo $HOME/plugins/cks-slack-notifier-${SLACK_PLUGIN_VERSION}.jar \
	https://github.com/kogitant/sonar-slack-notifier-plugin/releases/download/${SLACK_PLUGIN_VERSION}/cks-slack-notifier-${SLACK_PLUGIN_VERSION}.jar

ENV SWIFT_PLUGIN_VERSION 0.4.2
RUN set -x && curl -sLo $HOME/plugins/backelite-sonar-swift-plugin-${SWIFT_PLUGIN_VERSION}.jar \
	https://github.com/Backelite/sonar-swift/releases/download/${SWIFT_PLUGIN_VERSION}/backelite-sonar-swift-plugin-${SWIFT_PLUGIN_VERSION}.jar

ENV ANDROID_LINT_PLUGIN_VERSION 1.1
RUN set -x && curl -sLo $HOME/plugins/sonar-android-plugin-${ANDROID_LINT_PLUGIN_VERSION}.jar \
	https://github.com/SonarQubeCommunity/sonar-android/releases/download/${ANDROID_LINT_PLUGIN_VERSION}/sonar-android-plugin-${ANDROID_LINT_PLUGIN_VERSION}.jar

ENV JAVA_PLUGIN_VERSION 5.9.2.16552
RUN set -x && curl -sLo $HOME/plugins/sonar-java-plugin-${JAVA_PLUGIN_VERSION}.jar \
	https://binaries.sonarsource.com/Distribution/sonar-java-plugin/sonar-java-plugin-${JAVA_PLUGIN_VERSION}.jar

ENV KOTLIN_PLUGIN_VERSION 0.5.2
RUN set -x && curl -sLo $HOME/plugins/sonar-kotlin-plugin-${KOTLIN_PLUGIN_VERSION}.jar \
	https://github.com/arturbosch/sonar-kotlin/releases/download/${KOTLIN_PLUGIN_VERSION}/sonar-kotlin-${KOTLIN_PLUGIN_VERSION}.jar

ENV SONAR_BRANCH_COMMUNITY 2.0.0
RUN set -x && curl -sLo $HOME/plugins/sonar-branch-community-${SONAR_BRANCH_COMMUNITY}.jar \
    https://raw.githubusercontent.com/wz2cool/java-resource/master/jar/sonar-branch-community/2.0/sonar-branch-plugin-2.0.0.jar

ENV SONAR_CHECK_DEPENDENCY 1.1.3
RUN set -x && curl -sLo $HOME/plugins/sonar-dependency-check-${SONAR_CHECK_DEPENDENCY}.jar \
    https://github.com/stevespringett/dependency-check-sonar-plugin/releases/download/1.1.3/sonar-dependency-check-plugin-1.1.3.jar

RUN cp $HOME/plugins/* $SONARQUBE_HOME/extensions/plugins

COPY entrypoint.sh ./bin/

RUN chmod +x ./bin/entrypoint.sh

ENTRYPOINT ["./bin/entrypoint.sh"]



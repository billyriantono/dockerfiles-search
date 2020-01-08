FROM swun9/docker-ubuntu-java:latest
MAINTAINER swun9 "swung.cn@gmail.com"
ENV REFRESHED_AT 2015-01-11

ENV JENKINS_HOME /opt/jenkins/home
ENV JENKINS_MIRROR http://mirrors.jenkins-ci.org

RUN mkdir -p $JENKINS_HOME/plugins
RUN curl -sf -o /opt/jenkins/jenkins.war -L $JENKINS_MIRROR/war-stable/latest/jenkins.war

RUN \
  for plugin in \
    analysis-core \
    artifactdeployer \
    build-pipeline-plugin \
    build-name-setter \
    checkstyle \
    copyartifact \
    delivery-pipeline-plugin \
    description-setter \
    dependency-check-jenkins-plugin \
    dry \
    email-ext \
    envinject \
    external-monitor-job \
    findbugs \
    gerrit-trigger \
    greenballs \
    git-client \
    git \
    hipchat \
    htmlpublisher \
    jacoco \
    jquery \
    jquery-ui\
    log-parser \
    next-executions \
    parameterized-trigger \
    pmd \
    promoted-builds \
    publish-over-ssh \
    sidebar-link \
    sloccount \
    ssh-agent \
    tasks \
    thinBackup \
    token-macro \
    warnings \
    scm-api \
    swarm \
    ws-cleanup ; \
  do curl -sf -o $JENKINS_HOME/plugins/${plugin}.hpi \
    -L $JENKINS_MIRROR/plugins/${plugin}/latest/${plugin}.hpi ; \
  done

EXPOSE 8088

ENTRYPOINT ["java", "-jar", "/opt/jenkins/jenkins.war", "--httpPort=8088"]

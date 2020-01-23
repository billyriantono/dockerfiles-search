FROM jenkins/jenkins:2.73.2-alpine

ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false

USER root
# install docker-ce

RUN apk update 
RUN apk add docker

#/var/run/docker.sock:/var/run/docker.sock:ro
RUN apk add tzdata &&  cp /usr/share/zoneinfo/Europe/Berlin /etc/localtime\ && echo "Europe/Berlin" >  /etc/timezone
  
USER jenkins

RUN /usr/local/bin/install-plugins.sh windows-slaves: 1.3.1 &&
    /usr/local/bin/install-plugins.sh bouncycastle-api: 2.16.2 &&
    /usr/local/bin/install-plugins.sh docker-commons: 1.9 &&
    /usr/local/bin/install-plugins.sh structs: 1.10 &&
    /usr/local/bin/install-plugins.sh docker-workflow: 1.13 &&
    /usr/local/bin/install-plugins.sh junit: 1.21 &&
    /usr/local/bin/install-plugins.sh antisamy-markup-formatter: 1.5 &&
    /usr/local/bin/install-plugins.sh display-url-api: 2.1.0 &&
    /usr/local/bin/install-plugins.sh workflow-step-api: 2.13 &&
    /usr/local/bin/install-plugins.sh scm-api: 2.2.3 &&
    /usr/local/bin/install-plugins.sh script-security: 1.34 &&
    /usr/local/bin/install-plugins.sh workflow-api: 2.23.1 &&
    /usr/local/bin/install-plugins.sh mailer: 1.20 &&
    /usr/local/bin/install-plugins.sh workflow-support: 2.16 &&
    /usr/local/bin/install-plugins.sh workflow-job: 2.12.2 &&
    /usr/local/bin/install-plugins.sh token-macro: 2.3 &&
    /usr/local/bin/install-plugins.sh build-timeout: 1.19 &&
    /usr/local/bin/install-plugins.sh credentials: 2.1.16 &&
    /usr/local/bin/install-plugins.sh matrix-auth: 2.1 &&
    /usr/local/bin/install-plugins.sh ssh-credentials: 1.13 &&
    /usr/local/bin/install-plugins.sh pam-auth: 1.3 &&
    /usr/local/bin/install-plugins.sh plain-credentials: 1.4 &&
    /usr/local/bin/install-plugins.sh jsch: 0.1.54.1 &&
    /usr/local/bin/install-plugins.sh credentials-binding: 1.13 &&
    /usr/local/bin/install-plugins.sh github-api: 1.89 &&
    /usr/local/bin/install-plugins.sh timestamper: 1.8.8 &&
    /usr/local/bin/install-plugins.sh durable-task: 1.15 &&
    /usr/local/bin/install-plugins.sh pipeline-rest-api: 2.9 &&
    /usr/local/bin/install-plugins.sh workflow-durable-task-step: 2.17 &&
    /usr/local/bin/install-plugins.sh matrix-project: 1.12 &&
    /usr/local/bin/install-plugins.sh git-client: 2.6.0 &&
    /usr/local/bin/install-plugins.sh resource-disposer: 0.8 &&
    /usr/local/bin/install-plugins.sh git: 3.6.3 &&
    /usr/local/bin/install-plugins.sh ws-cleanup: 0.34 &&
    /usr/local/bin/install-plugins.sh ant: 1.7 &&
    /usr/local/bin/install-plugins.sh gradle: 1.28 &&
    /usr/local/bin/install-plugins.sh pipeline-milestone-step: 1.3.1 &&
    /usr/local/bin/install-plugins.sh jquery-detached: 1.2.1 &&
    /usr/local/bin/install-plugins.sh github: 1.28.1 &&
    /usr/local/bin/install-plugins.sh jackson2-api: 2.8.7.0 &&
    /usr/local/bin/install-plugins.sh ace-editor: 1.1 &&
    /usr/local/bin/install-plugins.sh git-server: 1.7 &&
    /usr/local/bin/install-plugins.sh workflow-scm-step: 2.6 &&
    /usr/local/bin/install-plugins.sh workflow-cps: 2.41 &&
    /usr/local/bin/install-plugins.sh workflow-cps-global-lib: 2.9 &&
    /usr/local/bin/install-plugins.sh pipeline-input-step: 2.8 &&
    /usr/local/bin/install-plugins.sh pipeline-stage-step: 2.2 &&
    /usr/local/bin/install-plugins.sh pipeline-graph-analysis: 1.5 &&
    /usr/local/bin/install-plugins.sh handlebars: 1.1.1 &&
    /usr/local/bin/install-plugins.sh momentjs: 1.1.1 &&
    /usr/local/bin/install-plugins.sh pipeline-stage-view: 2.9 &&
    /usr/local/bin/install-plugins.sh branch-api: 2.0.15 &&
    /usr/local/bin/install-plugins.sh pipeline-build-step: 2.5.1 &&
    /usr/local/bin/install-plugins.sh pipeline-model-api: 1.2.2 &&
    /usr/local/bin/install-plugins.sh pipeline-model-extensions: 1.2.2 &&
    /usr/local/bin/install-plugins.sh apache-httpcomponents-client-4-api: 4.5.3-2.0 &&
    /usr/local/bin/install-plugins.sh workflow-multibranch: 2.16 &&
    /usr/local/bin/install-plugins.sh authentication-tokens: 1.3 &&
    /usr/local/bin/install-plugins.sh pipeline-stage-tags-metadata: 1.2.2 &&
    /usr/local/bin/install-plugins.sh pipeline-model-declarative-agent: 1.1.1 &&
    /usr/local/bin/install-plugins.sh workflow-basic-steps: 2.6 &&
    /usr/local/bin/install-plugins.sh pipeline-model-definition: 1.2.2 &&
    /usr/local/bin/install-plugins.sh workflow-aggregator: 2.5 &&
    /usr/local/bin/install-plugins.sh github-branch-source: 2.2.4 &&
    /usr/local/bin/install-plugins.sh pipeline-github-lib: 1.0 &&
    /usr/local/bin/install-plugins.sh mapdb-api: 1.0.9.0 &&
    /usr/local/bin/install-plugins.sh docker-java-api: 3.0.14 &&
    /usr/local/bin/install-plugins.sh subversion: 2.9 &&
    /usr/local/bin/install-plugins.sh docker-plugin: 1.0.4 &&
    /usr/local/bin/install-plugins.sh ssh-slaves: 1.22 &&
    /usr/local/bin/install-plugins.sh ldap: 1.17 &&
    /usr/local/bin/install-plugins.sh email-ext: 2.61 &&
    /usr/local/bin/install-plugins.sh gerrit-trigger: 2.26.1 &&
    /usr/local/bin/install-plugins.sh javadoc: 1.4 &&
    /usr/local/bin/install-plugins.sh maven-plugin: 3.0 &&
    /usr/local/bin/install-plugins.sh blueocean-commons: 1.3.1 &&
    /usr/local/bin/install-plugins.sh active-directory: 2.6 &&
    /usr/local/bin/install-plugins.sh blueocean-rest: 1.3.1 &&
    /usr/local/bin/install-plugins.sh pubsub-light: 1.12 &&
    /usr/local/bin/install-plugins.sh blueocean-pipeline-scm-api: 1.3.1 &&
    /usr/local/bin/install-plugins.sh htmlpublisher: 1.14 &&
    /usr/local/bin/install-plugins.sh variant: 1.1 &&
    /usr/local/bin/install-plugins.sh role-strategy: 2.6.1 &&
    /usr/local/bin/install-plugins.sh blueocean-web: 1.3.1 &&
    /usr/local/bin/install-plugins.sh blueocean-jwt: 1.3.1 &&
    /usr/local/bin/install-plugins.sh favorite: 2.3.1 &&
    /usr/local/bin/install-plugins.sh config-file-provider: 2.16.4 &&
    /usr/local/bin/install-plugins.sh blueocean-rest-impl: 1.3.1 &&
    /usr/local/bin/install-plugins.sh blueocean-pipeline-api-impl: 1.3.1 &&
    /usr/local/bin/install-plugins.sh blueocean-github-pipeline: 1.3.1 &&
    /usr/local/bin/install-plugins.sh blueocean-git-pipeline: 1.3.1 &&
    /usr/local/bin/install-plugins.sh blueocean-config: 1.3.1 &&
    /usr/local/bin/install-plugins.sh mercurial: 2.2 &&
    /usr/local/bin/install-plugins.sh cloudbees-bitbucket-branch-source: 2.2.4 &&
    /usr/local/bin/install-plugins.sh blueocean-bitbucket-pipeline: 1.3.1 &&
    /usr/local/bin/install-plugins.sh blueocean-personalization: 1.3.1 &&
    /usr/local/bin/install-plugins.sh jira: 2.4.2 &&
    /usr/local/bin/install-plugins.sh pipeline-maven: 3.0.2 &&
    /usr/local/bin/install-plugins.sh blueocean-jira: 1.3.1 &&
    /usr/local/bin/install-plugins.sh blueocean-display-url: 2.1.1 &&
    /usr/local/bin/install-plugins.sh sse-gateway: 1.15 &&
    /usr/local/bin/install-plugins.sh blueocean-events: 1.3.1 &&
    /usr/local/bin/install-plugins.sh blueocean-pipeline-editor: 1.3.1 &&
    /usr/local/bin/install-plugins.sh nexus-jenkins-plugin: 1.4.20170929-233916.04479e6 &&
    /usr/local/bin/install-plugins.sh blueocean-i18n: 1.3.1 &&
    /usr/local/bin/install-plugins.sh blueocean-autofavorite: 1.0.0 &&
    /usr/local/bin/install-plugins.sh blueocean-dashboard: 1.3.1 &&
    /usr/local/bin/install-plugins.sh blueocean: 1.3.1
        
WORKDIR $JENKINS_HOME
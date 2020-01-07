FROM jenkins/jenkins:2.195-alpine

RUN /usr/local/bin/install-plugins.sh \
    ant:1.10 \
    antisamy-markup-formatter:1.6 \
    authorize-project:1.3.0 \
    build-timeout:1.19 \
    cloudbees-folder:6.9 \
    configuration-as-code:1.30 \
    configuration-as-code-support:1.18 \
    credentials-binding:1.20 \
    email-ext:2.66 \
    git:3.12.1 \
    git-client:2.8.6 \
    github-branch-source:2.5.7 \
    gradle:1.34 \
    kubernetes:1.19.0 \
    kubernetes-cd:2.1.2 \
    ldap:1.20 \
    mailer:1.28 \
    matrix-auth:2.4.2 \
    pam-auth:1.5.1 \
    pipeline-github-lib:1.0 \
    pipeline-stage-view:2.12 \
    prometheus:2.0.6 \
    role-strategy:2.13 \
    script-security:1.64 \
    ssh-slaves:1.30.2 \
    timestamper:1.10 \
    workflow-aggregator:2.6 \
    ws-cleanup:0.37

RUN echo 2.0 > /usr/share/jenkins/ref/jenkins.install.UpgradeWizard.state

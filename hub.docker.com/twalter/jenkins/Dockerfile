FROM jenkins/jenkins:lts
RUN /usr/local/bin/install-plugins.sh \
    command-launcher:1.3 \
    configuration-as-code:1.30 \
    credentials-binding:1.20 \
    git:3.12.1 \
    jdk-tool:1.3 \
    kubernetes:1.18.3 \
    workflow-aggregator:2.6 \
    workflow-job:2.34

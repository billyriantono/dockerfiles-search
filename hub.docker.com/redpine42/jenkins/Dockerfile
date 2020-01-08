FROM jenkins

USER root
RUN apt-get update \
      && apt-get install -y sudo \
      && rm -rf /var/lib/apt/lists/*
RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers
 
USER jenkins

RUN /usr/local/bin/install-plugins.sh authentication-tokens icon-shim credentials ssh-credentials 
RUN /usr/local/bin/install-plugins.sh structs junit javadoc mailer script-security jackson2-api matrix-project ace-editor scm-api jquery-detached cloudbees-folder branch-api durable-task conditional-buildstep parameterized-trigger git-server pipeline-rest-api handlebars momentjs 
RUN /usr/local/bin/install-plugins.sh maven-plugin aws-java-sdk copyartifact
RUN /usr/local/bin/install-plugins.sh parameterized-trigger jquery
RUN /usr/local/bin/install-plugins.sh workflow-support workflow-cps pipeline-stage-step pipeline-stage-view workflow-cps-global-lib pipeline-input-step workflow-basic-steps workflow-multibranch workflow-scm-step workflow-job workflow-durable-task-step workflow-step-api:2.2 pipeline-build-step workflow-api
RUN /usr/local/bin/install-plugins.sh token-macro

RUN /usr/local/bin/install-plugins.sh build-pipeline-plugin:1.5.3.1 docker-build-publish:1.3.1 discard-old-build:1.05 workflow-aggregator:2.2 s3:0.10.6

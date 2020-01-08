FROM jenkins
MAINTAINER Stephan Stachurski "ses1984@gmail.com"

USER root

ADD https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64 /usr/bin/jq
RUN chmod +x /usr/bin/jq

RUN mkdir -p /usr/share/jenkins/ref/plugins/

# git
ADD http://updates.jenkins-ci.org/latest/git.hpi /usr/share/jenkins/ref/plugins/

# workflow
ADD http://mirrors.jenkins-ci.org/plugins/workflow-aggregator/latest/workflow-aggregator.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/workflow-api/latest/workflow-api.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/workflow-basic-steps/latest/workflow-basic-steps.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/workflow-cps-global-lib/latest/workflow-cps-global-lib.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/workflow-cps/latest/workflow-cps.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/workflow-durable-task-step/latest/workflow-durable-task-step.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/workflow-job/latest/workflow-job.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/workflow-multibranch/latest/workflow-multibranch.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/workflow-scm-step/latest/workflow-scm-step.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/workflow-step-api/latest/workflow-step-api.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/workflow-stm/latest/workflow-stm.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/workflow-support/latest/workflow-support.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/workflow-remote-loader/latest/workflow-remote-loader.hpi /usr/share/jenkins/ref/plugins/

# mesos
ADD http://mirrors.jenkins-ci.org/plugins/mesos/latest/mesos.hpi /usr/share/jenkins/ref/plugins/

# docker
ADD http://mirrors.jenkins-ci.org/plugins/docker-plugin/latest/docker-plugin.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/docker-build-publish/latest/docker-build-publish.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/docker-commons/latest/docker-commons.hpi /usr/share/jenkins/ref/plugins/

# dependencies
ADD http://mirrors.jenkins-ci.org/plugins/token-macro/latest/token-macro.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/ssh-slaves/latest/ssh-slaves.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/credentials/latest/credentials.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/icon-shim/latest/icon-shim.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/durable-task/latest/durable-task.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/authentication-tokens/latest/authentication-tokens.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/ace-editor/latest/ace-editor.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/branch-api/latest/branch-api.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/cloudbees-folder/latest/cloudbees-folder.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/git/latest/git.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/git-client/latest/git-client.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/git-server/latest/git-server.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/jquery-detached/latest/jquery-detached.hpi /usr/share/jenkins/ref/plugins/
ADD http://mirrors.jenkins-ci.org/plugins/scm-api/latest/scm-api.hpi /usr/share/jenkins/ref/plugins/
ADD http://updates.jenkins-ci.org/latest/ssh-credentials.hpi /usr/share/jenkins/ref/plugins/
ADD http://updates.jenkins-ci.org/latest/mailer.hpi /usr/share/jenkins/ref/plugins/
ADD http://updates.jenkins-ci.org/latest/promoted-builds.hpi /usr/share/jenkins/ref/plugins/
ADD http://updates.jenkins-ci.org/latest/rebuild.hpi /usr/share/jenkins/ref/plugins/
ADD http://updates.jenkins-ci.org/latest/project-inheritance.hpi /usr/share/jenkins/ref/plugins/
ADD http://updates.jenkins-ci.org/latest/maven-plugin.hpi /usr/share/jenkins/ref/plugins/
ADD http://updates.jenkins-ci.org/latest/javadoc.hpi /usr/share/jenkins/ref/plugins/
ADD http://updates.jenkins-ci.org/latest/junit.hpi /usr/share/jenkins/ref/plugins/
ADD http://updates.jenkins-ci.org/latest/matrix-project.hpi /usr/share/jenkins/ref/plugins/
ADD http://updates.jenkins-ci.org/latest/script-security.hpi /usr/share/jenkins/ref/plugins/
ADD http://updates.jenkins-ci.org/latest/conditional-buildstep.hpi /usr/share/jenkins/ref/plugins/
ADD http://updates.jenkins-ci.org/latest/parameterized-trigger.hpi /usr/share/jenkins/ref/plugins/

RUN chown -R jenkins:jenkins /usr/share/jenkins/ref/plugins/
RUN chmod -R 777 /usr/share/jenkins/ref/plugins/
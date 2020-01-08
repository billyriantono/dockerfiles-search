FROM jenkins/jenkins:lts

RUN /usr/local/bin/install-plugins.sh git && /usr/local/bin/install-plugins.sh workflow-multibranch && /usr/local/bin/install-plugins.sh cloudbees-folder && /usr/local/bin/install-plugins.sh aws-codebuild && /usr/local/bin/install-plugins.sh bitbucket

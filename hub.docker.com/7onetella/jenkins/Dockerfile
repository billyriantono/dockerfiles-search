FROM shimmi/jenkins:latest

USER root

RUN apt-get update && apt-get install -y \
    python python-pip python3 python3-pip
    
RUN pip install awscli --upgrade --user

USER jenkins

# Base image install the following
# RUN install-plugins.sh \
#     blueocean \
#     docker-workflow \
#     locale \
#     workflow-aggregator \
#     pipeline-stage-view \
#     git \
#     cloudbees-bitbucket-branch-source \
#     github-organization-folder

RUN install-plugins.sh \
    parameterized-trigger
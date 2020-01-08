FROM jenkins/jenkins:lts

USER root

# RUN apt-get update \
#       && apt-get install -y sudo \
#       && rm -rf /var/lib/apt/lists/*
# RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers

RUN groupadd docker && usermod -aG docker jenkins

EXPOSE 8080
EXPOSE 50000

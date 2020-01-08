FROM jenkinsci/blueocean

USER root

RUN apk add --no-cache shadow && \
  groupmod -g 993 docker && \
  usermod -aG docker jenkins

USER jenkins

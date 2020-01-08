FROM jenkins:2.32.2-alpine
# -- add sudo package
USER root
RUN apk add --no-cache sudo docker && \
    delgroup docker && \
    addgroup -g 1101 docker && \
    adduser jenkins docker && \
    echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers
# -- back to jenkins user
USER jenkins

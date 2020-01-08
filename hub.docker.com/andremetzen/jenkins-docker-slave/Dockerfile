FROM jenkinsci/jnlp-slave

USER root

COPY get-docker.sh .
COPY plugins.txt /tmp/plugins.txt

RUN ./get-docker.sh \
    && curl -L https://github.com/docker/compose/releases/download/1.16.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

RUN apt-get update && apt-get install awscli -y

#RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers




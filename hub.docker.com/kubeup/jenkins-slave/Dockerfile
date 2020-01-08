FROM jenkinsci/jnlp-slave:2.62
COPY jenkins-slave /usr/local/bin/jenkins-slave
USER root
RUN curl -O https://get.docker.com/builds/Linux/x86_64/docker-1.11.2.tgz && tar zxf docker-1.11.2.tgz && mv docker/docker /usr/bin/docker && rm -rf docker && rm -rf docker-1.11.2.tgz
RUN curl -O https://storage.googleapis.com/kubernetes-release/release/v1.6.1/bin/linux/amd64/kubectl && chmod +x kubectl && mv kubectl /usr/bin/kubectl

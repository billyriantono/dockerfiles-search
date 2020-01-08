From jenkinsci/jenkins:2.13

USER root
RUN apt-get update && apt-get install -y make vim python-pip jq maven

EXPOSE 8080
ENV JENKINS_OPTS --httpPort=8080

COPY sshkey/ /root/.ssh
COPY docker/ /root/.docker
COPY settings.xml /root/.m2/
RUN chmod 600 /root/.ssh/id_rsa

WORKDIR /tmp

RUN curl -sSL -O https://get.docker.com/builds/Linux/x86_64/docker-1.11.1.tgz \
    && tar zxf docker-1.11.1.tgz -C /tmp \
    && rm docker-1.11.1.tgz \
    && mv /tmp/docker/* /usr/local/bin

RUN curl -sSL -O https://releases.hashicorp.com/terraform/0.7.5/terraform_0.7.5_linux_amd64.zip \
    && unzip terraform_0.7.5_linux_amd64.zip \
    && rm terraform_0.7.5_linux_amd64.zip \
    && mv terraform /usr/local/bin

RUN curl -sSL https://github.com/docker/machine/releases/download/v0.6.0/docker-machine-`uname -s`-`uname -m` > /usr/local/bin/docker-machine \
    && chmod +x /usr/local/bin/docker-machine

RUN curl -sSL https://storage.googleapis.com/kubernetes-release/release/v1.4.1/bin/linux/amd64/kubectl >/usr/local/bin/kubectl \
    && chmod +x /usr/local/bin/kubectl

ENV JAVA_OPTS="-Dorg.apache.commons.jelly.tags.fmt.timeZone=America/Toronto"
ENV SHELL="/bin/bash"
ENV PATH=/opt/google-cloud-sdk/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

COPY plugins.txt /usr/share/jenkins/plugins.txt
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt

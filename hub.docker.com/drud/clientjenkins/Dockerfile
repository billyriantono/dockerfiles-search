FROM phusion/baseimage:latest

ENV PACKER_VERSION 0.8.6
ENV PACKER_SHA256 2f1ca794e51de831ace30792ab0886aca516bf6b407f6027e816ba7ca79703b5
ENV GOLANG_VERSION 1.5.1
ENV GOLANG_SHA256 2593132ca490b9ee17509d65ee2cd078441ff544899f6afb97a03d08c25524e7
ENV PATH $PATH:/bin/go/bin
ENV JENKINS_UC https://updates.jenkins-ci.org

RUN  curl -L http://pkg.jenkins-ci.org/debian-stable/jenkins-ci.org.key | sudo apt-key add - \
  && echo deb http://pkg.jenkins-ci.org/debian-stable binary/ >> /etc/apt/sources.list \
  && apt-get update \
  && apt-get install -y git curl unzip \
  && apt-get install -y --no-install-recommends openjdk-7-jdk unzip \
  && apt-get install -y jenkins \
  && apt-get clean \
  && mkdir -p /var/jenkins_home \
  && chown -R jenkins /var/jenkins_home


# Install Golang.
ADD https://storage.googleapis.com/golang/go${GOLANG_VERSION}.linux-amd64.tar.gz /tmp/go.tar.gz
RUN echo "${GOLANG_SHA256} */tmp/go.tar.gz" | sha256sum -c - \
  && cd /bin \
  && tar -xf /tmp/go.tar.gz -C /bin \
  && chmod +x /bin/go \
  && rm /tmp/go.tar.gz


# Install Packer
ADD https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip /tmp/packer.zip
RUN echo "${PACKER_SHA256} */tmp/packer.zip" | sha256sum -c - \
  && cd /bin \
  && unzip /tmp/packer.zip \
  && chmod +x /bin/packer \
  && rm /tmp/packer.zip


ADD files /

RUN  chmod 755 /bin/* && chmod 755 /etc/service/jenkins/run \
  && /bin/plugins.sh /jenkins-plugins.txt

# VOLUME /var/jenkins_home - bind this in via -v if you want to make this persistent.
ENV JENKINS_HOME /var/jenkins_home
EXPOSE 8080
EXPOSE 5000

ADD start.sh /
RUN chmod 755 /start.sh

# Use baseimage-docker's init system.
CMD ["/bin/bash", "/start.sh"]

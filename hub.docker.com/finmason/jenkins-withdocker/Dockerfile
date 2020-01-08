FROM jenkins/jenkins:lts
MAINTAINER mkozak@finmason.com
USER root
ARG VERSION_ANSIBLE=2.7.11
ARG VERSION_TERRAFORM=0.11.13
ARG FLYWAY_VERSION=6.0.8
ARG http_port=8081


# Install the latest Docker CE binaries
RUN apt-get update && \
    apt-get -y install apt-transport-https \
      ca-certificates \
      python-pip \
      python-paramiko \
      curl \
      gnupg2 \
      sshpass \
      python-lxml \
      software-properties-common && \
    curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey; apt-key add /tmp/dkey && \
    add-apt-repository \
      "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
      $(lsb_release -cs) \
      stable" && \
   apt-get update && \
   apt-get -y install docker-ce && \
   apt-get autoremove -y -q && \
   apt-get clean -y -q && \
   rm -rf /var/lib/apt/lists/*


# Install DevOps tools
RUN wget https://releases.hashicorp.com/terraform/${VERSION_TERRAFORM}/terraform_${VERSION_TERRAFORM}_linux_amd64.zip && \
    unzip terraform_${VERSION_TERRAFORM}_linux_amd64.zip && \
    mv terraform /usr/local/bin/ && \
    rm terraform_${VERSION_TERRAFORM}_linux_amd64.zip && \
    pip install ansible==${VERSION_ANSIBLE} jmespath awscli git+https://github.com/mantl/terraform.py.git && \
    wget https://repo1.maven.org/maven2/org/flywaydb/flyway-commandline/${FLYWAY_VERSION}/flyway-commandline-${FLYWAY_VERSION}.zip && \
    unzip flyway-commandline-${FLYWAY_VERSION}.zip -d /opt && \
    rm -rf flyway-commandline-${FLYWAY_VERSION}.zip && \
    ln -s /opt/flyway-${FLYWAY_VERSION}/flyway /bin/flyway


# Install plugins
COPY plugins.txt /plugins.txt
RUN /usr/local/bin/install-plugins.sh < /plugins.txt

# Explicitly enable some functions for pipelines
COPY core_configs/scriptApproval.xml /usr/share/jenkins/ref/scriptApproval.xml

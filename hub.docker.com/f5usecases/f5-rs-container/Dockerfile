############################################################
# Dockerfile to build f5-super-netops:base enablement container
# Based on Alpine Linux, seasoned with tools and workflows
#############################################################

# Start with an awesome, tiny Linux distro.

FROM alpine:3.10.2


LABEL maintainer "y.rosenboim@f5.com"

ENV SNOPS_REPO https://github.com/F5-use-cases/f5-rs-container.git

# Set the SNOPS image name
ENV SNOPS_IMAGE f5-rs-container

# setuid so things like ping work
RUN chmod +s /bin/busybox

# Add in S6 overlay so we can run some services
ADD https://github.com/just-containers/s6-overlay/releases/download/v1.19.1.1/s6-overlay-x86.tar.gz /tmp/
RUN gunzip -c /tmp/s6-overlay-x86.tar.gz | tar -xf - -C / && rm -f /tmp/s6-overlay-x86.tar.gz

# Add go-dnsmasq so resolver works
ADD https://github.com/janeczku/go-dnsmasq/releases/download/1.0.7/go-dnsmasq-min_linux-amd64 /usr/sbin/go-dnsmasq
RUN chmod +x /usr/sbin/go-dnsmasq


# Add useful APKs
RUN apk add --update openssh bash curl git vim nano python3 rpm py-pip ansible

# Upgrade pip
RUN pip install --upgrade pip

# Setup various users and passwords
RUN adduser -h /home/snops -u 1000 -s /bin/bash snops -D && echo 'snops:default' | chpasswd && echo 'root:default' | chpasswd

# Copy in base FS from repo
COPY fs /

# Expose SSH and HTTP
EXPOSE 22 80 50000 8080 8000

# Set Git Credentials
# !!WARNING!! - password is stored in plaintext
# Set our default host redirect ports SNOPS_HOST_HTTP="8080" SNOPS_HOST_SSH="2222"
# Enable cloning/install of useful repositories on boot SNOPS_AUTOCLONE="1"
# ENV variable used by various scripts to detect the container environment SNOPS_ISALIVE =1 
ENV SNOPS_GIT_HOST="github.com" SNOPS_HOST_HTTP="8080" SNOPS_HOST_SSH="2222" SNOPS_AUTOCLONE="1" SNOPS_GH_BRANCH="master" SNOPS_ISALIVE="1"
COPY fs/snopsboot/udf.pub /root/.ssh/authorized_keys
RUN sed -i "s/#PermitRootLogin.*/PermitRootLogin yes/g" /etc/ssh/sshd_config

####################################jekins install#######################################################
RUN chmod 777 /tmp

RUN apk add --no-cache openjdk8 openssh-client unzip ttf-dejavu coreutils

ENV PATH ${PATH}:/usr/lib/jvm/java-1.8-openjdk/bin/

ENV JENKINS_HOME /var/jenkins_home
ENV JENKINS_SLAVE_AGENT_PORT 50000

ARG user=jenkins
ARG group=snops
ARG uid=1001
ARG gid=1000

# Jenkins is run with user `jenkins`, uid = 1001
# If you bind mount a volume from the host or a data container,
# ensure you use the same uid
RUN adduser -h "$JENKINS_HOME" -u ${uid} -G ${group} -s /bin/bash -D ${user}

# Jenkins home directory is a volume, so configuration and build history
# can be persisted and survive image upgrades
VOLUME /var/jenkins_home

# `/usr/share/jenkins/ref/` contains all reference configuration we want
# to set on a fresh new installation. Use it to bundle additional plugins
# or config file with your custom jenkins Docker image.
RUN mkdir -p /usr/share/jenkins/ref/init.groovy.d

# jenkins version being bundled in this docker image
ARG JENKINS_VERSION
#ENV JENKINS_VERSION ${JENKINS_VERSION:-2.46.2}
ENV JENKINS_VERSION ${JENKINS_VERSION:-2.178}
ENV COPY_REFERENCE_FILE_LOG $JENKINS_HOME/copy_reference_file.log

# jenkins.war checksum, download will be validated using it
#ARG JENKINS_SHA=aa7f243a4c84d3d6cfb99a218950b8f7b926af7aa2570b0e1707279d464472c7
ARG JENKINS_SHA=b0778a1763e582ecbbece698e9ef78b45579ef8945db0198fe02295de8da15b7

# Can be used to customize where jenkins.war get downloaded from
#ARG JENKINS_URL=https://repo.jenkins-ci.org/public/org/jenkins-ci/main/jenkins-war/${JENKINS_VERSION}/jenkins-war-${JENKINS_VERSION}.war
ARG JENKINS_URL=http://mirrors.jenkins.io/war-stable/latest/jenkins.war
# could use ADD but this one does not check Last-Modified header neither does it allow to control checksum
# see https://github.com/docker/docker/issues/8331
RUN curl -fsSL ${JENKINS_URL} -o /usr/share/jenkins/jenkins.war 

ARG JENKINS_CI_URL=https://raw.githubusercontent.com/jenkinsci/docker/alpine
ADD ${JENKINS_CI_URL}/init.groovy /usr/share/jenkins/ref/init.groovy.d/tcp-slave-agent-port.groovy
ADD ${JENKINS_CI_URL}/jenkins-support /usr/local/bin/jenkins-support
ADD ${JENKINS_CI_URL}/jenkins.sh /usr/local/bin/jenkins.sh
ADD ${JENKINS_CI_URL}/plugins.sh /usr/local/bin/plugins.sh
ADD ${JENKINS_CI_URL}/install-plugins.sh /usr/local/bin/install-plugins.sh
RUN chmod 755 /usr/local/bin/jenkins* /usr/local/bin/*plugins*

ENV JENKINS_UC https://updates.jenkins.io

RUN /usr/local/bin/install-plugins.sh bouncycastle-api splunk-devops structs pam-auth windows-slaves mailer ldap external-monitor-job matrix-auth script-security matrix-project credentials credentials-binding timestamper scm-api durable-task workflow-durable-task-step resource-disposer ws-cleanup ant gradle pipeline-milestone-step pipeline-input-step ace-editor workflow-scm-step workflow-cps pipeline-stage-step workflow-job pipeline-graph-analysis pipeline-rest-api handlebars momentjs pipeline-stage-view pipeline-build-step pipeline-model-api ssh-credentials git-client git-server workflow-cps-global-lib branch-api workflow-multibranch authentication-tokens docker-commons docker-workflow pipeline-model-declarative-agent workflow-basic-steps pipeline-model-definition workflow-aggregator github github-branch-source pipeline-github-lib github-organization-folder mapdb-api email-ext slack build-pipeline-plugin

RUN chown -R ${user}:${group} "$JENKINS_HOME" /usr/share/jenkins/ref /usr/local/bin/jenkins* /usr/local/bin/*plugins*

############################################ Ansible installation ########################################
#Add libraries to compile ansible
RUN apk add --update gcc linux-headers libc-dev libffi libffi-dev openssl openssl-dev

#install ansible
#RUN pip3 install ansible==2.8

###########################################install terraform##################################
ENV TERRAFORM_VERSION=0.12.9
WORKDIR /home/snops
RUN apk update && \
    apk add ca-certificates unzip wget && \
    cd /tmp && \
    wget https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip && \
    unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip -d /usr/bin && \
    rm -rf /tmp/terraform* && \
    rm -rf /var/cache/apk/* && \
    rm -rf /var/tmp/terraform*

###########################################install etcd########################################
ENV ETCD_VER v3.3.0
ENV GOOGLE_URL https://storage.googleapis.com/etcd
ENV GITHUB_URL https://github.com/coreos/etcd/releases/download
RUN DOWNLOAD_URL=${GOOGLE_URL}

RUN rm -f /tmp/etcd-${ETCD_VER}-linux-amd64.tar.gz && rm -rf /tmp/etcd-download-test && mkdir -p /tmp/etcd-download-test && curl -L https://storage.googleapis.com/etcd/v3.3.0/etcd-v3.3.0-linux-amd64.tar.gz -o /tmp/etcd-v3.3.0-linux-amd64.tar.gz && tar xzvf /tmp/etcd-v3.3.0-linux-amd64.tar.gz -C /usr/bin --strip-components=1 && rm -f /tmp/etcd-v3.3.0-linux-amd64.tar.gz

# Alpine Linux doesn't use pam, which means that there is no /etc/nsswitch.conf,
# but Golang relies on /etc/nsswitch.conf to check the order of DNS resolving
# (see https://github.com/golang/go/commit/9dee7771f561cf6aee081c0af6658cc81fac3918)
# To fix this we just create /etc/nsswitch.conf and add the following line:
RUN echo 'hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4' >> /etc/nsswitch.conf

###########################################extra things - add here ########################################
#install boto3 for AWS management via ansible 
#install boto for some python scripts that use this version
#install aws cli 
#install ansible[azure] to manage azure 
#install xmltodict for ansible examples from f5devcentral
#install q for ansible examples from f5devcentral

RUN pip3 install boto3 botocore awscli
RUN pip install requests
#RUN pip install ansible[azure] xmltodict q

#creates SSH folders 
RUN mkdir -p /home/snops/.ssh && chown -R snops:snops /home/snops/.ssh && mkdir -p /var/jenkins_home/.ssh && chown -R jenkins:snops /var/jenkins_home/.ssh

#####################
WORKDIR /home/snops
# Start S6 init
ENTRYPOINT ["/init"]
CMD ["/snopsboot/start"]


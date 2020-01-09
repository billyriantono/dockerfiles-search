FROM ubuntu:16.04

ARG VCS_REF
ARG BUILD_DATE

LABEL org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/ajohnstone/docker-build-tools" \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.docker.dockerfile="/Dockerfile"

RUN apt-get update -qqy \
    && apt-get -qqy --no-install-recommends install software-properties-common \
    && add-apt-repository -y ppa:git-core/ppa

RUN apt-get update -qqy \
    && apt-get -qqy --no-install-recommends install \
    iproute \
    openssh-client ssh-askpass \
    ca-certificates \
    openjdk-8-jdk \
    tar zip unzip \
    wget curl \
    git \
    build-essential \
    less nano tree \
    jq \
    python python-pip groff \
    rlwrap \
    rsync

# workaround "You are using pip version 8.1.1, however version 9.0.1 is available."
RUN pip install --upgrade pip setuptools

RUN pip install yq

RUN pip install awscli

#========================================
# Add normal user with passwordless sudo
#========================================
RUN useradd jenkins --shell /bin/bash --create-home \
    && usermod -a -G sudo jenkins \
    && echo 'ALL ALL = (ALL) NOPASSWD: ALL' >> /etc/sudoers \
    && echo 'jenkins:secret' | chpasswd

# compatibility with CloudBees AWS CLI Plugin which expects pip to be installed as user
RUN mkdir -p /home/jenkins/.local/bin/ \
    && ln -s /usr/bin/pip /home/jenkins/.local/bin/pip \
    && chown -R jenkins:jenkins /home/jenkins/.local

ENV KUBE_LATEST_VERSION="v1.13.2"

RUN curl -L https://storage.googleapis.com/kubernetes-release/release/${KUBE_LATEST_VERSION}/bin/linux/amd64/kubectl -o /usr/local/bin/kubectl \
    && chmod +x /usr/local/bin/kubectl

COPY --from=docker:18.09 /usr/local/bin/docker /usr/local/bin/docker
COPY --from=docker:18.09 /usr/local/bin/dockerd /usr/local/bin/dockerd

COPY --from=hashicorp/packer:1.3.3 /bin/packer /bin/packer
COPY --from=hashicorp/terraform:0.11.11 /bin/terraform /bin/terraform

CMD ["bash"]

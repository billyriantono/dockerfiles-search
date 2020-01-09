FROM alpine:latest

# Working directory
ENV OO_WORKDIR /root

ENV OO_SRC_WORKDIR $OO_WORKDIR/src


# Package versions
##################

# Concourse version
ENV OO_CONCOURSE_VERSION 'v3.9.0'

# cf-cli version
ENV OO_CF_CLI_VERSION '6.36.2'

# git-crypt version
ENV OO_GIT_CRYPT_VERSION '0.6.0'


# Create Volume entry points
############################

VOLUME $OO_SRC_WORKDIR


# Create missing directories
############################

RUN mkdir -p $OO_SRC_WORKDIR

# Set the work directory
########################

WORKDIR $OO_WORKDIR

# Install required packages
##############################

RUN apk --update add --no-cache \
      # Preferred Shell environment
      bash \
      # curl
      curl \
      # git client
      git git-svn \
      # Terraform binary
      terraform \
      # Required by AWS-CLI
      py2-pip \
      # might comes in handy at some point
      zip unzip openssh-client rsync wget jq

# Add remaining binaries
######################

# cf-cli
ADD https://s3-us-west-1.amazonaws.com/cf-cli-releases/releases/v${OO_CF_CLI_VERSION}/cf-cli_${OO_CF_CLI_VERSION}_linux_x86-64.tgz $OO_WORKDIR
RUN tar -xvf cf-cli_${OO_CF_CLI_VERSION}_linux_x86-64.tgz -C $OO_WORKDIR
RUN mv $OO_WORKDIR/cf /usr/sbin/cf

# AWS CLI
RUN pip install awscli

# Fix permissions
#################

RUN chmod -R 0644 $OO_WORKDIR/* \
    && chmod 0755 /usr/sbin/cf

# kubectl
#########
ENV KUBE_LATEST_VERSION="v1.12.2"
RUN apk add --update ca-certificates \
 && apk add --update -t deps curl \
 && curl -L https://storage.googleapis.com/kubernetes-release/release/${KUBE_LATEST_VERSION}/bin/linux/amd64/kubectl -o /usr/local/bin/kubectl \
 && chmod +x /usr/local/bin/kubectl \
 && apk del --purge deps \
 && rm /var/cache/apk/*


# git-crypt
#########
RUN apk --update add \
  bash \
  g++ \
  make \
  openssh \
  openssl \
  openssl-dev

RUN curl -L https://github.com/AGWA/git-crypt/archive/debian/${OO_GIT_CRYPT_VERSION}.tar.gz | tar zxv -C /var/tmp
RUN cd /var/tmp/git-crypt-debian && make && make install PREFIX=/usr/local



# Cleanup
#########

RUN apk del --purge make openssl-dev openssh ca-certificates bash \
  && rm -rf /var/cache/apk/* \
  && rm -rf /var/tmp/* \
  && rm -rf /root/.cache/*

RUN find /usr/local \
      \( -type d -a -name test -o -name tests \) \
      -o \( -type f -a -name '*.pyc' -o -name '*.pyo' \) \
      -exec rm -rf '{}' + \
    && rm -rf /var/cache/apk/* \
    && rm -rf $OO_WORKDIR/*.tgz


# Allow redirection of stdout to docker logs
############################################
RUN ln -sf /proc/1/fd/1 /var/log/docker.log

# Change Shell
##############
SHELL ["/bin/bash", "-c"]

# ************************************************************************
# ** GitLab Docker Runner                                               **
# ** -----------------------------                                      **
# ** This image will have a full tool chain for:                        **
# **    Building docker images                                          **
# **    Google Cloud SDK                                                **
# **    Working with Kubernetes (Helm and Kubectl)                      **
# **    Python                                                          **
# **    git                                                             **
# **    GCC                                                             **
# **    Jsonnet                                                         **
# ************************************************************************
FROM docker:latest

MAINTAINER Marc Ford

WORKDIR /

# ********************BASIC TOOL INSTALATION******************************
RUN apk add --no-cache --update \
coreutils \
python \
curl \
wget \
tar \
jq \
openssl \
gcc \
git \
bash \
ca-certificates \
make \
build-base \
libffi-dev \ 
postgresql-dev \
linux-headers \
libc-dev \
musl-dev \
python-dev \
py-pip \
zlib-dev \
jpeg-dev \
bzip2-dev \
readline-dev \
sqlite-dev

# *****************************PYENV INSTALL****************************
RUN curl https://pyenv.run | bash 
ENV PATH /root/.pyenv/bin:$PATH
RUN pyenv install 3.7.2

# *****************************PYENV INSTALL****************************
RUN pip install pipenv

# *****************************JSONNET INSTALL****************************
# Installation of https://jsonnet.org/ 
# jsonnet will be installed to /opt/jsonnet and added to the path
# ************************************************************************
RUN mkdir -p /opt/jsonnet && \
cd /opt/jsonnet && \
git clone https://github.com/google/jsonnet.git . && \
make
ENV PATH /opt/jsonnet:$PATH

# ********************GCP SDK and KUBECTL INSTALATION*********************
# kubectl will be available at /google-cloud-sdk/bin/kubectl
# This is added to $PATH
# ************************************************************************
ENV HOME /
ENV PATH /google-cloud-sdk/bin:$PATH
ENV CLOUDSDK_PYTHON_SITEPACKAGES 1
RUN wget https://dl.google.com/dl/cloudsdk/channels/rapid/google-cloud-sdk.zip && unzip google-cloud-sdk.zip && rm google-cloud-sdk.zip
RUN google-cloud-sdk/install.sh --usage-reporting=true --path-update=true --bash-completion=true --rc-path=/.bashrc --additional-components app kubectl alpha beta
# Disable updater check for the whole installation.
# Users won't be bugged with notifications to update to the latest version of gcloud.
RUN google-cloud-sdk/bin/gcloud config set --installation component_manager/disable_update_check true

# ********************HELM INSTALATION*************************************
ENV HELM_VERSION v2.13.0-rc.2
ENV FILENAME helm-${HELM_VERSION}-linux-amd64.tar.gz
ENV HELM_URL https://storage.googleapis.com/kubernetes-helm/${FILENAME}

RUN echo $HELM_URL

RUN curl -o /tmp/$FILENAME ${HELM_URL} \
  && tar -zxvf /tmp/${FILENAME} -C /tmp \
  && mv /tmp/linux-amd64/helm /bin/helm \
  && rm -rf /tmp

# Install envsubst [better than using 'sed' for yaml substitutions]
ENV BUILD_DEPS="gettext"  \
    RUNTIME_DEPS="libintl"

RUN set -x && \
    apk add --update $RUNTIME_DEPS && \
    apk add --virtual build_deps $BUILD_DEPS &&  \
    cp /usr/bin/envsubst /usr/local/bin/envsubst && \
    apk del build_deps

# ********************HELM PLUGIN INSTALATION*****************************
# Plugin is downloaded to /tmp, which must exist
# ************************************************************************
RUN mkdir /tmp
RUN helm init --client-only
RUN helm plugin install https://github.com/viglesiasce/helm-gcs.git
RUN helm plugin install https://github.com/databus23/helm-diff
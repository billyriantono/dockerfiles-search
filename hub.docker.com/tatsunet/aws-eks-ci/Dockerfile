FROM python:3.8-slim

RUN \
    # Install dependency and jq
    apt-get update -qq \
    && apt-get install -y --no-install-recommends \
       apt-transport-https \
       ca-certificates \
       curl \
       gnupg2 \
       groff-base \
       jq \
       software-properties-common \
    # Install kubectl
    && curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - \
    && echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | tee -a /etc/apt/sources.list.d/kubernetes.list \
    && apt-get update -qq \
    && apt-get install -y --no-install-recommends \
       kubectl \
    # Install kubesec
    && curl -sSL https://github.com/shyiko/kubesec/releases/download/0.9.2/kubesec-0.9.2-linux-amd64 -o kubesec \
    && chmod a+x kubesec \
    && mv kubesec /usr/local/bin/ \
    # Install Docker CE
    && curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - \
    && apt-key fingerprint 0EBFCD88 \
    && add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/debian \
       $(lsb_release -cs) \
       stable" \
    && apt-get update -qq \
    && apt-get install -y \
       docker-ce-cli \
    # Install AWS CLI
    && pip install --no-cache-dir --upgrade awscli

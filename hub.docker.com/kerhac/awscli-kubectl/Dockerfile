FROM python:slim

RUN apt-get update \
    && apt-get install -y \
        apt-transport-https \
        ca-certificates \
        curl \
        gnupg2 \
    && pip install awscli \
    && curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg \
        | apt-key add - \
    && echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" \
        | tee -a /etc/apt/sources.list.d/kubernetes.list \
    && apt-get update \
    && apt-get install -y kubectl

CMD ["bash"]

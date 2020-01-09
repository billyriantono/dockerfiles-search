FROM debian:stretch-slim
LABEL mantainer "hacklab/ <contato@hacklab.com.br>"

# Install assist tools for kubectl
RUN apt-get update &&\
    apt-get install -y \
        curl \
        apt-transport-https \
        gnupg

# Add the official kubectl repository
RUN curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - &&\
    echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | tee -a /etc/apt/sources.list.d/kubernetes.list

# Install kubectl
RUN apt-get update \
    && apt-get install -y kubectl

# Clean up
RUN rm -rf /var/lib/apt/lists/*

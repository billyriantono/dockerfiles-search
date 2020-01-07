FROM ubuntu:bionic

ARG HELM_VERSION=2.12.2

RUN export DEBIAN_FRONTEND=noninteractive \
 && apt-get update -y && apt-get -y install \
      awscli \
      bash-completion \
      command-not-found \
      curl \
      dialog \
      direnv \
      dnsutils \
      ebtables \
      gdb \
      git \
      iproute2 \
      iptables \
      iputils-ping \
      jq \
      less \
      man-db \
      manpages \
      manpages-dev \
      ncurses-term \
      net-tools \
      netcat-openbsd \
      python-pip \
      python3-pip \
      virtualenv \
      tcpdump \
      vim \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl \
  && chmod +x ./kubectl \
  && mv kubectl /usr/local/bin/ \
  && curl -LO https://storage.googleapis.com/kubernetes-helm/helm-v${HELM_VERSION}-linux-amd64.tar.gz \
  && tar zxf helm-v${HELM_VERSION}-linux-amd64.tar.gz linux-amd64/helm \
  && mv linux-amd64/helm /usr/local/bin/helm \
  && echo "Done"

COPY overlay/ /

CMD ["/bin/bash", "-l" ]


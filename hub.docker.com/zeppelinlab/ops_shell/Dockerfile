FROM zeppelinlab/ops_shell:latest

USER ops-shell
WORKDIR /ops-shell

ENV PATH="${PATH}:/ops-shell/.krew/bin"

RUN mkdir -p $HOME/bin
RUN curl -o $HOME/bin/aws-iam-authenticator https://amazon-eks.s3-us-west-2.amazonaws.com/1.14.6/2019-08-22/bin/linux/amd64/aws-iam-authenticator
RUN curl -o $HOME/bin/kubectx https://raw.githubusercontent.com/ahmetb/kubectx/v0.7.0/kubectx
RUN curl -o $HOME/bin/kubens https://raw.githubusercontent.com/ahmetb/kubectx/v0.7.0/kubens
RUN curl -o $HOME/bin/kube-ps1.sh https://raw.githubusercontent.com/jonmosco/kube-ps1/v0.7.0/kube-ps1.sh

RUN set -x; cd "$(mktemp -d)" && \
  curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/download/v0.3.1/krew.{tar.gz,yaml}" && \
  tar zxvf krew.tar.gz && \
  ./krew-"$(uname | tr '[:upper:]' '[:lower:]')_amd64" install \
  --manifest=krew.yaml --archive=krew.tar.gz

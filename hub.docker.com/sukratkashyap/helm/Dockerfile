FROM debian:stretch

RUN apt-get update \
    && apt-get install -y apt-transport-https curl gnupg wget
RUN curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - \
    && echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | tee -a /etc/apt/sources.list.d/kubernetes.list
RUN apt-get update \
    && apt-get install -y kubectl=1.16.1-00

RUN wget https://get.helm.sh/helm-v2.14.3-linux-amd64.tar.gz \
    && tar -zxvf helm-v2.14.3-linux-amd64.tar.gz \
    && mv linux-amd64/helm /usr/local/bin/helm

RUN kubectl version --client=true \
    && helm version -c

CMD [ "kubectl", "version", "--client=true" ]

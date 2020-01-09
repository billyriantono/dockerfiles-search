FROM alpine:3.7

ENV KUBECTL_VERSION v1.9.4
ENV HELM_VERSION 2.8.2
ENV HELM_FILENAME helm-v${HELM_VERSION}-linux-amd64.tar.gz

RUN apk update && apk add curl bash make openssl ansible git docker \
		&& echo "PS1='\u:\w\$ '" > /root/.bashrc \
		&& mkdir /home/Development

RUN mkdir -p /aws && \
		apk -Uuv add groff less python py-pip && \
		pip install awscli && \
		apk --purge -v del py-pip && \
		rm /var/cache/apk/*

RUN set -ex \
    && curl -sSL https://storage.googleapis.com/kubernetes-release/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl -o /usr/local/bin/kubectl \
    && chmod +x /usr/local/bin/kubectl
RUN set -ex \
    && curl -sSL https://storage.googleapis.com/kubernetes-helm/${HELM_FILENAME} | tar xz \
    && mv linux-amd64/helm /usr/local/bin/helm \
    && rm -rf linux-amd64

VOLUME /root/.kube/
VOLUME /home/Development
WORKDIR /home/Development

CMD ["bash"]

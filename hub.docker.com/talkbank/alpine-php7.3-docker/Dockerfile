FROM talkbank/alpine-php7.3-cli

RUN apk add docker

RUN curl -L https://storage.googleapis.com/kubernetes-release/release/v1.6.4/bin/linux/amd64/kubectl -o /usr/local/bin/kubectl \
 && chmod +x /usr/local/bin/kubectl

RUN rc-update add docker boot

WORKDIR /var/www/

ENTRYPOINT ["dockerd"]
FROM mesosphere/aws-cli

WORKDIR /tmp

ENV VERSION_KUBECTL=v1.13.9

RUN apk --no-cache add openssl \
 && wget -q -O kubectl https://storage.googleapis.com/kubernetes-release/release/${VERSION_KUBECTL}/bin/linux/amd64/kubectl \
 && chmod +x kubectl \
 && mv kubectl /usr/local/bin


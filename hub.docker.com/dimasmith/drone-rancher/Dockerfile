FROM alpine:3.4
RUN apk --no-cache add curl ca-certificates bash

# installing kubectl
RUN curl -Lo /usr/local/bin/kubectl https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
RUN chmod +x /usr/local/bin/kubectl

# installing rancher
RUN cd /tmp
RUN curl -Lo rancher.tar.gz https://releases.rancher.com/cli/v2.0.3/rancher-linux-amd64-v2.0.3.tar.gz
RUN tar xzf rancher.tar.gz && cp rancher-v2.0.3/rancher /usr/local/bin/
RUN chmod +x /usr/local/bin/rancher

COPY update.sh /bin/
ENTRYPOINT ["/bin/bash"]
CMD ["/bin/update.sh"]
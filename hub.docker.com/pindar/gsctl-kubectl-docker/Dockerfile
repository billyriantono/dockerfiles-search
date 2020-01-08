FROM docker:latest

# install jq
RUN apk update && apk add jq && rm -rf /var/cache/apk/*

# The gsctl command line utility provides access to your Giant Swarm resources.
RUN curl -O http://downloads.giantswarm.io/gsctl/0.3.1/gsctl-0.3.1-linux-amd64.tar.gz \
  && tar xzf gsctl-0.3.1-linux-amd64.tar.gz \
  && mv gsctl-0.3.1-linux-amd64/gsctl /usr/local/bin/ \
  && rm -rf gsctl-0.3.1-linux-amd64.tar.gz

# Install kubectl
RUN curl -O https://storage.googleapis.com/kubernetes-release/release/v1.4.6/bin/linux/amd64/kubectl \
  && chmod +x kubectl \
  && mv kubectl /usr/local/bin/kubectl

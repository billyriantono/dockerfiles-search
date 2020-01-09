FROM google/cloud-sdk:235.0.0-alpine

# TODO: cleanup and add more utilities

# let's get those kubes
RUN gcloud components install kubectl

# helm
ENV HELM_VERSION="v2.13.0"
RUN apk add --update ca-certificates \
    && apk add --update -t deps wget \
    && wget -q https://storage.googleapis.com/kubernetes-helm/helm-${HELM_VERSION}-linux-amd64.tar.gz \
    && tar -xvf helm-${HELM_VERSION}-linux-amd64.tar.gz \
    && mv linux-amd64/helm /usr/local/bin \
    && apk del --purge deps \
    && rm /var/cache/apk/* \
    && rm -f /helm-${HELM_VERSION}-linux-amd64.tar.gz

# helm client init
RUN helm init --client-only

# helm-tiller
RUN helm plugin install https://github.com/rimusz/helm-tiller --version 0.8.1
# helm-diff
RUN helm plugin install https://github.com/databus23/helm-diff

# tiller
RUN curl -L 'https://storage.googleapis.com/kubernetes-helm/helm-v2.13.1-linux-amd64.tar.gz' --output /tmp/helm.tar.gz \
	&& mkdir /tmp/helm \
	&& tar xvzf /tmp/helm.tar.gz -C /tmp/helm \
	&& mv /tmp/helm/linux-amd64/tiller /usr/local/bin/tiller \
	&& rm -r /tmp/helm /tmp/helm.tar.gz

# helmfile
RUN curl -L 'https://github.com/roboll/helmfile/releases/download/v0.59.0/helmfile_linux_amd64' --output /usr/local/bin/helmfile
RUN chmod +x /usr/local/bin/helmfile

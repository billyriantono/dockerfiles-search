FROM jenkinsci/jnlp-slave

ENV CLOUDSDK_CORE_DISABLE_PROMPTS 1
ENV PATH /opt/google-cloud-sdk/bin:$PATH

USER root

RUN apt-get update && apt-get install -y --no-install-recommends \
		g++ \
		gcc \
		libc6-dev \
		make \
        jq \
	&& rm -rf /var/lib/apt/lists/*

RUN curl https://sdk.cloud.google.com | bash && mv google-cloud-sdk /opt
RUN gcloud components install kubectl
RUN gcloud components install docker-credential-gcr


ENV DOCKER_VERSION 17.09.0-ce

RUN curl -fsSL https://download.docker.com/linux/static/stable/x86_64/docker-$DOCKER_VERSION.tgz -o docker.tar.gz \
	&& tar -xzf docker.tar.gz \
	&& mv ./docker/* /usr/bin/ \
	&& rm -rf ./docker ./docker.tar.gz

ENV HELM_VERSION v2.7.0-rc1

RUN curl -fsSL https://storage.googleapis.com/kubernetes-helm/helm-$HELM_VERSION-linux-amd64.tar.gz -o helm.tar.gz \
	&& tar -xzf helm.tar.gz \
	&& cp ./linux-amd64/helm /usr/local/bin/ \
	&& rm -rf ./linux-amd64 ./helm.tar.gz
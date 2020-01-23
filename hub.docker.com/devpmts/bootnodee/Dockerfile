FROM jenkinsci/jnlp-slave

ENV CLOUDSDK_CORE_DISABLE_PROMPTS 1
ENV PATH /opt/google-cloud-sdk/bin:$PATH

USER root

# Install Google Cloud Components
RUN curl https://sdk.cloud.google.com | bash && mv google-cloud-sdk /opt
RUN gcloud components install kubectl

# Install docker
RUN curl -fsSL https://get.docker.com/ | sh

# Required for ensuring we use the Gcloud docker API version
ENV DOCKER_API_VERSION=1.21


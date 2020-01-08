# https://circleci.com/docs/2.0/circleci-images/
FROM circleci/node:12.13

USER root

RUN echo "deb https://packages.cloud.google.com/apt cloud-sdk-stretch main" > /etc/apt/sources.list.d/google-cloud-sdk.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
    apt-get install -y apt-transport-https && \
    apt-get update -y && \
    apt-get install -y google-cloud-sdk && \
    apt-get clean && \
    apt-get autoclean && \
    apt-get autoremove && \
    gcloud config set core/disable_usage_reporting true && \
    gcloud config set component_manager/disable_update_check true && \
    gcloud --version

USER circleci

COPY --chown=circleci:circleci deploy-notification /usr/local/bin/

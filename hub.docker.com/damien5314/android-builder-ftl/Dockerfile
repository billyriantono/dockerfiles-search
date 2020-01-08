FROM damien5314/android-builder:latest

LABEL version="1.0.3" \
  maintainer="Damien Diehl" \
  maintainer.email="damien5314@gmail.com" \
  description="Android Build Docker image with support for Firebase Test Lab, forked from https://github.com/carlospaulino/android-builder" \
  repository="https://github.com/damien5314/android-builder-ftl"

# setup gcloud
RUN apt-get install curl apt-transport-https -y \
  && echo "deb https://packages.cloud.google.com/apt cloud-sdk-xenial main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list \
  && curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - \
  && apt-get update \
  && apt-get install google-cloud-sdk -y \
  && apt-get clean

WORKDIR /tmp/project

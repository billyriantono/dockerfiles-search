FROM node:6.4-wheezy

# install the base gcloud SDK
RUN wget -q https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-118.0.0-linux-x86_64.tar.gz
RUN tar -xzf google-cloud-sdk-118.0.0-linux-x86_64.tar.gz
RUN ./google-cloud-sdk/install.sh
RUN mv google-cloud-sdk /usr/local/google-cloud-sdk

# install kubectl
RUN /usr/local/google-cloud-sdk/bin/gcloud components update kubectl

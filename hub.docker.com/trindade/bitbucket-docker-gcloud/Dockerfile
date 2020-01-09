FROM atlassian/default-image:latest

# Installing gcloud
RUN curl -o /tmp/google-cloud-sdk.tar.gz https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-206.0.0-linux-x86.tar.gz
RUN tar -xvf /tmp/google-cloud-sdk.tar.gz -C /tmp/
RUN /tmp/google-cloud-sdk/install.sh -q
RUN /bin/bash -c "source /tmp/google-cloud-sdk/path.bash.inc"

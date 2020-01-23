FROM gradle:4.5.1-jdk8
USER root
RUN curl https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-186.0.0-linux-x86_64.tar.gz > /tmp/google-cloud-sdk.tar.gz
RUN mkdir -p /opt/gcloud
RUN tar -C /opt/gcloud -xvf /tmp/google-cloud-sdk.tar.gz
RUN /opt/gcloud/google-cloud-sdk/install.sh --quiet
RUN /opt/gcloud/google-cloud-sdk/bin/gcloud components install app-engine-java --quiet
ENV PATH $PATH:/opt/gcloud/google-cloud-sdk/bin

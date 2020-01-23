FROM google/cloud-sdk

RUN curl -o docker.tgz https://download.docker.com/linux/static/stable/x86_64/docker-17.06.2-ce.tgz \
  && tar --extract \
    --file docker.tgz \
    --strip-components 1 \
    --directory /usr/local/bin/

RUN apt-get install -y make

COPY authorize.sh /authorize.sh

ENV GCLOUD_ZONE us-central1-a
ENV GCLOUD_PROJECT my-project-1-152801

RUN curl --fail https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash -

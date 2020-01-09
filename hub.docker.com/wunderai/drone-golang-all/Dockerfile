FROM gcr.io/kaniko-project/executor:v0.14.0 as KANIKO

FROM wunderai/drone-golang-kafka:latest

COPY --from=KANIKO /kaniko /kaniko
COPY drone-kaniko.sh /usr/local/bin/
RUN chmod 755 /usr/local/bin/drone-kaniko.sh

ENV HOME /root
ENV USER root
ENV SSL_CERT_DIR=/kaniko/ssl/certs
ENV DOCKER_CONFIG /kaniko/.docker/
ENV DOCKER_CREDENTIAL_GCR_CONFIG /kaniko/.config/gcloud/docker_credential_gcr_config.json

ENV PATH="/kaniko:${PATH}"

FROM gcr.io/kaniko-project/executor:latest AS build-env

FROM alpine:3.9

RUN apk --no-cache add ca-certificates
RUN mkdir /workspace
COPY --from=build-env /kaniko/* /kaniko/
ENV HOME /root
ENV USER /root
ENV PATH /usr/local/bin:/usr/bin:/bin:/kaniko
ENV SSL_CERT_DIR=/kaniko/ssl/certs
ENV DOCKER_CONFIG /kaniko/.docker/
ENV DOCKER_CREDENTIAL_GCR_CONFIG /kaniko/.config/gcloud/docker_credential_gcr_config.json
WORKDIR /workspace

CMD ["/bin/sh"]

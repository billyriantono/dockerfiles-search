FROM docker:17.12.0-ce as static-docker-source

FROM google/cloud-sdk:alpine

COPY --from=static-docker-source /usr/local/bin/docker /usr/local/bin/docker

RUN set -x && \
  apk add --update libintl && \
  apk add --virtual build_deps gettext &&  \
  cp /usr/bin/envsubst /usr/local/bin/envsubst && \
  apk del build_deps && \
  gcloud components install kubectl

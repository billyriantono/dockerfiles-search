FROM gitlab/gitlab-runner:alpine-v12.0.0

USER root
COPY Letsencrypt_Root_CA.crt /usr/local/share/ca-certificates/
RUN apk --no-cache add ca-certificates \
  && rm -rf /var/cache/apk/* \
  && update-ca-certificates

USER gitlab-runner

FROM alpine:3.3

ENV AWS_ACCESS_KEY_ID=
ENV AWS_SECRET_ACCESS_KEY=
ENV AWS_SESSION_TOKEN=
ENV AWS_DEFAULT_REGION=
ENV AWS_DEFAULT_PROFILE=
ENV AWS_CONFIG_FILE=

RUN \
  apk -U add groff less python py-pip && \
  pip install awscli==1.10.1 && \
  apk --purge -v del py-pip && \
  rm /var/cache/apk/*
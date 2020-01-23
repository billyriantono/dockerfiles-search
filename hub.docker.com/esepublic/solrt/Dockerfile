FROM alpine:3.10

ARG AWS_CLI_VERSION=1.16.246

RUN apk -uv add --no-cache \
  groff \
  jq \
  less \
  python \
  py-pip \
  && pip install --no-cache-dir awscli==$AWS_CLI_VERSION \
  && apk -v --purge del py-pip

ENTRYPOINT ["aws"]

FROM alpine:3.7

RUN apk add --update --no-cache py-pip jq=1.5-r4 \
  && pip install --no-cache-dir yq==2.4.1

ENTRYPOINT ["yq"]

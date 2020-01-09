FROM alpine

COPY get_helm.sh /tmp/
RUN apk update && apk add openssl gettext
RUN sh /tmp/get_helm.sh

FROM alpine:latest

RUN apk add --update --no-cache curl openssl bash

RUN curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 > get_helm.sh && bash get_helm.sh && rm -rf get_helm.sh


FROM alpine:latest
COPY --from=0 /usr/local/bin/helm /usr/local/bin/helm

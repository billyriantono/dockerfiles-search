FROM ruby:2.5.1-alpine

ENV KUBERNETES_VERSION="1.11.2"
ENV KUBERNETES_DEPLOY_VERSION="0.29.0"
RUN apk update && apk add alpine-sdk cmake

RUN gem install ejson kubernetes-deploy:$KUBERNETES_DEPLOY_VERSION

RUN curl -L -o /usr/bin/kubectl https://storage.googleapis.com/kubernetes-release/release/v$KUBERNETES_VERSION/bin/linux/amd64/kubectl && \
  chmod +x /usr/bin/kubectl

COPY docker-entrypoint.sh /docker-entrypoint.sh

CMD ["/docker-entrypoint.sh"]

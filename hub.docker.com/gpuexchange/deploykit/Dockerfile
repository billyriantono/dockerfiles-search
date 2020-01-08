FROM ruby:2

MAINTAINER GPU Exchange <hosting@gpu.exchange>

RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl; \
    chmod +x ./kubectl; \
    mv ./kubectl /usr/local/bin/kubectl

RUN gem install kubernetes-deploy
RUN gem install ejson
RUN gem install ejson2env

ADD env2key.sh /usr/local/bin/env2key
RUN chmod +x /usr/local/bin/env2key

ADD entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh

RUN mkdir -p /app
WORKDIR /app

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]

CMD ["echo","This is deploy kit."]

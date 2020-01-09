FROM foxundermoon/java8

ARG RELEASE_URL=https://github.com/foxundermoon/rocketmq-3.2.6/releases/download/3.2.6/alibaba-rocketmq-3.2.6.tar.gz

RUN wget -qO- ${RELEASE_URL}  \
  | tar xvz   -C / \
  && mv /alibaba-rocketmq /app

CMD cat /app/bin/README.md
FROM alpine:3.8

RUN apk add openssh-client curl rsync bash \
  && eval $(ssh-agent -s) \
  && mkdir -p ~/.ssh \
  && touch ~/.ssh/id_rsa \
  && chmod 600 ~/.ssh/id_rsa \
  && echo "Host *" >> ~/.ssh/config \
  && echo "  UserKnownHostsFile=/dev/null" >> ~/.ssh/config \
  && echo "  StrictHostKeyChecking no" >> ~/.ssh/config \
  && chmod 400 ~/.ssh/config

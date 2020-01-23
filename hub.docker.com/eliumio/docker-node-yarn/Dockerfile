FROM node:8-wheezy
MAINTAINER Elium Tech <tech@elium.io>

RUN rm -rf /usr/local/lib/node_modules && rm -rf ~/.npm && yarn global add npm@5.2.0

ENV PATH /root/.yarn/bin:$PATH

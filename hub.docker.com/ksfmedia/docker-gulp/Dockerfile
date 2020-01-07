FROM node:11

ARG DEBIAN_FRONTEND=noninteractive

ENV NPM_CONFIG_PREFIX=/root/.npm-global
ENV PATH=$PATH:/root/.npm-global/bin

RUN apt-get update && apt-get -y install ruby-full

# update yarn to ^1.13.0
RUN yarn global add yarn@^1.13.0
RUN rm /usr/local/bin/yarn

RUN yarn global add gulp@3.9.1 parcel-bundler

ADD run.sh /run.sh
RUN chmod +x /run.sh

RUN mkdir /www

WORKDIR /www

ENTRYPOINT ["/run.sh"]

CMD ["default"]

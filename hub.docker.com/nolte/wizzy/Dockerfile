FROM node:11-alpine
MAINTAINER Utkarsh Bhatnagar <utkarsh.cmu@gmail.com>
ADD . /app
WORKDIR /app
RUN npm install
RUN npm pack

FROM node:11-alpine

WORKDIR /wizzy

COPY --from=0 /app/wizzy-*.tgz /wizzy/wizzy.tar

RUN npm install -g --production /wizzy/wizzy.tar
RUN wizzy version
ENTRYPOINT ["wizzy"]

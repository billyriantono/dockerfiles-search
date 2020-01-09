FROM verdaccio/verdaccio:4 AS origin

FROM node:12.13 AS build

WORKDIR /opt/verdaccio

COPY --from=origin . ./

RUN npm i verdaccio-bitbucket verdaccio-s3-storage

FROM verdaccio/verdaccio:4

WORKDIR /opt/verdaccio

USER root

COPY --from=build . ./

USER verdaccio

FROM node:10.16.3-alpine

RUN npm install --global @testmace/cli@0.0.1-8
COPY ./Project /project
WORKDIR /out
CMD testmace-cli /project --reporter=junit -e stage

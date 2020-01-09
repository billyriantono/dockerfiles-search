
FROM node:8

ENV environment DEV

WORKDIR /usr/src/app/

RUN mkdir codesearch-ui
RUN mkdir codesearch-service

WORKDIR /usr/src/app/codesearch-ui
# COPY ./codesearch-ui/package.json ./package.json
# RUN npm install

WORKDIR /usr/src/app/codesearch-service
COPY ./codesearch-service/package.json ./package.json
RUN npm install

WORKDIR /usr/src/app/
COPY ./codesearch-ui/ ./codesearch-ui/
COPY ./codesearch-service/ ./codesearch-service/

# WORKDIR /usr/src/app/codesearch-ui
# RUN npm run build

WORKDIR /usr/src/app/foosball-service

# EXPOSE 443
EXPOSE 80

CMD [ "npm", "run", "start" ]
FROM node as node

ARG APP_ROOT=/app

WORKDIR ${APP_ROOT}
COPY package.json ${APP_ROOT}

RUN   npm install --dev \
   && npm install -g @angular/cli


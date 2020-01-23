FROM python:alpine

# Install node prereqs, nodejs and yarn
# Ref: https://raw.githubusercontent.com/nodejs/docker-node/master/Dockerfile-alpine.template
# Ref: https://yarnpkg.com/en/docs/install

RUN apk add --no-cache npm nodejs yarn libstdc++ && \
    pip install -U pip && pip install pipenv
RUN npm i -g npm@^6
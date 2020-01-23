FROM davidthornton/node6-awscli

WORKDIR /code

ARG NODE_ENV

ADD package.json /code/package.json
ADD yarn.lock /code/yarn.lock
ADD .gitignore .gitignore
ADD env env
ADD internals /code/internals
ADD server /code/server
ADD app /code/app

RUN yarn setup

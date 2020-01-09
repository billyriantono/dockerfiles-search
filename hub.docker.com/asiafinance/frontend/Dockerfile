# use latest node
FROM node

# quieter logs during build
ENV NPM_CONFIG_LOGLEVEL warn

# open up port 3000 (used by Next below) from Docker to the outside world
EXPOSE 3000

# accept app_env arg and set it to var APP_ENV
ARG app_env
ENV APP_ENV $app_env

# create app directory within container
RUN mkdir -p /usr/src/frontend
WORKDIR /usr/src/frontend

# copy code from local folder into container
COPY . /usr/src/frontend

# install dependencies from package.json
RUN yarn install

# run docker in prod or dev depending on arg
CMD if [ ${APP_ENV} = production ]; \
  then \
  yarn build && \
  yarn start -p 3000; \
  else \
  yarn dev -p 3000; \
  fi

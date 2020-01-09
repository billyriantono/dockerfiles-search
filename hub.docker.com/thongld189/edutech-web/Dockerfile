FROM node:9

RUN npm install pm2 -g

ARG APP_BRANCH
ARG APP_ENVIRONMENT
ARG APP_SLUG_COMMIT
ARG APP_RELEASE_VERSION
ARG APP_RELEASE_CREATED_AT

ARG MONGODB_URI
ARG REDIS_URL

ENV APP_BRANCH ${APP_BRANCH}
ENV APP_ENVIRONMENT ${APP_ENVIRONMENT}
ENV APP_SLUG_COMMIT ${APP_SLUG_COMMIT}
ENV APP_RELEASE_VERSION ${APP_RELEASE_VERSION}
ENV APP_RELEASE_CREATED_AT ${APP_RELEASE_CREATED_AT}

ENV MONGODB_URI ${MONGODB_URI}
ENV REDIS_URL ${REDIS_URL}

# WORKDIR /opt/videoedu-web/app

# COPY ./package.json ./yarn.lock ./LICENSE.txt ./
# COPY ./pm2.json ./
# COPY ./node_modules ./node_modules
# COPY ./public ./public
# COPY ./build ./build
# COPY ./mail_template ./mail_template

# CMD ["pm2-runtime", "start", "pm2.json"]

RUN mkdir -p /opt/edutech-admin/app
WORKDIR /opt/edutech-admin/app

ADD . /opt/edutech-admin/app

ADD .env /opt/edutech-admin/app/

# COPY ./package.json ./yarn.lock ./LICENSE.txt ./
# COPY ./pm2.json ./
# COPY ./public ./public
# COPY ./build ./build

RUN pwd
RUN ls -lh
#RUN cat .env
RUN yarn

ENTRYPOINT ["pm2-runtime", "start", "pm2.json"]


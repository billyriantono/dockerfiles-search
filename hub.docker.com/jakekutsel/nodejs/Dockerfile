FROM node:7.0.0

ARG BUILD_USER=vue
ARG BUILD_USER_GROUP=vues
ARG BUILD_USER_PASSWORD=vue
ARG BUILD_USER_SHELL=/bin/sh
ARG BUILD_USER_UID=1000
ARG BUILD_PROJECT_HOME=/app

ENV NODE_USER=${BUILD_USER}
ENV NODE_USER_GROUP=${BUILD_USER_GROUP}
ENV NODE_USER_PASSWORD=${BUILD_USER_PASSWORD}
ENV NODE_USER_SHELL=${BUILD_USER_SHELL}
ENV NODE_USER_UID=${BUILD_USER_UID}
ENV PROJECT_HOME=${BUILD_PROJECT_HOME}

# Create app directory
RUN mkdir -p ${PROJECT_HOME}
WORKDIR ${PROJECT_HOME}

#RUN adduser --group ${NODE_USER_GROUP}  \
#    && adduser ${NODE_USER} \
#    && echo "${NODE_USER}:${BUILD_USER_PASSWORD}" | chpasswd \
#

RUN /usr/local/bin/npm install -g \
        generator-ractive-webpack

RUN /usr/local/bin/npm install -g \
        autoprefixer \
        precss \
        react-css-modules \
        sugarcss

# Uninstalling system reqs
RUN rm -rf /var/cache/apk/*;


CMD ["/usr/local/bin/npm"]

EXPOSE 3000

WORKDIR ${PROJECT_HOME}

CMD ${PROJECT_HOME}/.util/entrypoint.sh
ENTRYPOINT ${PROJECT_HOME}/.util/entrypoint.sh
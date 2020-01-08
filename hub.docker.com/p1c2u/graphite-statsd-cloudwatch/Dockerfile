FROM graphiteapp/graphite-statsd:1.1.5-12 as base
LABEL maintainer="Artur Maciag <maciag.artur@gmail.com>"

FROM base as build
LABEL maintainer="Artur Maciag <maciag.artur@gmail.com>"

RUN apk add --no-cache --update alpine-sdk

WORKDIR /opt

# install statsd (as we have to use this ugly way)
ARG statsd_version=0.8.5
WORKDIR /opt
RUN cd /opt/statsd \
 && git fetch \
 && git reset --hard "tags/v${statsd_version}" \
 && npm install

# install cloudwatch backend
ARG cloudwatch_backend_version=master
RUN npm install camitz/aws-cloudwatch-statsd-backend#"${cloudwatch_backend_version}"

WORKDIR /opt/graphite/webapp

FROM base as production
LABEL maintainer="Artur Maciag <maciag.artur@gmail.com>"

COPY --from=build /opt /opt

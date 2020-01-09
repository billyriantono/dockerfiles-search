FROM node:8-stretch as builder

WORKDIR /app
ADD . .
RUN apt-get -qq update
RUN apt-get -qq install netbase build-essential autoconf libffi-dev
RUN npm install
RUN npm run build

FROM grafana/grafana:5.3.1
COPY --from=builder /app/dist/ /var/lib/grafana/plugins/astarte-datasource/

FROM debian:stretch-slim

ARG credentials="/config/ps4-credentials.json"
ENV credentials=$credentials

ARG port="3030"
ENV port=$port

ARG host="0.0.0.0"
ENV host=$host


WORKDIR /
COPY . /
RUN apt-get update && apt-get install -y gnupg && /setup_8.x \
  && apt-get update && apt-get install -y nodejs && npm install -g
ENTRYPOINT ps4-hassio-waker --credentials $credentials \
           --port $port --host $host

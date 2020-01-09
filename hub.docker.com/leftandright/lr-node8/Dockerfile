# https://hub.docker.com/_/node/
# https://github.com/nodejs/docker-node/blob/de76fb48b532d6be012098dc3538bd15329a27d0/8/stretch/Dockerfile
FROM node:8.15.1-stretch

# Add some utils
RUN apt-get update \
    && apt-get install -y \
    nano \
    net-tools \
    git \
    dnsutils \
    dos2unix \
    && apt-get clean
#ssmtp \

# Add all source files & fix line endings
COPY ./conf /tmp/conf
RUN find /tmp/conf -type f -print0 | xargs -0 dos2unix


RUN mv /tmp/conf/.bashrc /root/.bashrc \
    && chmod 777 /root/.bashrc

RUN rm -rf /tmp/conf

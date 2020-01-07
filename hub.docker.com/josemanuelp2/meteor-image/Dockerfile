FROM ubuntu:16.04

RUN apt-get update && apt-get install -y curl nodejs && curl https://install.meteor.com/ | sh
RUN apt-get install locales && locale-gen en_US.UTF-8 && localedef -i en_US -f UTF-8 en_US.UTF-8
ENV METEORD_DIR /home
COPY .meteor $METEORD_DIR/.meteor
RUN cd $METEORD_DIR && meteor build /tmp/

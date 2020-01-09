FROM openjdk:8-jdk

ENV APP_HOME /usr/src/app

USER root
RUN apt-get update \
  && apt-get install -y --no-install-recommends maven \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mkdir -p $APP_HOME
WORKDIR $APP_HOME

#USER docker
COPY . $APP_HOME
RUN mvn install -e -Dlicense.skip=true

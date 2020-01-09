FROM stellarity/openjdk8
MAINTAINER Sergey Podobry <sergey.podobry@stellaritysoftware.com>
LABEL Description="webtest"

# install packages
RUN apt-get update &&\
    apt-get install -y --no-install-recommends chromium-browser chromium-chromedriver curl &&\
    rm -rf /var/lib/apt/lists/*

# disable gradle daemon
RUN mkdir -p ~/.gradle && echo "org.gradle.daemon=false" >> ~/.gradle/gradle.properties

ENV PATH="${PATH}:/usr/lib/chromium-browser"

# copy configs
ADD root /

WORKDIR /opt

# create entrypoint
ENTRYPOINT ["/bootstrap.sh"]

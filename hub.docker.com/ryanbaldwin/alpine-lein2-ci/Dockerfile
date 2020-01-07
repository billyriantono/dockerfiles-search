FROM frolvlad/alpine-oraclejdk8:slim
MAINTAINER Ryan Baldwin <ryanbaldwin@gmail.com>

# to disable the warning about lein running as root
ENV LEIN_ROOT=true

# get curl and bash, which we'll use to build.
RUN apk add --update curl bash && rm -rf /var/cache/apk/*

# download and install Leiningen
RUN curl https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein > ./lein
RUN chmod a+x ./lein 
RUN mv ./lein /usr/bin/lein 
RUN lein
RUN mkdir /src && mkdir -p /root/.m2/repository

VOLUME ["/src", "/root/.m2/repository"]
WORKDIR /src

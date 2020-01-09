# NOTE: this Dockerfile builds Metabase from source. We recommend deploying the pre-built
# images hosted on Docker Hub https://hub.docker.com/r/metabase/metabase/ which use the
# Dockerfile located at ./bin/docker/Dockerfile
# from metabase/Docker build system docker
FROM nerelohw/docker-nodejs-openjdk
#FROM java:openjdk-8-jre-alpine

ENV JAVA_HOME=/usr/lib/jvm/default-jvm
ENV PATH /usr/local/bin:$PATH
ENV LEIN_ROOT 1

ENV FC_LANG en-US
ENV LC_CTYPE en_US.UTF-8

# install core build tools
# nodejs yarn from docker-nodejs
RUN apk add --update git wget bash python make g++ java-cacerts ttf-dejavu fontconfig gettext && \
    ln -sf "${JAVA_HOME}/bin/"* "/usr/bin/"

# fix broken cacerts
RUN rm -f /usr/lib/jvm/default-jvm/jre/lib/security/cacerts && \
    ln -s /etc/ssl/certs/java/cacerts /usr/lib/jvm/default-jvm/jre/lib/security/cacerts

# install lein
ADD https://raw.github.com/technomancy/leiningen/stable/bin/lein /usr/local/bin/lein
RUN chmod 744 /usr/local/bin/lein

# add the application source to the image
#ADD . /app/source
VOLUME /app/source
# build the app
#RUN bin/build

# remove unnecessary packages & tidy up
#RUN apk del nodejs git wget python make g++
#RUN rm -rf /root/.lein /root/.m2 /root/.node-gyp /root/.yarn /root/.yarn-cache /tmp/* /var/cache/apk/* /app/source/node_modules

# expose our default runtime port
EXPOSE 3000

# build and then run it
WORKDIR /app/source
#ENTRYPOINT ["./bin/start"]
CMD [ "bin/build" ]

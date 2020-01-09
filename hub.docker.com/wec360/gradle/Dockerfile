FROM openjdk:8-jdk

MAINTAINER wec360 Devops Team <devops@wec360.com>

ENV GRADLE_VERSION 3.4
ENV GRADLE_HOME /usr/local/gradle
ENV GRADLE_USER_HOME /cache/gradle
ENV IVY_HOME /cache/ivy
ENV PATH ${PATH}:${GRADLE_HOME}/bin

# Install gradle
WORKDIR /usr/local

# Create caches
RUN mkdir -p /cache/ivy && mkdir -p /cache/gradle

RUN wget  https://services.gradle.org/distributions/gradle-$GRADLE_VERSION-bin.zip && \
    unzip gradle-$GRADLE_VERSION-bin.zip && \
    rm -f gradle-$GRADLE_VERSION-bin.zip && \
    ln -s gradle-$GRADLE_VERSION gradle && \
    echo -ne "- with Gradle $GRADLE_VERSION\n" >> /root/.built

WORKDIR /app

# Expose ivy cache so that we can use docker volumes to persist the cache
VOLUME /cache

# Allow tmp files
VOLUME /tmp

# The gradle application to run
VOLUME /app

ENTRYPOINT ["gradle"]

CMD ["-v"]

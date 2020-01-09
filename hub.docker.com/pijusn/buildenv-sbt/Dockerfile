FROM openjdk:8u151

MAINTAINER Pijus Navickas <pijus.navickas@gmail.com>

ENV SCALA_VERSION 2.12.4
ENV SBT_VERSION 1.0.2
ENV DOCKER_VERSION 17.11.0-ce

# Set up Scala.

RUN touch /usr/lib/jvm/java-8-openjdk-amd64/release

RUN \
  curl -fsL https://downloads.typesafe.com/scala/$SCALA_VERSION/scala-$SCALA_VERSION.tgz | tar xfz - -C /root/ && \
  echo >> /root/.bashrc && \
  echo "export PATH=~/scala-$SCALA_VERSION/bin:$PATH" >> /root/.bashrc

# Set up SBT.

RUN \
  curl -L -o sbt-$SBT_VERSION.deb https://dl.bintray.com/sbt/debian/sbt-$SBT_VERSION.deb && \
  dpkg -i sbt-$SBT_VERSION.deb && \
  rm sbt-$SBT_VERSION.deb && \
  apt-get update && \
  apt-get install sbt && \
  sbt sbtVersion

# Set up Docker.

RUN set -x \
	&& curl -fSL "https://download.docker.com/linux/static/edge/x86_64/docker-${DOCKER_VERSION}.tgz" -o docker.tgz \
	&& tar -xzvf docker.tgz \
	&& mv docker/* /usr/local/bin/ \
	&& rmdir docker \
	&& rm docker.tgz

WORKDIR /root

# Set up entry point.
COPY entrypoint.sh /usr/local/bin/
ENTRYPOINT ["entrypoint.sh"]
CMD ["sh"]
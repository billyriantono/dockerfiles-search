FROM jekyll/builder:3.8.5

WORKDIR /

ENV SCALA_VERSION 2.12.8
ENV SBT_VERSION 1.2.8

ENV PATH /sbt/bin:$PATH

RUN apk add -U bash graphviz npm git openjdk8 fontconfig ttf-ubuntu-font-family ttf-opensans

# Install Scala
## Piping wget directly into tar
RUN \
  wget -O - https://downloads.typesafe.com/scala/$SCALA_VERSION/scala-$SCALA_VERSION.tgz | tar xfz - -C /root/ && \
  echo >> /root/.bashrc && \
  echo "export PATH=~/scala-$SCALA_VERSION/bin:$PATH" >> /root/.bashrc

# Install SBT
## Piping wget directly into tar
RUN \
  wget -O - https://github.com/sbt/sbt/releases/download/v$SBT_VERSION/sbt-$SBT_VERSION.tgz | tar xfz - -C / && \
  sbt sbtVersion

# Install typedoc
RUN \
  npm install --global typedoc

EXPOSE 4000

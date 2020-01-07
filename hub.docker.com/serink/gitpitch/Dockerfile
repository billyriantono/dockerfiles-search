FROM openjdk:8u181

ENV SCALA_VERSION 2.12.8
ENV SBT_VERSION 1.2.8

# Install zip (needed by gitpitch)
RUN \
  apt-get update && \
  apt-get install -y zip && \
  apt-get clean autoclean && \
  apt-get autoremove --yes && \
  rm -rf /var/lib/{apt,dpkg,cache,log}/

# Install scala
RUN \
  curl -fsL https://downloads.typesafe.com/scala/$SCALA_VERSION/scala-$SCALA_VERSION.tgz | tar xfz - -C /root/ && \
  echo >> /root/.bashrc && \
  echo "export PATH=~/scala-$SCALA_VERSION/bin:$PATH" >> /root/.bashrc

# Install sbt
RUN \
  curl -L -o sbt-$SBT_VERSION.deb https://dl.bintray.com/sbt/debian/sbt-$SBT_VERSION.deb && \
  dpkg -i sbt-$SBT_VERSION.deb && \
  rm sbt-$SBT_VERSION.deb && \
  apt-get update && \
  apt-get install sbt && \
  sbt sbtVersion && \
  mkdir project && \
  echo "scalaVersion := \"${SCALA_VERSION}\"" > build.sbt && \
  echo "sbt.version=${SBT_VERSION}" > project/build.properties && \
  echo "case object Temp" > Temp.scala && \
  sbt compile && \
  rm -r project && rm build.sbt && rm Temp.scala && rm -r target

# Install gitpitch
RUN \
  git clone https://github.com/gitpitch/gitpitch.git && \
  cd gitpitch && \
  sbt dist && \
  mkdir -p /opt/gitpitch && \
  unzip target/universal/server-2.0.zip -d /opt/gitpitch/ && \
  cd .. && \
  rm -rf gitpitch

# Remove sbt and scala
RUN \
  rm -rf ~/scala-$SCALA_VERSION && \
  apt-get remove -y sbt && \
  apt-get clean autoclean && \
  apt-get autoremove --yes && \
  rm -rf /var/lib/{apt,dpkg,cache,log}/

ADD application.conf /opt/gitpitch/

EXPOSE 9000

ENTRYPOINT ["/opt/gitpitch/server-2.0/bin/server", "-Dconfig.file=/opt/gitpitch/application.conf"]

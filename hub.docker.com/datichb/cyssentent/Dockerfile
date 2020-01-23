FROM java:8
MAINTAINER Binh Van Nguyen

ENV TERM xterm
ENV STORM_HOME /home/storm
ENV STORM_VERSION 0.10.0
WORKDIR $STORM_HOME

ENTRYPOINT ["bash", "bin/entrypoint.sh"]
RUN apt-get update && apt-get install -y supervisor tar nutcracker && groupadd storm && useradd --gid storm --home-dir $STORM_HOME --create-home --shell /bin/bash storm && mkdir /var/log/storm && chown -R storm:storm /var/log/storm && ln -s /var/log/storm $STORM_HOME/log
RUN curl -L http://apache.mirrors.tds.net/storm/apache-storm-${STORM_VERSION}/apache-storm-${STORM_VERSION}.tar.gz | tar -xzC $STORM_HOME --strip-components=1

# Download build and deploy storm-graphite
#RUN cd /tmp && git clone https://github.com/verisign/storm-graphite.git && cd storm-graphite && ./gradlew clean build && cp build/libs/storm-graphite-*-all.jar ${STORM_HOME}/lib

COPY entrypoint.sh bin/entrypoint.sh
RUN chmod +x bin/entrypoint.sh

COPY storm.yaml conf/storm.yaml
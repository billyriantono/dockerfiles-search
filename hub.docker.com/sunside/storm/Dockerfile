FROM sunside/java-base
MAINTAINER Markus Mayer <widemeadows@gmail.com>

ENV STORM_DL_VERSION apache-storm-0.10.0
ENV STORM_DL_MIRROR ftp://ftp.fu-berlin.de/unix/www/apache/storm/

RUN wget -q -O - ${STORM_DL_MIRROR}${STORM_DL_VERSION}/$STORM_DL_VERSION.tar.gz | tar -xzf - -C /opt

ENV STORM_HOME /opt/$STORM_DL_VERSION
RUN groupadd storm \
	&& useradd --gid storm --home-dir /home/storm --create-home --shell /bin/bash storm \
	&& chown -R storm:storm $STORM_HOME \
	&& mkdir -p /var/log/storm \
	&& chown -R storm:storm /var/log/storm \
	&& ln -s $STORM_HOME/bin/storm /usr/bin/storm

RUN echo [supervisord] | tee -a /etc/supervisor/supervisord.conf \
	&& echo nodaemon=true | tee -a /etc/supervisor/supervisord.conf

COPY bin/config-supervisord.sh /usr/bin/
COPY bin/configure-storm.sh /usr/bin/
COPY bin/start-supervisord.sh /usr/bin/

COPY conf/storm.yaml $STORM_HOME/conf/
COPY conf/cluster.xml $STORM_HOME/logback/

WORKDIR $STORM_HOME
VOLUME $STORM_HOME/conf/

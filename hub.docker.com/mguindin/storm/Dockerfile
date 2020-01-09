from ubuntu:14.04
MAINTAINER Matt Guindin (originally from Wurstmeister and dgageot)

RUN apt-get update
RUN apt-get install -y unzip wget supervisor
# Install curl with ssl support
RUN (wget -O - http://www.magicermine.com/demos/curl/curl/curl-7.30.0.ermine.tar.bz2 | bunzip2 -c - | tar xf -) \
        && mv /curl-7.30.0.ermine/curl.ermine /bin/curl \
        && rm -Rf /curl-7.30.0.ermine

# Install jre with tools.jar
RUN (curl -s -k -L -C - -b "oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u20-b26/jdk-8u20-linux-x64.tar.gz | tar xfz -) \
        && mv /jdk1.8.0_20/jre /jre1.8.0_20 \
        && mv /jdk1.8.0_20/lib/tools.jar /jre1.8.0_20/lib/ext \
        && rm -Rf /jdk1.8.0_20

ENV JAVA_HOME /jre1.8.0_20
ENV PATH $PATH:$JAVA_HOME/bin

RUN wget -q -N http://www.interior-dsgn.com/apache/storm/apache-storm-0.9.3/apache-storm-0.9.3.zip; unzip -o /apache-storm-0.9.3.zip -d /usr/share/; rm apache-storm-0.9.3.zip
ENV STORM_HOME /usr/share/apache-storm-0.9.3
RUN groupadd storm; useradd --gid storm --home-dir /home/storm --create-home --shell /bin/bash storm; chown -R storm:storm $STORM_HOME; mkdir /var/log/storm ; chown -R storm:storm /var/log/storm
RUN ln -s $STORM_HOME/bin/storm /usr/bin/storm

ADD storm.yaml $STORM_HOME/conf/storm.yaml
ADD cluster.xml $STORM_HOME/logback/cluster.xml
ADD config-supervisord.sh /usr/bin/config-supervisord.sh
ADD start-supervisor.sh /usr/bin/start-supervisor.sh

RUN echo [supervisord] | tee -a /etc/supervisor/supervisord.conf ; echo nodaemon=true | tee -a /etc/supervisor/supervisord.conf

FROM ruo91/hadoop

MAINTAINER smduarte (smd@fct.unl.pt)


ENV TERM vt100

#install NTP
RUN apt-get update && apt-get install -y ntp

# Apache FLUME
ENV SRC_DIR /opt
ENV FLUME_URL http://www-eu.apache.org/dist/flume/
ENV FLUME_VERSION 1.7.0
ENV FLUME_FILENAME apache-flume-$FLUME_VERSION-bin.tar.gz

RUN cd $SRC_DIR && curl -LO "$FLUME_URL/$FLUME_VERSION/$FLUME_FILENAME" \
 && ls -al && tar xzf $FLUME_FILENAME ; rm -f $FLUME_FILENAME

ENV FLUME_DIR=$SRC_DIR/apache-flume-$FLUME_VERSION-bin

ENV PATH $PATH:$FLUME_DIR/bin
ENV CLASSPATH=$FLUME_DIR/$FLUME_DIR

COPY twitter.conf /flume/
COPY twitter+kafka.conf /flume/
COPY flume-sources-1.0-SNAPSHOT.jar /flume/lib

RUN echo "Europe/Lisbon" > /etc/timezone
RUN cp /usr/share/zoneinfo/Portugal /etc/localtime


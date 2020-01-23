FROM anapsix/alpine-java

MAINTAINER David Hahn "davidka.h@gmail.com"

LABEL name="openhab" version="1.8.2"

ENV OPENHAB_VERSION=1.8.2
ENV OPENHAB_DIR=/opt/openhab
ENV BINDINGS_DIR=/opt/openhab-all-bindings
ENV HABMIN_DIR=$OPENHAB_DIR/webapps/habmin

# Install OpenHAB
RUN mkdir -p $OPENHAB_DIR \
	&& wget https://bintray.com/artifact/download/openhab/bin/distribution-$OPENHAB_VERSION-runtime.zip \
	&& unzip distribution-$OPENHAB_VERSION-runtime.zip -d $OPENHAB_DIR \
	&& rm distribution-$OPENHAB_VERSION-runtime.zip \
	&& mkdir -p $OPENHAB_DIR/logs

# Extract Bindings
RUN mkdir -p $BINDINGS_DIR \
	&& wget https://bintray.com/artifact/download/openhab/bin/distribution-$OPENHAB_VERSION-addons.zip \
	&& unzip distribution-$OPENHAB_VERSION-addons.zip -d $BINDINGS_DIR \
	&& rm distribution-$OPENHAB_VERSION-addons.zip

# Install HabMin
RUN mkdir -p $HABMIN_DIR \
	&& wget https://github.com/cdjackson/HABmin/archive/master.zip \
	&& unzip master.zip \
	&& mv HABmin-master/* $HABMIN_DIR \
	&& rm -r HABmin-master master.zip \
	&& mv $HABMIN_DIR/addons/*.jar $OPENHAB_DIR/addons


COPY ./start-openhab.sh /opt/
RUN chmod +x /opt/start-openhab.sh

EXPOSE 8080

VOLUME ["/opt/openhab/webapps/images"]

CMD ["/opt/start-openhab.sh"]



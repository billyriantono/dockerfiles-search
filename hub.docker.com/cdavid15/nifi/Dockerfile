FROM apache/nifi:1.9.2

# Bundle Oracle driver with image
COPY --chown=nifi:nifi ojdbc6-11.2.0.4.jar /opt/nifi/nifi-current/lib

# Bundle our modded Run|MongoAggregation nar
COPY --chown=nifi:nifi nifi-mongodb-nar-1.9.2.nar /opt/nifi/nifi-current/lib

# Updated Bootstrap.conf with increased memory
COPY --chown=nifi:nifi  bootstrap.conf /opt/nifi/nifi-current/conf

RUN chmod 664 /opt/nifi/nifi-current/lib/ojdbc6-11.2.0.4.jar && \
    chmod 664 /opt/nifi/nifi-current/lib/nifi-mongodb-nar-1.9.2.nar && \
    chmod 664 /opt/nifi/nifi-current/conf/bootstrap.conf

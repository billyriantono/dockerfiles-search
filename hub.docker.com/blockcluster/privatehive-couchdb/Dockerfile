FROM hyperledger/fabric-couchdb

COPY payload/local.ini /opt/couchdb/etc/


RUN mkdir -p /etc/hyperledger/privatehive/couchdb/ && chmod 0777 /etc/hyperledger/privatehive/couchdb/

CMD ["/opt/couchdb/bin/couchdb"]
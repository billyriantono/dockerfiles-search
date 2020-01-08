FROM luismcplopes/couchbasece-5
MAINTAINER Luis Lopes <luis.mcp.lopes@gmail.com>
COPY configure-node.sh /opt/couchbase
RUN chmod a+x /opt/couchbase/configure-node.sh
ENTRYPOINT ["/bin/bash"]
CMD ["/opt/couchbase/configure-node.sh"]
EXPOSE 8091 8092 8093 8094 11207 11210 11211 18091 18092 18093 18094
VOLUME /opt/couchbase/var/lib/couchbase/data
WORKDIR /opt/couchbase/var/lib/couchbase/data

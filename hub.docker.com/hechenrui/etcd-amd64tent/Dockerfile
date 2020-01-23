# Alpine linux would be great for this, but it's DNS does not use search paths.
FROM progrium/busybox
LABEL maintainer="imran.qureshi@healthcatalyst.com"

# based on: # https://github.com/kubernetes/contrib/tree/master/for-demos/proxy-to-service

RUN opkg-install socat
ADD start.sh start.sh

RUN chmod a+x ./start.sh

# Usage: docker run -p <host-port>:<port> <this-container> <tcp|udp> <port> <service-name> [timeout]
ENTRYPOINT ["/start.sh"]
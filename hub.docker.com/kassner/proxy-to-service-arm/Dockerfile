FROM arm32v7/busybox

ADD socat-armv7l.bin /bin/socat
ADD start.sh start.sh

# Usage: docker run -p <host-port>:<port> <this-container> <tcp|udp> <port> <service-name> [timeout]
ENTRYPOINT ["/start.sh"]

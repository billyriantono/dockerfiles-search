FROM redis:3.2

HEALTHCHECK --start-period=10s --interval=5s --timeout=10s --retries=4 \
  CMD echo "PING" | redis-cli -h 127.0.0.1 -p 6379 | grep PONG || exit 1
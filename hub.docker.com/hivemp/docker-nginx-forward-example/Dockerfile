FROM nginx:latest

RUN apt-get update && \
    apt-get install --no-install-recommends --no-install-suggests -y curl ca-certificates && \
    curl -L -o /forward-logs https://github.com/HiveMP/forward-logs/releases/download/1.0.23/forward-logs && \
    chmod a+x /forward-logs && \
    apt-get remove --purge --auto-remove -y curl ca-certificates && \
    rm -rf /var/lib/apt/lists/* /etc/apt/sources.list.d/nginx.list

ENV FORWARD_LOGS_USE_PTY true

CMD ["/forward-logs", "nginx", "-g", "daemon off;"]
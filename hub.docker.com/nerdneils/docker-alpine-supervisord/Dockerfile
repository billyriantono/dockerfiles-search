FROM alpine

# Install Supervisor.
RUN \
  apk update && \
  apk add  supervisor && \
  rm -rf /var/cache/apk/* 

RUN  sed -i 's/^\(\[supervisord\]\)$/\1\nnodaemon=true/' /etc/supervisord.conf

# Define mountable directories.
VOLUME ["/etc/supervisor/conf.d"]

# Define working directory.
WORKDIR /etc/supervisor/conf.d

# Define default command.
CMD ["supervisord", "-c", "/etc/supervisord.conf"]

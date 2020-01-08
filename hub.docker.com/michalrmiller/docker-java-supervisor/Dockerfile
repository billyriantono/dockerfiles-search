FROM java:8

RUN apt-get update && \
    apt-get install -y supervisor && \
    rm -rf /var/lib/apt/lists/*
CMD ["/usr/bin/supervisord"]

# Configure with /etc/supervisor/conf.d/supervisord.conf
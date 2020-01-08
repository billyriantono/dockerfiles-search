# Base image
FROM mongo-express:0.45

# Base dependencies
RUN apt-get update \
  && apt-get install -y \
    curl \
  && rm -rf /var/lib/apt/lists/*

# Expose ports
EXPOSE 8081

# Healthcheck
ADD ./docker-healthcheck.sh /usr/local/bin/docker-healthcheck
RUN chmod +x /usr/local/bin/docker-healthcheck
HEALTHCHECK CMD docker-healthcheck

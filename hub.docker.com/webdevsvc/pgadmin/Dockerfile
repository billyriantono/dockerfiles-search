# Base image
FROM chorss/docker-pgadmin4:4.11

# Base dependencies
RUN apk add --no-cache \
  curl

# Expose ports
EXPOSE 5050

# Healthcheck
ADD ./docker-healthcheck.sh /usr/local/bin/docker-healthcheck
RUN chmod +x /usr/local/bin/docker-healthcheck
HEALTHCHECK CMD docker-healthcheck

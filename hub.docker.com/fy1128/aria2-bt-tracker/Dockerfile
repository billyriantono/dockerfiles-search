FROM amd64/alpine:3.8

# Install packages
RUN apk --no-cache add curl

# Copy scripts
COPY update-bt-tracker.sh /
COPY crontab /var/spool/cron/crontabs/root

# Give execution rights on the cron job
RUN chmod 0644 /var/spool/cron/crontabs/root

# Entrypoint
COPY entrypoint.sh /
ENTRYPOINT ["/bin/sh", "/entrypoint.sh"]


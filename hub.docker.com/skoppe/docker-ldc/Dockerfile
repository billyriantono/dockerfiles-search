FROM skoppe/docker-ldc

MAINTAINER Sebastiaan Koppe <mail@skoppe.eu>

RUN apt-get update && apt-get install -y curl libevent-dev libssl-dev \
 && rm -rf /var/cache/apt

ENTRYPOINT ["/entrypoint.sh"]
CMD ["ldc2"]

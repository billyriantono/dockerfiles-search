FROM selenium/standalone-chrome

COPY additionals/docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh
USER root
ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]

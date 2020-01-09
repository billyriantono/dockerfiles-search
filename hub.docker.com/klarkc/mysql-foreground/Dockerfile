FROM mysql:latest

# Entrypoint overload to catch the ctrl+c and stop signals
ENTRYPOINT ["/bin/bash", "/run.sh"]
CMD ["mysqld"]

COPY run.sh /run.sh

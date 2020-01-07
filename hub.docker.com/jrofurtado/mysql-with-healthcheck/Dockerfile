FROM mysql:5.7.28

HEALTHCHECK --interval=30s --timeout=3s --retries=3 CMD ["/docker-healthcheck.sh"]
COPY files/ /

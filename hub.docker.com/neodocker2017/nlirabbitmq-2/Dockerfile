FROM rabbitmq

COPY docker-healthcheck /usr/local/bin/

HEALTHCHECK --interval=5s --timeout=3s CMD curl --fail http://localhost:5672/pools || exit 1

HEALTHCHECK CMD ["docker-healthcheck"]
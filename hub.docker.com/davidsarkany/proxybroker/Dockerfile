FROM python:alpine
RUN apk --no-cache add --update \
            gcc \
            musl-dev \
            git \
            ca-certificates \
			libffi-dev \
            openssl && \
        pip install proxybroker && \
        rm -rf /var/cache/apk/* && \
        rm -rf /tmp/*
ENTRYPOINT ["proxybroker"]

# :: Header
    FROM 11notes/node:stable

    # :: SSL Settings
        ENV SSL_RSA_BITS=4096
        ENV SSL_ROOT=/api/ssl

    # :: Certbot Settings
        ENV CERTBOT_VERSION=1.0.0

# :: Run
    USER root

    RUN mkdir -p /certbot/ssl \
        && mkdir -p /certbot/www \
        && mkdir -p /certbot/var \
        && mkdir -p /certbot/etc \
        && mkdir -p /certbot/log \
        && mkdir -p /api/js \
        && mkdir -p /api/ssl \
        && mkdir -p /api/etc \
        && npm install express http-auth body-parser nocache --prefix /api/js \
        && apk add --update --no-cache \
            curl openssl

        ADD ./source/api/js /api/js
        ADD ./source/api/etc /api/etc
        ADD ./source/healthcheck.sh /usr/local/bin/healthcheck.sh
        ADD ./source/entrypoint.sh /usr/local/bin/entrypoint.sh
        RUN chmod +x /usr/local/bin/healthcheck.sh
        RUN chmod +x /usr/local/bin/entrypoint.sh
        RUN chmod 0644 /api/etc/auth.htpasswd

    # :: Certbot
        WORKDIR /opt/certbot
        ENV PATH /opt/certbot/venv/bin:$PATH

        RUN apk --no-cache add \
                python3 python3-dev \
            && ln -s /usr/bin/python3 /usr/bin/python \
            && ln -s /usr/bin/pydoc3 /usr/bin/pydoc \
            && ln -s /usr/bin/pip3 /usr/bin/pip \
            && ln -s /usr/bin/python3-config /usr/bin/python-config \
            && pip install --upgrade pip

        RUN mkdir -p src \
            && wget -O certbot-${CERTBOT_VERSION}.tar.gz https://github.com/certbot/certbot/archive/v${CERTBOT_VERSION}.tar.gz \
            && tar xf certbot-${CERTBOT_VERSION}.tar.gz \
            && cp certbot-${CERTBOT_VERSION}/CHANGELOG.md certbot-${CERTBOT_VERSION}/README.rst src/ \
            && cp certbot-${CERTBOT_VERSION}/letsencrypt-auto-source/pieces/dependency-requirements.txt . \
            && cp -r certbot-${CERTBOT_VERSION}/tools tools \
            && cp -r certbot-${CERTBOT_VERSION}/acme src/acme \
            && cp -r certbot-${CERTBOT_VERSION}/certbot src/certbot \
            && rm -rf certbot-${CERTBOT_VERSION}.tar.gz certbot-${CERTBOT_VERSION}

        RUN cat dependency-requirements.txt | tools/strip_hashes.py > unhashed_requirements.txt \
            && cat tools/dev_constraints.txt unhashed_requirements.txt | tools/merge_requirements.py > docker_constraints.txt

        RUN apk add --no-cache --virtual .certbot-deps \
                libffi \
                libssl1.1 \
                openssl \
                ca-certificates \
                binutils

        RUN apk add --no-cache --virtual .build-deps \
                gcc \
                linux-headers \
                openssl-dev \
                musl-dev \
                libffi-dev \
            && pip install -r dependency-requirements.txt \
            && pip install --no-cache-dir --no-deps \
                --editable src/acme \
                --editable src/certbot \
            && apk del .build-deps
 
# :: Version
    RUN echo "CI/CD{{$(certbot --version 2>&1)}}"

# :: docker -u 1000:1000 (no root initiative)
    RUN chown -R node:node \
        /api \
        /certbot \
        /opt/certbot

# :: Volumes
    VOLUME ["/certbot/ssl", "/certbot/www", "/api/etc"]

# :: Monitor
    HEALTHCHECK CMD /usr/local/bin/healthcheck.sh || exit 1

# :: Start
    USER node
    ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
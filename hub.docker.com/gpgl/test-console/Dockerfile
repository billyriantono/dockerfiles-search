FROM gpgl/test-core

MAINTAINER Jeff Puckett

RUN apt-get update && \
    apt-get install -y curl php-sqlite3 && \
    mkdir -p /code/server/ && \
    cd /code/server/ && \
    curl -sLO https://github.com/gpgl/server/archive/master.tar.gz && \
    curl -sO https://raw.githubusercontent.com/gpgl/server/master/server.php && \
    tar zxfv master.tar.gz --strip 1 && \
    composer install --no-dev && \
    apt-get purge -y curl && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* master.tar.gz node_modules/

COPY run.bash fixtures/database.sqlite /
COPY fixtures/oauth-private.key fixtures/oauth-public.key /code/server/storage/

ENV APP_KEY="base64:p4cjma5FQm2B8Lk4T83dr5a4GPuYnsgl9VblIs3GZxE=" \
    APP_DEBUG=true \
    DB_CONNECTION=sqlite \
    DB_DATABASE=/database.sqlite

WORKDIR /code/console

CMD /run.bash

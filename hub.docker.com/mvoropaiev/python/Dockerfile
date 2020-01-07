FROM python:3.5-alpine

# setup working directory
ENV WORKER_APP_DIR '/usr/local/worker-app'
ENV PATH "$PATH:$WORKER_APP_DIR"
WORKDIR "/usr/local/worker-app"

# setup group/user
RUN set -ex \
    && addgroup -g '120' -S 'worker' \
    && adduser -u '120' -G 'worker' -S -s '/bin/false' \
        -h '$WORKER_APP_DIR' 'worker'

# install required packages
RUN set -ex \
    && apk add --no-cache \
        g++ \
        gcc \
        git \
        libffi-dev \
        make \
        openssh-client \
        postgresql-dev \
        su-exec \
    && apk add --no-cache \
        --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ \
            tini

# install gunicorn
RUN set -ex \
    && pip install --no-cache-dir \
        gunicorn=='19.5.0'

# setup custom python packages base directory
# it is required to use pip with --user flag
ENV PYTHONUSERBASE '/pip-cache'
ENV PATH "$PYTHONUSERBASE/bin:$PATH"

FROM python:3.6-slim-stretch

ARG CURRUSERID=1000
ARG HOME=/srv/app
ENV HOME=$HOME

RUN useradd --uid $CURRUSERID --home-dir $HOME --create-home \
            --shell=/usr/sbin/nologin user && \
    chown user.user $HOME

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends\
       busybox-static \
       && \
    rm -rf /var/lib/apt/lists/* && \
    pip install --no-cache --upgrade pip==19.0.3 setuptools && \
    mkdir -p /var/spool/cron/crontabs && \
    echo '*/5 * * * * /srv/app/prices.py >/dev/null 2>&1' > /var/spool/cron/crontabs/user

ENTRYPOINT ["./natriumcast.py"]
EXPOSE 443/tcp

COPY requirements.txt /tmp/requirements.txt

RUN pip install --no-cache \
        -r /tmp/requirements.txt \
        && rm -f /tmp/requirements.txt

WORKDIR /srv

COPY * app/

WORKDIR $HOME
USER $CURRUSERID

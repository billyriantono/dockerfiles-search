FROM debian:jessie-backports
MAINTAINER Michal Čihař <michal@cihar.com>

# Add user early to get a consistent userid
RUN useradd -u 1001 --shell /bin/sh --user-group weblate

ADD requirements.txt /tmp/requirements.txt

ENV REFRESHED_AT 201710221736

# Install dependencies
RUN env DEBIAN_FRONTEND=noninteractive apt-get update \
  && apt-get install --no-install-recommends -y ssh curl python-pip python-lxml python-pillow python-psycopg2 python-memcache python-dateutil python-rcssmin python-rjsmin gettext postgresql-client \
  && apt-get install --no-install-recommends -y -t jessie-backports mercurial git git-svn \
  && apt-get -y upgrade \
  && pip install -r /tmp/requirements.txt \
  && rm /tmp/requirements.txt \
  && apt-get -y purge python-pip \
  && apt-get clean

# Settings
ADD settings.py /app/etc/
RUN chmod a+r /app/etc/settings.py

# Entrypoint
ADD start /app/bin/
RUN chmod a+rx /app/bin/start

# Examples
RUN curl -L https://github.com/nijel/weblate/archive/master.tar.gz | tar xzf - --strip-components=1 -C /app weblate-master/examples

RUN install -d -o weblate -g weblate -m 755 /app/data
RUN ln -s /app/etc/settings.py /usr/local/lib/python2.7/dist-packages/weblate/settings.py
ENV DJANGO_SETTINGS_MODULE weblate.settings
ENV START_CMD "/usr/local/bin/django-admin"

RUN curl https://raw.githubusercontent.com/appuio/libmapuid/master/lib/libmapuid.so -o /usr/local/lib/libmapuid.so && \
    chmod 755 /usr/local/lib/libmapuid.so && \
    chmod g+w /usr/local/lib/python2.7/dist-packages/weblate/trans/migrations

VOLUME ["/app/etc", "/app/data"]
USER weblate

EXPOSE 8000
ENTRYPOINT ["/usr/bin/env", "LD_PRELOAD=/usr/local/lib/libmapuid.so", "/app/bin/start"]
CMD ["runserver", "0.0.0.0:8000"]

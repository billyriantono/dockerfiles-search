FROM ubuntu:trusty
MAINTAINER Renzo Meister <rm@jamotion.ch>

# Install some deps, lessc and less-plugin-clean-css, and wkhtmltopdf
RUN apt-get update 
RUN apt-get install -y --no-install-recommends \
    ca-certificates curl nodejs npm python-support python-pyinotify  python-pip wget git

# Add PostgreSQL 9.4 source
RUN apt-get install -y --no-install-recommends wget && sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list' \
    && wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add - \
    && apt-get update \
    && apt-get install -y --no-install-recommends postgresql-client

ADD bin /opt/odoo/bin

ENV AUTHORIZED_KEYS **None**

ENTRYPOINT ["/opt/odoo/bin/run.sh"]

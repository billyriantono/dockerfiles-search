FROM python:3.6

ENV PYTHONUNBUFFERED 1

# Install postgres-client-9.5 so Django could use pg_dump for DB backups.
RUN set -ex; \
    key='B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8'; \
	export GNUPGHOME="$(mktemp -d)"; \
	gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \
	gpg --export "$key" > /etc/apt/trusted.gpg.d/postgres.gpg; \
	rm -r "$GNUPGHOME"; \
	apt-key list \
	&& \
	echo 'deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main' 9.5 > /etc/apt/sources.list.d/pgdg.list \
    && \
    apt-get update && apt-get install -y --no-install-recommends \
		postgresql-client-9.5 \
	&& rm -rf /var/lib/apt/lists/*

# Install uwsgi and psycopg2
RUN pip install --no-cache-dir uwsgi psycopg2

# Add Django user
RUN groupadd -r django \
    && useradd -r -g django django

# Install requirements
COPY ./requirements.txt /requirements.txt
RUN pip install --no-cache-dir -r /requirements.txt

# Setup entry point
COPY ./compose/django/entrypoint.sh /
RUN chmod +x /entrypoint.sh \
    && chown django /entrypoint.sh

# Setup Django project and its dependencies
COPY ./code /app

# Set project dir as working directory
WORKDIR /app

# Add stub env variables to allow manage.py commands run later
ENV DJANGO_READ_DOT_ENV_FILE=False \
DJANGO_SECRET_KEY='stub' \
DJANGO_ALLOWED_HOSTS='stub' \
POSTGRES_DB='stub' \
POSTGRES_USER='stub' \
POSTGRES_PASSWORD='stub' \
POSTGRES_HOST='stub'
# Make sure statifiles dir exists, collect and compress static files and set Django as project owner
RUN mkdir -p ./staticfiles && python ./manage.py collectstatic -i node_modules --no-input && python ./manage.py compress --force && chown -R django:django .

# Act as Django from now on
USER django

ENTRYPOINT ["/entrypoint.sh"]
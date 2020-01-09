FROM luigidifraia/datacube-notebook:v1.2.0-alpha

LABEL maintainer="Luigi Di Fraia"

USER root

# Install PostgreSQL and supervisor
RUN apt-get update && apt-get install -yq --no-install-recommends \
    postgresql \
    supervisor \
    && rm -rf /var/lib/apt/lists/*

COPY supervisord.conf /etc/supervisor/supervisord.conf

COPY postgres.conf /etc/supervisor/conf.d/postgres.conf
COPY notebook.conf /etc/supervisor/conf.d/notebook.conf

COPY pg_hba.conf /etc/postgresql/10/main/pg_hba.conf

COPY datacube.conf /etc/datacube.conf

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]

# Switch back to jovyan to avoid accidental container runs as root
#USER $NB_UID

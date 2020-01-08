FROM postgres:9.6
LABEL maintainer "mkordi@gmail.com"

ARG database
ARG user
ARG pass

ENV POSTGRES_DB ${database}
ENV POSTGRES_USER ${user}
ENV POSTGRES_PASSWORD ${pass}

# Set recommended Postgres config for Teamcity
COPY postgresql-teamcity.conf postgresql-teamcity.conf

# Override command to use the alternative config
CMD ["postgres", "-c", "config_file=postgresql-teamcity.conf"]
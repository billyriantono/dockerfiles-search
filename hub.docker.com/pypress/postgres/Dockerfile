FROM postgres:11.1

LABEL net.pypress.postgres.version="0.1.0"
LABEL net.pypress.postgres.author="Hacknisty"
LABEL net.pypress.postgres.description="postgres docker image for pypress project."
LABEL maintainer="claude.juif@gmail.com"

ADD init_project_db.sh /docker-entrypoint-initdb.d/init-user-db.sh

RUN chmod +x /docker-entrypoint-initdb.d/init-user-db.sh

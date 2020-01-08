FROM postgres:9.6
MAINTAINER Philipp Goellner <philipp.goellner@xaltbc.de>

ENV BACKUP_HOST             false
ENV BACKUP_PATH             false
ENV BACKUP_USER             false
ENV BACKUP_KEY_FILE         /tmp/id_rsa

ENV POSTGRES_HOME           /var/lib/postgresql/data

ENV TIME_ZONE               false

RUN apt-get update --quiet \
 && apt-get install --quiet --no-install-recommends -y openssh-client \
                                                       rsync \
                                                       tzdata \
 && rm -rf /var/lib/apt/lists/*

COPY configure-and-start.sh /

# expose default Postgres port
EXPOSE 5432

# set volume mount points for installation and home directory
VOLUME ["${POSTGRES_HOME}"]

ENTRYPOINT ["/configure-and-start.sh"]
CMD ["postgres"]

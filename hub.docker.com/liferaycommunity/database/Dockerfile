FROM mariadb:10.2

RUN apt-get update && apt-get install -y python-pip && rm -rf /var/lib/apt && pip install s3cmd

COPY --chown=mysql:mysql rootfs/ /
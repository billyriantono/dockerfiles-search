FROM debian:jessie

VOLUME ["mnt/shuffle", "/mnt/notification", "mnt/openfire"]

RUN apt-get update && apt-get install -y git vim

CMD ["tail", "-f", "/dev/null"]
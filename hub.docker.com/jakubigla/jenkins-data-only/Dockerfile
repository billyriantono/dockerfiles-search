FROM debian:latest

MAINTAINER Jakub Igla <jakub.igla@gmail.com>

RUN groupadd -g 1000 jenkins
RUN adduser --system --uid=1000 --gid=1000 \
        --home /var/lib/jenkins --shell /bin/bash jenkins

RUN chown -R 1000 /var/lib/jenkins

VOLUME /var/lib/jenkins

ENTRYPOINT ["true"]
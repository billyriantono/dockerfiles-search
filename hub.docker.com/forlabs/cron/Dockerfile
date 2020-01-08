FROM debian:stretch-slim

RUN apt-get update && apt-get install -y \
        cron \
        curl; \
    mkdir -p /home/docker/logs; \
    rm -rf /etc/cron.*/

CMD ["cron", "-f"]

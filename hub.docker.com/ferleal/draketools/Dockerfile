FROM debian:stretch-slim

##install cron and curl — so we can register dns regularly
RUN     apt-get update \
       && apt-get install -y cron  ca-certificates unzip curl man-db mysql-client libatomic1 libglib2.0-dev  --no-install-recommends \
       && apt-get clean \
       && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Add current mydumper 
RUN  curl -LO https://github.com/maxbube/mydumper/releases/download/v0.9.5/mydumper_0.9.5-2.stretch_amd64.deb \ 
&& dpkg -i mydumper_0.9.5-2.stretch_amd64.deb \
&& rm mydumper_0.9.5-2.stretch_amd64.deb

# Add crontab file in the cron directory
COPY docker/crons/ /etc/cron.d/

# Give execution rights on the cron job
RUN chmod -Rf 0644 /etc/cron.d/

# Create the log file to be able to run tail
RUN touch /var/log/cron.log

ENTRYPOINT docker/scripts/tools.sh
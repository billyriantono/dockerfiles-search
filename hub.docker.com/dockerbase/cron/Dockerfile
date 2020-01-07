# VERSION 1.0
# DOCKER-VERSION  1.2.0
# AUTHOR:         Richard Lee <lifuzu@gmail.com>
# DESCRIPTION:    Cron Image Container

FROM dockerbase/runit

# Run dockerbase script
ADD     cron.sh /dockerbase/
RUN     /dockerbase/cron.sh

# Add cron into runit
ADD     build/runit/cron /etc/service/cron/run

# Remove useless cron entries.
# Checks for lost+found and scans for mtab.
RUN     rm -f /etc/cron.daily/standard

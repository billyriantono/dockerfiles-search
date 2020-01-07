FROM java:7

# install cron
RUN apt-get update && apt-get install -y cron && rm -r /var/lib/apt/lists/*

# set timezone
RUN cp -f /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

CMD cron -f

FROM nextcloud:fpm

RUN apt-get update && apt-get install cifs-utils -y  && rm -rf /var/lib/apt/lists/*
COPY run.sh /run.sh
CMD ["/run.sh"]

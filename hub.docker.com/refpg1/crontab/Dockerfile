FROM php:5-apache

RUN apt-get update && apt-get install -y wget curl cron nano 

RUN service cron start
CMD cron && exec /bin/bash -c "trap : TERM INT; sleep infinity & wait"

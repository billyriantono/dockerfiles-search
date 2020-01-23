# Image custo d'akkro
FROM stilliard/pure-ftpd:latest
MAINTAINER Mathieu akkro GERAULT <mathieu.gerault@gmail.com>
LABEL Description="Pureftpd from Mathieu GERAULT"

# Change timezone
ENV TZ=Europe/Paris
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone


FROM wordpress:latest

RUN apt update && \
apt install -y ffmpeg

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["apache2-foreground"]

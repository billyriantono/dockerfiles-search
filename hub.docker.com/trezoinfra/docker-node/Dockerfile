FROM node:8.9-slim

RUN apt-get update && apt-get install -y libpng-dev

WORKDIR /var/www

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

CMD ["/entrypoint.sh"]
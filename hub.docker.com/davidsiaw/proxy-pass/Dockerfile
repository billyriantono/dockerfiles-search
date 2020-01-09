FROM nginx:1.13.0-alpine
MAINTAINER David Siaw davidsiaw@gmail.com

ENV VIRTUAL_HOST example.example.com
ENV TARGET_HOST example.com

COPY conf.template /conf.template
COPY start.sh /start.sh

EXPOSE 80

CMD ["sh", "/start.sh"]

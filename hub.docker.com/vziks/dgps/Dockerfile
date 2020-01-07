FROM node:7-alpine

MAINTAINER vziks@live.ru.ru

RUN npm install --save -g psi-v4

COPY entrypoint.sh /
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
CMD ["--help"]
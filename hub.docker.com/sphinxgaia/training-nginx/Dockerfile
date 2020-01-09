FROM nginx:1.12-alpine

LABEL maintainer jerome masson <sphinxgaia@jeromemasson.fr>
LABEL description sample nginx

RUN mkdir -p /tmp/hello

WORKDIR /tmp/hello
COPY hlw.txt hlw.txt

RUN cat hlw.txt

WORKDIR /usr/share/nginx/html
COPY ./index.html /usr/share/nginx/html/index.html

COPY ./docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["nginx", "-g", "daemon off;"]

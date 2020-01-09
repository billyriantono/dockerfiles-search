FROM openjdk:8-jre-alpine

ENV UID=991 GID=991 \
    DB_TYPE=h2 \
    DB_USER=root \
    DB_PASSWORD=streama \
    DB_HOST=mysql \
    DB_NAME=streama

RUN apk add --no-cache curl

COPY rootfs /
RUN chmod +x /usr/local/bin/*

WORKDIR /streama
RUN wget -O streama.war -q `curl -s https://api.github.com/repos/dularion/streama/releases/latest \
| grep "browser_download_url.*war" \
| cut -d : -f 2,3 \
| tr -d \"  `

VOLUME /config /upload

EXPOSE 8080

CMD ["run.sh"]

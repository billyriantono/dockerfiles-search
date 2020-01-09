FROM alpine

RUN apk add --no-cache bash \
                       tzdata

ENV TZ=Europe/Zurich

COPY src /tmp/

CMD cd /tmp/ && bash start.sh

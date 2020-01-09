FROM python:alpine

RUN apk update && apk add chromium curl wget py3-requests git && pip install requests

RUN adduser archivist -h /app -D -H

RUN mkdir /app

RUN chown -R archivist /app

USER archivist

RUN cd /app && git clone https://github.com/pirate/bookmark-archiver.git ./

CMD python /app/archive /links.txt